---
layout: post
title: "Command - Behavioral Design Pattern"
date: 2019-02-12 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: behavioral-pattern
icon: blogging.png
---

👮 Command
------------------
Allows you to encapsulate actions in objects. The key idea behind this pattern is to provide the means to decouple client from receiver.
```java

/** The Command interface */
interface Command {
    void execute();
}

/** The Invoker class */
class Switch {
    private final HashMap<String, Command> commandMap = new HashMap<>();
    public void register(String commandName, Command command) {
        commandMap.put(commandName, command);
    }
    public void execute(String commandName) {
        Command command = commandMap.get(commandName);
        if (command == null) {
            throw new IllegalStateException("no command registered for " + commandName);
        }
        command.execute();
    }
}

/** The Receiver class */
class Light {
    public void turnOn() {
        System.out.println("The light is on");
    }
    public void turnOff() {
        System.out.println("The light is off");
    }
}

/** The Command for turning on the light - ConcreteCommand #1 */
class SwitchOnCommand implements Command {
    private final Light light;
    public SwitchOnCommand(Light light) {
        this.light = light;
    }
    @Override // Command
    public void execute() {
        light.turnOn();
    }
}

/** The Command for turning off the light - ConcreteCommand #2 */
class SwitchOffCommand implements Command {
    private final Light light;
    public SwitchOffCommand(Light light) {
        this.light = light;
    }
    @Override // Command
    public void execute() {
        light.turnOff();
    }
}
public class CommandDemo {
    public static void main(final String[] arguments) {
        Light lamp = new Light();

        Command switchOn = lamp::turnOn;
        Command switchOff = lamp::turnOff;

        Switch mySwitch = new Switch();
        mySwitch.register("on", switchOn);
        mySwitch.register("off", switchOff);

        mySwitch.execute("on");
        mySwitch.execute("off");
    }
}
```
