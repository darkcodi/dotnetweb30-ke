# Type Reflection

{% hint style="success" %}
In the .NET universe, **reflection** is the process of runtime type discovery.
{% endhint %}

Using reflection services, you are able to programmatically obtain the same metadata information displayed by _ildasm.exe_ using a friendly object model.

For example, through reflection, you can obtain a list of all types contained within a given _.dll or_ .exe assembly, including the methods, fields, properties, and events defined by a given type.

#### Core items of reflection

| Type | Meaning in Life |
| :--- | :--- |
| Assembly | This abstract class contains a number of static methods that allow you to load, investigate, and manipulate an assembly. |
| AssemblyName | This class allows you to discover numerous details behind an assembly’s identity \(version information, culture information, and so forth\). |
| EventInfo | This abstract class holds information for a given event. |
| FieldInfo | This abstract class holds information for a given field. |
| MemberInfo | This is the abstract base class that defines common behaviors for the `EventInfo`, `FieldInfo`, `MethodInfo`, and `PropertyInfo` types. |
| MethodInfo | This abstract class contains information for a given method. |
| Module | This abstract class allows you to access a given module within a multifile assembly. |
| ParameterInfo | This class holds information for a given parameter. |
| PropertyInfo | This abstract class holds information for a given property. |

#### The `System.Type` Class

The **`System.Type`** class defines a number of members that can be used to examine a type’s metadata, a great number of which return types from the `System.Reflection` namespace. For example, `Type.GetMethods()` returns an array of `MethodInfo` objects.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Meaning in Life</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>IsAbstract</p>
        <p>IsArray</p>
        <p>IsClass</p>
        <p>IsCOMObject</p>
        <p>IsEnum IsGenericTypeDefinition</p>
        <p>IsGenericParameter</p>
        <p>IsInterface</p>
        <p>IsPrimitive</p>
        <p>IsNestedPrivate</p>
        <p>IsNestedPublic</p>
        <p>IsSealed</p>
        <p>IsValueType</p>
      </td>
      <td style="text-align:left">These properties (among others) allow you to discover a number of basic
        traits about the Type you are referring to (e.g., if it is an abstract
        entity, an array, a nested class, and so forth).</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>GetConstructors()</p>
        <p>GetEvents()</p>
        <p>GetFields()</p>
        <p>GetInterfaces()</p>
        <p>GetMembers()</p>
        <p>GetMethods()</p>
        <p>GetNestedTypes()</p>
        <p>GetProperties()</p>
      </td>
      <td style="text-align:left">These methods (among others) allow you to obtain an array representing
        the items (interface, method, property, etc.) you are interested in. Each
        method returns a related array.</td>
    </tr>
    <tr>
      <td style="text-align:left">FindMembers()</td>
      <td style="text-align:left">This method returns a <code>MemberInfo</code> array based on search criteria.</td>
    </tr>
    <tr>
      <td style="text-align:left">GetType()</td>
      <td style="text-align:left">This static method returns a <code>Type</code> instance given a string name.</td>
    </tr>
    <tr>
      <td style="text-align:left">InvokeMember()</td>
      <td style="text-align:left">This method allows &#x201C;late binding&#x201D; for a given item.</td>
    </tr>
  </tbody>
</table>#### GetType\(\) vs typeof\(T\)

{% hint style="info" %}
You cannot do is directly create a `Type` object using the new keyword, as `Type` is an abstract class.
{% endhint %}

`System.Object` defines a method named `GetType()`, which returns an instance of the `Type` class that represents the metadata for the current object.

```csharp
// Obtain type information using a SportsCar instance.
SportsCar sc = new SportsCar();
Type t = sc.GetType(); 
```

The next way to obtain type information is using the C\# `typeof` operator, like so:

```csharp
// Get the type using typeof.
Type t = typeof(SportsCar);
```

Unlike `System.Object.GetType()`, the `typeof` operator is compile-time and it does not need to first create an object instance to extract type information.

