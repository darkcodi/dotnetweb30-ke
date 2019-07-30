# File Providers

ASP.NET Core abstracts file system access through the use of File Providers. File Providers are used throughout the ASP.NET Core framework:

* **IHostingEnvironment** exposes the app's content root and web root as `IFileProvider` types.
* **Static File Middleware** uses File Providers to locate static files.
* **Razor** uses File Providers to locate pages and views.

### File Provider interfaces <a id="file-provider-interfaces"></a>

The primary interface is **`IFileProvider`**. It exposes methods to:

* Obtain file information \(`IFileInfo`\).
* Obtain directory information \(`IDirectoryContents`\).
* Set up change notifications \(using an `IChangeToken`\).

**`IFileInfo`** provides methods and properties for working with files:

* Exists
* IsDirectory
* Name
* Length \(in bytes\)
* LastModified date

### File Provider implementations <a id="file-provider-implementations"></a>

Three implementations of `IFileProvider` are available.

| Implementation | Description |
| :--- | :--- |
| **PhysicalFileProvider** | The physical provider is used to access the system's physical files. |
| **ManifestEmbeddedFileProvider** | The manifest embedded provider is used to access files embedded in assemblies. |
| **CompositeFileProvider** | The composite provider is used to provide combined access to files and directories from one or more other providers. |

