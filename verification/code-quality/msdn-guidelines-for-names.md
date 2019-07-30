# MSDN: Guidelines for Names

### Capitalization Conventions

**Capitalization Rules for Identifiers**

To differentiate words in an identifier, capitalize the first letter of each word in the identifier. There are two appropriate ways to capitalize identifiers, depending on the use of the identifier:

* PascalCasing \(upper camel case\), used for all identifiers except parameter names
* dromedaryCasing \(lower camel case\), used only for parameter names

**Case Sensitivity**

Languages that can run on the CLR are not required to support case-sensitivity, although some do. Even if your language supports it, other languages that might access your framework do not. Any APIs that are externally accessible, therefore, cannot rely on case alone to distinguish between two names in the same context.

**X DO NOT** assume that all programming languages are case sensitive. They are not. Names cannot differ by case alone.

### General Naming Conventions

**Word Choice**

**✓** **DO** choose easily readable identifier names.

**✓** **DO** favor readability over brevity.

**X DO NOT** use underscores, hyphens, or any other nonalphanumeric characters.

**X DO NOT** use Hungarian notation.

**X AVOID** using identifiers that conflict with keywords of widely used programming languages.

**Using Abbreviations and Acronyms**

**X DO NOT** use abbreviations or contractions as part of identifier names.

**X DO NOT** use any acronyms that are not widely accepted, and even if they are, only when necessary.

**Avoiding Language-Specific Names**

**✓** **DO** use semantically interesting names rather than language-specific keywords for type names.

**✓** **DO** use a generic CLR type name, rather than a language-specific name, in the rare cases when an identifier has no semantic meaning beyond its type.

 **✓** **DO** use a common name, such as `value` or `item`, rather than repeating the type name, in the rare cases when an identifier has no semantic meaning and the type of the parameter is not important.

**Naming New Versions of Existing APIs**

**✓** **DO** use a name similar to the old API when creating new versions of an existing API.

**✓** **DO** prefer adding a suffix rather than a prefix to indicate a new version of an existing API.

**✓** **CONSIDER** using a brand new, but meaningful identifier, instead of adding a suffix or a prefix.

**✓** **DO** use a numeric suffix to indicate a new version of an existing API, particularly if the existing name of the API is the only name that makes sense \(i.e., if it is an industry standard\) and if adding any meaningful suffix \(or changing the name\) is not an appropriate option.

**X DO NOT** use the "Ex" \(or a similar\) suffix for an identifier to distinguish it from an earlier version of the same API.

**✓** **DO** use the "64" suffix when introducing versions of APIs that operate on a 64-bit integer \(a long integer\) instead of a 32-bit integer.

### Names of Assemblies and DLLs

An assembly is the unit of deployment and identity for managed code programs. Although assemblies can span one or more files, typically an assembly maps one-to-one with a DLL. Therefore, this section describes only DLL naming conventions, which then can be mapped to assembly naming conventions.

**✓** **DO** choose names for your assembly DLLs that suggest large chunks of functionality, such as System.Data.

Assembly and DLL names don’t have to correspond to namespace names, but it is reasonable to follow the namespace name when naming assemblies. A good rule of thumb is to name the DLL based on the common prefix of the namespaces contained in the assembly. For example, an assembly with two namespaces, `MyCompany.MyTechnology.FirstFeature` and `MyCompany.MyTechnology.SecondFeature`, could be called `MyCompany.MyTechnology.dll`.

**✓** **CONSIDER** naming DLLs according to the following pattern:

`<Company>.<Component>.dll`

### Names of Classes, Structs, and Interfaces

**✓** **DO** name classes and structs with nouns or noun phrases, using PascalCasing.

**✓** **DO** name interfaces with adjective phrases, or occasionally with nouns or noun phrases.

**X DO NOT** give class names a prefix \(e.g., "C"\).

**✓** **CONSIDER** ending the name of derived classes with the name of the base class.

**✓** **DO** prefix interface names with the letter I, to indicate that the type is an interface.

**✓** **DO** ensure that the names differ only by the "I" prefix on the interface name when you are defining a class–interface pair where the class is a standard implementation of the interface.

**Names of Generic Type Parameters**

**✓** **DO** name generic type parameters with descriptive names unless a single-letter name is completely self-explanatory and a descriptive name would not add value.

**✓** **CONSIDER** using `T` as the type parameter name for types with one single-letter type parameter.

**✓** **DO** prefix descriptive type parameter names with `T`.

**✓** **CONSIDER** indicating constraints placed on a type parameter in the name of the parameter.

For example, a parameter constrained to `ISession` might be called `TSession`.

**Names of Common Types**

**✓** **DO** follow the guidelines described in the following table when naming types derived from or implementing certain .NET Framework types.

