---
layout: post
title: "Singleton - Creational Design Pattern"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: notes-1.png # Add image post (optional)
tags: DesignPatterns CreationalPatterns
---
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