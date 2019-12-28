---
title: "Design 2: 3rd Party ID Generation"
linktitle: "Design 2: 3rd Party ID Generation"
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  url-shortener:
    parent: Course Overview
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

## Analysis
The second design requires a 3rd system to be involved. We want to explore a different approach to generating ids than design 1. This could be a system which generates sequential ids and sends them back to the app servers.

![Design2](/courses/url-shortener/design2.png)

## Application design limits
Can we auto increment fast enough?

In this case, we are essentially going to make a single counter. Incrementing a counter in memory takes about 0.2-0.3 microseconds given it should take 2 memory accesses and an addition. This is $0.3 * 10^{-6} = 3 * 10^{-7}$. This would give $0.33 * 10^7 = 3.33 * 10^6$ increments in a second. A rough estimate of 3 million in a second, or 3333 increments per millisecond. Note: this is for a single threaded counter. With a multi-threaded counter, we would have to deal with locks on the memory if we wanted accuracy for the counter to be atomic, which we would need to have in order to guarantee uniqueness in the system.

Although our memory may be fast enough, the bottleneck occurs somewhere else. From Redis benchmarks, the INCR operations maxes out at $150e3$ requests per second. In our first phase of the lifecycle, we only need to do 333 writes per second on average and 3333 reads per second at peak (10x).

At this point, this design requires a 3rd component, so we should avoid additional complexity unless necessary. We need to figure out how to make this resilient, which could be tricky.
