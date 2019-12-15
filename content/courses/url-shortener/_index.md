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

## URL Shortening Service
Learn how to design a highly scalable URL shortening service.

## What is a URL shortener?
A URL shortening service simply creates a short URL for a longer, more complex URL. For example, a user may want to have a handy, short url instead of `https://longandunwieldy.com/url/with/parameters?makes=this+too+long`. The URL shortening service would return a URL like `https://sho.rt/Xv7d` which will resolve to the long url when entered into the browser.
