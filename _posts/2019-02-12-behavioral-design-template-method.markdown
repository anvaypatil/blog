---
layout: post
title: "Template Method - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

🗜 Template Method
-------------------
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses / Template Method lets subclasses redefine certain steps of an algorithm without letting them to change the algorithm's structure.

```java
public abstract class AppBuilder {
    public abstract void test();
    public abstract void lint();
    public abstract void assemble();
    public abstract void deploy();
    // Template method 
    public void build() {
        this.test()
        this.lint()
        this.assemble()
        this.deploy()
    }
}
public class AndroidBuilder extends AppBuilder {
    public void test() {
        System.out.println("Running android tests")
    }
    public void lint() {
        System.out.println("Linting the android code")
    }
    public void assemble() {
        System.out.println("Assembling the android build")
    }
    public void deploy() {
        System.out.println("Deploying android build to server")
    }
}
public class IosBuilder extends AppBuilder {
    public void test() {
        System.out.println("Running ios tests")
    }
    public void lint() {
        System.out.println("Linting the ios code")
    }
    public void assemble() {
        System.out.println("Assembling the ios build")
    }
    public void deploy() {
        System.out.println("Deploying ios build to server")
    }
}
```
