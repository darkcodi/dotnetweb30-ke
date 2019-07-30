# Indexers and operator overloading

### Indexers

Indexers are a syntactic convenience that enable you to create a [class](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/class), [struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/struct), or [interface](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface) that client applications can access just as an array. Indexers are most frequently implemented in types whose primary purpose is to encapsulate an internal collection or array. 

* Indexers enable objects to be indexed in a similar manner to arrays.
* A `get` accessor returns a value. A `set` accessor assigns a value.
* The [this](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/this) keyword is used to define the indexer.
* The [value](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/value) keyword is used to define the value being assigned by the `set` indexer.
* Indexers do not have to be indexed by an integer value; it is up to you how to define the specific look-up mechanism.
* Indexers can be overloaded.
* Indexers can have more than one formal parameter, for example, when accessing a two-dimensional array.

```csharp
public int this[int index]   // Indexer declaration  
{
    // get and set accessors  
}  
```

Indexers are like properties. Except for the differences shown in the following table, all the rules that are defined for property accessors apply to indexer accessors also.

| Property | Indexer |
| :--- | :--- |
| Allows methods to be called as if they were public data members. | Allows elements of an internal collection of an object to be accessed by using array notation on the object itself. |
| Accessed through a simple name. | Accessed through an index. |
| Can be a static or an instance member. | Must be an instance member. |
| A [get](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/get) accessor of a property has no parameters. | A `get` accessor of an indexer has the same formal parameter list as the indexer. |
| A [set](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/set) accessor of a property contains the implicit `value` parameter. | A `set` accessor of an indexer has the same formal parameter list as the indexer, and also to the [value](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/value) parameter. |
| Supports shortened syntax with [Auto-Implemented Properties](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties). | Does not support shortened syntax. |

```csharp
// Using a string as an indexer value
class DayCollection
{
    string[] days = { "Sun", "Mon", "Tues", "Wed", "Thurs", "Fri", "Sat" };

    // This method finds the day or returns an Exception if the day is not found
    private int GetDay(string testDay)
    {

        for (int j = 0; j < days.Length; j++)
        {
            if (days[j] == testDay)
            {
                return j;
            }
        }

        throw new System.ArgumentOutOfRangeException(testDay, "testDay must be in the form \"Sun\", \"Mon\", etc");
    }

    // The get accessor returns an integer for a given string
    public int this[string day]
    {
        get
        {
            return (GetDay(day));
        }
    }
}

```

### Operator overloading

A user-defined type can overload a predefined C\# operator. That is, a type can provide the custom implementation of an operation when one or both operands are of that type. The [Overloadable operators](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/operator-overloading#overloadable-operators) section shows which C\# operators can be overloaded.

Use the `operator` keyword to declare an operator. An operator declaration must satisfy the following rules:

* It includes both a `public` and a `static` modifier.
* A unary operator takes one parameter. A binary operator takes two parameters. In each case, at least one parameter must have type `T` or `T?` where `T` is the type that contains the operator declaration.

The following table provides information about overloadability of C\# operators:

| Operators | Overloadability |
| :--- | :--- |
| [+](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#unary-plus-and-minus-operators), [-](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#unary-plus-and-minus-operators), [!](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#logical-negation-operator-), [~](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators#bitwise-complement-operator-), [++](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#increment-operator-), [--](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#decrement-operator---), [true](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/true-false-operators), [false](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/true-false-operators) | These unary operators can be overloaded. |
| [+](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/addition-operator), [-](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/subtraction-operator), [\*](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#multiplication-operator-), [/](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#division-operator-), [%](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#remainder-operator-), [&](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#logical-and-operator-), [\|](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#logical-or-operator-), [^](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#logical-exclusive-or-operator-), [&lt;&lt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators#left-shift-operator-), [&gt;&gt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators#right-shift-operator-), [==](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/equality-operators#equality-operator-), [!=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/equality-operators#inequality-operator-), [&lt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/comparison-operators#less-than-operator-), [&gt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/comparison-operators#greater-than-operator-), [&lt;=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/comparison-operators#less-than-or-equal-operator-), [&gt;=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/comparison-operators#greater-than-or-equal-operator-) | These binary operators can be overloaded. Certain operators must be overloaded in pairs; for more information, see the note that follows this table. |
| [&&](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#conditional-logical-and-operator-), [\|\|](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#conditional-logical-or-operator-) | Conditional logical operators cannot be overloaded. However, if a type with the overloaded [`true` and `false`operators](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/true-false-operators) also overloads the `&` or `|` operator in a certain way, the `&&` or `||` operator, respectively, can be evaluated for the operands of that type. For more information, see the [User-defined conditional logical operators](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/expressions#user-defined-conditional-logical-operators)section of the [C\# language specification](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/introduction). |
| [\[\]](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#indexer-operator-) | Element access is not considered an overloadable operator, but you can define an [indexer](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/indexers/index). |
| [\(T\)x](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/type-testing-and-conversion-operators#cast-operator-) | The cast operator cannot be overloaded, but you can define new conversion operators. For more information, see [User-defined conversion operators](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/user-defined-conversion-operators). |
| [+=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#compound-assignment), [-=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#compound-assignment), [\*=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#compound-assignment), [/=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#compound-assignment), [%=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#compound-assignment), [&=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#compound-assignment), [\|=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#compound-assignment), [^=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators#compound-assignment), [&lt;&lt;=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators#compound-assignment), [&gt;&gt;=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators#compound-assignment) | Compound assignment operators cannot be explicitly overloaded. However, when you overload a binary operator, the corresponding compound assignment operator, if any, is also implicitly overloaded. For example, `+=` is evaluated using `+`, which can be overloaded. |
| [=](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/assignment-operator), [.](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#member-access-operator-), [?:](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/conditional-operator), [??](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator), [-&gt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/pointer-related-operators#pointer-member-access-operator--), [=&gt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator), [f\(x\)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#invocation-operator-), [as](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/type-testing-and-conversion-operators#as-operator), [checked](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/checked), [unchecked](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/unchecked), [default](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions), [delegate](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-methods), [is](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/type-testing-and-conversion-operators#is-operator), [nameof](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/nameof), [new](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/new-operator), [sizeof](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/sizeof), [typeof](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/type-testing-and-conversion-operators#typeof-operator) | These operators cannot be overloaded. |

{% hint style="info" %}
The comparison operators must be overloaded in pairs. That is, if either operator of a pair is overloaded, the other operator must be overloaded as well. Such pairs are as follows:

* `==` and `!=` operators
* `<` and `>` operators
* `<=` and `>=` operators
{% endhint %}

