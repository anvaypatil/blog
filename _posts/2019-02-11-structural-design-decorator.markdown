---
layout: post
title: "Decorator - Structural Design Pattern"
date: 2019-02-11 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: structural-pattern
icon: blogging.png
---
☕ Decorator
------------
Decorator pattern lets you dynamically change the behavior of an object at run time by wrapping them in an object of a decorator class.
```java
// The Window interface class
public interface Window {
    void draw(); // Draws the Window
    String getDescription(); // Returns a description of the Window
}
// Implementation of a simple Window without any scrollbars
class SimpleWindow implements Window {
    public void draw() {
        // Draw window
    }
    public String getDescription() {
        return "simple window";
    }
}
abstract class WindowDecorator implements Window {
    private final Window windowToBeDecorated; // the Window being decorated
    public WindowDecorator (Window windowToBeDecorated) {
        this.windowToBeDecorated = windowToBeDecorated;
    }
    @Override
    public void draw() {
        windowToBeDecorated.draw(); //Delegation
    }
    @Override
    public String getDescription() {
        return windowToBeDecorated.getDescription(); //Delegation
    }
}
// The first concrete decorator which adds vertical scrollbar functionality
class VerticalScrollBarDecorator extends WindowDecorator {
    public VerticalScrollBarDecorator (Window windowToBeDecorated) {
        super(windowToBeDecorated);
    }
    public void draw() {
        super.draw();
        drawVerticalScrollBar();
    }
    private void drawVerticalScrollBar() {
        // Draw the vertical scrollbar
    }
    public String getDescription() {
        return super.getDescription() + ", including vertical scrollbars";
    }
}
// The second concrete decorator which adds horizontal scrollbar functionality
class HorizontalScrollBarDecorator extends WindowDecorator {
    public HorizontalScrollBarDecorator (Window windowToBeDecorated) {
        super(windowToBeDecorated);
    }
    public void draw() {
        super.draw();
        drawHorizontalScrollBar();
    }
    private void drawHorizontalScrollBar() {
        // Draw the horizontal scrollbar
    }
    public String getDescription() {
        return super.getDescription() + ", including horizontal scrollbars";
    }
}
public class DecoratedWindowTest {
    public static void main(String[] args) {
        // Create a decorated Window with horizontal and vertical scrollbars
        Window decoratedWindow = new HorizontalScrollBarDecorator (
                new VerticalScrollBarDecorator (new SimpleWindow()));
        // Print the Window's description
        System.out.println(decoratedWindow.getDescription());
    }
}
```
