# Collections and Generics

For many applications, you want to create and manage groups of related objects. There are two ways to group objects: by creating arrays of objects, and by creating collections of objects. Arrays are most useful for creating and working with a fixed number of strongly-typed objects. Collections provide a more flexible way to work with groups of objects. Unlike arrays, the group of objects you work with can grow and shrink dynamically as the needs of the application change.

{% hint style="success" %}
A collection is a class, so you must declare an instance of the class before you can add elements to that collection.
{% endhint %}

### Problems of non-generic collections

The basic difference is that generic collections are strongly typed and non-generic collections \(ArrayList, Hashtable, Queue, Stack,  SortedList etc\) are not, unless they've been specially written to accept just a single type of data.  The classes in the `System.Collections` namespace do not store elements as specifically typed objects, but as objects of type `Object`.

This means that, in the case of value types \(int, double, bool, char etc\), they have to be 'boxed' first and then 'unboxed' when you retrieve them which is quite a slow operation.

Whilst you don't have this problem with reference types, you still have to cast them to their actual types before you can use them.

This means that generic collections are faster than their non-generic counterparts when using value types and more convenient when using reference types. In short, the non-generic collections are now virtually redundant.

### System.Collections.Generic Namespace

If your collection contains elements of only one data type, you can use one of the classes in the `System.Collections.Generic` namespace. A generic collection enforces type safety so that no other data type can be added to it. When you retrieve an element from a generic collection, you do not have to determine its data type or convert it.

### List&lt;T&gt;, Queue&lt;T&gt;, Stack&lt;T&gt;, SortedSet&lt;T&gt;, ObservableCollection&lt;T&gt;

#### List&lt;T&gt; 

Represents a strongly typed list of objects that can be accessed by index. Provides methods to search, sort, and manipulate lists.

Non-generic analog - ArrayList.

It is safe to perform multiple read operations on a `List`, but issues can occur if the collection is modified while it's being read. To ensure thread safety, **lock** the collection **during a read or write operation**. To enable a collection to be accessed by multiple threads for reading and writing, you must implement your own synchronization. For an inherently thread-safe alternative  ImmutableList class can be used.

#### Queue&lt;T&gt;

Represents a first-in, first-out collection of objects. This class implements a generic queue as a circular array.

Objects stored in a `Queue<T>` are inserted at one end and removed from the other. Queues and stacks are useful when you need temporary storage for information; that is, when you might want to discard an element after retrieving its value. Use `Queue<T>` if you need to access the information in the same order that it is stored in the collection. 

Three main operations can be performed on a `Queue<T>` and its elements:

* Enqueue adds an element to the end of the `Queue<T>`.
* Dequeue removes the oldest element from the start of the `Queue<T>`.
* Peek peek returns the oldest element that is at the start of the `Queue<T>` but does not remove it from the `Queue<T>`.

The capacity of a `Queue<T>` is the number of elements the `Queue<T>` can hold. As elements are added to a `Queue<T>`, the capacity is automatically increased as required by reallocating the internal array. The capacity can be decreased by calling `TrimExcess`.

`Queue<T>` accepts `null` as a valid value for reference types and allows duplicate elements.

 A Queue&lt;T&gt; can support multiple readers concurrently, as long as the collection is not modified. Even so, enumerating through a collection is intrinsically not a thread-safe procedure. Use `ConcurrentQueue<T>` if you need to access the collection from multiple threads concurrently.

#### Stack&lt;T&gt;

`Stack<T>` is implemented as an array. Represents a variable size last-in-first-out \(LIFO\) collection of instances of the same specified type.

Stacks and queues are useful when you need temporary storage for information; that is, when you might want to discard an element after retrieving its value. Use `Stack<T>` if you need to access the information in reverse order that it is stored in the collection.

A common use for `System.Collections.Generic.Stack<T>` is to preserve variable states during calls to other procedures.

Three main operations can be performed on a `System.Collections.Generic.Stack<T>` and its elements:

* `Push` inserts an element at the top of the `Stack`.
* `Pop` removes an element from the top of the `Stack<T>`.
* `Peek` returns an element that is at the top of the `Stack<T>` but does not remove it from the `Stack<T>`.

The capacity of a `Stack<T>` is the number of elements the `Stack<T>` can hold. As elements are added to a `Stack<T>`, the capacity is automatically increased as required by reallocating the internal array. The capacity can be decreased by calling `TrimExcess`.

If `Count` is less than the capacity of the stack, `Push` is an O\(1\) operation. If the capacity needs to be increased to accommodate the new element, `Push` becomes an O\(`n`\) operation, where `n` is `Coun`t. `Pop` is an O\(1\) operation.

