# Nullable types

C\# data types have a fixed range and are represented as a type in the System namespace. All the numerical data types \(as well as the Boolean data type\) are value types. Value types can never be assigned the value of null, as that is used to establish an empty object reference.

C\# supports the concept of _nullable data types_. Simply put, a nullable type can represent all the values of its underlying type, plus the value null. Thus, if you declare a nullable bool, it could be assigned a value from the set {true, false, null}. This can be extremely helpful when working with relational databases, given that it is quite common to encounter undefined columns in database tables. Without the concept of a nullable data type, there is no convenient manner in C\# to represent a numerical data point with no value.

To define a nullable variable type, the question mark symbol \(**`?`**\) is suffixed to the underlying data type. Do note that this syntax is legal only when applied to value types. If you attempt to create a nullable reference type \(including strings\), you are issued a compile-time error. Like a nonnullable variable, local nullable variables must be assigned an initial value before you can use them.

In C\#, the `?` suffix notation is a shorthand for creating an instance of the generic `System.Nullable<T>` structure type. It is important to understand that the `System.Nullable<T>` type provides a set of members that all nullable types can make use of.

You are able to programmatically discover whether the nullable variable indeed has been assigned a null value using the `HasValue` property or the != operator. The assigned value of a nullable type may be obtained directly or via the Value property. In fact, given that the `?` suffix is just a shorthand for using `Nullable<T>`.

The next aspect to be aware of is any variable that might have a null value \(i.e., a reference-type variable or a nullable value-type variable\) can make use of the C\# **`??`** operator, which is formally termed the _null coalescing operator_. This operator allows you to assign a value to a nullable type if the retrieved value is in fact null. The benefit of using the **`??`** operator is that it provides a more compact version of a traditional **if/else** condition.

It is common to check incoming parameters, values returned from type members \(methods, properties, indexers\) against the value null. Now possible to leverage the null conditional operator token \(a question mark placed after a variable type but before an access operator\) to simplify the previous error checking. Rather than explicitly building a conditional statement to check for null, you can suffixing the ? operator directly after the variable you need to check. If this is null, its call to the property will not throw a runtime error. If you want to print an actual value, you could leverage the null coalescing operator to assign a default value as so:

```csharp
Console.WriteLine($"You sent me {args?.Length ?? 0} arguments.");
```



