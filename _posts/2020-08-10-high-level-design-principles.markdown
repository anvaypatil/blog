---
layout: post
title: "High Level Design Principles"
date: 2020-08-10 13:01:20 +0300
description: Principles to keep in mind while desiging software. # Add post description (optional)
img:  principle.jpeg # Add image post (optional)(optional)
categories: [design-&-architecture]
icon: blogging.png
---

These are some of the guiding high-level principles which are important to keep in mind while desiging software component/system

#### Enforce Loose Coupling
- Two classes, components or modules are coupled when at least one of them uses the other. the less these items knows about each other, the losser they are coupled.
- A component that is only loosely coupled to its environment can be more easily changed or replaced than a strongly component.

#### Adopt High Cohesion
- Cohesion is the degree to which elements of a whole belong together. 
- Methods and properties in a single class and classes of a component should have high cohesion. 
- High Cohesion in classes and components results in simpler, more easily understandabe code structure and design

#### Enable design which will help changed to local as much as possible
- When a software system has to be maintained, extended and changed for a long time, keeping changes local reduces involved costs and risks.
- Keeping change local means that there are boundaries in the design which changes should not cross.
- Design by contract and perfer <a target="_blank" href="{{ site.baseurl }}/object-oriented-design/dependency-inversion-principle/">Dependency Inversion Principle</a>

#### It should be easy to remove
- We normally build software by adding, extending or changing features.
- Removing elements is important so that overall design can be kept as simple as possible.
- When a block (Method, Class, Component, Module) gets too complicated, it has to be removed and replaced with one or more simpler granular blocks

#### Design Mind-Sized Components
- Break your system down into components that are of a size you can grasp within your mind so that you can predict consequences of changes easily. (dependencies, control flow, ..)