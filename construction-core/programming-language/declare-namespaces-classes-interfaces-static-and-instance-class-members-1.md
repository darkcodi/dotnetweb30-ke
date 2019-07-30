# Declare namespaces, classes, interfaces, static and instance class members

### Namespaces

The **namespaces** keyword is used to declare a scope that contains a set of related objects. Namespaces are used in C\# to organize and provide a level of separation of codes and to create globally unique types. They can be considered as a container which consists of other namespaces, classes, etc.

A namespace can have following types as its members:

* another namespaces \(Nested Namespace\)
* classes
* interfaces
* structures
* enum
* delegates

Namespaces are heavily used in C\# programming in two ways:

* First, the .NET Framework uses namespaces to organize its many classes.
* Second, declaring your own namespaces can help you control the scope of class and method names in larger programming projects.

Whether or not you explicitly declare a namespace in a C\# source file, the compiler adds a default namespace. This unnamed namespace, sometimes referred to as the global namespace, is present in every file. Any identifier in the global namespace is available for use in a named namespace.

**Namespaces implicitly have public access and this is not modifiable.** The access modifiers can be assigned to elements in a namespace.

Namespaces have the following properties:

* They organize large code projects.
* They are delimited by using the `.` operator.
* The `using` directive obviates the requirement to specify the name of the namespace for every class.
* The `global` namespace is the "root" namespace: `global::System` will always refer to the .NET System namespace.

 The `using`directive can also be used to create an alias for a namespace:

```csharp
using Co = Company.Proj.Nested;  // define an alias to represent a namespace
```

Nested namespace - one namespace is part of another:

```csharp
namespace SomeNameSpace
{
    public class MyClass 
    {
        static void Main() 
        {
            Nested.NestedNameSpaceClass.SayHello();
        }
    }

    // a nested namespace
    namespace Nested   
    {
        public class NestedNameSpaceClass 
        {
            public static void SayHello() 
            {
                Console.WriteLine("Hello");
            }
        }
    }
}
```

### Classes

 Class is a _reference type._  At run time, when you declare a variable of a reference type, the variable contains the value `null` until you explicitly create an instance of the class by using the `new` operator, or assign it an object of a compatible type that may have been created elsewhere.

When the object is created, enough memory is allocated on the managed heap for that specific object, and the variable holds only a reference to the location of said object. Types on the managed heap require overhead both when they are allocated and when they are reclaimed by the automatic memory management functionality of the CLR, which is known as _garbage collection_. 

 Classes are declared by using the `class` keyword followed by a unique identifier.

```csharp
//[access modifier] - [class] - [identifier]
public class Customer
{
   // Fields, properties, methods and events go here...
}
```

Classes fully support _inheritance_, a fundamental characteristic of object-oriented programming. When you create a class, you can inherit from any other interface or class that is not defined as sealed, and other classes can inherit from your class and override class virtual methods.

{% hint style="success" %}
  The **sealed** keyword enables you to prevent the inheritance of a class or certain class members that were previously marked `virtual`.
{% endhint %}

Inheritance is accomplished by using a _derivation_, which means a class is declared by using a _base class_ from which it inherits data and behavior. When a class declares a base class, it inherits all the members of the base class except the constructors.

 A class can be declared **abstract**. An abstract class contains abstract methods that have a signature definition but no implementation. **Abstract classes cannot be instantiated**. They can only be used through derived classes that implement the abstract methods. 

 Class definitions can be split between different source files \(**Partial Classes**\).

{% hint style="warning" %}
Only single inheritance is allowed in C\#. In other words, a class can inherit implementation from one base class only. However, a class can implement more than one interface.
{% endhint %}

You can declare generic classes that have type parameters \(**Generic Classes**\).

Classes that you declare directly within a namespace, not nested within other classes, can be either **public** or **internal**. Classes are `internal` by default.

{% hint style="success" %}
**Public** - the type or member can be accessed by any other code in the same assembly or another assembly that references it.

**Internal** - ****the type or member can be accessed by any code in the same assembly, but not from another assembly.
{% endhint %}

A class can contain declarations of the following members:

* Constructors
* Constants
* Fields
* Finalizers
* Methods
* Properties
* Indexers
* Operators
* Events
* Delegates
* Classes
* Interfaces
* Structs
* Enumerations

Class members, including nested classes, can be public, protected internal, protected, internal, private, or private protected. Members are `private` by default.

{% hint style="success" %}
**Protected** - the type or member can be accessed only by code in the same class, or in a class that is derived from that class.

**Private** - the type or member can be accessed only by code in the same class or struct.

