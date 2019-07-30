# AutoFixture

**AutoFixture** is an open source library for .NET designed to minimize the 'Arrange' phase of your unit tests in order to maximize maintainability. Its primary goal is to allow developers to focus on what is being tested rather than how to setup the test scenario, by making it easier to create object graphs containing test data.

### Overview

AutoFixture is designed to make Test-Driven Development more productive and unit tests more refactoring-safe. It does so by removing the need for hand-coding anonymous variables as part of a test's Fixture Setup phase. Among other features, it offers a generic implementation of the [Test Data Builder](http://www.natpryce.com/articles/000714.html) pattern.

When writing unit tests, you typically need to create some objects that represent the initial state of the test. Often, an API will force you to specify much more data than you really care about, so you frequently end up creating objects that has no influence on the test, simply to make the code compile.

AutoFixture can help by creating such [Anonymous Variables](http://blogs.msdn.com/ploeh/archive/2008/11/17/anonymous-variables.aspx) for you. Here's a simple example:

```csharp
[Fact]
public void IntroductoryTest()
{
    // Arrange
    Fixture fixture = new Fixture();

    int expectedNumber = fixture.Create<int>();
    MyClass sut = fixture.Create<MyClass>();
    // Act
    int result = sut.Echo(expectedNumber);
    // Assert
    Assert.Equal(expectedNumber, result);
}
```

This example illustrates the basic principle of AutoFixture: It can create values of virtually any type without the need for you to explicitly define which values should be used. The number _expectedNumber_ is created by a call to Create - this will create a 'nice', regular integer value, saving you the effort of explicitly coming up with one.

The example also illustrates how AutoFixture can be used as a [SUT Factory](http://blog.ploeh.dk/2009/02/13/SUTFactory.aspx) that creates the actual System Under Test \(the MyClass instance\).

Given the right combination of unit testing framework and extensions for AutoFixture, we can further reduce the above test to be even more declarative:

[xUnit](http://blog.ploeh.dk/2010/10/08/AutoDataTheoriesWithAutoFixture.aspx)

```csharp
[Theory, AutoData]
public void IntroductoryTest(
    int expectedNumber, MyClass sut)
{
    int result = sut.Echo(expectedNumber);
    Assert.Equal(expectedNumber, result);
}
```

Notice how we can reduce unit tests to state only the relevant parts of the test. The rest \(variables, Fixture object\) is relegated to attributes and parameter values that are supplied automatically by AutoFixture. The test is now only two lines of code.

Using AutoFixture is as easy as referencing the library and creating a new instance of the Fixture class!

