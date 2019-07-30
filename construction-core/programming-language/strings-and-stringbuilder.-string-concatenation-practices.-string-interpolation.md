# Strings and StringBuilder. String concatenation practices. String Interpolation

### Strings and StringBuilder

A **string** is a reference data type in **C\#**. A **string** is a sequential collection of characters that is used to represent text. The value of the **String** object is the content of the sequential collection of System.Char objects, and that value is **immutable** \(that is, it is read-only\). 

[StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8) and [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8) both represent sequences of characters, they are implemented differently. [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8) is an immutable type. That is, each operation that appears to modify a [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8) object actually creates a new string.

[StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8), which is a mutable string class. Mutability means that once an instance of the class has been created, it can be modified by appending, removing, replacing, or inserting characters. A [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8) object maintains a buffer to accommodate expansions to the string. New data is appended to the buffer if room is available; otherwise, a new, larger buffer is allocated, data from the original buffer is copied to the new buffer, and the new data is then appended to the new buffer.

Consider using the [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8) class under these conditions:

* When the number of changes that your app will make to a string is small. In these cases, [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8) might offer negligible or no performance improvement over [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8).
* When you are performing a fixed number of concatenation operations, particularly with string literals. In this case, the compiler might combine the concatenation operations into a single operation.
* When you have to perform extensive search operations while you are building your string. The [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8) class lacks search methods such as `IndexOf` or `StartsWith`. You'll have to convert the [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8) object to a [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8) for these operations, and this can negate the performance benefit from using [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8). For more information, see the [Searching the text in a StringBuilder object](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8#Searching) section.

Consider using the [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netframework-4.8) class under these conditions:

* When you expect your app to make an unknown number of changes to a string at design time \(for example, when you are using a loop to concatenate a random number of strings that contain user input\).
* When you expect your app to make a significant number of changes to a string.

### String concatenation

#### **+ Operator**

Concatenation using the + operator therefore always creating a new string. 

Consider, for example, a concatenation of string A, B and C in the form “A = A + B + C”. Here, B and C cannot be simply attached to A. Rather, new memory is reserved in the total length of the two values ​​A and B and the contents of the A and B values ​​will be copied into the new memory. The same procedure is then performed to concatenate this intermediate result with the string C. 

To concatenate many strings therefore results in many temporary objects which consume memory unnecessarily. Furthermore, this variant is relatively slow due to the many copy operations.

####   **String.Concat**

Using the _String.Concat_ function also allows to concatenate strings. To do so you may pass all strings as function parameters. The above example can therefore change as follow: “A String.Concat = \(A, B, C\)”. During the function execution, first the total length of the new string is determined by the lengths of all values ​​passed. Then memory is allocated only once and the strings are copied to the memory. The functionality is thus similar to that of the + operator, with the crucial difference that the many intermediate variables are eliminated and new memory is allocated only once.

####  **StringBuilder**

The _StringBuilder_ class manages memory to accommodate strings in it. For this purpose, the class forms a large char array. This is gradually filled with the passed values. The initial size of the array can be specified. When adding strings, the array is automatically enlarged if necessary. The _StringBuilder_ class has just like the _String.Concat_ function the advantage that only single memory must be reserved and it can be used for multiple string concatenations. But the resulting gain in performance may be reduced by the necessary internal administrative operations. This can even result in a decrease of the execution speed.

_StringBuilder_ and _String.Concat_ differ in one crucial point. When the _String.Concat_ function is used, all strings to concatenate must be given as parameters. By using the _StringBuilder_ class, these values ​​can be added step by step by calling the _add_ function. So this is also the main use case of the class. _StringBuilder_ should only be used when multiple values ​​must be connected, but cannot be specified in a single function call. Otherwise, the _String.Concat_ function is usually preferable.

The following best practices will help to select the best solution for an individual use case

Use Case 1: Only a few strings should be concatenated and the memory consumption and performance play a subordinate role.

You can usethe following rule: readability is more important than performance and memory consumption. You should choose the function which creates the most readable source code.

Use Case 2: There are many strings which should be concatenated. Therefore this has an impact on performance and memory consumption. Here, the selection of the right function should depend on the kind of values that are used.

* Concatenation of fixed values: use the + operator
* Concatenation of variable values: use _Concat_
* Successively concatenation of values ​​which cannot or should not be done in a single function call: use _Builder_

### String Interpolation

`String.Format` and its cousins are very versatile and useful, but their use is a little clunky and error prone. Particularly unfortunate is the use of `{0}` etc. placeholders in the format string, which must line up with arguments supplied separately:

```csharp
var s = String.Format("{0} is {1} year{{s}} old", p.Name, p.Age);
```

String interpolation lets you put the expressions right in their place, by having “holes” directly in the string literal:

```csharp
var s = $"{p.Name} is {p.Age} year{{s}} old";
```

Just as with `String.Format`, optional alignment and format specifiers can be given:

```csharp
var s = $"{p.Name,20} is {p.Age:D3} year{{s}} old";
```

The contents of the holes can be pretty much any expression, including even other strings:

```csharp
var s = $"{p.Name} is {p.Age} year{(p.Age == 1 ? "" : "s")} old";
```

Notice that the conditional expression is parenthesized, so that the `: "s"` doesn’t get confused with a format specifier.

