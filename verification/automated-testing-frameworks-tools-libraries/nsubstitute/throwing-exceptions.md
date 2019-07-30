# Throwing exceptions

[Callbacks](https://nsubstitute.github.io/help/callbacks) can be used to throw exceptions when a member is called.

```csharp
//For non-voids:
calculator.Add(-1, -1).Returns(x => { throw new Exception(); });

//For voids and non-voids:
calculator
    .When(x => x.Add(-2, -2))
    .Do(x => { throw new Exception(); });

//Both calls will now throw.
Assert.Throws<Exception>(() => calculator.Add(-1, -1));
Assert.Throws<Exception>(() => calculator.Add(-2, -2));
```

