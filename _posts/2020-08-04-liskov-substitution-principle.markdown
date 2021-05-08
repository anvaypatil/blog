---
layout: post
title: "Liskov Substitution Principle"
date: 2020-08-04 13:01:20 +0300
description: Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it. # Add post description (optional)
img:  principle.jpeg # Add image post (optional)(optional)
categories: [object-oriented-design]
icon: blogging.png
---
**Subtypes must be substitutable for their base types.**

>
Substitutability is a principle in object-oriented programming stating that, in a computer program, if S is a subtype of T, then objects of type T may be replaced with objects of type S
>

```java
public class Bird{}
public class FlyingBird extends Bird{
    public void fly(){}
}
public class Duck extends FlyingBird{}
public class Ostrich extends Bird{} 
```