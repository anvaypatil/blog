---
layout: post
title: "Code Code: System Design"
date: 2020-08-12 15:01:20 +0300
description: How should we do system design
img:  clean-code.png # Add image post (optional)(optional)
categories: [clean-code]
icon: blogging.png
---

- ### Keep Configurable Data at High Levels
If you have a constant such as default or configuration value that is known and expected at a high level of abstraction, do not bury it in a low-level function. Expose it as an argument to the low-level function called from the high-level function.

- ### Don't be Arbitary
Have a reason for the way you structure your code, and make sure that reason is communicated by the structure of the code. If a structure appears arbitrary, others will feel empowered to change it.

- ### Be Precise
When you make a decision in your code, make sure you make it precisely. Know why you have made it and how you will deal with any exceptions.

- ### Structure over Convention
Enforce design decisions with structure over convention. Naming conventions are good, but they are inferior to structures that force compliance.

- ### Prefer Polymorphism To If/Else or Switch/Case
“ONE SWITCH”: There may be no more than one switch statement for a given type of selection. The cases in that switch statement must create polymorphic objects that take the place of other such switch statements in the rest of the system

- ### Symmetry / Analogy
Favour symmetric designs (e.g. Load – Save) and designs that follow analogies.

- ### Seperate Multi-Threading Code
Do not mix code that handles multi-threading aspects with the rest of the code. Separate them into different classes.

- ### Ensure for not Misplacing Responsiblity
Don't Misplace responsiblity not matter if it could yeild any shorter win.

- ### Ensure we don't code at wrong level of Abstraction
Ensure for not putting a functionality at wrong level of abstraction, e.g. a PercentageFull property on a generic interface IStack<T>.

- ### Don't define Fields which are not defining State
Fields holding data that does not belong to the state of the instance but are used to hold temporary data. Use local variables or extract to a class abstracting the performed action.

- ### Ensure for Over Configurablity
Prevent configuration just for the sake of it – or because nobody can decide how it should be. Otherwise, this will result in overly complex, unstable systems.

- ### Ensure of not putting redundent Micro Layers
Do not just add functionality on top, but simplify overall