# Asserts

### Assertions

| xUnit.net | Comments |
| :--- | :--- |
| `Equal` | MSTest and xUnit.net support generic versions of this method |
| `NotEqual` | MSTest and xUnit.net support generic versions of this method |
| `NotSame` |  |
| `Same` |  |
| `Contains` |  |
| `DoesNotContain` |  |
| `InRange` | Ensures that a value is in a given inclusive range |
| `IsAssignableFrom` |  |
| `Empty` |  |
| `False` |  |
| `IsType<T>` |  |
| `NotEmpty` |  |
| `IsNotType<T>` |  |
| `NotNull` |  |
| `Null` |  |
| `True` |  |
| `NotInRange` | Ensures that a value is not in a given inclusive range |
| `Throws<T>` | Ensures that the code throws an exact exception |

{% hint style="info" %}
Older versions of xUnit.net provided an Assert.DoesNotThrow which was later removed. It revealed itself to be an anti-pattern of sorts; every line of code is itself an implicit “does not throw” check, since any thrown exceptions would cause the test to fail. Simply “not throwing” is not generally a sufficient validation, so it would be expected that additional assertions would exist.
{% endhint %}

