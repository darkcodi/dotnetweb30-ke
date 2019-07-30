# Building comparable types

`IComparable` Interface defines a generalized type-specific comparison method that a value type or class implements to order or sort its instances.

This interface is implemented by types whose values can be ordered or sorted. It requires that implementing types define a single method, `CompareTo(Object)`, that indicates whether the position of the current instance in the sort order is before, after, or the same as a second object of the same type. The instance's `IComparable` implementation is called automatically by methods such as `Array.Sort` and `ArrayList.Sort`.

The implementation of the `CompareTo(Object)` method must return an `Int32` that has one of three values, as shown in the following table.

| Value | Meaning |
| :--- | :--- |
| Less than zero | The current instance precedes the object specified by the `CompareTo` method in the sort order. |
| Zero | This current instance occurs in the same position in the sort order as the object specified by the `CompareTo` method. |
| Greater than zero | This current instance follows the object specified by the `CompareTo` method in the sort order. |

All numeric types \(such as `Int32` and `Double`\) implement `IComparable`, as do `String`, `Char`, and `DateTime`. Custom types should also provide their own implementation of `IComparable` to enable object instances to be ordered or sorted.

```csharp
public class Temperature : IComparable 
{
    // The temperature value
    protected double temperatureF;

    public int CompareTo(object obj) {
        if (obj == null) return 1;
        
        Temperature otherTemperature = obj as Temperature;
        if (otherTemperature != null) 
            return this.temperatureF.CompareTo(otherTemperature.temperatureF);
        else
           throw new ArgumentException("Object is not a Temperature");
    }
}
```

