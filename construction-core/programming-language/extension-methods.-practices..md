# Extension methods. Practices.

Extension methods are a language feature that allows static methods to be called using instance method call syntax. These methods must take at least one parameter, which represents the instance the method is to operate on.

The class that defines such extension methods is referred to as the "sponsor" class, and it must be declared as static. To use extension methods, one must import the namespace defining the sponsor class.

```csharp
class Program
{
    static void Main(string[] args)
    {
        string s = "Hello";
        char c = '!';
        int i = s.WordCount(c);
        Console.WriteLine(i);
 
        Console.ReadLine();
    }
}

public static class StringExtension
{
    public static int WordCount(this string str, char c)
    {
        int counter = 0;
        for (int i = 0; i<str.Length; i++)
        {
            if (str[i] == c)
                counter++;
        }
        return counter;
    }
```

**X AVOID** frivolously defining extension methods, especially on types you don’t own.

**✓ CONSIDER** using extension methods in any of the following scenarios:

* To provide helper functionality relevant to every implementation of an interface, if said functionality can be written in terms of the core interface. This is because concrete implementations cannot otherwise be assigned to interfaces. For example, the `LINQ to Objects` operators are implemented as extension methods for all [IEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1) types. Thus, any `IEnumerable<>`implementation is automatically LINQ-enabled.
* When an instance method would introduce a dependency on some type, but such a dependency would break dependency management rules. For example, a dependency from [String](https://docs.microsoft.com/en-us/dotnet/api/system.string) to [System.Uri](https://docs.microsoft.com/en-us/dotnet/api/system.uri) is probably not desirable, and so `String.ToUri()`instance method returning `System.Uri` would be the wrong design from a dependency management perspective. A static extension method `Uri.ToUri(this string str)` returning `System.Uri` would be a much better design.

**X AVOID** defining extension methods on [System.Object](https://docs.microsoft.com/en-us/dotnet/api/system.object).

**X DO NOT** put extension methods in the same namespace as the extended type unless it is for adding methods to interfaces or for dependency management.

**X AVOID** defining two or more extension methods with the same signature, even if they reside in different namespaces.

**✓ CONSIDER** defining extension methods in the same namespace as the extended type if the type is an interface and if the extension methods are meant to be used in most or all cases.

**X DO NOT** define extension methods implementing a feature in namespaces normally associated with other features. Instead, define them in the namespace associated with the feature they belong to.

**X AVOID** generic naming of namespaces dedicated to extension methods \(e.g., "Extensions"\). Use a descriptive name \(e.g., "Routing"\) instead.

