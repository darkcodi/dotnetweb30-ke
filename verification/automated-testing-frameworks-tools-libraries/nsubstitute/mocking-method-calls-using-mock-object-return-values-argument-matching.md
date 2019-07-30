# Mocking Method Calls \(Using Mock Object, Return Values, Argument Matching\)

### Creating a substitute

The basic syntax for creating a substitute is:

```csharp
var substitute = Substitute.For<ISomeInterface>();
```

This is how you’ll normally create substitutes for types. Generally this type will be an interface, but you can also substitute classes in cases of emergency.

#### Substituting for classes

```csharp
var someClass = Substitute.For<SomeClassWithCtorArgs>(5, "hello world");
```

#### Substituting for multiple interfaces

There are times when you want to substitute for multiple types. The best example of this is when you have code that works with a type, then checks whether it implements IDisposable and disposes of it if it doesn’t.

```csharp
var command = Substitute.For<ICommand, IDisposable>();
var runner = new CommandRunner(command);

runner.RunCommand();

command.Received().Execute();
((IDisposable)command).Received().Dispose();
```

Your substitute can implement several types this way, but remember you can only implement a maximum of one class. You can specify as many interfaces as you like, but only one of these can be a class. The most flexible way of creating substitutes for multiple types is using this overload:

```csharp
var substitute = Substitute.For(
		new[] { typeof(ICommand), typeof(ISomeInterface), typeof(SomeClassWithCtorArgs) },
		new object[] { 5, "hello world" }
	);
Assert.IsInstanceOf<ICommand>(substitute);
Assert.IsInstanceOf<ISomeInterface>(substitute);
Assert.IsInstanceOf<SomeClassWithCtorArgs>(substitute);
```

#### Substituting for delegates

NSubstitute can also substitute for delegate types by using Substiute.For\(\). When substituting for delegate types you will not be able to get the substitute to implement additional interfaces or classes.

```csharp
var func = Substitute.For<Func<string>>();

func().Returns("hello");
Assert.AreEqual("hello", func());
```

### Setting a return value

The following examples relate to substituting for the following interface:

```csharp
public interface ICalculator {
	int Add(int a, int b);
	string Mode { get; set; }
}
```

#### For methods

To set a return value for a method call on a substitute, call the method as normal, then follow it with a call to NSubstitute’s `Returns()` extension method.

```csharp
var calculator = Substitute.For<ICalculator>();
calculator.Add(1, 2).Returns(3);
```

This value will be returned every time this call is made. `Returns()` will only apply to this combination of arguments, so other calls to this method will return a default value instead.

```csharp
//Make a call return 3:
calculator.Add(1, 2).Returns(3);
Assert.AreEqual(calculator.Add(1, 2), 3);
Assert.AreEqual(calculator.Add(1, 2), 3);

//Call with different arguments does not return 3
Assert.AreNotEqual(calculator.Add(3, 6), 3);
```

#### For properties

The return value for a property can be set in the same was as for a method, using `Returns()`. You can also just use plain old property setters for read/write properties; they’ll behave just the way you expect them to.

```csharp
calculator.Mode.Returns("DEC");
Assert.AreEqual(calculator.Mode, "DEC");

calculator.Mode = "HEX";
Assert.AreEqual(calculator.Mode, "HEX");
```

### Argument matchers

Argument matchers can be used when [setting return values](https://nsubstitute.github.io/help/return-for-args) and when [checking received calls](https://nsubstitute.github.io/help/received-calls). They provide a way to _specify_ a call or group of calls, so that a return value can be set for all matching calls, or to check a matching call has been received.

The argument matchers syntax shown here depends on having C\# 7.0 or later. If you are stuck on an earlier version \(getting an error such as `CS7085: By-reference return type 'ref T' is not supported` while trying to use them\) please use [compatibility argument matchers](https://nsubstitute.github.io/help/compat-args) instead.

{% hint style="warning" %}
Argument matchers should only be used when setting return values or checking received calls. Using Arg.Is or Arg.Any without a call to Returns\(...\) or Received\(\) can cause your tests to behave in unexpected ways. See How NOT to use argument matchers for more information.
{% endhint %}

### Ignoring arguments <a id="ignoring-arguments"></a>

An argument of type `T` can be ignored using `Arg.Any<T>()`.

```csharp
calculator.Add(Arg.Any<int>(), 5).Returns(7);

Assert.AreEqual(7, calculator.Add(42, 5));
Assert.AreEqual(7, calculator.Add(123, 5));
Assert.AreNotEqual(7, calculator.Add(1, 7));
```

In this example we return `7` when adding any number to `5`. We use `Arg.Any<int>()` to tell NSubstitute to ignore the first argument.

We can also use this to match any argument of a specific sub-type.

```csharp
formatter.Format(new object());
formatter.Format("some string");

formatter.Received().Format(Arg.Any<object>());
formatter.Received().Format(Arg.Any<string>());
formatter.DidNotReceive().Format(Arg.Any<int>());
```

### Conditionally matching an argument <a id="conditionally-matching-an-argument"></a>

An argument of type `T` can be conditionally matched using `Arg.Is<T>(Predicate<T> condition)`.

```csharp
calculator.Add(1, -10);

//Received call with first arg 1 and second arg less than 0:
calculator.Received().Add(1, Arg.Is<int>(x => x < 0));
//Received call with first arg 1 and second arg of -2, -5, or -10:
calculator
    .Received()
    .Add(1, Arg.Is<int>(x => new[] {-2,-5,-10}.Contains(x)));
//Did not receive call with first arg greater than 10:
calculator.DidNotReceive().Add(Arg.Is<int>(x => x > 10), -10);
```

If the condition throws an exception for an argument, then it will be assumed that the argument does not match. The exception itself will be swallowed.

```csharp
formatter.Format(Arg.Is<string>(x => x.Length <= 10)).Returns("matched");

Assert.AreEqual("matched", formatter.Format("short"));
Assert.AreNotEqual("matched", formatter.Format("not matched, too long"));
// Will not match because trying to access .Length on null will throw an exception when testing
// our condition. NSubstitute will assume it does not match and swallow the exception.
Assert.AreNotEqual("matched", formatter.Format(null));
```

### Matching a specific argument <a id="matching-a-specific-argument"></a>

An argument of type `T` can be matched using `Arg.Is<T>(T value)`.

```csharp
calculator.Add(0, 42);

//This won't work; NSubstitute isn't sure which arg the matcher applies to:
//calculator.Received().Add(0, Arg.Any<int>());

calculator.Received().Add(Arg.Is(0), Arg.Any<int>());
```

This matcher normally isn’t required; most of the time we can just use `0` instead of `Arg.Is(0)`. In some cases though, NSubstitute can’t work out which matcher applies to which argument \(arg matchers are actually fuzzily matched; not passed directly to the function call\). In these cases it will throw an `AmbiguousArgumentsException` and ask you to specify one or more additional argument matchers. In some cases you may have to explicitly use argument matchers for every argument.

### Matching `out` and `ref` args <a id="matching-out-and-ref-args"></a>

Argument matchers can also be used with `out` and `ref` \(NSubstitute 4.0 and later with C\# 7.0 and later\).

```csharp
calculator
    .LoadMemory(1, out Arg.Any<int>())
    .Returns(x => {
        x[1] = 42;
        return true;
    });

var hasEntry = calculator.LoadMemory(1, out var memoryValue);
Assert.AreEqual(true, hasEntry);
Assert.AreEqual(42, memoryValue);
```