`Stack<T>` accepts `null` as a valid value for reference types and allows duplicate elements.

A `Stack<T>` can support multiple readers concurrently, as long as the collection is not modified. Even so, enumerating through a collection is intrinsically not a thread-safe procedure. Use `ConcurrentStack<T>` if you need to access the collection from multiple threads concurrently.

#### SortedSet&lt;T&gt;

Represents a collection of objects that is maintained in sorted order.

A `SortedSet<T>` object maintains a sorted order without affecting performance as elements are inserted and deleted. Duplicate elements are not allowed. Changing the sort values of existing items is not supported and may lead to unexpected behavior.

For a thread safe alternative to `SortedSet<T>`, see `ImmutableSortedSet<T>`

#### ObservableCollection&lt;T&gt;

Represents a dynamic data collection that provides notifications when items get added, removed, or when the whole list is refreshed.

 To set up dynamic bindings so that insertions or deletions in the collection update the UI automatically, the collection must implement the `INotifyCollectionChanged` interface. This interface exposes the `CollectionChanged` event, an event that should be raised whenever the underlying collection changes.

To fully support transferring data values from binding source objects to binding targets, each object in your collection that supports bindable properties must implement an appropriate property changed notification mechanism such as the `INotifyPropertyChanged` interface.

| Operation | List&lt;T&gt; | Queue&lt;T&gt; | Stack&lt;T&gt; | SortedSet&lt;T&gt; | ObservableCollection&lt;T&gt; |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Add | Add\(T\) | Enqueue\(T\) | Push\(T\) | Add\(T\) | Add\(T\) |
| Remove | Remove\(T\) | Dequeue\(\) | Pop\(\) | Remove\(T\) | Remove\(T\) |
| Remove all | Clear\(\) | Clear\(\) | Clear\(\) | Clear\(\) | Clear\(\) |
| Contains | Contains\(T\) | Contains\(T\) | Contains\(T\) | Contains\(T\) | Contains\(T\) |
| Indexer \(property\) | Item\[Int32\] | - | - | - | Item\[Int32\] |
| Count \(property\) | Count | Count | Count | Count | Count |

### Collection Initialization Syntax

 Collection initializers let you specify one or more element initializers when you initialize a collection type that implements `IEnumerable` and has `Add` with the appropriate signature as an instance method or an extension method. The element initializers can be a simple value, an expression, or an object initializer. By using a collection initializer, you do not have to specify multiple calls; the compiler adds the calls automatically.

Simple collection initializers:

```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };

List<Cat> cats = new List<Cat>
{
    new Cat{ Name = "Sylvester", Age=8 },
    new Cat{ Name = "Whiskers", Age=2 },
    new Cat{ Name = "Sasha", Age=14 }
};
```

 You can specify `null` as an element in a collection initializer if the collection's `Add` method allows it.

```csharp
List<Cat> moreCats = new List<Cat>
{
    new Cat{ Name = "Furrytail", Age=5 },
    new Cat{ Name = "Peaches", Age=4 },
    null
};
```

You can specify indexed elements if the collection supports read / write indexing.

```csharp
var numbers = new Dictionary<int, string>
{
    [7] = "seven",
    [9] = "nine",
    [13] = "thirteen"
};
```

 This initializer example calls `Add(TKey, TValue)` to add the three items into the dictionary: 

```csharp
var moreNumbers = new Dictionary<int, string>
{
    {19, "nineteen" },
    {23, "twenty-three" },
    {42, "forty-two" }
};
```

These two different ways to initialize associative collections have slightly different behavior because of the method calls the compiler generates. Both variants work with the `Dictionary` class.

### Creating Custom Generic Classes

Generics were added to version 2.0 of the C\# language and the common language runtime \(CLR\). 

Generics introduce the concept of type parameters, which make it possible to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code. For example, by using a generic type parameter T you can write a single class that other client code can use without incurring the cost or risk of runtime casts or boxing operations.

Generic classes and methods combine reusability, type safety and efficiency in a way that their non-generic counterparts cannot.

* Use generic types to maximize code reuse, type safety, and performance.
* The most common use of generics is to create collection classes.
* You can create your own generic interfaces, classes, methods, events and delegates.
* Generic classes may be constrained to enable access to methods on particular data types.
* Information on the types that are used in a generic data type may be obtained at run-time by using reflection.

Of course, you can also create custom generic types and methods to provide your own generalized solutions and design patterns that are type-safe and efficient. Just  use type parameter `T` at the locations locations where a concrete type would ordinarily be used.

