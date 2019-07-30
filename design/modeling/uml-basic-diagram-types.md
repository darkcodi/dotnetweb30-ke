# UML: Basic Diagram Types

{% hint style="success" %}
The **Unified Modeling Language** \(UML\) is a family of graphical notations, backed by single metamodel, that help in describing and designing software systems, particularly software systems built using the object-oriented \(OO\) style.
{% endhint %}

![](../../.gitbook/assets/uml-diagram-types.png)

#### **Structure Diagrams**

* Class Diagram
* Component Diagram
* Deployment Diagram
* Object Diagram
* Package Diagram
* Profile Diagram
* Composite Structure Diagram

#### **Behavioral Diagrams**

* Use Case Diagram
* Activity Diagram
* State Machine Diagram
* Interaction Diagram
  * Sequence Diagram
  * Communication Diagram
  * Interaction Overview Diagram
  * Timing Diagram

## **Structure Diagrams**

### Class Diagram

Describes the structure of a system by showing the **system's classes, their attributes, operations** \(or methods\), and the **relationships** among objects.

![](../../.gitbook/assets/image%20%2868%29.png)

### Component Diagram

It does not describe the functionality of the system but it describes **the components** used to make those functionalities.

![](../../.gitbook/assets/image%20%28138%29.png)

### Deployment Diagram

Represents the **deployment view of a system**. It consists of nodes. Nodes are nothing but physical hardware used to deploy the application.

![](../../.gitbook/assets/image%20%28168%29.png)

### Object Diagram

Object diagrams represent an instance of a class diagram. Object diagrams also represent the static view of a system but this static view is **a snapshot of the system at a particular moment**.

![](../../.gitbook/assets/image%20%28126%29.png)

### Package Diagram

Describes the **dependencies between the packages** that make up a model.

![](../../.gitbook/assets/image%20%28132%29.png)

### Profile Diagram

Operates at the metamodel level to show stereotypes as classes with the `«stereotype»` stereotype, and **profiles as packages** with the `«profile»` stereotype.

![](../../.gitbook/assets/image%20%2896%29.png)

### Composite Structure Diagram

Shows the internal structure of a class and the collaborations that this structure makes possible.

![](../../.gitbook/assets/image%20%2895%29.png)

## **Behavioral Diagrams**

### Use Case Diagram

A representation of a **user's interaction with the system** that shows the relationship between the user and the different use cases in which the user is involved.

![](../../.gitbook/assets/image%20%2835%29.png)

### Activity Diagram

Graphical representations of workflows of stepwise activities and actions with support for choice, iteration and concurrency.

![](../../.gitbook/assets/image%20%28143%29.png)

### State Machine Diagram

Describes **the behavior of system**. This behavior is analyzed and represented as a series of events that can occur in one or more possible states.

![](../../.gitbook/assets/image%20%28141%29.png)

### Sequence diagram

Shows object interactions arranged in time sequence. It depicts the objects and classes involved in the scenario and the sequence of messages exchanged between the objects needed to carry out the functionality of the scenario.

![](../../.gitbook/assets/image%20%2894%29.png)

### Communication Diagram

Models the **interactions between objects or parts** in terms of sequenced messages. Communication diagrams represent a combination of information taken from _Class_, _Sequence_, and _Use Case Diagrams_ describing both the static structure and dynamic behavior of a system.

![](../../.gitbook/assets/image%20%28121%29.png)

### Interaction overview diagram

It's similar to the _activity diagram_, in that both visualize a sequence of activities. The difference is that, for an interaction overview, each individual activity is pictured as a frame which can contain a nested interaction diagram.

![](../../.gitbook/assets/image%20%28123%29.png)

### Timing Diagram

Changes from one **state** to another are represented by **a change in the level of the lifeline**. For the period of time when the object is a given state, the timeline runs parallel to that state.

![](../../.gitbook/assets/image%20%2884%29.png)

Alternative notation:

![](../../.gitbook/assets/image%20%28166%29.png)

