# Primary test framework attributes

### Attributes

| xUnit.net | Comments |
| :--- | :--- |
| `[Fact]` | Marks a test method. |
| _n/a_ | xUnit.net does not require an attribute for a test class; it looks for all test methods in all public \(exported\) classes in the assembly. |
| `Assert.Throws` `Record.Exception` | xUnit.net has done away with the ExpectedException attribute in favor of `Assert.Throws`.  |
| Constructor | We believe that use of `[SetUp]` is generally bad. However, you can implement a parameterless constructor as a direct replacement.  |
| `IDisposable.Dispose` | We believe that use of `[TearDown]` is generally bad. However, you can implement `IDisposable.Dispose` as a direct replacement. |
| `IClassFixture<T>` | To get per-class fixture setup, implement `IClassFixture<T>` on your test class. |
| `IClassFixture<T>` | To get per-class fixture teardown, implement `IClassFixture<T>` on your test class. |
| `ICollectionFixture<T>` | To get per-collection fixture setup and teardown, implement `ICollectionFixture<T>` on your test collection. |
| `[Fact(Skip="reason")]` | Set the Skip parameter on the `[Fact]` attribute to temporarily skip a test. |
| `[Trait]` | Set arbitrary metadata on a test |
| `[Theory]` `[XxxData]` | Theory \(data-driven test\). |

### Attribute Notes

{% hint style="info" %}
Unit.net provides a new way to think about per-fixture data with the use of the IClassFixture and ICollectionFixture interfaces. The runner will create a single instance of the fixture data and pass it through to your constructor before running each test. All the tests share the same instance of fixture data. After all the tests have run, the runner will dispose of the fixture data, if it implements IDisposable.
{% endhint %}

{% hint style="info" %}
xUnit.net ships with support for data-driven tests call Theories. Mark your test with the \[Theory\] attribute \(instead of \[Fact\]\), then decorate it with one or more \[XxxData\] attributes, including \[InlineData\] and \[MemberData\].
{% endhint %}

