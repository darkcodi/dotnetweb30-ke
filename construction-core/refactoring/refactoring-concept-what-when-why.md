# Refactoring Concept \(what/when/why\)

### what

{% hint style="success" %}
Refactoring \(noun\): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior
{% endhint %}

{% hint style="success" %}
Refactoring \(verb\): to restructure software by applying a series of refactorings without changing its observable behavior.
{% endhint %}

Refactoring is all about applying small behavior preserving steps and making a big change by stringing together a sequence of these behavior preserving steps. Each individual refactoring is either pretty small itself or a combination of small steps. As a result, when I’m refactoring, my code doesn’t spend much time in a broken state, allowing me to stop at any moment even if I haven’t finished.

{% hint style="danger" %}
If someone says their code was broken for a couple of days while they are refactoring, you can be pretty sure they were not refactoring.
{% endhint %}

Refactoring is always done to make the code “easier to understand and cheaper to modify.

### when

{% hint style="success" %}
The Rule of Three

Here’s a guideline Don Roberts gave me: The first time you do something, you just do it. The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway. The third time you do something similar, you refactor.

Or for those who like baseball: Three strikes, then you refactor.
{% endhint %}

* **Preparatory Refactoring** — Making It Easier to Add a Feature

  > the best time to refactor is just before I need to add a new feature to the code base. As I do this, I look at the existing code and, often, see that if it were structured a little differently, my work would be much easier.

* **Comprehension Refactoring**: Making Code Easier to Understand

  > before I can change some code, I need to understand what it does.

* **Litter-Pickup Refactoring**

  > a variation of comprehension refactoring is when I understand what the code is doing, but realize that it’s doing it badly.

The examples above—preparatory, comprehension, litter-pickup refactoring — are all opportunistic.

> You have to refactor when you run into ugly code—but excellent code needs plenty of refactoring too.

* **Long-Term Refactoring**
* **Refactoring in a Code Review**

### why

* Refactoring Improves the Design of Software
* Refactoring Makes Software Easier to Understand
* Refactoring Helps Me Find Bugs
* Refactoring Helps Me Program Faster

