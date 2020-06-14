---
layout: post
title: "OO Design Patterns - Creational 101"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img:  # Add image post (optional)
tags: DesignPatterns CreationalPatterns
---
## Creational Design Patterns. 
Creational patterns are focused towards how to instantiate an object or group of related objects. It provide various object creation mechanisms, which increase flexibility and reuse of existing code.

 * [Simple Factory](#-simple-factory)
 * [Factory Method](#-factory-method)
 * [Abstract Factory](#-abstract-factory)
 * [Builder](#-builder)
 * [Prototype](#-prototype)
 * [Singleton](#-singleton)

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

🏭 Factory Method
---------------
It provides a way to delegate the instantiation logic to child classes.
Example:
```java
interface Interviewer {
   public function takeInterview();
}
class Developer implements Interviewer {
    public function askQuestions() {
        // 'Ask Programming Question!';
    }
}
class CommunityExecutive implements Interviewer {
    public function askQuestions() {
        // 'Ask about Community Building!';
    }
}
abstract class HiringManager {
    abstract protected makeInterviewer();
    public function takeInterviews() {
        Interviewer interviewer = this.makeInterviewer();
        interviewer.askQuestions();
    }
}
// any child can extend it and provide the required interviewer
class DevelopmentManager extends HiringManager {
    protected Interviewer makeInterviewer() {
        return new Developer();
    }
}
class MarketingManager extends HiringManager {
    protected Interviewer makeInterviewer() {
        return new CommunityExecutive();
    }
}
```
**When to Use?** Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn't know what exact sub-class it might need.

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

👷 Builder
------------
Allows you to create different flavors of an object while avoiding constructor pollution. Useful when there could be several flavors of an object. Or when there are a lot of steps involved in creation of an object. This is useful to create fluent API's 
Example:
```java
class Burger {
    protected int size;
    protected boolean cheese = false;
    protected boolean pepperoni = false;
    protected boolean lettuce = false;
    protected boolean tomato = false;
    public Burger(BurgerBuilder builder) {
        this.size = builder.size;
        this.cheese = builder.cheese;
        this.pepperoni = builder.pepperoni;
        this.lettuce = builder.lettuce;
        this.tomato = builder.tomato;
    }
}
class BurgerBuilder {
    public int size;
    public boolean cheese = false;
    public boolean pepperoni = false;
    public boolean lettuce = false;
    public boolean tomato = false;
    public BurgerBuilder(int size) {
        this.size = size;
    }
    public boolean addPepperoni() {
        this.pepperoni = true;
        return this;
    }
    public boolean addLettuce() {
        this.lettuce = true;
        return this;
    }
    public boolean addCheese() {
        this.cheese = true;
        return this;
    }
    public boolean addTomato() {
        this.tomato = true;
        return this;
    }
    public Burger build() {
        return new Burger(this);
    }
}
// usage:
Burger burger = (new BurgerBuilder(14))
                    .addPepperoni()
                    .addLettuce()
                    .addTomato()
                    .build();
```
**When to use?** When there could be several flavors of an object and to avoid the constructor telescoping. The key difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

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

☝ Singleton
---------
Ensures that only one object of a particular class is ever created in an execution environment.
Example:
```java
public class Singleton {
    private Singleton() {}
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```
**When to use?** When you need some kind of a global state to represent in your application. 