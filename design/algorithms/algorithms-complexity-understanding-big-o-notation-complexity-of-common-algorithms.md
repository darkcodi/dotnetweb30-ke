# Algorithms complexity \(understanding, big O notation, complexity of common algorithms\)

{% hint style="success" %}
**Big O** notation is a mathematical notation that describes the **limiting behavior** of a function when the argument tends towards a particular **value or infinity**. It is a member of a family of notations invented by Paul Bachmann, Edmund Landau, and others, collectively called Bachmann–Landau notation or asymptotic notation.
{% endhint %}

{% hint style="success" %}
**Big O**  is simplified analysis of an algorithm's efficiency

* complexity in terms ofinput size, **n**
* machine-independent
* basic computer steps
* time & space
{% endhint %}

![](../../.gitbook/assets/image%20%28144%29.png)

![](https://softserveke.firebaseapp.com/assets/img/common-data-structure.c22ff6e5.png)

**Types of measurements**

* worst-case
* best-case
* average-case

**Big O notation** is the language we use for talking about how long an algorithm takes to run. It's how we compare the efficiency of different approaches to a problem.

It's like math except it's an _**awesome**_, _**not-boring**_ kind of math where you get to wave your hands through the details and just focus on what's basically happening.

With big O notation we express the runtime in terms of—brace yourself—how quickly it grows relative to the input, as the input gets arbitrarily large.

Let's break that down:

* **how quickly the runtime grows** — it's hard to pin down the exact runtime of an algorithm. It depends on the speed of the processor, what else the computer is running, etc. So instead of talking about the runtime directly, we use big O notation to talk about how quickly the runtime grows.
* **relative to the input** - if we were measuring our runtime directly, we could express our speed in seconds. Since we're measuring how quickly our runtime grows, we need to express our speed in terms of...something else. With Big O notation, we use the size of the input, which we call **"n."** So we can say things like the runtime grows "on the order of the size of the input" \(O\(n\)\) or "on the order of the square of the size of the input" \(O\(n2\)\)
* **as the input gets arbitrarily large** - our algorithm may have steps that seem expensive when nn is small but are eclipsed eventually by other steps as nn gets huge. For big O analysis, we care most about the stuff that grows fastest as the input grows, because everything else is quickly eclipsed as nn gets very large. \(If you know what an asymptote is, you might see why "big O analysis" is sometimes called "asymptotic analysis."\)

![](../../.gitbook/assets/image%20%28150%29.png)

![](../../.gitbook/assets/image%20%287%29.png)

![](../../.gitbook/assets/image%20%28112%29.png)

