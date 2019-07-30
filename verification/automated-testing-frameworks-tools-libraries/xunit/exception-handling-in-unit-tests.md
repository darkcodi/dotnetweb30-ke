# Exception Handling in Unit Tests

When writing tests it is sometimes useful to check that the correct exceptions are thrown at the expected time. When using xUnit.net there are a number of ways to accomplish this.

As an example consider the following simple class:

```csharp
public class TemperatureSensor
{
    bool _isInitialized;

    public void Initialize()
    {
        _isInitialized = true;
    }
 
    public int ReadCurrentTemperature()
    {
        if (!_isInitialized)
            throw new InvalidOperationException("Cannot read temperature before initializing.");
 
        return 42; // Simulate for demo code purposes
    }        
}
```

The first test we could write against the preceding class is to check the “happy path”:

```csharp
[Fact]
public void ReadTemperature()
{
    var sut = new TemperatureSensor();

    sut.Initialize();
 
    var temperature = sut.ReadCurrentTemperature();
 
    Assert.Equal(42, temperature);
}
```

Next a test could be written to check that if the temperature is read before initializing the sensor, an exception of type `InvalidOperationException` is thrown. To do this the xUnit.net `Assert.Throws` method can be used. When using this method the generic type parameter indicates the type of expected exception and the method parameter takes an action that should cause this exception to be thrown, for example:

```csharp
[Fact]
public void ErrorIfReadingBeforeInitialized()
{
    var sut = new TemperatureSensor();
 
    Assert.Throws<InvalidOperationException>(() => sut.ReadCurrentTemperature());
}
```

In the preceding test, if an `InvalidOperationException` is not thrown when the `ReadCurrentTemperature` method is called the test will fail.

The thrown exception can also be captured in a variable to make further asserts against the exception property values, for example:

```csharp
[Fact]
public void ErrorIfReadingBeforeInitialized_CaptureExDemo()
{
    var sut = new TemperatureSensor();
 
    var ex = Assert.Throws<InvalidOperationException>(() => sut.ReadCurrentTemperature());
 
    Assert.Equal("Cannot read temperature before initializing.", ex.Message);
}
```

The Assert.Throws method expects the exact type of exception and not derived exceptions. In the case where you want to also allow derived exceptions, the `Assert.ThrowsAny` method can be used.

