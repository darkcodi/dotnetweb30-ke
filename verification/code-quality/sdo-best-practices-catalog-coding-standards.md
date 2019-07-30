# SDO Best Practices Catalog - Coding Standards

### Benefits

Uniformly organized code allows focusing on meaning instead of formatting, reflects project structure and architecture and follows industry paradigm for given technology stack.  
Good coding convention prevents a developer from coding errors, simplifies involvement of new team members and code understanding.  
Coding standards reduce cost of support by minimizing time for debugging and reverse engineering analysis, enhance code maintainability.

### Indicators of successful process

* Coding standard policy is documented, published in the project team space o   Naming and style conventions o   Coding best practices o   Project common settings and project structure o   Framework specific guidelines      §  Data Access      §  Web Services      §  Multithreading  etc.
* Coding convention corresponds to industry recognized conventions \(for new development\)
* Code is sufficiently commented and documented
* Code standards and best practices are present on project "wiki"
* Code convention stimulates creation of self-documented or self-descriptive code
*  Code formatting and naming is consistent across the module, library or solution
* File and folder organization is consistent, reflects project structure and architecture and follows industry paradigm for given technology stack
*  Development team tools and environment are configured identically to enforce code standards across the team

### Standards, Best Practices, and Templates

**Tabs & Indenting**

Tab characters \(\0x09\) should not be used in code. All indentation should be done with 4 space characters.

**Bracing**

Open braces should always be at the beginning of the line after the statement that begins the block. Contents of the brace should be indented by 4 spaces. For example:

`if (someExpression)  
 {  
    DoSomething();  
 }  
 else  
 {  
    DoSomethingElse();  
 }`

“case” statements should be indented from the switch statement like this:

`switch (someExpression)   
 {  
   case 0:  
       DoSomething();  
       break;  
   case 1:  
       DoSomethingElse();  
       break;  
   case 2:   
       {  
          int n = 1;  
          DoAnotherThing(n);  
       }  
       break;  
 }`

Braces should never be considered optional. Even for single statement blocks, you should always use braces. This increases code readability and maintainability.

**Single line statements**

Single line statements can have braces that begin and end on the same line.

`public class Foo  
 {  
    int bar;  
   public int Bar  
    {  
       get { return bar; }  
       set { bar = value; }  
    }  
}`

It is suggested that all control structures \(if, while, for, etc.\) use braces, but it is not required.

**Copyright notice**

Each file should start with a copyright notice. To avoid errors in doc comment builds, you don’t want to use triple-slash doc comments, but using XML makes the comments easy to replace in the future. Final text will vary by product \(you should contact legal for the exact text\), but should be similar to:

`//-----------------------------------------------------------------------  
 // <copyright file="ContainerControl.cs" company="Microsoft">  
 //     Copyright (c) Microsoft Corporation.  All rights reserved.  
 // </copyright>  
 //-----------------------------------------------------------------------`

**Documentation Comments**

All methods should use XML doc comments. For internal dev comments, the &lt;devdoc&gt; tag should be used.

`public class Foo   
 {  
/// <summary>Public stuff about the method</summary>  
 /// <param name=”bar”>What a neat parameter!</param>  
 /// <devdoc>Cool internal stuff!</devdoc>  
 ///  
 public void MyMethod(int bar) { … }  
}`

However, it is common that you would want to move the XML documentation to an external file – for that, use the &lt;include&gt; tag.

`public class Foo   
 {  
   /// <include file='doc\Foo.uex' path='docs/doc[@for="Foo.MyMethod"]/*' />  
    ///  
    public void MyMethod(int bar) { … }  
}`

**Comment Style**

The // \(two slashes\) style of comment tags should be used in most situations. Where ever possible, place comments above the code instead of beside it.  

Comments can be placed at the end of a line when space allows:

`public class SomethingUseful   
 {  
     private int          itemHash;            // instance member  
     private static bool  hasDoneSomething;    // static member  
 }`

**Spacing**

Spaces improve readability by decreasing code density. Here are some guidelines for the use of space characters within code:

* Do use a single space after a comma between function arguments.  Right:          `Console.In.Read(myChar, 0, 1);`  Wrong:       `Console.In.Read(myChar,0,1);` 
* Do not use a space after the parenthesis and function arguments  Right:         `CreateFoo(myChar, 0, 1)`  Wrong:       `CreateFoo( myChar, 0, 1 )`
* Do not use spaces between a function name and parenthesis.  Right:          `CreateFoo()`  Wrong:       `CreateFoo ()`
* Do not use spaces inside brackets.  Right:    `x = dataArray[index];`  Wrong:       `x = dataArray[ index ];`
* Do use a single space before flow control statements  Right:          `while (x == y)`  Wrong:       `while(x==y)`
* Do use a single space before and after comparison operators  Right:          `if (x == y)`  Wrong:       `if (x==y)`

**File Organization**

* Source files should contain only one public type, although multiple internal classes are allowed
* Source files should be given the name of the public class in the file
* Directory names should follow the namespace for the class
* Classes member should be **alphabetized**, and grouped into sections \(Fields, Constructors, Properties, Events, Methods, Private interface implementations, Nested types\)
* Using statements should be inside the namespace declaration.

`namespace MyNamespace   
 {  
using System;  
public class MyClass : IFoo   
 {  
      // members  
                  }  
}`

