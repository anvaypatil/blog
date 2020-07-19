---
layout: post
title: "Visitor - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

🚜 Visitor
---------------
Represents an operation to be performed on the elements of an object structure / Visitor lets you define a new operation without changing the classes of the elements on which it operates.

```java
interface Element {
    void accept(Visitor v);
}
class Foo implements Element {
    public void accept(Visitor v) {
        v.visit(this);
    }
    public String getFoo() {
        return "Foo";
    }
}
class Bar implements Element {
    public void accept( Visitor v ) {
        v.visit( this );
    }
    public String getBar() {
        return "Bar";
    }
}
class Baz implements Element {
    public void accept(Visitor v) {
        v.visit(this);
    }
    public String getBaz) {
        return "Baz";
    }
}

interface Visitor {
    void visit(Foo foo);
    void visit(Bar bar);
    void visit(Baz baz);
}
class UpVisitor implements Visitor {
    public void visit(Foo foo) {
        System.out.println("do Up on " + foo.getFoo());
    }
    public void visit(Bar bar) {
        System.out.println("do Up on " + bar.getBar());
    }
    public void visit(Baz baz) {
        System.out.println( "do Up on " + baz.getBaz() );
    }
}
class DownVisitor implements Visitor {
    public void visit(Foo foo) {
        System.out.println("do Down on " + foo.getFoo());
    }
    public void visit(Bar bar) {
        System.out.println("do Down on " + bar.getBar());
    }
    public void visit(Baz baz ) {
        System.out.println("do Down on " + baz.getBaz());
    }
}
public class VisitorDemo {
    public static void main( String[] args ) {
        Element[] list = {new Foo(), new Bar(), new Baz()};
        UpVisitor up = new UpVisitor();
        DownVisitor down = new DownVisitor();
        for (Element element : list) {
            element.accept(up);
        }
        for (Element element : list) {
            element.accept(down);
        }
    }
}
```
