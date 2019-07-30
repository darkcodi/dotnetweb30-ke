# LINQ to Objects

### LINQ Queries to Primitive Arrays and Collections

When you have any array of data, it is very common to extract a subset of items based on a given requirement, or to obtain only the subitems that contain a number, have more or less than some number of characters, or don’t contain embedded spaces, etc.

The query expression created here makes use of the _from, in, where, orderby_, and _select_ LINQ query operators.

```csharp
IEnumerable<string> subset = from game in currentVideoGames
                             where game.Contains(" ")
                             orderby game select game;
```

The returned sequence is held in a variable named subset, typed as a type that implements the generic version of `IEnumerable<T>`.

{% hint style="info" %}
LINQ queries can be used to radically **simplify the process** of extracting new subsets of data from a source, rather than building nested loops, complex if/else logic, temporary data types, and so on.
{% endhint %}

Beyond pulling results from a simple array of data, LINQ query expressions can also manipulate data within members of the `System.Collections.Generic` namespace, such as the `List` type.

### LINQ Query Operators

C\# defines a good number of query operators out of the box.

| Query Operators | Meaning in Life |
| :--- | :--- |
| from, in | Used to define the backbone for any LINQ expression, which allows you to extract a subset of data from a fitting container. |
| where | Used to define a restriction for which items to extract from a container. |
| select | Used to select a sequence from the container. |
| join, on, equals, into | Performs joins based on specified key. Remember, these “joins” do not need to have anything to do with data in a relational database. |
| orderby ascending/descending | Allows the resulting subset to be ordered in ascending or descending order. |
| groupby | Yields a subset with data grouped by a specified value. |

In addition to this partial list of operators, the `System.Linq.Enumerable` class provides a set of methods that do not have a direct C\# query operator shorthand notation, but are instead exposed as extension methods like _Reverse&lt;&gt;\(\), ToArray&lt;&gt;\(\), ToList&lt;&gt;\(\), Distinct&lt;&gt;\(\), Union&lt;&gt;\(\), Intersect&lt;&gt;\(\), Count&lt;&gt;\(\), Sum&lt;&gt;\(\), Min&lt;&gt;\(\), Max&lt;&gt;\(\)_, etc.

### Internal Representation of LINQ Query

When compiled, the C\# compiler actually translates all C\# LINQ operators into calls on methods of the **`Enumerable`** class. A great many of the methods of `Enumerable` have been prototyped to take delegates as arguments. In particular, many methods require a generic delegate named `Func<>`.

```csharp
// Overloaded versions of the Enumerable.Where<T>() method.
// Note the second parameter is of type System.Func<>.
public static IEnumerable<TSource> Where<TSource>(this IEnumerable<TSource> source, System.Func<TSource,int,bool> predicate)
public static IEnumerable<TSource> Where<TSource>(this IEnumerable<TSource> source, System.Func<TSource,bool> predicate)
```

Given that many members of `System.Linq.Enumerable` demand a delegate as input, when invoking them, you can either manually create a new delegate type and author the necessary target methods, make use of a C\# anonymous method, or define a proper lambda expression.

### Building Query Using Lambda Expressions

This “longhand” LINQ query is a bit more complex to tease apart than the previous C\# LINQ query operator example. Part of the complexity is, no doubt, due to the chaining together of calls using the dot operator.

```csharp
static void QueryStringsWithEnumerableAndLambdas2()
{
    string[] currentVideoGames = {"Morrowind", "Uncharted 2",
        "Fallout 3", "Daxter", "System Shock 2"};
    
    // Break it down!
    var gamesWithSpaces = currentVideoGames.Where(game => game.Contains(" "));
    var orderedGames = gamesWithSpaces.OrderBy(game => game);
    var subset = orderedGames.Select(game => game);
    
    foreach (var game in subset)
        Console.WriteLine("Item: {0}", game);
    
    Console.WriteLine();
}
```

