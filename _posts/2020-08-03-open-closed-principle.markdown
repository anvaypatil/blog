---
layout: post
title: "Open Closed Principle"
date: 2020-08-03 13:01:20 +0300
description: Software entities... should be open for extension, but closed for modification # Add post description (optional)
img:  principle.jpeg # Add image post (optional)(optional)
categories: [object-oriented-design]
icon: blogging.png
---
- The principle states **"software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"**.
- A module will be **said to be open, if it is still available for extension**. For example, **it should be possible to add fields to the data structures it contains, or new elements to the set of functions it performs**.
- A module will be **said to be closed if it is available for use by other modules**. This **assumes that the module has been given a well-defined, stable description (the interface in the sense of information hiding)**.
- The principle became popularly redefined to **refer to the use of abstracted interfaces, where the implementations can be changed and multiple implementations could be created and polymorphically substituted for each other**.
- Program by Interface, not by Implementation, {Strategy Design Pattern}

```java
public interface CalculatorOperation {
    void perform();
}

// Calculator class doesn't need to implement new logic as we introduce more operations
public class Calculator {
    public void calculate(CalculatorOperation operation) {
        if (operation == null) {
            throw new InvalidParameterException("Cannot perform operation");
        }
        operation.perform();
    }
}

public class Addition implements CalculatorOperation {
    private double left;
    private double right;
    private double result;
    // constructor, getters and setters
    @Override
    public void perform() {
        result = left + right;
    }
}

public class Division implements CalculatorOperation {
    private double left;
    private double right;
    private double result;
    // constructor, getters and setters
    @Override
    public void perform() {
        if (right != 0) {
            result = left / right;
        }
    }
}

```