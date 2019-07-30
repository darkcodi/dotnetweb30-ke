# Types vs. Classes

{% hint style="success" %}
A **type** is an abstract interface. Types generally represent nouns, such as a person, place or thing, or something nominalized.
{% endhint %}

{% hint style="success" %}
A **class** is a concrete data structure and collection of subroutines. It represents an implementation of the type.
{% endhint %}

An object's **class** defines how the object is implemented .The class defines object's internal state and the implementation of its operations.

In contrast, an object's **type** only refers to its interface - a set of requests to which it can respond.

An object can have many types, and objects of different classes can have the same type.

#### Example

For example, one might implement the type Stack with two classes: SmallStack \(fast for small stacks, but scales poorly\) and ScalableStack \(scales well but high overhead for small stacks\).

