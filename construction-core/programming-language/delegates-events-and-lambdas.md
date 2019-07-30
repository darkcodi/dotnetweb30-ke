# Delegates, events and lambdas

### Delegates

The declaration of a delegate type is similar to a method signature. It has a return value and any number of parameters of any type:

```csharp
public delegate void TestDelegate(string message);
public delegate int TestDelegate(MyType m, long num);
```

 A `delegate` is a reference type that can be used to encapsulate a named or an anonymous method. Delegates are similar to function pointers in C++; however, delegates are type-safe and secure.

Delegates are used to pass methods as arguments to other methods. Event handlers are nothing more than methods that are invoked through delegates.This ability to refer to a method as a parameter makes delegates ideal for defining callback methods.

Any method from any accessible class or struct that matches the delegate type can be assigned to the delegate. The method can be either static or an instance method. This makes it possible to programmatically change method calls, and also plug new code into existing classes.

Delegates have the following properties:

* Delegates are similar to C++ function pointers, but delegates are fully object-oriented, and unlike C++ pointers to member functions, delegates encapsulate both an object instance and a method.
* Delegates allow methods to be passed as parameters.
* Delegates can be used to define callback methods.
* Delegates can be chained together; for example, multiple methods can be called on a single event.
* Methods do not have to match the delegate type exactly. 
* C\# version 2.0 introduced the concept of `Anonymous Methods`, which allow code blocks to be passed as parameters in place of a separately defined method. C\# 3.0 introduced lambda expressions as a more concise way of writing inline code blocks. Both anonymous methods and lambda expressions \(in certain contexts\) are compiled to delegate types. Together, these features are now known as anonymous functions. For more information about lambda expressions, see `Anonymous Functions`.

```csharp
class Stack<T>
{
    T[] items;
    int index;

    public delegate void StackDelegate(T[] items);
}

private static void DoWork(float[] items) { }

public static void TestStack()
{
    Stack<float> s = new Stack<float>();
    Stack<float>.StackDelegate d = DoWork;
}
```

 Delegates are the basis for `Events`.

### Events

Events enable a class or object to notify other classes or objects when something of interest occurs. The class that sends \(or _raises_\) the event is called the _publisher_ and the classes that receive \(or _handle_\) the event are called _subscribers_.

Events have the following properties:

* The publisher determines when an event is raised; the subscribers determine what action is taken in response to the event.
* An event can have multiple subscribers. A subscriber can handle multiple events from multiple publishers.
* Events that have no subscribers are never raised.
* Events are typically used to signal user actions such as button clicks or menu selections in graphical user interfaces.
* When an event has multiple subscribers, the event handlers are invoked synchronously when an event is raised. 
* In the .NET Framework class library, events are based on the `EventHandler` delegate and the `EventArgs` base class.

```csharp
public class SampleEventArgs
{
    public SampleEventArgs(string s) { Text = s; }
    public String Text { get; } // readonly
}

public class Publisher
{
    // Declare the delegate (if using non-generic pattern).
    public delegate void SampleEventHandler(object sender, SampleEventArgs e);

    // Declare the event.
    public event SampleEventHandler SampleEvent;

    // Wrap the event in a protected virtual method
    // to enable derived classes to raise the event.
    protected virtual void RaiseSampleEvent()
    {
        // Raise the event by using the () operator.
        if (SampleEvent != null)
            SampleEvent(this, new SampleEventArgs("Hello"));
    }
}

public class Subscriber
{
    public void Subscribe(Publisher publisher)
    {
        publisher.SampleEvent += SampleEventHandler;
    }
    
    private void SampleEventHandler(object sender, SampleEventArgs e)
    {
        Console.WriteLine(e.Text);
    }
}
```

### Lambdas

A _lambda expression_ is a block of code \(an expression or a statement block\) that is treated as an object. It can be passed as an argument to methods, and it can also be returned by method calls. Lambda expressions are used extensively for:

