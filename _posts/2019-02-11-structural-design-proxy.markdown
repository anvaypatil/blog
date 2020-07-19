---
layout: post
title: "Proxy - Structural Design Pattern"
date: 2019-02-11 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: structural-pattern
icon: blogging.png
---
🎱 Proxy
----------
Using the proxy pattern, a class represents the functionality of another class.

```java
interface Door {
    public void open();
    public void close();
}
class LabDoor implements Door {
    public void open() {
        // "Opening lab door";
    }
    public void close() {
        // "Closing the lab door";
    }
}
class SecuredDoor{
    protected Door door;
    public SecuredDoor(Door door) {
        this.door = door;
    }
    public void open(String password) {
        if (this.authenticate(password)) {
            this.door.open();
        } else {
            // "Error you are not allowed";
        }
    }
    public boolean authenticate(String password) {
        return password == "$ecr@t";
    }
    public void close() {
        this.door.close();
    }
}

Door door = new SecuredDoor(new LabDoor());
door.open("invalid"); // Big no! It ain't possible.

Door door.open("$ecr@t"); // Opening lab door
door.close(); // Closing lab door
```