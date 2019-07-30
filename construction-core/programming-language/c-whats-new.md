# C\# - What's new?

### Readonly members <a id="readonly-members"></a>

You can apply the `readonly` modifier to any member of a struct. It indicates that the member does not modify state. It's more granular than applying the `readonly` modifier to a `struct` declaration. 

Notice that the `readonly` modifier is necessary on a read only property. The compiler doesn't assume `get` accessors do not modify state; you must declare `readonly` explicitly. The compiler does enforce the rule that `readonly` members do not modify state. 

This feature lets you specify your design intent so the compiler can enforce it, and make optimizations based on that intent.

### Default interface members <a id="default-interface-members"></a>

You can now add members to interfaces and provide an implementation for those members. This language feature enables API authors to add methods to an interface in later versions without breaking source or binary compatibility with existing implementations of that interface. Existing implementations _inherit_ the default implementation. 

### More patterns in more places <a id="more-patterns-in-more-places"></a>

#### switch expressions <a id="switch-expressions"></a>

Often, a [`switch`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/switch) statement produces a value in each of its `case` blocks. **Switch expressions** enable you to use more concise expression syntax. There are fewer repetitive `case` and `break` keywords, and fewer curly braces. 

```csharp
public enum Rainbow
{
    Red,
    Orange,
    Yellow,
    Green,
    Blue,
    Indigo,
    Violet
}

public static RGBColor FromRainbow(Rainbow colorBand) =>
    colorBand switch
    {
        Rainbow.Red    => new RGBColor(0xFF, 0x00, 0x00),
        Rainbow.Orange => new RGBColor(0xFF, 0x7F, 0x00),
        Rainbow.Yellow => new RGBColor(0xFF, 0xFF, 0x00),
        Rainbow.Green  => new RGBColor(0x00, 0xFF, 0x00),
        Rainbow.Blue   => new RGBColor(0x00, 0x00, 0xFF),
        Rainbow.Indigo => new RGBColor(0x4B, 0x00, 0x82),
        Rainbow.Violet => new RGBColor(0x94, 0x00, 0xD3),
        _              => throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand)),
    };
```

There are several syntax improvements here:

* The variable comes before the `switch` keyword. The different order makes it visually easy to distinguish the switch expression from the switch statement.
* The `case` and `:` elements are replaced with `=>`. It's more concise and intuitive.
* The `default` case is replaced with a `_` discard.
* The bodies are expressions, not statements.

Contrast that with the equivalent code using the classic `switch` statement:

```csharp
public static RGBColor FromRainbowClassic(Rainbow colorBand)
{
    switch (colorBand)
    {
        case Rainbow.Red:
            return new RGBColor(0xFF, 0x00, 0x00);
        case Rainbow.Orange:
            return new RGBColor(0xFF, 0x7F, 0x00);
        case Rainbow.Yellow:
            return new RGBColor(0xFF, 0xFF, 0x00);
        case Rainbow.Green:
            return new RGBColor(0x00, 0xFF, 0x00);
        case Rainbow.Blue:
            return new RGBColor(0x00, 0x00, 0xFF);
        case Rainbow.Indigo:
            return new RGBColor(0x4B, 0x00, 0x82);
        case Rainbow.Violet:
            return new RGBColor(0x94, 0x00, 0xD3);
        default:
            throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand));
    };
}
```

#### Property patterns <a id="property-patterns"></a>

The **property pattern** enables you to match on properties of the object examined. 

```csharp
public static decimal ComputeSalesTax(Address location, decimal salePrice) =>
    location switch
    {
        { State: "WA" } => salePrice * 0.06M,
        { State: "MN" } => salePrice * 0.75M,
        { State: "MI" } => salePrice * 0.05M,
        // other cases removed for brevity...
        _ => 0M
    };
```

Pattern matching creates a concise syntax for expressing this algorithm.

#### Tuple patterns <a id="tuple-patterns"></a>

