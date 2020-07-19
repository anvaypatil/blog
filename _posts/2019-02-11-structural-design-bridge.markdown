---
layout: post
title: "Bridge - Structural Design Pattern"
date: 2019-02-11 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: structural-pattern
icon: blogging.png
---
🚡 Bridge
-----------
Bridge pattern is about preferring composition over inheritance. Implementation details are pushed from a hierarchy to another object with a separate hierarchy. 
>Decouple an abstraction from its implementation so that the two can vary independently.

Example:
![With and without the bridge pattern]({{site.baseurl}}/assets/img/bridge_pattern.png){:class="img-responsive"}
```java
interface WebPage {
    public void setTheme(Theme theme);
    public String getContent();
}
class AboutPage implements WebPage {
    protected Theme theme;
    public void setTheme(Theme theme) {
        this.theme = theme;
    }
    public String getContent() {
        return "About page in "+ this.theme.getColor();
    }
}
class CareersPage implements WebPage {
    protected Theme theme;
    public void setTheme(Theme theme) {
        this.theme = theme;
    }
    public String getContent() {
        return "Careers page in "+ this.theme.getColor();
    }
}
interface Theme {
    public Color getColor();
}
class DarkTheme implements Theme {
    public Color getColor() {
        return Color.DarkBlack;
    }
}
class LightTheme implements Theme {
    public Color getColor() {
        return Color.OffWhite;
    }
}
class AquaTheme implements Theme{
    public Color getColor() {
        return Color.LightBlue;
    }
}
Theme darkTheme = new DarkTheme();
AboutPage about = new AboutPage(darkTheme);
CareersPage careers = new CareersPage(darkTheme);
```
**When to use?** When we want to decouple an abstraction from its implementation so that the two can vary independently.
