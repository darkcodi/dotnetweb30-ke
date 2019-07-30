# Building cloneable objects

`ICloneable` Interface supports cloning, which creates a new instance of a class with the same value as an existing instance.

The `ICloneable` interface enables you to provide a customized implementation that creates a copy of an existing object. The `ICloneable` interface contains one member, the `Clone` method, which is intended to provide cloning support beyond that supplied by `Object.MemberwiseClone`. 

The `ICloneable` interface simply requires that your implementation of the `Clone()` method return a copy of the current object instance. It does not specify whether the cloning operation performs a deep copy, a shallow copy, or something in between. Nor does it require all property values of the original instance to be copied to the new instance. For example, the `Clone()` method performs a shallow copy of all properties except the `IsReadOnly` property; it always sets this property value to `false` in the cloned object. Because callers of `Clone()` cannot depend on the method performing a predictable cloning operation, we recommend that `ICloneable` not be implemented in public APIs.

```csharp
public class Person 
{
    public int Age;
    public string Name;
    public IdInfo IdInfo;

    public Person ShallowCopy()
    {
       return (Person) this.MemberwiseClone();
    }

    public Person DeepCopy()
    {
       Person other = (Person) this.MemberwiseClone();
       other.IdInfo = new IdInfo(IdInfo.IdNumber);
       other.Name = String.Copy(Name);
       return other;
    }
}
```

