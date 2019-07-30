# Skipping Tests

**`[Fact(Skip="reason")]`** 

Set the `Skip` parameter on the `[Fact]` attribute to temporarily skip a test.

```csharp
[Fact(Skip = "Doesn't work at the moment")]
public void ClassScenarioShouldFail()
{
    ...
}
```

