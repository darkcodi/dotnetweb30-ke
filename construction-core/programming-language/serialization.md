# Serialization

### Configuring Objects for Serialization

The term serialization describes the **process of persisting \(and possibly transferring\)** the state of an **object into a stream** \(e.g., file stream and memory stream\). The persisted data sequence contains all the necessary information you need to **reconstruct \(or deserialize\)** the state of the object for use later. Using this technology makes it trivial to save vast amounts of data \(in various formats\). In many cases, saving application data using serialization services results in less code than using the readers/writers you find in the `System.IO` namespace.

To make an object available to .NET serialization services, all you need to do is decorate each related class \(or structure\) **with the `[Serializable]` attribute**.

If you determine that a given type has some member data that should not \(or perhaps cannot\) participate in the serialization scheme, you can mark such fields **with the `[NonSerialized]` attribute**.

```csharp
[Serializable]
public class UserPrefs
{
    public string WindowColor;
    public int FontSize;
}
```

{% hint style="info" %}
Serializers type will only serialize **public data fields** or private data exposed by **public properties**.
{% endhint %}

### Choosing a Serialization Formatter \(binary, soap, xml, etc\)

#### BinaryFormatter

The `BinaryFormatter` type serializes your object’s state to a stream using a compact **binary format**. This type is defined within the `System.Runtime.Serialization.Formatters.Binary` namespace that is part of `mscorlib.dll`.

#### SoapFormatter

The `SoapFormatter` type persists an object’s state as a SOAP message \(the standard **XML format** for passing messages to/from a web service\). This type is defined within the `System.Runtime.Serialization.Formatters.Soap` namespace, which is defined in a separate assembly.

#### XmlSerializer

If you want to persist a tree of objects as an **XML document**, you can use the `XmlSerializertype`. To use this type, you need to specify that you are using the `System.Xml.Serialization` namespace and set a reference to the assembly `System.Xml.dll`.

### Type Fidelity Among the Formatters

The most obvious difference among the three formatters is how the object graph is persisted to the stream \(binary, SOAP, or XML\). You should also be aware of a few more subtle points of distinction; specifically, how the formatters contend with **type fidelity**.

When you use the **`BinaryFormatter`** type, it will persist not only the field data of the objects in the object graph, but also each type’s fully qualified name and the full name of the defining assembly \(name, version, public key token, and culture\). These extra points of data make the `BinaryFormatter` an ideal choice when you want to transport objects by value \(e.g., as a full copy\) across machine boundaries for .NET-centric applications.

```markup
<a1:Person id="ref-1" xmlns:a1="http://schemas.microsoft.com/clr/nsassem/SimpleSerialize/MyApp%2C%20Version%3D1.0.0.0%2C%20Culture%3Dneutral%2C%20PublicKeyToken%3Dnull">
    <isAlive>true</isAlive>
    <personAge>21</personAge>
    <fName id="ref-3">Mel</fName>
</a1:Person>
```

The **`SoapFormatter`** persists traces of the assembly of origin through the use of an XML namespace. However, the `XmlSerializer` does not attempt to preserve full type fidelity; therefore, it does not record the type’s fully qualified name or assembly of origin.

```markup
<?xml version="1.0"?>
<Person xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <isAlive>true</isAlive>
    <PersonAge>21</PersonAge>
    <FirstName>Frank</FirstName>
</Person> 
```

