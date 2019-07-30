# Dealing with Generalization

Generalization produces its own batch of refactorings, mostly dealing with moving methods around a hierarchy of inheritance. **Pull Up Field** and **Pull Up Method** both promote function up a hierarchy, and **Push Down Method** and **Push Down Field** push function downward. Constructors are a little bit more awkward to pull up, so **Pull Up Constructor Body** deals with those issues. Rather than pushing down a constructor, it is often useful to use **Replace Constructor with Factory Method**.

If you have methods that have a similar outline body but vary in details, you can use **Form Template Method** to separate the differences from the similarities.

In addition to moving function around a hierarchy, you can change the hierarchy by creating new classes. **Extract Subclass**, **Extract Superclass**, and **Extract Interface** all do this by forming new elements out of various points. **Extract Interface** is particularly important when you want to mark a small amount of function for the type system. If you find yourself with unnecessary classes in your hierarchy, you can use **Collapse Hierarchy** to remove them.

Sometimes you find that inheritance is not the best way of handling a situation and that you need delegation instead. **Replace Inheritance with Delegation** helps make this change. Sometimes life is the other way around and you have to use **Replace Delegation with Inheritance**.

