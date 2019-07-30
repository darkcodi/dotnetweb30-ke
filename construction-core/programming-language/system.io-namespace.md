# System.IO namespace

### Abstract Stream Class

{% hint style="success" %}
In the world of I/O manipulation, a **stream** represents a chunk of data flowing between a source and a destination.
{% endhint %}

Streams provide a common way to interact with a _sequence of bytes_, regardless of what kind of device \(e.g., file, network connection, or printer\) stores or displays the bytes in question.

The abstract `System.IO.Stream` class defines several members that provide support for synchronous and asynchronous interactions with the storage medium \(e.g., an underlying file or memory location\).

<table>
  <thead>
    <tr>
      <th style="text-align:left">Member</th>
      <th style="text-align:left">Meaning in Life</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>CanRead</p>
        <p>CanWrite</p>
        <p>CanSeek</p>
      </td>
      <td style="text-align:left">Determines whether the current stream supports reading, seeking, and/or
        writing.</td>
    </tr>
    <tr>
      <td style="text-align:left">Close()</td>
      <td style="text-align:left">Closes the current stream and releases any resources (such as sockets
        and file handles) associated with the current stream. Kinda <code>Dispose()</code> for
        streams.</td>
    </tr>
    <tr>
      <td style="text-align:left">Flush()</td>
      <td style="text-align:left">Updates the underlying data source or repository with the current state
        of the buffer and then clears the buffer.</td>
    </tr>
    <tr>
      <td style="text-align:left">Length</td>
      <td style="text-align:left">Returns the length of the stream in bytes.</td>
    </tr>
    <tr>
      <td style="text-align:left">Position</td>
      <td style="text-align:left">Determines the position in the current stream.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Read()</p>
        <p>ReadByte()</p>
      </td>
      <td style="text-align:left">Reads a sequence of bytes (or a single byte) from the current stream and
        advances the current position in the stream by the number of bytes read.</td>
    </tr>
    <tr>
      <td style="text-align:left">Seek()</td>
      <td style="text-align:left">Sets the position in the current stream.</td>
    </tr>
    <tr>
      <td style="text-align:left">SetLength()</td>
      <td style="text-align:left">Sets the length of the current stream.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Write()</p>
        <p>WriteByte(</p>
      </td>
      <td style="text-align:left">Writes a sequence of bytes (or a single byte) to the current stream and
        advances the current position in this stream by the number of bytes written.</td>
    </tr>
  </tbody>
</table>### StreamWriters and StreamReaders

The `StreamWriter` and `StreamReader` classes are useful whenever you need to read or write character-based data \(e.g., strings\). Both of these types work by default with Unicode characters; however, you can change this by supplying a properly configured `System.Text.Encoding` object reference.

#### StreamReader

`StreamReader` derives from an abstract type named `TextReader`, as does the related `StringReader` type. The `TextReader` base class provides a limited set of functionality to each of these descendants; specifically it provides the ability to read and peek into a character stream.

#### StreamWriter

The `StreamWriter` type \(as well as `StringWriter`\) derives from an abstract base class named `TextWriter`. This class defines members that allow derived types to write textual data to a given character stream.

```csharp
static void Main(string[] args)
{
    // Get a StreamWriter and write string data.
    using(StreamWriter writer = File.CreateText("reminders.txt"))
    {
        writer.WriteLine("Don't forget these numbers:");
        for(int i = 0; i < 10; i++)
            writer.Write(i + " ");
        
        // Insert a new line.
        writer.Write(writer.NewLine);
    }
}
```

### StringWriters and StringReaders

You can use the `StringWriter` and `StringReader` types to treat textual information as a stream of in-memory characters. This can prove helpful when you would like to append character-based information to an underlying buffer.

```csharp
static void Main(string[] args)
{
    // Create a StringWriter and emit character data to memory.
    using(StringWriter strWriter = new StringWriter())
    {
        strWriter.WriteLine("Don't forget Mother's Day this year...");
        
        // Get a copy of the contents (stored in a string) and dump to console.
        Console.WriteLine("Contents of StringWriter:\n{0}", strWriter);
    }
    Console.ReadLine();
}
```

`StringWriter` and `StreamWriter` both derive from the same base class \(`TextWriter`\), so the writing logic is more or less identical. However, given the nature of `StringWriter`, you can use **`GetStringBuilder()`** ``method to extract a `System.Text.StringBuilder` object.

### Watching Files Programmatically

**`FileSystemWatcher`** class can be quite helpful when you want to monitor \(or “watch”\) files on your system programmatically. Specifically, you can instruct the `FileSystemWatcher` type to monitor files for any of the actions specified by the `System.IO.NotifyFilters` enumeration:

```csharp
public enum NotifyFilters
{
    Attributes, CreationTime,
    DirectoryName, FileName,
    LastAccess, LastWrite,
    Security, Size
}
```

You can also specify filename regex filter.

```csharp
static void Main(string[] args)
{
   // Establish the path to the directory to watch.
   FileSystemWatcher watcher = new FileSystemWatcher();
   try
   {
      watcher.Path = @"C:\MyFolder";
   }
   catch(ArgumentException ex)
   {
      Console.WriteLine(ex.Message);
      return;
   }
   
   // Set up the things to be on the lookout for.
   watcher.NotifyFilter = NotifyFilters.LastAccess
      | NotifyFilters.LastWrite
      | NotifyFilters.FileName
      | NotifyFilters.DirectoryName;
   
   // Only watch text files.
   watcher.Filter = "*.txt";
   
   // Add event handlers.
   watcher.Changed += new FileSystemEventHandler(OnChanged);
   watcher.Created += new FileSystemEventHandler(OnChanged);
   watcher.Deleted += new FileSystemEventHandler(OnChanged);
   watcher.Renamed += new RenamedEventHandler(OnRenamed);
   
   // Begin watching the directory.
   watcher.EnableRaisingEvents = true;
   
   // Wait for the user to quit the program.
   Console.WriteLine(@"Press 'q' to quit app.");
   while(Console.Read()!='q');
} 
```

