# Naming standards for unit tests

The basic naming of a test comprises of three main parts:

 **\[UnitOfWork\_StateUnderTest\_ExpectedBehavior\]**

A unit of work is a use case in the system that startes with a public method and ends up with one of three types of results: a return value/exception, a state change to the system which changes its behavior, or a call to a third party \(when we use mocks\). so a unit of work can be a small as a method, or as large as a class, or even multiple classes. as long is it all runs in memory, and is fully under our control.

### Examples

```csharp
public void Sum_NegativeNumberAs1stParam_ExceptionThrown()
```

```csharp
public void Sum_NegativeNumberAs2ndParam_ExceptionThrown()
```

```csharp
public void Sum_simpleValues_Calculated()
```

### **Reasons**

**Test name should express a specific requirement**

Your unit test name should express a specific requirement. This requirement should be somehow derived from either a business requirement or a technical requirement. In any case, that requirement has been broken down into small enough pieces, each of which represents a test case. If your test is not representing a requirement, why are you writing it? Why is that code even there?

