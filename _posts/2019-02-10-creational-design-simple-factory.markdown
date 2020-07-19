---
layout: post
title: "Simple Factory - Creational Design Pattern"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: creational-pattern
icon: blogging.png
---
🏠 Simple Factory
--------------
Simple factory simply generates an instance for client without exposing any instantiation logic to the client

Example:
```java
interface Door {
    public function getWidth(): float;
    public function getHeight(): float;
} 
class WoodenDoor implements Door {
    protected int width;
    protected int height;
    public int getWidth() {
        return width;
    }
    public int getHeight() {
        return height;
    }
    public WoodenDoor(int width, int height){
        this.width = width;
        this.height = height;
    }
}
class DoorFactory {
    public static function makeDoor(width, height): Door
    {
        return new WoodenDoor(width, height);
    }
}
```
**When to Use?**
When creating an object is not just a few assignments and involves some logic, it makes sense to put it in a dedicated factory instead of repeating the same code everywhere.