---
layout: post
title: "Builder - Creational Design Pattern"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: creational-pattern
icon: blogging.png
---
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