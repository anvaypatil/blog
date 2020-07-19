---
layout: post
title: "Factory Method - Creational Design Pattern"
date: 2019-02-10 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: creational-pattern
icon: blogging.png
---
🏭 Factory Method
---------------
It provides a way to delegate the instantiation logic to child classes.
Example:
```java
interface Interviewer {
   public function takeInterview();
}
class Developer implements Interviewer {
    public function askQuestions() {
        // 'Ask Programming Question!';
    }
}
class CommunityExecutive implements Interviewer {
    public function askQuestions() {
        // 'Ask about Community Building!';
    }
}
abstract class HiringManager {
    abstract protected makeInterviewer();
    public function takeInterviews() {
        Interviewer interviewer = this.makeInterviewer();
        interviewer.askQuestions();
    }
}
// any child can extend it and provide the required interviewer
class DevelopmentManager extends HiringManager {
    protected Interviewer makeInterviewer() {
        return new Developer();
    }
}
class MarketingManager extends HiringManager {
    protected Interviewer makeInterviewer() {
        return new CommunityExecutive();
    }
}
```
**When to Use?** Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn't know what exact sub-class it might need.