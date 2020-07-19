---
layout: post
title: "Chain of Responsibility - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

🔗 Chain of Responsibility
-----------------------
It helps building a chain of objects. Request enters from one end and keeps going from object to object till it finds the suitable handler.

```java
@FunctionalInterface
public interface Logger {
    public enum LogLevel {
        INFO, DEBUG, WARNING, ERROR, FUNCTIONAL_MESSAGE, FUNCTIONAL_ERROR;

        public static LogLevel[] all() {
            return values();
        }
    }
    abstract void message(String msg, LogLevel severity);
    default Logger appendNext(Logger nextLogger) {
        return (msg, severity) -> {
            message(msg, severity);
            nextLogger.message(msg, severity);
        };
    }
    static Logger writeLogger(LogLevel[] levels, Consumer<String> stringConsumer) {
        EnumSet<LogLevel> set = EnumSet.copyOf(Arrays.asList(levels));
        return (msg, severity) -> {
            if (set.contains(severity)) {
                stringConsumer.accept(msg);
            }
        };
    }
    static Logger consoleLogger(LogLevel... levels) {
        return writeLogger(
                levels, msg -> System.err.println("Writing to console: " + msg)
            );
    }
    static Logger emailLogger(LogLevel... levels) {
        return writeLogger(
                levels, msg -> System.err.println("Sending via email: " + msg)
            );
    }
    static Logger fileLogger(LogLevel... levels) {
        return writeLogger(
                levels, msg -> System.err.println("Writing to Log File: " + msg)
            );
    }
    public static void main(String[] args) {
        // Build an immutable chain of responsibility
        Logger logger = consoleLogger(LogLevel.all())
                .appendNext(
                    emailLogger(LogLevel.FUNCTIONAL_MESSAGE, LogLevel.FUNCTIONAL_ERROR)
                ).appendNext(fileLogger(LogLevel.WARNING, LogLevel.ERROR));

        // Handled by consoleLogger since the console has a LogLevel of all
        logger.message("Entering function ProcessOrder().", LogLevel.DEBUG);
        logger.message("Order record retrieved.", LogLevel.INFO);

        // Handled by consoleLogger and emailLogger since emailLogger implements 
        // Functional_Error & Functional_Error
        logger.message(
            "Unable to Process Order ORD1 Dated D1", LogLevel.FUNCTIONAL_ERROR
        );
        logger.message("Order Dispatched.", LogLevel.FUNCTIONAL_MESSAGE);

        // Handled by consoleLogger and fileLogger since fileLogger implements 
        // Warning & Error
        logger.message("Customer Address missing in Branch.", LogLevel.WARNING);
        logger.message("Customer Address missing in Organization.", LogLevel.ERROR);
    }
}
```
