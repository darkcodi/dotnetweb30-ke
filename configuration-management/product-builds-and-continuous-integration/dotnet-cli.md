# Dotnet cli

### dotnet cli prerequisites

Supported Windows Versions

.NET Core is supported on the following versions of Windows −

Windows 7 SP1

Windows 8.1

Windows 10

Windows Server 2008 R2 SP1 \(Full Server or Server Core\)

Windows Server 2012 SP1 \(Full Server or Server Core\)

Windows Server 2012 R2 SP1 \(Full Server or Server Core\)

Windows Server 2016 \(Full Server, Server Core or Nano Server\)

Dependencies

If you are running your .NET Core application on Windows versions earlier than Windows 10 and Windows Server 2016, then it will also require the Visual C++ Redistributable.

This dependency is automatically installed for you if you use the .NET Core installer.

You need to manually install the Visual C++ Redistributable for Visual Studio 2015 if you are installing .NET Core via the installer script or deploying a self-contained .NET Core application.

For Windows 7 and Windows Server 2008 machines, you need to make sure that your Windows installation is up-to-date and also includes hotfix KB2533623 installed through Windows Update.

Prerequisites with Visual Studio

To develop .NET Core applications using the .NET Core SDK, you can use any editor of your choice.

However, if you want to develop .NET Core applications on Windows using Visual Studio, you can use the following two versions −

Visual Studio 2015

Visual Studio 2017 RC

Projects created with Visual Studio 2015 will be project.json-based by default while projects created with Visual Studio 2017 RC will always be MSBuild-based.

### Clean

The dotnet clean command cleans the output of the previous build. It's implemented as an MSBuild target, so the project is evaluated when the command is run. Only the outputs created during the build are cleaned. Both intermediate \(obj\) and final output \(bin\) folders are cleaned.

**Arguments**

The MSBuild project or solution to clean. If a project or solution file is not specified, MSBuild searches the current working directory for a file that has a file extension that ends in proj or sln, and uses that file.

**Options**

·         **-c\|--configuration {Debug\|Release}**

Defines the build configuration. The default value is Debug. This option is only required when cleaning if you specified it during build time.

·         **-f\|--framework &lt;FRAMEWORK&gt;**

