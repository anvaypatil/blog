---
layout: post
title: "Abstract Factory - Creational Design Pattern"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: creational-pattern
icon: blogging.png
---
🔨 Abstract Factory
------------------
A factory of factories; a factory that groups the individual but related/dependent factories together without specifying their concrete classes.
```java
interface Door {
    public function getDescription();
}
class WoodenDoor implements Door {
    public function getDescription() {
        return "I am a wooden door";
    }
}
class IronDoor implements Door {
    public function getDescription() {
        return "I am an iron door";
    }
}
// experts 
interface DoorFittingExpert {
    public function getDescription();
}
class Welder implements DoorFittingExpert {
    public function getDescription() {
        return "I can only fit iron doors";
    }
}
class Carpenter implements DoorFittingExpert {
    public function getDescription() {
        return "I can only fit wooden doors";
    }
}
// Solving a problem we need problem factory.
interface DoorFactory {
    public Door makeDoor();
    public DoorFittingExpert makeFittingExpert();
}
class WoodenDoorFactory implements DoorFactory {
    public Door makeDoor() {
        return new WoodenDoor();
    }
    public DoorFittingExpert makeFittingExpert() {
        return new Carpenter();
    }
}
class IronDoorFactory implements DoorFactory {
    public Door makeDoor() {
        return new IronDoor();
    }
    public DoorFittingExpert makeFittingExpert() {
        return new Welder();
    }
}
```
**When to use?** When there are interrelated dependencies with not-that-simple creation logic involved