**Protected internal** -the type or member can be accessed by any code in the assembly in which it is declared, or from within a derived class in another assembly.

**Private protected** - the type or member can be accessed only within its declaring assembly, by code in the same class or in a type that is derived from that class.
{% endhint %}

 In **C\#**, there are two types of **class members**, **instance** and static.

### Interfaces

An interface contains definitions for a group of related functionalities that a `class` or a `struct` can implement.

By using interfaces, you can, for example, include behavior from multiple sources in a class. That capability is important in C\# because the language doesn't support multiple inheritance of classes. In addition, you must use an interface if you want to simulate inheritance for structs, because they can't actually inherit from another struct or class.

You define an interface by using the `interface` keyword.

The interface defines only the signature. In that way, an interface in C\# is similar to an abstract class in which all the methods are abstract. However, a class or struct can implement multiple interfaces, but a class can inherit only a single class, abstract or not.

Interfaces can contain methods, properties, events, indexers, or any combination of those four member types.

 An interface can't contain constants, fields, operators, instance constructors, finalizers, or types. Interface members are automatically public, and they can't include any access modifiers. Members also can't be `static`.

To implement an interface member, the corresponding member of the implementing class must be public, non-static, and have the same name and signature as the interface member.

When a class or struct implements an interface, the class or struct must provide an implementation for all of the members that the interface defines. The interface itself provides no functionality that a class or struct can inherit in the way that it can inherit base class functionality. However, if a base class implements an interface, any class that's derived from the base class inherits that implementation.

Properties and indexers of a class can define extra accessors for a property or indexer that's defined in an interface. For example, an interface might declare a property that has a `get` accessor. The class that implements the interface can declare the same property with both a `get` and `set` accessor. 

Interfaces can inherit from other interfaces. A class might include an interface multiple times through base classes that it inherits or through interfaces that other interfaces inherit. However, the class can provide an implementation of an interface only one time and only if the class declares the interface as part of the definition of the class \(`class ClassName : InterfaceName`\). If the interface is inherited because you inherited a base class that implements the interface, the base class provides the implementation of the members of the interface. However, the derived class can reimplement any virtual interface members instead of using the inherited implementation.

A base class can also implement interface members by using virtual members. In that case, a derived class can change the interface behavior by overriding the virtual members.

An interface has the following properties:

* An interface is like an abstract base class with only abstract members. Any class or struct that implements the interface must implement all its members.
* An interface can't be instantiated directly. Its members are implemented by any class or struct that implements the interface.
* Interfaces can contain events, indexers, methods, and properties.
* Interfaces contain no implementation of methods.
* A class or struct can implement multiple interfaces. A class can inherit a base class and also implement one or more interfaces.

### Static class members

 Use the `static` modifier to declare a static member, which belongs to the type itself rather than to a specific object. The `static`modifier can be used with classes, fields, methods, properties, operators, events, and constructors, but it cannot be used with indexers, finalizers, or types other than classes. 

A non-static class can contain static methods, fields, properties, or events. The static member is callable on a class even when no instance of the class has been created. The static member is always accessed by the class name, not the instance name. Only one copy of a static member exists, regardless of how many instances of the class are created. Static methods and properties cannot access non-static fields and events in their containing type, and they cannot access an instance variable of any object unless it is explicitly passed in a method parameter.

{% hint style="info" %}
Two common uses of static fields are to keep a count of the number of objects that have been instantiated, or to store a value that must be shared among all instances.
{% endhint %}

Static methods can be overloaded but not overridden, because they belong to the class, and not to any instance of the class.

{% hint style="warning" %}
Although a field cannot be declared as `static const`, a **const** field is essentially static in its behavior. It belongs to the type, not to instances of the type. Therefore, const fields can be accessed by using the same `ClassName.MemberName` notation that is used for static fields. No object instance is required.
{% endhint %}

C\# does not support static local variables \(variables that are declared in method scope\).

Static members are initialized before the static member is accessed for the first time and before the static constructor, if there is one, is called. To access a static class member, use the name of the class instead of a variable name to specify the location of the member.

**If your class contains static fields, provide a static constructor that initializes them when the class is loaded.**

### Instance class members

A class or struct definition is like a blueprint that specifies what the type can do. An object is basically a block of memory that has been allocated and configured according to the blueprint. A program may create many objects of the same class. Objects are also called instances, and they can be stored in either a named variable or in an array or collection.

Instance _class_ members belong to a specific occurrence of a _class_. Every time you declare an object of a certain _class_, you create a new instance of that _class_. 

