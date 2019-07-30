# Smells Catalog and possible re-factorings

### Duplicated Code

If you see the same code structure in more than one place, you can be sure that your program will be better if you find a way to unify them. The simplest duplicated code problem is when you have the same expression in two methods of the **same class**. Then all you have to do is **Extract Method** and invoke the code from both places. 

Another common duplication problem is when you have the **same expression** in **two sibling subclasses**. You can eliminate this duplication by using **Extract Method** **in both classes then Pull Up Field**. 

If the code is similar but not the same, you need to use **Extract Method to separate the similar bits from the different bits**. 

If the methods do the same thing with a different algorithm, you can choose the clearer of the two algorithms and **use Substitute Algorithm**. 

If you have duplicated code in two unrelated classes, consider using **Extract Class** in one class and then use the new component in the other. Another possibility is that the method really belongs only in one of the classes and should be invoked by the other class or that the method belongs in a third class that should be referred to by both of the original classes. You have to decide where the method makes sense and ensure it is there and nowhere else.

### Long Method

The object programs that live best and longest are those with short methods. The key here is not method length but the semantic distance between what the method does and how it does it. Ninety-nine percent of the time, all you have to do to shorten a method is Extract Method. Find parts of the method that seem to go nicely together and make a new method. If you have a method with lots of parameters and temporary variables, these elements get in the way of extracting methods. If you try to use Extract Method, you end up passing so many of the parameters and temporary variables as parameters to the extracted method that the result is scarcely more readable than the original. You can often use Replace Temp with Query to eliminate the temps.

Long lists of parameters can be slimmed down with Introduce Parameter Object and Preserve Whole Object. If you've tried that, and you still have too many temps and parameters, it's time to get out the heavy artillery: **Replace Method with Method Object**.

**A good technique is to look for comments**. They often signal this kind of semantic distance. A block of code with a comment that tells you what it is doing can be replaced by a method whose name is based on the comment.

### Large Class

When a class is trying to do too much, it often shows up as too many instance variables. When a class has too many instance variables, duplicated code cannot be far behind.

You can **Extract Class** to bundle a number of the variables. Choose variables to go together in the component that makes sense for each. If the component makes sense as a subclass, you'll find **Extract Subclass** often is easier.

Sometimes a class does not use all of its instance variables all of the time. If so, you may be able to Extract Class or Extract Subclass many times.

As with a class with a huge wad of variables, the usual solution for a class with too much code is either to Extract Class or Extract Subclass. A useful trick is to determine how clients use the class and to use **Extract Interface** for each of these uses. That may give you ideas on how you can further break up the class.

### Long Parameter List

Long parameter lists are hard to understand, because they become inconsistent and difficult to use, and because you are forever changing them as you need more data. Most changes are removed by passing objects because you are much more likely to need to make only a couple of requests to get at a new piece of data.

**Use Replace Parameter with Method** when you can get the data in one parameter by making a request of an object you already know about. This object might be a field or it might be another 66 parameter. Use **Preserve Whole Object** to take a bunch of data gleaned from an object and replace it with the object itself. If you have several data items with no logical object, use **Introduce Parameter Object**.

### Divergent Change

Divergent change occurs when one class is commonly changed in different ways for different reasons. If you look at a class and say, "Well, I will have to change these three methods every time I get a new database; I have to change these four methods every time there is a new financial instrument," you likely have a situation in which two objects are better than one. That way each object is changed only as a result of one kind of change. To clean this up you identify everything that changes for a particular cause and use **Extract Class** to put them all together.

### Shotgun Surgery

Shotgun surgery is similar to divergent change but is the opposite. You whiff this when every time you make a kind of change, you have to make a lot of little changes to a lot of different classes. When the changes are all over the place, they are hard to find, and it's easy to miss an important change.

In this case you want to use **Move Method** and **Move Field** to put all the changes into a single class. If no current class looks like a good candidate, create one. Often you can use Inline Class to bring a whole bunch of behavior together. You get a small dose of divergent change, but you can easily deal with that.

**Divergent change is one class that suffers many kinds of changes, and shotgun surgery is one change that alters many classes. Either way you want to arrange things so that, ideally, there is a one-to-one link between common changes and classes.**

### Feature Envy

