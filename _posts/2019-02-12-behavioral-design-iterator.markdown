---
layout: post
title: "Iterator - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

➿ Iterator
------------------
Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

```java
interface IIterator {
    public boolean hasNext();
    public Object next();
}

interface IContainer {
    public IIterator createIterator();
}

class Collection implements IContainer {
    private String m_titles[] = {"0", "1", "2", "3", "4"};
    public IIterator createIterator() {
        ItemIterator result = new ItemIterator();
        return result;
    }
    private class ItemIterator implements IIterator {
        private int m_position = 0;
        public boolean hasNext() {
            return (m_position < m_titles.length)
        }
        public Object next() {
            if (this.hasNext()) {
                return m_titles[m_position++];
            }
            return null;
        }
    }
}
```
