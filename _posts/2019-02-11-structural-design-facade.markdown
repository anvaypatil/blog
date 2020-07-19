---
layout: post
title: "Facade - Structural Design Pattern"
date: 2019-02-11 20:00:00 +0530
description: Notes about design patterns. # Add post description (optional)
img: design-pattern.jpg # Add image post (optional)
tags: design-patterns
categories: structural-pattern
icon: blogging.png
---
📦 Facade
----------
Facade pattern provides a simplified interface to a complex subsystem.

Example:
```java
/* Complex parts */
class CPU {
    public void freeze() { ... }
    public void jump(long position) { ... }
    public void execute() { ... }
}
class HardDrive {
    public byte[] read(long lba, int size) { ... }
}
class Memory {
    public void load(long position, byte[] data) { ... }
}
/* Facade */
class ComputerFacade {
    private final CPU processor;
    private final Memory ram;
    private final HardDrive hd;
    public ComputerFacade() {
        this.processor = new CPU();
        this.ram = new Memory();
        this.hd = new HardDrive();
    }
    public void start() {
        processor.freeze();
        ram.load(BOOT_ADDRESS, hd.read(BOOT_SECTOR, SECTOR_SIZE));
        processor.jump(BOOT_ADDRESS);
        processor.execute();
    }
}
/* Client */
class You {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.start();
    }
}
```