# Span&lt;T&gt; struct

Provides a type- and memory-safe representation of a contiguous region of arbitrary memory.

`Span<T>` is a [ref struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ref?view=netstandard-2.1#ref-struct-types) that is allocated on the stack rather than on the managed heap. Ref struct types have a number of restrictions to ensure that they cannot be promoted to the managed heap:

* can't be boxed
* they can't be assigned to variables of type [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object?view=netstandard-2.1)\`\`
* `dynamic` or to any interface type
* can't be fields in a reference type 
* can't be used across `await` and `yield` boundaries
* In addition, calls to two methods, [Equals\(Object\)](https://docs.microsoft.com/en-us/dotnet/api/system.span-1.equals?view=netstandard-2.1#System_Span_1_Equals_System_Object_) and [GetHashCode](https://docs.microsoft.com/en-us/dotnet/api/system.span-1.gethashcode?view=netstandard-2.1), throw a [NotSupportedException](https://docs.microsoft.com/en-us/dotnet/api/system.notsupportedexception?view=netstandard-2.1).

Note: if you need to overcome this restrictions - consider using [Memory&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.memory-1?view=netstandard-2.1). It represents a contiguous region of memory as well.,but isn't [ref struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ref?view=netstandard-2.1#ref-struct-types). So Memory&lt;T&gt; can be placed on the heap.

For spans that represent immutable or read-only structures, use [System.ReadOnlySpan&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.readonlyspan-1?view=netstandard-2.1).  
 A `Span<T>` represents a contiguous region of arbitrary memory. A `Span<T>` instance is often used to hold the elements of an array or a portion of an array. Unlike an array, however, a `Span<T>` instance can point to managed memory, native memory, or memory managed on the stack. 

The following example creates a slice of the middle five elements of a 10-element integer array. Note that the code doubles the values of each integer in the slice. As the output shows, the changes made by the span are reflected in the values of the array.C\#Copy

```csharp
using System;

namespace span
{
    class Program
    {
        static void Main(string[] args)
        {
            var array = new int[] { 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 };
            var slice = new Span<int>(array, 2, 5);
            for (int ctr = 0; ctr < slice.Length; ctr++)
               slice[ctr] *= 2;
            
            // Examine the original array values.
            foreach (var value in array)
                Console.Write($"{value}  ");
            Console.WriteLine();
        }
    }
}
// The example displays the following output:
//      2  4  12  16  20  24  28  16  18  20
```

`Span<T>` includes two overloads of the [Slice](https://docs.microsoft.com/en-us/dotnet/api/system.span-1.slice?view=netstandard-2.1) method that form a slice out of the current span that starts at a specified index. This makes it possible to treat the data in a `Span<T>` as a set of logical chunks that can be processed as needed by portions of a data processing pipeline with minimal performance impact. For example, since modern server protocols are often text-based, manipulation of strings and substrings is particularly important. In the [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netstandard-2.1) class, the major method for extracting substrings is [Substring](https://docs.microsoft.com/en-us/dotnet/api/system.string.substring?view=netstandard-2.1). For data pipelines that rely on extensive string manipulation, its use offers some performance penalties, since it:

1. Creates a new string to hold the substring.
2. Copies a subset of the characters from the original string to the new string.

Following example won't create new string objects:

```text
using System;

class Program
{
    static void Main()
    {
        string contentLength = "Content-Length: 132";
        var length = GetContentLength(contentLength.ToCharArray());	
        Console.WriteLine($"Content length: {length}"); 
    }

    private static int GetContentLength(ReadOnlySpan<char> span)
    {
        var slice = span.Slice(16);
	    return int.Parse(slice);	
    }
}
// Output:
```

### Implementation under the hood

```csharp
public readonly ref struct Span<T>
{
  private readonly ref T _pointer;
  private readonly int _length;
  ...
}
```