Some algorithms depend on multiple inputs. **Tuple patterns** allow you to switch based on multiple values expressed as a [tuple](https://docs.microsoft.com/en-us/dotnet/csharp/tuples). The following code shows a switch expression for the game _rock, paper, scissors_:

```csharp
public static string RockPaperScissors(string first, string second)
    => (first, second) switch
    {
        ("rock", "paper") => "rock is covered by paper. Paper wins.",
        ("rock", "scissors") => "rock breaks scissors. Rock wins.",
        ("paper", "rock") => "paper covers rock. Paper wins.",
        ("paper", "scissors") => "paper is cut by scissors. Scissors wins.",
        ("scissors", "rock") => "scissors is broken by rock. Rock wins.",
        ("scissors", "paper") => "scissors cuts paper. Scissors wins.",
        (_, _) => "tie"
    };
```

The messages indicate the winner. The discard case represents the three combinations for ties, or other text inputs.

#### Positional patterns <a id="positional-patterns"></a>

Some types include a `Deconstruct` method that deconstructs its properties into discrete variables. When a `Deconstruct` method is accessible, you can use **positional patterns** to inspect properties of the object and use those properties for a pattern. Consider the following `Point` class that includes a `Deconstruct` method to create discrete variables for `X` and `Y`:

```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y) =>
        (x, y) = (X, Y);
}
```

Additionally, consider the following enum that represents various positions of a quadrant:

```csharp
public enum Quadrant
{
    Unknown,
    Origin,
    One,
    Two,
    Three,
    Four,
    OnBorder
}
```

The following method uses the **positional pattern** to extract the values of `x` and `y`. Then, it uses a `when` clause to determine the `Quadrant` of the point:C\#Copy

```csharp
static Quadrant GetQuadrant(Point point) => point switch
{
    (0, 0) => Quadrant.Origin,
    var (x, y) when x > 0 && y > 0 => Quadrant.One,
    var (x, y) when x < 0 && y > 0 => Quadrant.Two,
    var (x, y) when x < 0 && y < 0 => Quadrant.Three,
    var (x, y) when x > 0 && y < 0 => Quadrant.Four,
    var (_, _) => Quadrant.OnBorder,
    _ => Quadrant.Unknown
};
```

The discard pattern in the preceding switch matches when either `x` or `y` is 0, but not both. A switch expression must either produce a value or throw an exception. If none of the cases match, the switch expression throws an exception. The compiler generates a warning for you if you do not cover all possible cases in your switch expression.

### using declarations <a id="using-declarations"></a>

A **using declaration** is a variable declaration preceded by the `using` keyword. It tells the compiler that the variable being declared should be disposed at the end of the enclosing scope. For example, consider the following code that writes a text file:

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using var file = new System.IO.StreamWriter("WriteLines2.txt");
    foreach (string line in lines)
    {
        // If the line doesn't contain the word 'Second', write the line to the file.
        if (!line.Contains("Second"))
        {
            file.WriteLine(line);
        }
    }
// file is disposed here
}
```

In the preceding example, the file is disposed when the closing brace for the method is reached. That's the end of the scope in which `file` is declared. The preceding code is equivalent to the following code using the classic [using statements](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-statement) statement:

```csharp
static void WriteLinesToFile(IEnumerable<string> lines)
{
    using (var file = new System.IO.StreamWriter("WriteLines2.txt"))
    {
        foreach (string line in lines)
        {
            // If the line doesn't contain the word 'Second', write the line to the file.
            if (!line.Contains("Second"))
            {
                file.WriteLine(line);
            }
        }
    } // file is disposed here
}
```

In the preceding example, the file is disposed when the closing brace associated with the `using` statement is reached.

In both cases, the compiler generates the call to `Dispose()`. The compiler generates an error if the expression in the using statement is not disposable.

### Static local functions <a id="static-local-functions"></a>

You can now add the `static` modifier to local functions to ensure that local function doesn't capture \(reference\) any variables from the enclosing scope. Doing so generates `CS8421`, "A static local function can't contain a reference to &lt;variable&gt;."

Consider the following code. The local function `LocalFunction` accesses the variable `y`, declared in the enclosing scope \(the method `M`\). Therefore, `LocalFunction` can't be declared with the `static` modifier:

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

The following code contains a static local function. It can be static because it doesn't access any variables in the enclosing scope:

```csharp
int M()
{
    int y = 5;
    int x = 7;
    return Add(x, y);

    static int Add(int left, int right) => left + right;
}
```

### Disposable ref structs <a id="disposable-ref-structs"></a>

A `struct` declared with the `ref` modifier may not implement any interfaces and so cannot implement [IDisposable](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable). Therefore, to enable a `ref struct` to be disposed, it must have an accessible `void Dispose()` method. This also applies to `readonly ref struct`declarations.

### Nullable reference types <a id="nullable-reference-types"></a>

Inside a nullable annotation context, any variable of a reference type is considered to be a **nonnullable reference type**. If you want to indicate that a variable may be null, you must append the type name with the `?` to declare the variable as a **nullable reference type**.

Nullable reference types aren't checked to ensure they aren't assigned or initialized to null. However, the compiler uses flow analysis to ensure that any variable of a nullable reference type is checked against null before it's accessed or assigned to a nonnullable reference type.

### Asynchronous streams <a id="asynchronous-streams"></a>

Starting with C\# 8.0, you can create and consume streams asynchronously. A method that returns an asynchronous stream has three properties:

1. It's declared with the `async` modifier.
2. It returns an [IAsyncEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.iasyncenumerable-1).
3. The method contains `yield return` statements to return successive elements in the asynchronous stream.

Consuming an asynchronous stream requires you to add the `await` keyword before the `foreach` keyword when you enumerate the elements of the stream. Adding the `await` keyword requires the method that enumerates the asynchronous stream to be declared with the `async` modifier and to return a type allowed for an `async` method. Typically that means returning a [Task](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task) or [Task&lt;TResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task-1). It can also be a [ValueTask](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.valuetask) or [ValueTask&lt;TResult&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.valuetask-1). A method can both consume and produce an asynchronous stream, which means it would return an [IAsyncEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.iasyncenumerable-1). The following code generates a sequence from 0 to 19, waiting 100 ms between generating each number:

```csharp
public static async System.Collections.Generic.IAsyncEnumerable<int> GenerateSequence()
{
    for (int i = 0; i < 20; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}
```

You would enumerate the sequence using the `await foreach` statement:

```csharp
await foreach (var number in GenerateSequence())
{
    Console.WriteLine(number);
}
```

### Indices and ranges <a id="indices-and-ranges"></a>

Ranges and indices provide a succinct syntax for specifying subranges in an array, [Span&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.span-1), or [ReadOnlySpan&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.readonlyspan-1).

This language support relies on two new types, and two new operators.

* [System.Index](https://docs.microsoft.com/en-us/dotnet/api/system.index) represents an index into a sequence.
* The `^` operator, which specifies that an index is relative to the end of the sequence.
* [System.Range](https://docs.microsoft.com/en-us/dotnet/api/system.range) represents a sub range of a sequence.
* The Range operator \(`..`\), which specifies the start and end of a range as is operands.

Let's start with the rules for indexes. Consider an array `sequence`. The `0` index is the same as `sequence[0]`. The `^0` index is the same as `sequence[sequence.Length]`. Note that `sequence[^0]` does throw an exception, just as `sequence[sequence.Length]` does. For any number `n`, the index `^n` is the same as `sequence.Length - n`.

A range specifies the _start_ and _end_ of a range. The start of the range is inclusive, but the end of the range is exclusive, meaning the _start_ is included in the range but the _end_ is not included in the range. The range `[0..^0]` represents the entire range, just as `[0..sequence.Length]` represents the entire range.

```csharp
var words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

You can retrieve the last word with the `^1` index:

```csharp
Console.WriteLine($"The last word is {words[^1]}");
// writes "dog"
```

The following code creates a subrange with the words "quick", "brown", and "fox". It includes `words[1]` through `words[3]`. The element `words[4]` is not in the range.

```csharp
var quickBrownFox = words[1..4];
```

The following code creates a subrange with "lazy" and "dog". It includes `words[^2]` and `words[^1]`. The end index `words[^0]` is not included:C\#Copy

```csharp
var lazyDog = words[^2..^0];
```

The following examples create ranges that are open ended for the start, end, or both:

```csharp
var allWords = words[..]; // contains "The" through "dog".
var firstPhrase = words[..4]; // contains "The" through "fox"
var lastPhrase = words[6..]; // contains "the", "lazy" and "dog"
```

You can also declare ranges as variables:

```csharp
Range phrase = 1..4;
```

The range can then be used inside the `[` and `]` characters:

```csharp
var text = words[phrase];
```

