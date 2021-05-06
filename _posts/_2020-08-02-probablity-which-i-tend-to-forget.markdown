---
layout: post
title: "Probablity Notes"
date: 2020-08-02 13:01:20 +0300
description: Probablity which i tend forget. # Add post description (optional)
img:  blog.jpeg # Add image post (optional)
categories: design-&-architecture
icon: blogging.png
---
### Sample Space
Set of All outcomes that you can have

Example:  
- Coin Toss = {Head, Tail}
- Dice = {1,2,3,4,5,6}

### Random Variable
Random Variable 'X' is the variable that hold's the outcome.

P<sub>event=X</sub> = `(Number of favorable outcomes) / (Total number of possible outcomes)`

Example:
- P<sub>x</sub>[x=Head]=`1/2`

### Joint Probablity
Using two random variable X1 and X2

Example:
- For coin, P<sub>x1 and x2</sub>[x1=Head,x2=Tail]=`1/2*1/2 = 1/4`
- For Dice, P<sub>two-dice</sub>[x=1,y=2 or x=2,y=1]=`1/6*1/6 + 1/6*1/6 = 1/18`
- For Dice, P<sub>two-dice</sub>[x+y<=3]<br/>
`=(x=1 and y=1) or (x=1 and y=2) or (x=2 and y=1)`<br/>
`=(x=1 and (y=1 or y=2)) or (x=2 and y=1)`<br/>
`=1/12`

### Probablity Distribution
Defines the probablity of every outcome in same-space. Sum of all the probablites over sample space is equal to one.

For Coin: 
- P<sub>x</sub>[x=Head]=`1/2` 
- P<sub>x</sub>[x=Tail]=`1/2`

### Discrete Distribution
Sample space is discrete
 - Uniform Distribution: All outcomes are equally likely.
 - 
### Continuous Distribution
Sample space is continuous

