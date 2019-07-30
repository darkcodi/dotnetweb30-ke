# Value and reference types. Class vs Struct usage.

`System.ValueType` is to ensure that the derived type \(e.g., any structure\) is allocated on the stack, rather than the garbagecollected heap.

Data allocated on the stack can be created and destroyed quickly, as its lifetime is determined by the defining scope. Heap-allocated data, on the other hand, is monitored by the .NET garbage collector and has a lifetime that is determined by a large number of factors.

Functionally, the only purpose of `System.ValueType` is to override the virtual methods defined by `System.Object` to use value-based, versus reference-based, semantics. The base class of ValueType is `System.Object`. In fact, the instance methods defined by System.ValueType are identical to those of `System.Object`.

When you assign one value type to another, a member-by-member copy of the field data is achieved. In the case of a simple data type such as `System.Int32`, the only member to copy is the numerical value.

A variable of type `Point` \(named `p1`\) that is then assigned to another `Point` \(`p2`\). Because `Point` is a value type, you have two copies of the `MyPoint` type on the stack, each of which can be independently manipulated. Therefore, when you change the value of `p1.X`, the value of `p2.X` is unaffected.

In this case, you have two references pointing to the same object on the managed heap. Therefore, when you change the value of `X` using the `p1` reference, `p2.X` reports the same value.

### Value Types and Reference Types Comparison

| Intriguing Question | Value Type | Reference Type |
| :--- | :--- | :--- |
| Where are objects allocated? | Allocated on the stack. | Allocated on the managed heap. |
| How is a variable represented? | Value type variables are local copies. | Reference type variables are pointing to the memory occupied by the allocated instance. |
| What is the base type? | Implicitly extends System.ValueType. | Can derive from any other type \(except What is the base type? Implicitly extends System.ValueType. System. ValueType\), as long as that type is not “sealed”. |
| Can this type function as a base to other types? | No. Value types are always sealed and cannot be inherited from. | Yes. If the type is not sealed, it may function as a base to other types. |
| What is the default parameter passing behavior? | Variables are passed by value \(i.e., a copy of the variable is passed into the called function\). | For reference types, the reference is copied by value. |
| Can this type override System.Object.Finalize\(\)? | No | Yes, indirectly |
| Can I define constructors for this type? | Yes, but the default constructor is reserved \(i.e., your custom constructors must all have arguments\). | But, of course! |
| When do variables of this type die? | When they fall out of the defining scope. | When the object is garbage collected. |

Despite their differences, value types and reference types both have the ability to implement interfaces and may support any number of fields, methods, overloaded operators, constants, properties, and events.