The whole point of objects is that they are a technique to package data with the processes used on that data. A classic smell is a method that seems more interested in a class other than the one it actually is in. The most common focus of the envy is the data. We've lost count of the times we've seen a method that invokes half-a-dozen getting methods on another object to calculate some value. Fortunately the cure is obvious, the method clearly wants to be elsewhere, so you use **Move Method** to get it there. Sometimes only part of the method suffers from envy; in that case use **Extract Method** on the jealous bit and **Move Method** to give it a dream home.

### Data Clumps

Data items tend to be like children; they enjoy hanging around in groups together. Often you'll see the same three or four data items together in lots of places: fields in a couple of classes, parameters in many method signatures. Bunches of data that hang around together really ought to be made into their own object. The first step is to look for where the clumps appear as fields. 

Use **Extract Class** on the fields to turn the clumps into an object. Then turn your attention to method signatures using **Introduce Parameter Object** or **Preserve Whole Object** to slim them down. The immediate benefit is that you can shrink a lot of parameter lists and simplify method calling.

### Primitive Obsession

Primitive types are your building blocks. People new to objects usually are reluctant to use small objects for small tasks, such as money classes that combine number and currency, ranges with an upper and a lower, and special strings such as telephone numbers and ZIP codes. You can move out of the cave into the centrally heated world of objects by using **Replace Data Value with Object** on individual data values. If the data value is a type code, use **Replace Type Code with Class** if the value does not affect behavior. If you have conditionals that depend on the type code, use **Replace Type Code with Subclasses** or **Replace Type Code with State/Strategy**. 

If you have a group of fields that should go together, use **Extract Class**. If you see these primitives in parameter lists, try a civilizing dose of **Introduce Parameter Object**. If you find yourself picking apart an array, use **Replace Array with Object**.

### Switch Statements

Most times you see a switch statement you should consider polymorphism. The issue is where the polymorphism should occur. Often the switch statement switches on a type code. You want the method or class that hosts the type code value. So use **Extract Method** to extract the switch statement and then **Move Method** to get it onto the class where the polymorphism is needed. At that point you have to decide whether to **Replace Type Code with Subclasses** or **Replace Type Code with State/Strategy**. When you have set up the inheritance structure, you can use **Replace Conditional with Polymorphism**. 

If you only have a few cases that affect a single method, and you don't expect them to change, then polymorphism is overkill. In this case **Replace Parameter with Explicit Methods** is a good option. If one of your conditional cases is a null, try **Introduce Null Object**.

### Parallel Inheritance Hierarchies

Parallel inheritance hierarchies is really a special case of shotgun surgery. In this case, every time you make a subclass of one class, you also have to make a subclass of another. You can recognize this smell because the prefixes of the class names in one hierarchy are the same as the prefixes in another hierarchy. 

The general strategy for eliminating the duplication is to make sure that instances of one hierarchy refer to instances of the other. If you use **Move Method** and **Move Field**, the hierarchy on the referring class disappears.

### Lazy Class

Each class you create costs money to maintain and understand. A class that isn't doing enough to pay for itself should be eliminated. Often this might be a class that used to pay its way but has been downsized with refactoring. Or it might be a class that was added because of changes that were planned but not made. Either way, you let the class die with dignity. If you have subclasses that aren't doing enough, try to use **Collapse Hierarchy**. Nearly useless components should be subjected to **Inline Class**.

### Speculative Generality

If all this machinery were being used, it would be worth it. But if it isn't, it isn't. The machinery just gets in the way, so get rid of it.

If you have abstract classes that aren't doing much, use **Collapse Hierarchy**. Unnecessary delegation can be removed with **Inline Class**. Methods with unused parameters should be subject to **Remove Parameter**. Methods named with odd abstract names should be brought down to earth with **Rename Method**.

### Temporary Field

Use **Extract Class** to create a home for the poor orphan variables. Put all the code that concerns the variables into the component. You may also be able to eliminate conditional code by using **Introduce Null Object** to create an alternative component for when the variables aren't valid. 

A common case of temporary field occurs when a complicated algorithm needs several variables. Because the implementer didn't want to pass around a huge parameter list \(who does?\), he put them in fields. But the fields are valid only during the algorithm; in other contexts they are just plain confusing. In this case you can use Extract Class with these variables and the methods that require them.

### Message Chains

You see message chains when a client asks one object for another object, which the client then asks for yet another object, which the client then asks for yet another another object, and so on.

