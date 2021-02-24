---
# Course title, summary, and position.
linktitle: How to Design a Highly Scalable URL Shortening Service
summary: Learn fundamental scalability and system design concepts, how to effectively measure capacity and usage, and operate a highly available service.
weight: 1

# Page metadata.
title: Course Overview
date: "2019-12-15T00:00:00Z"
lastmod: "2019-12-15T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: true  # Show table of contents? true/false
type: docs  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.
menu:
  url-shortener:
    name: Course Overview
    weight: 1
---

## About this course
Learn how to design a highly scalable url shortening service, exercising fundamental system design principles and architecture diagramming. In this course, we will design a primitive url shortening service, then add requirements that cause us to redesign the system as we measure capacity limitations.

## What is a url shortener?
url shortening is a technique on the World Wide Web in which a Uniform Resource Locator (url) may be made substantially shorter and still direct to the required page. This is achieved by using a redirect which links to the web page that has a long url. For example, the url "https://example.com/assets/category_B/subcategory_C/Foo/" can be shortened to "https://example.com/Foo", and the url "http://example.com/about/index.html" can be shortened to "https://goo.gl/aO3Ssc ". Often the redirect domain name is shorter than the original one. A friendly url may be desired for messaging technologies that limit the number of characters in a message (for example SMS), for reducing the amount of typing required if the reader is copying a url from a print source, for making it easier for a person to remember, or for the intention of a permalink.

## Why a url shortener?
At its core, the url shortening problem is extremely simple. We will explore the problem space and introduce new scalability requirements to adapt and modify the system to cope with scale. These principles can be applied to a wide variety of systems needing to scale.

## The process
We will decompose the process into a few phases:
1. **Design Phase:** understand the problem and estimate the unknowns. Iterate on a few potential solutions to the problem.
2. **Compare Systems:** identify the limitations of the different solutions regarding application design, fault tolerance and recovery.
3. **Compare Capacities:** identify the limitations of the different solutions regarding CPU, memory, network, disk, etc.
4. **Compare Scalability:** take the existing design and simulate 100x the incoming request volume. Analyze the performance, cost and scalability under the additional load.

Let's get started!