* Passing the code that is to be executed to asynchronous methods, such as [Task.Run\(Action\)](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.task.run#System_Threading_Tasks_Task_Run_System_Action_).
* Writing [LINQ query expressions](https://docs.microsoft.com/en-us/dotnet/csharp/linq/index).
* Creating [expression trees](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/expression-trees/index).

A lambda expression uses `=>`, the [lambda declaration operator](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator), to separate the lambda's parameter list from its executable code. To create a lambda expression, you specify input parameters \(if any\) on the left side of the lambda operator, and you put the expression or statement block on the other side. For example, the single-line lambda expression `x => x * x` specifies a parameter that’s named `x` and returns the value of `x` squared. You can assign this expression to a delegate type, as the following example shows:

```csharp
Func<int, int> square = x => x * x;
Console.WriteLine(square(5));
// Output:
// 25
```

You also can assign a lambda expression to an expression tree type:

```csharp
System.Linq.Expressions.Expression<Func<int, int>> e = x => x * x;
Console.WriteLine(e);
// Output:
// x => (x * x)
```

Or you can pass it directly as a method argument:

```csharp
int[] numbers = { 2, 3, 4, 5 };
var squaredNumbers = numbers.Select(x => x * x);
Console.WriteLine(string.Join(" ", squaredNumbers));
// Output:
// 4 9 16 25
```

#### Expression lambdas 

A lambda expression with an expression on the right side of the `=>` operator is called an _expression lambda_.  xpression lambdas are used extensively in the construction of [expression trees](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/expression-trees/index). An expression lambda returns the result of the expression and takes the following basic form: 

```csharp
(input-parameters) => expression
```

The parentheses are optional only if the lambda has one input parameter; otherwise they are required.

Specify zero input parameters with empty parentheses:C\#Copy

```csharp
Action line = () => Console.WriteLine();
```

Two or more input parameters are separated by commas enclosed in parentheses:C\#Copy

```csharp
Func<int, int, bool> testForEquality = (x, y) => x == y;
```

Sometimes it's impossible for the compiler to infer the input types. You can specify the types explicitly as shown in the following example:C\#Copy

```csharp
Func<int, string, bool> isTooLong = (int x, string s) => s.Length > x;
```

Input parameter types must be all explicit or all implicit; otherwise, a [CS0748](https://docs.microsoft.com/en-us/dotnet/csharp/misc/cs0748) compiler error occurs.

#### Statement lambdas

A statement lambda resembles an expression lambda except that the statement\(s\) is enclosed in braces:

```csharp
(input-parameters) => { statement; }
```

The body of a statement lambda can consist of any number of statements; however, in practice there are typically no more than two or three.

```csharp
Action<string> greet = name => 
{ 
    string greeting = $"Hello {name}!";
    Console.WriteLine(greeting);
};
greet("World");
// Output:
// Hello World!
```

Statement lambdas, like anonymous methods, cannot be used to create expression trees.

#### Async lambdas

You can easily create lambda expressions and statements that incorporate asynchronous processing by using the [async](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/async) and [await](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/await) keywords. 

```csharp
utton1.Click += async (sender, e) =>
    {
        await ExampleMethodAsync();
        textBox1.Text += "\r\nControl returned to Click event handler.\n";
    };
```

#### Lambda expressions and tuples

Starting with C\# 7.0, the C\# language provides built-in support for [tuples](https://docs.microsoft.com/en-us/dotnet/csharp/tuples). You can provide a tuple as an argument to a lambda expression, and your lambda expression can also return a tuple. In some cases, the C\# compiler uses type inference to determine the types of tuple components.

You define a tuple by enclosing a comma-delimited list of its components in parentheses. The following example uses tuple with three components to pass a sequence of numbers to a lambda expression, which doubles each value and returns a tuple with three components that contains the result of the multiplications.

```csharp
Func<(int, int, int), (int, int, int)> doubleThem = ns => (2 * ns.Item1, 2 * ns.Item2, 2 * ns.Item3);
var numbers = (2, 3, 4);
var doubledNumbers = doubleThem(numbers);
Console.WriteLine($"The set {numbers} doubled: {doubledNumbers}");
// Output:
// The set (2, 3, 4) doubled: (4, 6, 8)
```

Ordinarily, the fields of a tuple are named `Item1`, `Item2`, etc. You can, however, define a tuple with named components, as the following example does.

```csharp
Func<(int n1, int n2, int n3), (int, int, int)> doubleThem = ns => (2 * ns.n1, 2 * ns.n2, 2 * ns.n3);
var numbers = (2, 3, 4);
var doubledNumbers = doubleThem(numbers);
Console.WriteLine($"The set {numbers} doubled: {doubledNumbers}");
```

