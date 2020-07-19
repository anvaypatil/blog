---
layout: post
title: "Prototype - Creational Design Pattern"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: creational-pattern
icon: blogging.png
---
🧱 Prototype
-----------
Create object based on an existing object through cloning.
```java
class Computer {
    protected int ramSize;
    protected KeyBoard keyboard;
    protected Mouse mouse;
    protected Motherboard chipset;
    protected CPUCabinet cabinet;
    // assume getters & setters. 
    public Computer clone(){
        Computer that = new Computer();
        // copy all the this content to that content, deeply. 
        return that;
    }
}
```
**When to use?** When an object is required that is similar to existing object or when the creation would be expensive as compared to cloning.