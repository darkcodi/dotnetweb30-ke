# Modularity

The act of **partitioning** a program into individual components can reduce its complexity to some degree. Although partitioning a program is helpful for this reason, a more powerful justification for partitioning a program is that it creates a number of well-defined, documented boundaries within the program.

![](https://lh3.googleusercontent.com/xmdOYJLbn-VRUy08mNNCo6xHwlp19hILTlryBCJmG_RLnkthDJ2j1vQcGjKiAo8yZCylulDoNw3YQzKvKrfUn4O3SX9__vvs4mb9fDDQyqqVjGNaiPb9mL6_PszIOcSGIUf8ytFpruDsx0Gozw)

{% hint style="success" %}
**Modularization** consists of dividing a program into modules which can be compiled separately, but which have connections with other modules.
{% endhint %}

Most languages that support the module as a separate concept also distinguish between the interface of a module and its implementation. Thus, it is fair to say that modularity and encapsulation go hand in hand.

In some languages, such as Smalltalk, there is no concept of a module, so the class forms the only physical unit of decomposition. Java has packages that contain classes. In many other languages, including Object Pascal, C++, and Ada, the module is a separate language construct and therefore warrants a separate set of design decisions. Especially for larger applications, in which we may have many hundreds of classes, the use of modules is essential to help manage complexity.

