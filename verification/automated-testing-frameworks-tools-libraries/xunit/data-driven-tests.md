# Data-driven Tests

### **Using the \[Theory\] attribute to create parameterised tests with \[InlineData\]**

xUnit uses the `[Fact]` attribute to denote a parameterless unit test, which tests invariants in your code.

In contrast, the `[Theory]` attribute denotes a parameterised test that is true for a subset of data. That data can be supplied in a number of ways, but the most common is with an `[InlineData]` attribute.

The following example shows how you could rewrite the previous `CanAdd` test method to use the `[Theory]` attribute, and add some extra values to test:

```csharp
[Theory]
[InlineData(1, 2, 3)]
[InlineData(-4, -6, -10)]
[InlineData(-2, 2, 0)]
[InlineData(int.MinValue, -1, int.MaxValue)]
public void CanAddTheory(int value1, int value2, int expected)
{
    var calculator = new Calculator();

    var result = calculator.Add(value1, value2);

    Assert.Equal(expected, result);
}
```

Instead of specifying the values to add \(`value1` and `value2`\) in the test body, we pass those values as parameters to the test. We also pass in the expected result of the calculation, to use in the `Assert.Equal()` call.

The data is provided by the `[InlineData]` attribute. Each instance of `[InlineData]` will create a separate execution of the `CanAddTheory` method. The values passed in the constructor of `[InlineData]` are used as the parameters for the method - the order of the parameters in the attribute matches the order in which they're supplied to the method.

If you run the tests for this method, you'll see each `[InlineData]` creates a separate instance. xUnit handily adds the parameter names and values to the test description, so you can easily see which iteration failed.

![](../../../.gitbook/assets/test-explorer-theory.png)

The `[InlineData]` attribute is great when your method parameters are constants, and you don't have too many cases to test. If that's not the case, then you might want to look at one of the other ways to provide data to your `[Theory]` methods.

### Using a dedicated data class with \[ClassData\]

If the values you need to pass to your \[Theory\] test aren't constants, then you can use an alternative attribute, \[ClassData\], to provide the parameters. This attribute takes a Type which xUnit will use to obtain the data:

```csharp
[Theory]
[ClassData(typeof(CalculatorTestData))]
public void CanAddTheoryClassData(int value1, int value2, int expected)
{
    var calculator = new Calculator();

    var result = calculator.Add(value1, value2);

    Assert.Equal(expected, result);
}
```

We've specified a type of `CalculatorTestData` in the `[ClassData]` attribute. This class must implement `IEnumerable<object[]>`, where each item returned is an array of `object`s to use as the method parameters. We could rewrite the data from the `[InlineData]` attribute using this approach:

```csharp
public class CalculatorTestData : IEnumerable<object[]>
{
    public IEnumerator<object[]> GetEnumerator()
    {
        yield return new object[] { 1, 2, 3 };
        yield return new object[] { -4, -6, -10 };
        yield return new object[] { -2, 2, 0 };
        yield return new object[] { int.MinValue, -1, int.MaxValue };
    }

    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}
```

Obviously you could write this enumerator in multiple ways, but I went for a simple iterator approach. xUnit will call `.ToList()` on your provided class before it runs any of the theory method instances, so it's important the data is all independent. You don't want to have shared objects between tests runs causing weird bugs!

The `[ClassData]` attribute is a convenient way of removing clutter from your test files, but what if you don't want to create an extra class? For these situations, you can use the `[MemberData]` attribute.

### Using generator properties with the \[MemberData\] properties

The `[MemberData]` attribute can load data from an `IEnnumerable<object[]>` property on the test class. The xUnit analyzers will pick up any issues with your configuration, such as missing properties, or using properties that return invalid types.

In the following example I've added a `Data` property which returns an `IEnumerable<object[]>`, just like for the `[ClassData]`

```csharp
public class CalculatorTests
{
    [Theory]
    [MemberData(nameof(Data))]
    public void CanAddTheoryMemberDataProperty(int value1, int value2, int expected)
    {
        var calculator = new Calculator();

        var result = calculator.Add(value1, value2);

        Assert.Equal(expected, result);
    }

    public static IEnumerable<object[]> Data =>
        new List<object[]>
        {
            new object[] { 1, 2, 3 },
            new object[] { -4, -6, -10 },
            new object[] { -2, 2, 0 },
            new object[] { int.MinValue, -1, int.MaxValue },
        };
}
```

