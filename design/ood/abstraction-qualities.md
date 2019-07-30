# Abstraction Qualities \(cohesion, coupling, etc\)

#### Quality metrics of an abstraction:

* Coupling
* Cohesion
* Sufficiency
* Completeness
* Primitiveness

### Coupling

{% hint style="success" %}
**Coupling** is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are; the strength of the relationships between modules.
{% endhint %}

_Coupling_ is usually contrasted with _cohesion_. **Low coupling** often correlates with **high cohesion**, and vice versa. Low coupling is often a sign of a well-structured computer system and a good design, and when combined with high cohesion, supports the general goals of high readability and maintainability.

#### **Types of coupling in Procedural programming:**

* Content coupling \(high\) \(one module uses the code of other module\)
* Common coupling \(several modules have access to the same global data\)
* External coupling \(two modules share an externally imposed data format, communication protocol, or device interface\)
* Control coupling \(one module controlling the flow of another, by passing it information on what to do\)
* Stamp coupling \(modules share a composite data structure and use only parts of it, possibly different parts\)
* Data coupling \(modules share data through, for example, parameters\)

#### **Types of coupling in Object-Oriented programming:**

* Subclass coupling \(inheritance\)
* Temporal coupling \(when two actions are bundled together into one module just because they happen to occur at the same time\)

### Cohesion

{% hint style="success" %}
**Cohesion** refers to the degree to which the elements inside a module belong together. It is a measure of the strength of relationship between the class’s methods and data themselves.
{% endhint %}

#### **Cohesion is increased if:**

* The functionalities embedded in a class, accessed through its methods, have much in common.
* Methods carry out a small number of related activities, by avoiding coarsely grained or unrelated sets of data

### **Sufficiency**

{% hint style="success" %}
By **sufficient**, we mean that the class or module captures enough characteristics of the abstraction to permit meaningful and efficient interaction.
{% endhint %}

For example, if we are designing the class _Set_, it is wise to include an operation that removes an item from the set, but our wisdom is futile if we neglect an operation that adds an item.

### Completeness

{% hint style="success" %}
By **complete**, we mean that the interface of the class or module captures all of the meaningful characteristics of the abstraction.
{% endhint %}

Whereas _sufficiency_ implies a minimal interface, a _complete_ interface is one that covers all aspects of the abstraction.

A complete class or module is thus one whose interface is general enough to be commonlyusable to anyclient.

{% hint style="info" %}
Completeness is a subjective matter, and it can be overdone.
{% endhint %}

### **Primitiveness**

{% hint style="success" %}
**Primitive** operations are those that can be efficiently implemented only if given access to the underlying representation of the abstraction.
{% endhint %}

An operation is indisputably primitive if we can implement it only through access to the underlying representation. An operation that could be implemented on top of existing primitive operations, but at the cost of significantly more computational resources, is also a candidate for inclusion as a primitive operation.

