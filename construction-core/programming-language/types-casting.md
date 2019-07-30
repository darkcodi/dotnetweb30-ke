# Types casting

Because C\# is statically-typed at compile time, after a variable is declared, it cannot be declared again or assigned a value of another type unless that type is implicitly convertible to the variable's type.

 _Type conversion_ is a process of converting one type into another.  A _**conversion**_ enables an expression to be treated as being of a particular type. A conversion may cause an expression of a given type to be treated as having a different type, or it may cause an expression without a type to get a type. Conversions can be _**implicit**_ or _**explicit**_, and this determines whether an explicit cast is required. 

```csharp
int a = 123;
long b = a;         // implicit conversion from int to long
int c = (int) b;    // explicit conversion from long to int
```

### **Implicit conversions**

No special syntax is required because the conversion is type safe and no data will be lost. Examples include conversions from smaller to larger integral types, and conversions from derived classes to base classes.

```csharp
// Implicit conversion. A long can
// hold any value an int can hold, and more!
int num = 2147483647;
long bigNum = num;
```

For reference types, an implicit conversion always exists from a class to any one of its direct or indirect base classes or interfaces. No special syntax is necessary because a derived class always contains all the members of a base class.

```csharp
Derived d = new Derived();  
Base b = d; // Always OK. 
```

### **Explicit conversions \(casts\)**

Explicit conversions require a cast operator. Casting is required when information might be lost in the conversion, or when the conversion might not succeed for other reasons. Typical examples include numeric conversion to a type that has less precision or a smaller range, and conversion of a base-class instance to a derived class.

A cast is a way of explicitly informing the compiler that you intend to make the conversion and that you are aware that data loss might occur. To perform a cast, specify the type that you are casting to in parentheses in front of the value or variable to be converted. The following program casts a **double** to an **int**. The program will not compile without the cast.

```csharp
class Test
{
    static void Main()
    {
        double x = 1234.7;
        int a;
        // Cast double to int.
        a = (int)x;
        System.Console.WriteLine(a);
    }
}
// Output: 1234
```

For reference types, an explicit cast is required if you need to convert from a base type to a derived type:

```csharp
// Create a new derived type.  
Giraffe g = new Giraffe();  
  
// Implicit conversion to base type is safe.  
Animal a = g;  
  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe) a;
```

A cast operation between reference types does not change the run-time type of the underlying object; it only changes the type of the value that is being used as a reference to that object.

### **User-defined conversions**

User-defined conversions are performed by special methods that you can define to enable explicit and implicit conversions between custom types that do not have a base class–derived class relationship.

### **Conversions with helper classes**

To convert between non-compatible types, such as integers and `System.DateTime` objects, or hexadecimal strings and byte arrays, you can use the `System.BitConverter` class, the `System.Convert` class, and the `Parse`methods of the built-in numeric types, such as `Int32.Parse`. 

### Type conversion exceptions

In some reference type conversions, the compiler cannot determine whether a cast will be valid. It is possible for a cast operation that compiles correctly to fail at run time that creates the risk of throwing an `InvalidCastException`.  C\# provides the `is` and `as` operators to test if a value is of a certain type.

#### IS

The `is` operator checks if the runtime type of an expression result is compatible with a given type. 

```csharp
E is T
```

where `E` is an expression that returns a value and `T` is the name of a type or a type parameter. `E` cannot be an anonymous method or a lambda expression.

The `E is T` expression returns `true` if the result of `E` is non-null and can be converted to type `T` by a reference conversion, a boxing conversion, or an unboxing conversion; otherwise, it returns `false`. The `is` operator doesn't consider user-defined conversions.

Starting with C\# 7.0, the `is` operator also tests an expression result against a pattern. In particular, it supports the type pattern in the following form:

```csharp
E is T v
```

where `E` is an expression that returns a value, `T` is the name of a type or a type parameter, and `v` is a new local variable of type `T`. If the result of `E` is non-null and can be converted to `T` by a reference, boxing, or unboxing conversion, the `E is T v` expression returns `true` and the converted value of the result of `E` is assigned to variable `v`.

```csharp
int i = 23;
object iBoxed = i;
int? jNullable = 7;
if (iBoxed is int a && jNullable is int b)
{
    Console.WriteLine(a + b);  // output 30
}
```

#### AS

 The `as` operator explicitly converts the result of an expression to a given reference or nullable value type. If the conversion is not possible, the `as` operator returns `null`. Unlike the **cast operator \(**\), the `as` operator never throws an exception.

```csharp
E as T
```

 where `E` is an expression that returns a value and `T` is the name of a type or a type parameter, produces the same result as

```csharp
E is T ? (T)(E) : (T)null
```

except that `E` is only evaluated once.

The `as` operator considers only reference, nullable, boxing, and unboxing conversions. You cannot use the `as` operator to perform a user-defined conversion. To do that, use the [cast operator \(\)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/type-testing-and-conversion-operators#cast-operator-).

```csharp
IEnumerable<int> numbers = new[] { 10, 20, 30 };
IList<int> indexable = numbers as IList<int>;
if (indexable != null)
{
    Console.WriteLine(indexable[0] + indexable[indexable.Count - 1]);  // output: 40
}
```