```csharp
// type parameter T in angle brackets
public class GenericClass<T> 
{
    // The nested class is also generic on T.
    private class NestedClass
    {
        // T used in non-generic constructor.
        public NestedClass(T t)
        {
            data = t;
        }
        
        // T as private member data type.
        private T data;

        // T as return type of property.
        public T Data  
        {
            get { return data; }
            set { data = value; }
        }
    }

    // T as method parameter type:
    public void MethodClass(T t) 
    {
        NestedClass n = new NestedClass(t);
        // do somethings 
    }
}
```

### Constraining Type Parameters

 Constraints inform the compiler about the capabilities a type argument must have. Without any constraints, the type argument could be any type. Constraints are specified by using the `where` contextual keyword. 

The `where` clause in a generic definition specifies constraints on the types that are used as arguments for type parameters in a generic type, method, delegate, or local function. Constraints can specify interfaces, base classes, or require a generic type to be a reference, value or unmanaged type. They declare capabilities that the type argument must possess.

```csharp
public class AGenericClass<T> where T : IComparable<T> { }
```

The `where` clause can also include a base class constraint. The base class constraint states that a type to be used as a type argument for that generic type has the specified class as a base class \(or is that base class\) to be used as a type argument for that generic type. If the base class constraint is used, it must appear before any other constraints on that type parameter. Some types are disallowed as a base class constraint: `Object`, `Array`, and `ValueType`. Prior to C\# 7.3, `Enum`, `Delegate`, and `MulticastDelegate` were also disallowed as base class constraints. 

```csharp
public class UsingEnum<T> where T : System.Enum { }

public class UsingDelegate<T> where T : System.Delegate { }

public class Multicaster<T> where T : System.MulticastDelegate { }
```

 The `where` clause can specify that the type is a `class` or a `struct`. The `struct` constraint removes the need to specify a base class constraint of `System.ValueType`. 

```csharp
class MyClass<T, U>
    where T : class
    where U : struct
{ }
```

 The `where` clause may also include an `unmanaged` constraint. The `unmanaged` constraint limits the type parameter to types known as **unmanaged types**. An **unmanaged type** is a type that isn't a reference type and doesn't contain reference type fields at any level of nesting. The `unmanaged` constraint makes it easier to write low-level interop code in C\#. This constraint enables reusable routines across all unmanaged types. **The `unmanaged` constraint can't be combined with the `class` or `struct` constraint.** The `unmanaged`constraint enforces that the type must be a `struct`:

```csharp
class UnManagedWrapper<T>
    where T : unmanaged
{ }
```

 The `where` clause may also include a constructor constraint, `new()`. That constraint makes it possible to create an instance of a type parameter using the `new` operator. The `new() Constraint` lets the compiler know that any type argument supplied must have an accessible parameterless--or default-- constructor.  

The `new()` constraint appears last in the `where` clause. **The `new()` constraint can't be combined with the `struct` or `unmanaged`constraints.** All types satisfying those constraints must have an accessible parameterless constructor, making the `new()` constraint redundant.

```csharp
public class MyGenericClass<T> where T : IComparable<T>, new()
{
    // The following line is not possible without new() constraint:
    T item = new T();
}
```

 With multiple type parameters, use one `where` clause for each type parameter:

```csharp
public interface IMyInterface { }

namespace CodeExample
{
    class Dictionary<TKey, TVal>
        where TKey : IComparable<TKey>
        where TVal : IMyInterface
    {
        public void Add(TKey key, TVal val) { }
    }
}
```

Constraints can be attached to type parameters of generic methods:

```csharp
public void MyMethod<T>(T t) where T : IMyInterface { }
```

Notice that the syntax to describe type parameter constraints on delegates is the same as that of methods:

```csharp
delegate T MyDelegate<T>() where T : new();
```

| Constraint | Description |
| :--- | :--- |
| `where T : struct` | The type argument must be a value type. Any value type except [Nullable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.nullable-1) can be specified. For more information about nullable types, see [Nullable types](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/nullable-types/index). |
| `where T : class` | The type argument must be a reference type. This constraint applies also to any class, interface, delegate, or array type. |
| `where T : unmanaged` | The type argument must not be a reference type and must not contain any reference type members at any level of nesting. |
| `where T : new()` | The type argument must have a public parameterless constructor. When used together with other constraints, the `new()`constraint must be specified last. |
| `where T :` _&lt;base class name&gt;_ | The type argument must be or derive from the specified base class. |
| `where T :` _&lt;interface name&gt;_ | The type argument must be or implement the specified interface. Multiple interface constraints can be specified. The constraining interface can also be generic. |
| `where T : U` | The type argument supplied for T must be or derive from the argument supplied for U. |