The move to use here is **Hide Delegate**. You can do this at various points in the chain. In principle you can do this to every object in the chain, but doing this often turns every intermediate object into a middle man. Often a better alternative is to see what the resulting object is used for. See whether you can use **Extract Method** to take a piece of the code that uses it and then **Move Method** to push it down the chain. If several clients of one of the objects in the chain want to navigate the rest of the way, add a method to do that.

### Middle Man

One of the prime features of objects is encapsulation—hiding internal details from the rest of the world. Encapsulation often comes with delegation.

You look at a class's interface and find half the methods are delegating to this other class. After a while it is time to use **Remove Middle Man** and talk to the object that really knows what's going on. If only a few methods aren't doing much, use **Inline Method** to inline them into the caller. If there is additional behavior, you can use **Replace Delegation with Inheritance** to turn the middle man into a subclass of the real object. That allows you to extend behavior without chasing all that delegation.

### Inappropriate Intimacy

Sometimes classes become far too intimate and spend too much time delving in each others'private parts. We may not be prudes when it comes to people, but we think our classes should follow strict, puritan rules.

Use **Move Method** and **Move Field** to separate the pieces to reduce the intimacy. See whether you can arrange a **Change Bidirectional Association to Unidirectional**. If the classes do have common interests, use **Extract Class** to put the commonality in a safe place and make honest classes of them. Or use **Hide Delegate** to let another class act as go-between.

Inheritance often can lead to overintimacy. Subclasses are always going to know more about their parents than their parents would like them to know. If it's time to leave home, apply **Replace Delegation with Inheritance**.

### Alternative Classes with Different Interfaces

Use **Rename Method** on any methods that do the same thing but have different signatures for what they do. Often this doesn't go far enough. In these cases the classes aren't yet doing enough. Keep using **Move Method** to move behavior to the classes until the protocols are the same. If you have to redundantly move code to accomplish this, you may be able to use **Extract Superclass** to atone.

### Incomplete Library Class

The trouble is that it is often bad form, and usually impossible, to modify a library class to do something you'd like it to do. This means that tried-and-true tactics such as **Move Method** lie useless. 

We have a couple of special-purpose tools for this job. If there are just a couple of methods that you wish the library class had, use **Introduce Foreign Method**. If there is a whole load of extra behavior, you need **Introduce Local Extension**.

### Data Class

These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are almost certainly being manipulated in far too much 71 detail by other classes. In early stages these classes may have public fields. If so, you should immediately apply **Encapsulate Field** before anyone notices. If you have collection fields, check to see whether they are properly encapsulated and apply **Encapsulate Collection** if they aren't. Use **Remove Setting Method** on any field that should not be changed. 

Look for where these getting and setting methods are used by other classes. Try to use **Move Method** to move behavior into the data class. If you can't move a whole method, use **Extract Method** to create a method that can be moved. After a while you can start using **Hide Method** on the getters and setters. 

Data classes are like children. They are okay as a starting point, but to participate as a grownup object, they need to take some responsibility.

### Refused Bequest

Subclasses get to inherit the methods and data of their parents. But what if they don't want or need what they are given? They are given all these great gifts and pick just a few to play with.

The traditional story is that this means the **hierarchy is wrong**. You need to create a new sibling class and use **Push Down Method** and **Push Down Field** to push all the unused methods to the sibling. That way the parent holds only what is common. Often you'll hear advice that all superclasses should be abstract.

### Comments

Don't worry, we aren't saying that people shouldn't write comments. In our olfactory analogy, comments aren't a bad smell; indeed they are a sweet smell. The reason we mention comments here is that comments often are used as a deodorant. It's surprising how often you look at thickly commented code and notice that the comments are there because the code is bad.

Our first action is to remove the bad smells by refactoring. When we're finished, we often find that the comments are superfluous.

If you need a comment to explain what a block of code does, try **Extract Method**. If the method is already extracted but you still need a comment to explain what it does, use **Rename Method**. If you need to state some rules about the required state of the system, use **Introduce Assertion**.

{% hint style="info" %}
When you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous.
{% endhint %}

A good time to use a comment is when you don't know what to do. In addition to describing what is going on, comments can indicate areas in which you aren't sure. A comment is a good place to say why you did something. This kind of information helps future modifiers, especially forgetful ones.

