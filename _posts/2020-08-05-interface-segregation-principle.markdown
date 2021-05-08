---
layout: post
title: "Interface Segregation Principle"
date: 2020-08-05 13:01:20 +0300
description: Clients should not be forced to depend upon interfaces that they do not use. # Add post description (optional)
img:  principle.jpeg # Add image post (optional)(optional)
categories: [object-oriented-design]
icon: blogging.png
---
- It splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them. Such shrunken interfaces are also called **role interfaces**.
- **“Clients should not be forced to depend upon interfaces that they do not use.”**
- **Reduce the side effects of using larger interfaces by breaking application interfaces into smaller ones.**