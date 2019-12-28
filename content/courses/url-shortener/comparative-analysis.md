---
title: "Comparative Analysis"
linktitle: "Comparative Analysis"
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  url-shortener:
    parent: Course Overview
    weight: 5

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

## Comparison / Analysis phase - second pass
Of the three designs we have considered, we did not look in depth into the storage because design 3 showed that we can naively fit the data into a single database instance. If we have to support 100x on the storage layer, we need to store up to 5 PB of data. We will need to investigate sharding techniques, what is shared and how to manage hotspots.

## Design 3
In this design, we are storing the data *and* generating the id at the database layer. Since now know we need to expand beyond a single instance, we need to look into sharding schemes while maintaining uniqueness across each instance. If we have 10 separate databases, we need to know which database contains the key we are looking for.

### How does this scale up?
What is the size of the pre-shard such that we don't run out of connections?

One idea is that we can use different sequence numbers on each database:
* Even and odd id generation on different databases
* Have each id generated start with a prefix based on the database

Both of these options are essentialy a pre-sharding scheme as the number of databases will need to be known beforehand.

Given that we need to store 5 PB of data, assuming we have a maximum of 50 TB of data per machine, this means we need 100 machines. This accounts for the storage volume and overall IOPS, given no hotspots. The memory and CPU calculations should remain the same from our previous analysis.

We have to handle $4e5\text{ IOPS}$ on average and $4e6\text{ IOPS}$ at peak for both reads and writes. If we can avoid hotspots, each shard will need to handle $\dfrac{4e6}{1e2} = 4e4\text{ IOPS}$. We may be able to handle peak load, but we would need to performance test this scenario. Alternatively, we could use caches to reduce the read load, changing the dynamics of the load profile.

We still need to reconsider the number of network connections and the number of app servers we may have. Given 100 data shards and assuming 20 TCP connections can handle the number of requests to a shard, for each app server we would need $\text{tcp_connection_pool_count} * \text{ db_shard_count} = 20 * 100 = 2000$. On the database end, we have $\text{app_server_count * \text{ tcp_connection_pool_count} = \text{total_connections}$

The next step is to understand how many app servers we need. Previously, we calculated that we need 400 cores at peak. Now we would need $4e4$. Given 40 cores per instance, that would be 1000 app servers needed. On each database, we would have $2e4$ active connections for the database pool. To solve this problem, we may need to add an additional layer of abstraction. Our possible solutions may be:
* Use a consolidated database pool between application servers
* Pin a set of app servers to database shards
* Move to the client side and use DNS

## Design 1
This is a shared-nothing design with a 64 bit hash.

### How does this scale up?
From the previous design, we know we would need 100 shards at 50 TB each. For the hash design, we could use the first 10 bits to represent up to 1024 shards. If we are using a database that represents data as a binary tree, this can cause some write amplification on some inserts where the child pages need to be split. With a binary tree index, we are trading off random writes for easier reads. Because the hash is essentially random, the IO patterns will also be mostly random, which is much slower than sequential. In fact, there are old bugs with MySQL such that UUID insert performance decreases proportional to the number of keys.

A UNIX timestamp is 32 bits, which lasts from 1970 to 2038. Perhaps we coul start a custom epoch that starts at 2020 instead of 1970.

We would like to include milliseconds in our epoch, which can be represented by 10 bits: $2^{10} = 1024$. Given 64 bits to work with:
* 10 bits for the number of shards: 1024 - random but we can still have hotspots.
* 42 bits for the custom epoch in milliseconds: 70 years of custom time: $32\text{ bits} + 10\text{ bits}$. We may not need the whole 70 years, so this might be reduced
* 12 bits = $2^{12} = 4096$ values per millisecond. We need to atomically increment a counter in some layer so we can generate more than one record per millisecond

This design will allow 4000 writes per ms per shard. Conveniently, we previously calculated that we can increment a counter on a single instance at around 3500 per second. We can pre-shard to 1024 and distribute over 1 instance to start and ramp up to n-machines as necessary.

Also, in addition to being a faster insert, another interesting property of this design is that it is roughly ordered.
