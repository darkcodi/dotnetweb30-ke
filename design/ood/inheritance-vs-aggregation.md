---
description: >-
  TODO: Rework to
  https://www.codeproject.com/Articles/330447/Understanding-Association-Aggregation-and-Composit
---

# Inheritance vs Aggregation

_Abstraction_ is a good thing, but in all except the most trivial applications, we may find many more different abstractions than we can comprehend at one time. _Encapsulation_ helps manage this complexity by hiding the inside view of our abstractions. _Modularity_ helps also, by giving us a way to cluster logically related abstractions. Still, this is not enough. A set of abstractions often forms a **hierarchy**, and by identifying these hierarchies in our design, we greatly simplify our understanding of the problem.

{% hint style="info" %}
Hierarchy is a ranking or ordering of abstractions.
{% endhint %}

#### Examples of hierarchy:

* Single Inheritance
* Multiple Inheritance
* Aggregation

### **Single Inheritance**

{% hint style="success" %}
**Inheritance** defines a relationship among classes, wherein one class shares the structure or behavior defined in one or more classes. Inheritance thus represents a hierarchy of abstractions, in which a subclass inherits from one or more superclasses.
{% endhint %}

Typically, a subclass **augments or redefines** the existing structure and behavior of its superclasses.

Semantically, inheritance denotes an **“is a”** relationship.

### **Multiple Inheritance**

A better way to express our abstractions and thereby **avoid redundancy** is to use multiple inheritance. It's conceptually straightforward, but it does introduce some practical complexities for programming languages.

#### Languages must address two issues:

* **Clashes among names from different superclasses.** Clashes will occur when two or more superclasses provide a field or operation with the same name or signature as a peer superclass.
* **Repeated inheritance.** Repeated inheritance occurs when two or more peer superclasses share a common superclass.

### Aggregation

Whereas these “is a” hierarchies denote generalization/specialization relationships, **“part of”** hierarchies describe aggregation relationships.

For example, consider the abstraction of a garden. We can contend that a garden consists of a collection of plants together with a growing plan. In other words, plants are “part of” the garden, and the growing plan is “part of” the garden. This “part of” relationship is known as **aggregation**.

