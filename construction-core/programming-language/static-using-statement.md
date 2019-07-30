# Static Using Statement

The feature allows all the accessible static members of a type to be imported, making them available without qualification in subsequent code:

```csharp
using static System.Console;
using static System.Math;
using static System.DayOfWeek;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4)); 
        WriteLine(Friday - Monday); 
    }
}
```

This is great for when you have a set of functions related to a certain domain that you use all the time. `System.Math` would be a common example of that. It also lets you directly specify the individual named values of an enum type, like the `System.DayOfWeek` members above.

