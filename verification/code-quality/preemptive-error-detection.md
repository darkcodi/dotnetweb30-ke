# Preemptive Error Detection

Visual Studio can perform code analysis of managed code in two ways: with **Binary analyzers**, also known as FxCop static analysis of managed assemblies, and with the more modern **Roslyn analyzers**. Roslyn analyzers, which analyze your code live as you type, replace FxCop static analysis, which only analyzes your code after a build.

\(!\)Static code analysis is not supported for .NET Core and .NET Standard projects in Visual Studio.

.NET Compiler Platform \("Roslyn"\) analyzers analyze your code for style, quality and maintainability, design, and other issues. Visual Studio includes a built-in set of analyzers that analyze your C\# or Visual Basic code as you type. You configure preferences for these built-in analyzers on the text editor Options page or in an .editorconfig file.

If rule violations are found by an analyzer, they are reported in the code editor \(as a squiggle under the offending code\) and in the Error List window.

Many analyzer rules, or diagnostics, have one or more associated code fixes that you can apply to correct the problem. The analyzer diagnostics that are built into Visual Studio each have an associated code fix. Code fixes are shown in the light bulb icon menu along with other types of Quick Actions.

