---
layout: post
title: "Code Smells"
date: 2020-08-11 13:01:20 +0300
description: Items which are included in Code Smells. # Add post description (optional)
img:  clean-code.png # Add image post (optional)(optional)
categories: [clean-code]
icon: blogging.png
---

### What is included in Code Smells
- #### Rigidity
The software is difficult to change. If a small change causes a cascade of subsequent changes, it is rigid.

- #### Fragility
Said to be Fragile if a software breaks in many places due to a single change

- #### Immobility
A software component/library/module is said to be immobile, If You cannot reuse parts of the code in other projects because of involved risks and high effort.

- #### Viscosity of Design
 Viscosity refers to the ease at which a developer can add design-preserving code to a system. If it is easy to add new code to the program while maintaining the design, then the program has low viscosity. 

- #### Viscosity of Environment
Building, testing and other tasks take a long time. Therefore, these activities are not executed properly by everyone and could even increase technical debt.

- #### Needless Complexity
If a design contains elements that are currently not useful. The added complexity makes the code harder to comprehend. Therefore, extending and changing the code results in higher effort than necessary.

- #### Needless Repetition
If a Code contains exact code duplications or design duplicates (doing the same thing in a different way). Making a change to a duplicated piece of code is more expensive and more error-prone because the change has to be made in several places with the risk that one place is not changed accordingly.

- #### Opacity
If a code is hard to understand. Therefore, any change takes additional time to first reengineer the code and is more likely to result in defects due to not understanding the side effects