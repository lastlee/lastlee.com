---
title: Basic Design
linktitle: Basic Design
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  url-shortener:
    parent: Course Overview
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## Designing a simple service
Let's figure out how to generate the short url of length less than 10 characters (after http://sho.rt/) before doing extensive analysis.

We will break this down into a few operations:
1. Generation of a unique id
2. Mapping of the id into a short url that is less than 10 characters
3. Storage and retrieval of the id and long url

Come up with several designs that can satisfy these operations.

## Generate an id
Some common methods for generating an id might be:
1. Write the long url into a database and auto-increment the primary id
2. Generate an id on the application side and attempt to insert it into a database. If there are multiple application instances, we would need to figure out how to avoid id collisions.
3. Generate an id on a 3rd party system and attempt to insert it into a database.

For options 2 and 3 we need to guarantee uniqueness or we may have to account for collisions. In the most primitive form, we could use MD5/SHA of the long-url or generate a UUID.

## Mapping of the id into a short url that is less than 10 characters
We need to guarantee this mapping is 1:1. Whether this is a 64-bit int primary key in the database or UUID, we can use an encoding scheme like Base64 to shorten the id to the required length, and return this a base url + encoded id to the user, for example: http://sho.rt/XyD6Ab.

### Estimate some performance and scalability limits of this system
Let's make a few assumptions regarding the scalability and do some rounding for convenience.

* The maximum size of a url is 512 bytes and the short url can only be 10 bytes. We can estimate this as 500 bytes / url.
* The number of reads is 10x the number of writes.
* At some point in time, we have 100x more urls the system.
* The number of seconds in a day is 86400 which we’ll estimate as $1e5$.
* Assume linear growth such that reads/sec and writes/sec are constant

**Yearly Performance and Scalability Table**

|  | Year 1 | Year 10 |
| ---- | -- | --- |
| Total urls / year | $1e9\text{ urls} ∗ 12\text{ months }= 12e9\text{ urls}$ | $12e9\text{ urls}$ |
| Cumulative urls | $12e9\text{ urls}$ | $12e9 * 10 = 12e10 ~= 1e11\text{ urls}$ |
| Total uncompressed storage | $500\text{ Bytes }* 12e9 = 6e12\text{ (6 TB)}$ | $500e11 ~= 50e12\text{ (50 TB)}$ |
| Total compressed storage | $3e12\text{ (3 TB)}$ | $~= 25e12\text{ (25 TB)}$ |
| Writes / sec | $\dfrac{\dfrac{1e9\text{ urls}}{1e5\text{ seconds}}}{30\text{ days}} = 333\text{ writes/sec}$ | $333\text{ writes/sec}$ |
| Reads / sec (100x writes) | $3333\text{ reads/sec}$ | $3333\text{ reads/sec}$ |
| IOPS (writes + reads) | $\approx 4e3\text{ IOPS}$ | $\approx 4e3\text{ IOPS}$ |

**100x**

|  | Year 1 | Year 10 |
| ---- | -- | --- |
| Total urls / year | $1e11\text{ urls} ∗ 12\text{ months }= 12e11\text{ urls}$ | $1.2e12\text{ urls}$ |
| Cumulative urls | $12e11\text{ urls}$ | $12e11 * 10 = 12e12 \simeq 1e13\text{ urls}$ |
| Total uncompressed storage | $500\text{ Bytes }* 12e11 = 600e12\text{ (600 TB)}$ | $500e13 = 5e15\text{ (5 PB)}$ |
| Total compressed storage | $300e12\text{ (300 TB)}$ | $\sim 2.5e15\text{ (2.5 PB)}$ |
| Writes / sec | $\dfrac{\dfrac{1e11\text{ urls}}{1e5\text{ seconds}}}{30\text{ days}} = 33e3\text{ writes/sec}$ | $33e3\text{ writes/sec}$ |
| Reads / sec (100x writes) | $33e4\text{ reads/sec}$ | $33e4\text{ reads/sec}$ |
| IOPS (writes + reads) | $\approx 4e5\text{ IOPS}$ | $\approx 4e5\text{ IOPS}$ |

NOTE: Depending on our storage medium, a write could take anywhere from 1 - 3 IOPS. We are approximating requirements so we don't need high levels of precision.

NOTE: The storage estimations of 5 PB are worst case. We will need to calculate the trade-off between disk vs CPU for compression. Generally we know we are growing at approximately 300 TB / year if we compress the data.

## Comparison / Analysis Phase
We have a few ideas of designs now, in addition to the requirements for initial launch and 100x scale in traffic. We need to first examine the system for the initial requirements.

### Overall application design limits
We need to store a total of 1e13 urls. First, we need to know the total number of bits we need to represent this:

Since $2^{10} = 10^{3}$, we need a total of

$10^{13} = 2^{10} * 2^{10} * 2^{10} * 2^{10} * 10$

$\approx 2^{44}$

This means we need 44 bits of address space to store all of our urls over the lifetime of the system.

Next, let's take a look at a few different designs and compare trade-offs!
