---
layout: post
title: "State - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

🏗 State
---------------
Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

```java
Function<String, String> upperCase = (String inputString) => inputString.toUpperCase();
Function<String, String> lowerCase = (String inputString) => inputString.toLowerCase();
Function<String, String> defaultTransform = (String inputString) => inputString;

public class TextEditor {
    private Function<String, String> _transform;
    TextEditor(Function<String, String> transform) {
        this._transform = transform;
    }
    public void setTransform(Function<String, String> transform) {
        this._transform = transform;
    }
    public void type(String words) {
        System.out.println(this._transform(words));
    }
}

TextEditor editor = new TextEditor(defaultTransform);
editor.type("First line");
editor.setTransform(upperCase);
editor.type("Second line");
editor.type("Third line");
editor.setTransform(lowerCase);
editor.type("Fourth line");
editor.type("Fifth line");
```