| **Base Type** | **Derived/Implementing Type Guideline** |
| :--- | :--- |
| `System.Attribute` | **✓** **DO** add the suffix "Attribute" to names of custom attribute classes. |
| `System.Delegate` | **✓** **DO** add the suffix "EventHandler" to names of delegates that are used in events.   **✓** **DO** add the suffix "Callback" to names of delegates other than those used as event handlers.   **X DO NOT** add the suffix "Delegate" to a delegate. |
| `System.EventArgs` | **✓** **DO** add the suffix "EventArgs." |
| `System.Enum` | **X DO NOT** derive from this class; use the keyword supported by your language instead; for example, in C\#, use the `enum` keyword.   **X DO NOT** add the suffix "Enum" or "Flag." |
| `System.Exception` | **✓** **DO** add the suffix "Exception." |
| `IDictionary`   `IDictionary<TKey,TValue>` | **✓** **DO** add the suffix "Dictionary." Note that `IDictionary` is a specific type of collection, but this guideline takes precedence over the more general collections guideline that follows. |
| `IEnumerable`   `ICollection`   `IList`   `IEnumerable<T>`   `ICollection<T>`   `IList<T>` | **✓** **DO** add the suffix "Collection." |
| `System.IO.Stream` | **✓** **DO** add the suffix "Stream." |
| `CodeAccessPermission IPermission` | **✓** **DO** add the suffix "Permission." |

**Naming Enumerations**

**✓** **DO** use a singular type name for an enumeration unless its values are bit fields.

**✓** **DO** use a plural type name for an enumeration with bit fields as values, also called flags enum.

**X DO NOT** use an "Enum" suffix in enum type names.

**X DO NOT** use "Flag" or "Flags" suffixes in enum type names.

**X DO NOT** use a prefix on enumeration value names \(e.g., "ad" for ADO enums, "rtf" for rich text enums, etc.\).

### Names of Type Members

**Names of Methods**

**✓** **DO** give methods names that are verbs or verb phrases.

**Names of Properties**

**✓** **DO** name properties using a noun, noun phrase, or adjective.

**X DO NOT** have properties that match the name of "Get" methods.

**✓** **DO** name collection properties with a plural phrase describing the items in the collection instead of using a singular phrase followed by "List" or "Collection."

**✓** **DO** name Boolean properties with an affirmative phrase \(`CanSeek` instead of `CantSeek`\). Optionally, you can also prefix Boolean properties with "Is," "Can," or "Has," but only where it adds value.

**✓** **CONSIDER** giving a property the same name as its type.

**Names of Events**

**✓** **DO** name events with a verb or a verb phrase.

**✓** **DO** give events names with a concept of before and after, using the present and past tenses.

For example, a close event that is raised before a window is closed would be called `Closing`, and one that is raised after the window is closed would be called `Closed`.

**X DO NOT** use "Before" or "After" prefixes or postfixes to indicate pre- and post-events. Use present and past tenses as just described.

**✓** **DO** name event handlers \(delegates used as types of events\) with the "EventHandler" suffix.

**✓** **DO** use two parameters named `sender` and `e` in event handlers.

**✓** **DO** name event argument classes with the "EventArgs" suffix.

**Names of Fields**

**✓** **DO** use PascalCasing in field names.

**✓** **DO** name fields using a noun, noun phrase, or adjective.

**X DO NOT** use a prefix for field names.

For example, do not use "g\_" or "s\_" to indicate static fields.

### Naming Parameters

**✓** **DO** use camelCasing in parameter names.

**✓** **DO** use descriptive parameter names.

**✓** **CONSIDER** using names based on a parameter’s meaning rather than the parameter’s type.

**Naming Operator Overload Parameters**

**✓** **DO** use `left` and `right` for binary operator overload parameter names if there is no meaning to the parameters.

**✓** **DO** use `value` for unary operator overload parameter names if there is no meaning to the parameters.

**✓** **CONSIDER** meaningful names for operator overload parameters if doing so adds significant value.

**X DO NOT** use abbreviations or numeric indices for operator overload parameter names.

### Naming Resources

Because localizable resources can be referenced via certain objects as if they were properties, the naming guidelines for resources are similar to property guidelines.

**✓** **DO** use PascalCasing in resource keys.

**✓** **DO** provide descriptive rather than short identifiers.

**X DO NOT** use language-specific keywords of the main CLR languages.

**✓** **DO** use only alphanumeric characters and underscores in naming resources.

**✓** **DO** use the following naming convention for exception message resources.

The resource identifier should be the exception type name plus a short identifier of the exception:

`ArgumentExceptionIllegalCharacters`  
 `ArgumentExceptionInvalidName`  
 `ArgumentExceptionFileNameIsMalformed`

