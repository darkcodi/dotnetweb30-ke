# Custom attributes

You can create your own custom attributes by defining an attribute class, a class that derives directly or indirectly from `Attribute`, which makes identifying attribute definitions in metadata fast and easy.

#### Example

```csharp
[System.AttributeUsage(System.AttributeTargets.Class |  
                       System.AttributeTargets.Struct)  
]  
public class Author : System.Attribute  
{  
    private string name;  
    public double version;  
  
    public Author(string name)  
    {  
        this.name = name;  
        version = 1.0;  
    }  
}  
```

You could use this new attribute as follows:

```csharp
[Author("P. Ackerman", version = 1.1)]  
class SampleClass  
{  
    // P. Ackerman's code goes here...  
}  
```

### AllowMultiple

`AttributeUsage` has a named parameter, `AllowMultiple`, with which you can make a custom attribute single-use or multiuse.

```csharp
[System.AttributeUsage(System.AttributeTargets.Class |  
                       System.AttributeTargets.Struct,  
                       AllowMultiple = true)  // multiuse attribute  
]  
public class Author : System.Attribute 
```

In the following code example, multiple attributes of the same type are applied to a class.

```csharp
[Author("P. Ackerman", version = 1.1)]  
[Author("R. Koch", version = 1.2)]  
class SampleClass  
{  
    // P. Ackerman's code goes here...  
    // R. Koch's code goes here...  
}  
```

### Attribute usage

The `AttributeUsageAttribute` class has a public constructor that allows you to pass bit flags that indicate where your attribute can legally be applied . The `System.AttributeTargets` enumerated type is defined as follows:

```csharp
[Flags, Serializable]
public enum AttributeTargets
{
    Assembly         = 0x0001,
    Module           = 0x0002,
    Class            = 0x0004,
    Struct           = 0x0008,
    Enum             = 0x0010,
    Constructor      = 0x0020,
    Method           = 0x0040,
    Property         = 0x0080,
    Field            = 0x0100,
    Event            = 0x0200,
    Interface        = 0x0400,
    Parameter        = 0x0800,
    Delegate         = 0x1000,
    ReturnValue      = 0x2000,
    GenericParameter = 0x4000,
    All           = Assembly    | Module    | Class    | Struct | Enum  |
                    Constructor | Method    | Property | Field  | Event |
                    Interface   | Parameter | Delegate | ReturnValue |
                    GenericParameter
}
```