The [framework](https://docs.microsoft.com/en-us/dotnet/standard/frameworks) that was specified at build time. The framework must be defined in the [project file](https://docs.microsoft.com/en-us/dotnet/core/tools/csproj). If you specified the framework at build time, you must specify the framework when cleaning.

·         **-h\|--help**

Prints out a short help for the command.

·         **--interactive**

Allows the command to stop and wait for user input or action. For example, to complete authentication. Available since .NET Core 3.0 SDK.

·         **--nologo**

Doesn't display the startup banner or the copyright message. Available since .NET Core 3.0 SDK.

·         **-o\|--output &lt;OUTPUT\_DIRECTORY&gt;**

The directory that contains the build artifacts to clean. Specify the -f\|--framework &lt;FRAMEWORK&gt; switch with the output directory switch if you specified the framework when the project was built.

·         **-r\|--runtime &lt;RUNTIME\_IDENTIFIER&gt;**

Cleans the output folder of the specified runtime. This is used when a [self-contained deployment](https://docs.microsoft.com/en-us/dotnet/core/deploying/index#self-contained-deployments-scd) was created. Option available since .NET Core 2.0 SDK.

·         **-v\|--verbosity &lt;LEVEL&gt;**

Sets the MSBuild verbosity level. Allowed values are q\[uiet\], m\[inimal\], n\[ormal\], d\[etailed\], and diag\[nostic\]. The default is normal.

### **msbuild**

The dotnet msbuild command allows access to a fully functional MSBuild. The command has the exact same capabilities as the existing MSBuild command-line client for SDK-style project only. The options are all the same. For more information about the available options, see the MSBuild Command-Line Reference. The dotnet build command is equivalent to dotnet msbuild -restore -target:Build. dotnet build is more commonly used for building projects, but dotnet msbuild gives you more control. For example, if you have a specific target you want to run \(without running the build target\), you probably want to use dotnet msbuild.

**Examples**

* Build a project and its dependencies: ****`dotnet msbuild`
* Build a project and its dependencies using Release configuration:

  `dotnet msbuild -p:Configuration=Release`

* Run the publish target and publish for the osx.10.11-x64 RID:

  `dotnet msbuild -t:Publish -p:RuntimeIdentifiers=osx.10.11-x64` 

* See the whole project with all targets included by the SDK:

  `dotnet msbuild -pp`

### Build

The dotnet build command builds the project and its dependencies into a set of binaries. The binaries include the project's code in Intermediate Language \(IL\) files with a .dll extension and symbol files used for debugging with a .pdb extension. A dependencies JSON file \(_.deps.json\) is produced that lists the dependencies of the application. A_ .runtimeconfig.json file is produced, which specifies the shared runtime and its version for the application.

If the project has third-party dependencies, such as libraries from NuGet, they're resolved from the NuGet cache and aren't available with the project's built output. With that in mind, the product of dotnet build isn't ready to be transferred to another machine to run. This is in contrast to the behavior of the .NET Framework in which building an executable project \(an application\) produces output that's runnable on any machine where the .NET Framework is installed. To have a similar experience with .NET Core, you need to use the dotnet publishcommand. For more information, see .NET Core Application Deployment.

Building requires the project.assets.json file, which lists the dependencies of your application. The file is created when dotnet restore is executed. Without the assets file in place, the tooling can't resolve reference assemblies, which results in errors. With .NET Core 1.x SDK, you needed to explicitly run the dotnet restore before running dotnet build. Starting with .NET Core 2.0 SDK, dotnet restore runs implicitly when you run dotnet build. If you want to disable implicit restore when running the build command, you can pass the --no-restore option.

{% hint style="info" %}
Starting with .NET Core 2.0, you don't have to run [dotnet restore](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-restore) because it's run implicitly by all commands, such as dotnet build and dotnet run, that require a restore to occur. It's still a valid command in certain scenarios where doing an explicit restore makes sense, such as [continuous integration builds in Azure DevOps Services](https://docs.microsoft.com/en-us/azure/devops/build-release/apps/aspnet/build-aspnet-core) or in build systems that need to explicitly control the time at which the restore occurs.
{% endhint %}

This command also supports the dotnet restore options when passed in the long form \(for example, --source\). Short form options, such as -s, are not supported.

Whether the project is executable or not is determined by the  property in the project file. The following example shows a project that produces executable code:

```text
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

To produce a library, omit the  property. The main difference in built output is that the IL DLL for a library doesn't contain entry points and can't be executed.

**Arguments**

The project or solution file to build. If a project or solution file isn't specified, MSBuild searches the current working directory for a file that has a file extension that ends in either proj or sln and uses that file.

**Options**

·         **`-c|--configuration {Debug|Release}`**

Defines the build configuration. The default value is `Debug`.

·         **`-f|--framework <FRAMEWORK>`**

Compiles for a specific [framework](https://docs.microsoft.com/en-us/dotnet/standard/frameworks). The framework must be defined in the [project file](https://docs.microsoft.com/en-us/dotnet/core/tools/csproj).

·         **`--force`**

Forces all dependencies to be resolved even if the last restore was successful. Specifying this flag is the same as deleting the _project.assets.json_ file. Available since .NET Core 2.0 SDK.

·         **`-h|--help`**

Prints out a short help for the command.

·         **`--interactive`**

Allows the command to stop and wait for user input or action. For example, to complete authentication. Available since .NET Core 3.0 SDK.

·         **`--no-dependencies`**

Ignores project-to-project \(P2P\) references and only builds the specified root project.

·         **`--no-incremental`**

Marks the build as unsafe for incremental build. This flag turns off incremental compilation and forces a clean rebuild of the project's dependency graph.

·         **`--no-logo`**

Doesn't display the startup banner or the copyright message. Available since .NET Core 3.0 SDK.

·         **`--no-restore`**

Doesn't execute an implicit restore during build. Available since .NET Core 2.0 SDK.

·         **`-o|--output <OUTPUT_DIRECTORY>`**

Directory in which to place the built binaries. You also need to define `--framework` when you specify this option. If not specified, the default path is `./bin/<configuration>/<framework>/`.

·         **`-r|--runtime <RUNTIME_IDENTIFIER>`**

Specifies the target runtime. For a list of Runtime Identifiers \(RIDs\), see the [RID catalog](https://docs.microsoft.com/en-us/dotnet/core/rid-catalog).

·         **`-v|--verbosity <LEVEL>`**

Sets the MSBuild verbosity level. Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`. The default is `minimal`.

·         **`--version-suffix <VERSION_SUFFIX>`**

Sets the value of the `$(VersionSuffix)` property to use when building the project. This only works if the `$(Version)` property isn't set. Then, `$(Version)` is set to the `$(VersionPrefix)` combined with the `$(VersionSuffix)`, separated by a dash.

### **Run**

The dotnet run command provides a convenient option to run your application from the source code with one command. It's useful for fast iterative development from the command line. The command depends on the dotnet build command to build the code. Any requirements for the build, such as that the project must be restored first, apply to dotnet run as well.

Output files are written into the default location, which is bin//. For example if you have a netcoreapp2.1 application and you run dotnet run, the output is placed in bin/Debug/netcoreapp2.1. Files are overwritten as needed. Temporary files are placed in the obj directory.

If the project specifies multiple frameworks, executing dotnet run results in an error unless the -f\|--framework  option is used to specify the framework.

The dotnet run command is used in the context of projects, not built assemblies. If you're trying to run a framework-dependent application DLL instead, you must use dotnet without a command. For example, to run myapp.dll, use:

```text
dotnet myapp.dll
```

For more information on the dotnet driver, see the .NET Core Command Line Tools \(CLI\) topic.

To run the application, the dotnet run command resolves the dependencies of the application that are outside of the shared runtime from the NuGet cache. Because it uses cached dependencies, it's not recommended to use dotnet run to run applications in production. Instead, create a deployment using the dotnet publishcommand and deploy the published output.

{% hint style="info" %}
Starting with .NET Core 2.0, you don't have to run dotnet restore because it's run implicitly by all commands, such as dotnet build and dotnet run, that require a restore to occur. It's still a valid command in certain scenarios where doing an explicit restore makes sense, such as continuous integration builds in Azure DevOps Services or in build systems that need to explicitly control the time at which the restore occurs. This command also supports the dotnet restore options when passed in the long form \(for example, --source\). Short form options, such as -s, are not supported.
{% endhint %}

**Options**

Delimits arguments to dotnet run from arguments for the application being run. All arguments after this delimiter are passed to the application run.

`-c|--configuration {Debug|Release}`

Defines the build configuration. The default value is Debug.

`-f|--framework <FRAMEWORK>`

Builds and runs the app using the specified [framework](https://docs.microsoft.com/en-us/dotnet/standard/frameworks). The framework must be specified in the project file.

`--force`

Forces all dependencies to be resolved even if the last restore was successful. Specifying this flag is the same as deleting the project.assets.json file.

`-h|--help`

Prints out a short help for the command.

`--launch-profile <NAME>`

The name of the launch profile \(if any\) to use when launching the application. Launch profiles are defined in the launchSettings.json file and are typically called Development, Staging, and Production. For more information, see [Working with multiple environments](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/environments).

`--no-build`

Doesn't build the project before running. It also implicit sets the --no-restore flag.

`--no-dependencies`

When restoring a project with project-to-project \(P2P\) references, restores the root project and not the references.

`--no-launch-profile`

Doesn't try to use launchSettings.json to configure the application.

`--no-restore`

Doesn't execute an implicit restore when running the command.

`-p|--project <PATH>`

Specifies the path of the project file to run \(folder name or full path\). If not specified, it defaults to the current directory.

`--runtime <RUNTIME_IDENTIFIER>`

Specifies the target runtime to restore packages for. For a list of Runtime Identifiers \(RIDs\), see the [RID catalog](https://docs.microsoft.com/en-us/dotnet/core/rid-catalog).

`-v|--verbosity <LEVEL>`

Sets the verbosity level of the command. Allowed values are q\[uiet\], m\[inimal\], n\[ormal\], d\[etailed\], and diag\[nostic\].

### **Publish**

dotnet publish compiles the application, reads through its dependencies specified in the project file, and publishes the resulting set of files to a directory. The output includes the following assets:

Intermediate Language \(IL\) code in an assembly with a dll extension.

.deps.json file that includes all of the dependencies of the project.

.runtime.config.json file that specifies the shared runtime that the application expects, as well as other configuration options for the runtime \(for example, garbage collection type\).

The application's dependencies, which are copied from the NuGet cache into the output folder.

The dotnet publish command's output is ready for deployment to a hosting system \(for example, a server, PC, Mac, laptop\) for execution. It's the only officially supported way to prepare the application for deployment. Depending on the type of deployment that the project specifies, the hosting system may or may not have the .NET Core shared runtime installed on it. For more information, see .NET Core Application Deployment. For the directory structure of a published application, see Directory structure.

{% hint style="info" %}
Starting with .NET Core 2.0, you don't have to run dotnet restore because it's run implicitly by all commands, such as dotnet build and dotnet run, that require a restore to occur. It's still a valid command in certain scenarios where doing an explicit restore makes sense, such as continuous integration builds in Azure DevOps Services or in build systems that need to explicitly control the time at which the restore occurs.
{% endhint %}

This command also supports the dotnet restore options when passed in the long form \(for example, --source\). Short form options, such as -s, are not supported.

**Arguments**

The project to publish. It's either the path and filename of a C\#, F\#, or Visual Basic project file, or the path to a directory that contains a C\#, F\#, or Visual Basic project file. If not specified, it defaults to the current directory.

**Options**

[.NET Core 2.1](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish?tabs=netcore21#tabpanel_CeZOj-G++Q-1_netcore21)

[.NET Core 2.0](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish?tabs=netcore21#tabpanel_CeZOj-G++Q-1_netcore20)

[.NET Core 1.x](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish?tabs=netcore21#tabpanel_CeZOj-G++Q-1_netcore1x)

`-c|--configuration {Debug|Release}`

Defines the build configuration. The default value is Debug.

`-f|--framework <FRAMEWORK>`

Publishes the application for the specified [target framework](https://docs.microsoft.com/en-us/dotnet/standard/frameworks). You must specify the target framework in the project file.

`--force`

Forces all dependencies to be resolved even if the last restore was successful. Specifying this flag is the same as deleting the project.assets.json file.

`-h|--help`

Prints out a short help for the command.

`--manifest <PATH_TO_MANIFEST_FILE>`

Specifies one or several [target manifests](https://docs.microsoft.com/en-us/dotnet/core/deploying/runtime-store) to use to trim the set of packages published with the app. The manifest file is part of the output of the [dotnet store command](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-store). To specify multiple manifests, add a --manifest option for each manifest. This option is available starting with .NET Core 2.0 SDK.

`--no-build`

Doesn't build the project before publishing. It also implicitly sets the --no-restore flag.

`--no-dependencies`

Ignores project-to-project references and only restores the root project.

`--no-restore`

Doesn't execute an implicit restore when running the command.

`-o|--output <OUTPUT_DIRECTORY>`

Specifies the path for the output directory. If not specified, it defaults to ./bin/\[configuration\]/\[framework\]/publish/ for a framework-dependent deployment or ./bin/\[configuration\]/\[framework\]/\[runtime\]/publish/ for a self-contained deployment. If the path is relative, the output directory generated is relative to the project file location, not to the current working directory.

`--self-contained`

Publishes the .NET Core runtime with your application so the runtime doesn't need to be installed on the target machine. If a runtime identifier is specified, its default value is true. For more information about the different deployment types, see [.NET Core application deployment](https://docs.microsoft.com/en-us/dotnet/core/deploying/index).

`-r|--runtime <RUNTIME_IDENTIFIER>`

Publishes the application for a given runtime. This is used when creating a [self-contained deployment \(SCD\)](https://docs.microsoft.com/en-us/dotnet/core/deploying/index#self-contained-deployments-scd). For a list of Runtime Identifiers \(RIDs\), see the [RID catalog](https://docs.microsoft.com/en-us/dotnet/core/rid-catalog). Default is to publish a [framework-dependent deployment \(FDD\)](https://docs.microsoft.com/en-us/dotnet/core/deploying/index#framework-dependent-deployments-fdd).

`-v|--verbosity <LEVEL>`

Sets the verbosity level of the command. Allowed values are q\[uiet\], m\[inimal\], n\[ormal\], d\[etailed\], and diag\[nostic\].

`--version-suffix <VERSION_SUFFIX>`

Defines the version suffix to replace the asterisk \(\*\) in the version field of the project file.

### **Test**

The dotnet test command is used to execute unit tests in a given project. The dotnet test command launches the test runner console application specified for a project. The test runner executes the tests defined for a unit test framework \(for example, MSTest, NUnit, or xUnit\) and reports the success or failure of each test. If all tests are successful, the test runner returns 0 as an exit code; otherwise if any test fails, it returns 1. The test runner and the unit test library are packaged as NuGet packages and are restored as ordinary dependencies for the project.

Test projects specify the test runner using an ordinary  element, as seen in the following sample project file:

```text
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.2</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.9.0" />
    <PackageReference Include="xunit" Version="2.4.0" />
    <PackageReference Include="xunit.runner.visualstudio" Version="2.4.0" />
  </ItemGroup>

</Project>
```

**Arguments**

Path to the test project. If not specified, it defaults to current directory.

**Options**

·         [.NET Core 2.1](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-test?tabs=netcore21#tabpanel_CeZOj-G++Q-1_netcore21)

·         [.NET Core 2.0](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-test?tabs=netcore21#tabpanel_CeZOj-G++Q-1_netcore20)

·         [.NET Core 1.x](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-test?tabs=netcore21#tabpanel_CeZOj-G++Q-1_netcore1x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

Use the custom test adapters from the specified path in the test run.

`--blame`

Runs the tests in blame mode. This option is helpful in isolating the problematic tests causing test host to crash. It creates an output file in the current directory as Sequence.xml that captures the order of tests execution before the crash.

`-c|--configuration {Debug|Release}`

Defines the build configuration. The default value is Debug, but your project's configuration could override this default SDK setting.

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

Enables data collector for the test run. For more information, see [Monitor and analyze test run](https://aka.ms/vstest-collect).

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

Enables diagnostic mode for the test platform and write diagnostic messages to the specified file.

`-f|--framework <FRAMEWORK>`

Looks for test binaries for a specific [framework](https://docs.microsoft.com/en-us/dotnet/standard/frameworks).

`--filter <EXPRESSION>`

Filters out tests in the current project using the given expression. For more information, see the [Filter option details](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-test?tabs=netcore21#filter-option-details) section. For more information and examples on how to use selective unit test filtering, see [Running selective unit tests](https://docs.microsoft.com/en-us/dotnet/core/testing/selective-unit-tests).

`-h|--help`

Prints out a short help for the command.

`-l|--logger <LoggerUri/FriendlyName>`

Specifies a logger for test results.

`--no-build`

Doesn't build the test project before running it. It also implicit sets the --no-restore flag.

`--no-restore`

Doesn't execute an implicit restore when running the command.

`-o|--output <OUTPUT_DIRECTORY>`

Directory in which to find the binaries to run.

`-r|--results-directory <PATH>`

The directory where the test results are going to be placed. If the specified directory doesn't exist, it's created.

`-s|--settings <SETTINGS_FILE>`

The .runsettings file to use for running the tests. [Configure unit tests by using a .runsettings file.](https://docs.microsoft.com/en-us/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file?view=vs-2019)

`-t|--list-tests`

List all of the discovered tests in the current project.

`-v|--verbosity <LEVEL>`

Sets the verbosity level of the command. Allowed values are q\[uiet\], m\[inimal\], n\[ormal\], d\[etailed\], and diag\[nostic\].

#### RunSettings arguments

Arguments passed as RunSettings configurations for the test. Arguments are specified as \[name\]=\[value\]pairs after "-- " \(note the space after --\). A space is used to separate multiple \[name\]=\[value\] pairs.

Example: dotnet test -- MSTest.DeploymentEnabled=false MSTest.MapInconclusiveToFailed=True For more information about RunSettings, see [vstest.console.exe: Passing RunSettings args](https://github.com/Microsoft/vstest-docs/blob/master/docs/RunSettingsArguments.md).

