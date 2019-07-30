# Structured Exception Handling, Exception filters

### Structured Exception Handling

#### Exception types:

* **Usage errors.** A usage error represents an error in program logic that can result in an exception. 
* **Program errors.** A program error is a run-time error that cannot necessarily be avoided by writing bug-free code.
* **System failures.** A system failure is a run-time error that cannot be handled programmatically in a meaningful way. For example, any method can throw an `OutOfMemoryException` exception if the common language runtime is unable to allocate additional memory. 

**Exception Class** is the base class for all exceptions. When an error occurs, either the system or the currently executing application reports it by throwing an exception that contains information about the error. After an exception is thrown, it is handled by the application or by the default exception handler.

 The `Exception` class is the base class of all exceptions in the .NET Framework. Many derived classes rely on the inherited behavior of the members of the `Exception` class; they do not override the members of `Exception`, nor do they define any unique members.

The `Exception` class includes a number of properties that help identify the code location, the type, the help file, and the reason for the exception: `StackTrace`, `InnerException`, `Message`, `HelpLink`, `HResult`, `Source`, `TargetSite`, and `Data`. When a causal relationship exists between two or more exceptions, the `InnerException` property maintains this information. 

The common language runtime provides an exception handling model that is based on the representation of exceptions as objects, and the separation of program code and exception handling code into `try` blocks and `catch` blocks.

 A `try` block is used by C\# programmers to partition code that might be affected by an exception. Associated `catch` blocks are used to handle any resulting exceptions. A `finally` block contains code that is run regardless of whether or not an exception is thrown in the `try` block, such as releasing resources that are allocated in the `try` block. A `try` block requires one or more associated `catch` blocks, or a `finally` block, or both.

 A `try` block without a `catch` or `finally` block causes a compiler error.

When an exception occurs in a `try` block, the system searches the associated `catch` blocks in the order they appear in application code, until it locates a `catch` block that handles the exception. Multiple `catch` blocks with different exception filters can be chained together. The `catch` blocks are evaluated from top to bottom in your code, but only one `catch` block is executed for each exception that is thrown. The first `catch` block that specifies the exact type or a base class of the thrown exception is executed. If no `catch` block specifies a matching exception filter, a `catch` block that does not have a filter is selected, if one is present in the statement. It is important to position `catch` blocks with the most specific \(that is, the most derived\) exception types first \(a catch block that handles `System.Exception` is specified last\).

If none of the `catch` blocks associated with the current `try` block handle the exception, and the current `try` block is nested within other `try` blocks in the current call, the `catch` blocks associated with the next enclosing `try` block are searched. If no `catch` block for the exception is found, the system searches previous nesting levels in the current call. If no `catch` block for the exception is found in the current call, the exception is passed up the call stack, and the previous stack frame is searched for a `catch` block that handles the exception. **The search of the call stack continues until the exception is handled or until no more frames exist on the call stack.** If the top of the call stack is reached without finding a `catch` block that handles the exception, **the default exception handler handles it and the application terminates**.

You should catch exceptions when the following conditions are true:

* You have a good understanding of why the exception might be thrown, and you can implement a specific recovery, such as prompting the user to enter a new file name when you catch a FileNotFoundException object.
* You can create and throw a new, more specific exception.
*  You want to partially handle an exception before passing it on for additional handling. In the following example, a `catch` block is used to add an entry to an error log before re-throwing the exception.

`finally` block enables you to clean up actions that are performed in a `try` block. If present, the `finally` block executes last, after the `try` block and any matched `catch` block. A `finally` block always runs, regardless of whether an exception is thrown or a `catch`block matching the exception type is found.

The `finally` block can be used to release resources such as file streams, database connections, and graphics handles without waiting for the garbage collector in the runtime to finalize the objects.

#### Performance considerations <a id="performance-considerations"></a>

Throwing or handling an exception consumes a significant amount of system resources and execution time. Throw exceptions only to handle truly extraordinary conditions, not to handle predictable events or flow control.

Do not throw an exception if user input is invalid, because you can expect users to occasionally enter invalid data. Instead, provide a retry mechanism so users can enter valid input. Nor should you use exceptions to handle usage errors. Instead, use **assertions** to identify and correct usage errors.

{% hint style="info" %}
An assertion, or `Assert` statement, tests a condition, which you specify as an argument to the `Assert` statement. If the condition evaluates to true, no action occurs. If the condition evaluates to false, the assertion fails. If you are running with a debug build, your program enters break mode.
{% endhint %}

**In addition, do not throw an exception when a return code is sufficient; do not convert a return code to an exception; and do not routinely catch an exception, ignore it, and then continue processing.**

{% hint style="success" %}
The recommended way to re-throw an exception is to simply use the `throw` statement without including an expression. This ensures that all call stack information is preserved when the exception is propagated to the caller. 
{% endhint %}

{% hint style="danger" %}
**throw vs throw e**

In contrast, if the exception is re-thrown by using the `throw e`statement, the full call stack is not preserved**.**
{% endhint %}

 A slightly more cumbersome alternative is to throw a new exception, and to preserve the original exception's call stack information in an inner exception. The caller can then use the new exception's `InnerException` property to retrieve stack frame and other information about the original exception. 

### Exception filters

**Exception Filters** are a new feature in C\# 6 which allows you to specify conditions along with a catch block. The catch block is only executed if the condition satisfies. 

If the expression used for an exception filter evaluates to `true`, the catch clause performs its normal processing on an exception. If the expression evaluates to `false`, then the `catch` clause is skipped. One use is to examine information about an exception to determine if a `catch` clause can process the exception:

```csharp
public static async Task<string> MakeRequest()
{
    WebRequestHandler webRequestHandler = new WebRequestHandler();
    webRequestHandler.AllowAutoRedirect = false;
    using (HttpClient client = new HttpClient(webRequestHandler))
    {
        var stringTask = client.GetStringAsync("https://docs.microsoft.com/en-us/dotnet/about/");
        try
        {
            var responseText = await stringTask;
            return responseText;
        }
        catch (System.Net.Http.HttpRequestException e) when (e.Message.Contains("301"))
        {
            return "Site Moved";
        }
    }
}
```

