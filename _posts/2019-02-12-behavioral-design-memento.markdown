---
layout: post
title: "Memento - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

🗃 Momento
------------------
Memento pattern is about capturing and storing the current state of an object in a manner that it can be restored later on in a smooth manner.

```java
public class EditorMemento {
    private String _content = null;
    EditorMemento(String content) {
        this._content = content
    }
    public String getContent() {
        return this._content;
    }
}
class Editor {
    private String _content = null;
    constructor(){
        this._content = "";
    }
    public void type(String words) {
        this._content = this._content + " " + words;
    }
    public String getContent() {
        return this._content;
    }
    public EditorMemento save() {
        return new EditorMemento(this._content);
    }    
   public void restore(memento) {
        this._content = memento.getContent();
    }
}

Editor editor = new Editor();
// Type some stuff
editor.type("This is the first sentence.");
editor.type("This is second.");
// Save the state to restore to : This is the first sentence. This is second.
EditorMomento saved = editor.save();
// Type some more
editor.type("And this is third.");
// Output: Content before Saving
System.out.println(editor.getContent()); 
// This is the first sentence. This is second. And this is third.
// Restoring to last saved state
editor.restore(saved);
System.out.println(editor.getContent());
// This is the first sentence. This is second.

```

