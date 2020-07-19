---
layout: post
title: "Adapter - Structural Design Pattern"
date: 2019-02-11 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: structural-pattern
icon: blogging.png
---
🔌 Adapter
-----------
Adapter pattern lets you wrap an otherwise incompatible object in an adapter to make it compatible with another class.
Example:
```java
public interface Stack {
    public void push(int x);
    public void pop();
    public int top();
    boolean empty();
}
public class FixedArray {
    public FixedArray() {
    index = -1;
    items = new int[10];
    }
    public void insert(int x) { items[++index] = x; }
    public void removeLast() { --index; }
    public boolean empty() { return index == -1; }
    public int top() { return items[index]; }
    private int index;
    private int [] items;
}
// making FixedArray used in Stack
public class ArrayStack implements Stack {
    private FixedArray array;
    public ArrayStack() { array = new FixedArray(); }
    public void push(int x) { array.insert(x); }
    public void pop() { array.removeLast(); }
    public int top() { return array.top(); }
    public boolean empty() { return array.empty(); }
}
```
**When to use?** When we want to make incompatible interfaces work with each other.