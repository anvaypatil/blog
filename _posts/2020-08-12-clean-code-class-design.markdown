---
layout: post
title: "Code Code: Class Design"
date: 2020-08-12 13:01:20 +0300
description: How should we do class design
img:  clean-code.png # Add image post (optional)(optional)
categories: [clean-code]
icon: blogging.png
---

### Class Design
- #### Single Responsiblity Principle (SRP)
There should never be more than one reason for a class/module to change. <a target="_blank" href="{{ site.baseurl }}/object-oriented-design/single-responsiblity-principle/">more..</a>

- #### Open Closed Principle (OCP)
 Software entities... should be open for extension, but closed for modification. <a target="_blank" href="{{ site.baseurl }}/object-oriented-design/open-closed-principle/">more..</a>

- #### Liskov Substitution Principle (LSP)
Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it. <a target="_blank" href="{{ site.baseurl }}/object-oriented-design/liskov-substitution-principle/">more..</a>

- #### Dependency Inversion Principle (DIP)
Software entities should be dependent on abstractions than concrete implementations.  <a target="_blank" href="{{ site.baseurl }}/object-oriented-design/dependency-inversion-principle/">more..</a>

- #### Interface Segregation Principle (ISP)
Clients should not be forced to depend upon interfaces that they do not use.  <a target="_blank" href="{{ site.baseurl }}/object-oriented-design/interface-segregation-principle/">more..</a>

- #### Classes should be small
Smaller classes are easier to grasp. Classes should be smaller than 100 lines of code. 

- #### Do stuff or know others but not both
Classes should either do stuff (algorithm, read data, write data, …) or orchestrate other classes. This reduces coupling and simplifies testing
