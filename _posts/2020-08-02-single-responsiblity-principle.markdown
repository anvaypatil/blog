---
layout: post
title: "Single Responsibility Principle"
date: 2020-08-02 13:01:20 +0300
description: There should never be more than one reason for a class/module to change. # Add post description (optional)
img:  principle.jpeg # Add image post (optional)(optional)
categories: [object-oriented-design]
icon: blogging.png
---

- A computer-programming principle that states that every module, **class or function in a computer program should have responsibility over a single part** of that program's functionality, and **it should encapsulate that part**. 
- All of that module, class or function's services **should be narrowly aligned with that responsibility**.
- The reason it is important to keep a class focused on a single concern is that it **makes the class more robust**.
- SRP help **reducing the effect of changes done** in case of modification to the overall system.
- it gives means **high cohesion**, as well as robustness, which together reduce errors.


```java
/*
 We can clearly make out that class have more than one reponsiblity,
    manipulating the text and printing the text
 */
public class TextManipulator {
    private String text;

    public TextManipulator(String text) {
        this.text = text;
    }

    public String getText() {
        return text;
    }

    public void appendText(String newText) {
        text = text.concat(newText);
    }
    
    public String findWordAndReplace(String word, String replacementWord) {
        if (text.contains(word)) {
            text = text.replace(word, replacementWord);
        }
        return text;
    }
    
    public String findWordAndDelete(String word) {
        if (text.contains(word)) {
            text = text.replace(word, "");
        }
        return text;
    }

    public void printText() {
        System.out.println(textManipulator.getText());
    }
}
```
**Refactoring the code, we can decompose the class by extracting printing related methods**
```java
public class TextPrinter {
    TextManipulator textManipulator;

    public TextPrinter(TextManipulator textManipulator) {
        this.textManipulator = textManipulator;
    }

    public void printText() {
        System.out.println(textManipulator.getText());
    }

    public void printOutEachWordOfText() {
        System.out.println(Arrays.toString(textManipulator.getText().split(" ")));
    }

    public void printRangeOfCharacters(int startingIndex, int endIndex) {
        System.out.println(
            textManipulator.getText().substring(startingIndex, endIndex)
            );
    }
}
```