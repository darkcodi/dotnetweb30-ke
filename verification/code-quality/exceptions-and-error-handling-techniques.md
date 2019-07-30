# Exceptions and error handling techniques

**X DO NOT** return error codes.

**✓** **DO** report execution failures by throwing exceptions.

**✓** **CONSIDER** terminating the process by calling System.Environment.FailFast \(.NET Framework 2.0 feature\) instead of throwing an exception if your code encounters a situation where it is unsafe for further execution.

**X DO NOT** use exceptions for the normal flow of control, if possible.

**✓** **CONSIDER** the performance implications of throwing exceptions. Throw rates above 100 per second are likely to noticeably impact the performance of most applications.

**✓** **DO** document all exceptions thrown by publicly callable members because of a violation of the member contract \(rather than a system failure\) and treat them as part of your contract.

**X DO NOT** have public members that can either throw or not based on some option.

**X DO NOT** have public members that return exceptions as the return value or an out parameter.-

**✓** **CONSIDER** using exception builder methods.

It is common to throw the same exception from different places. To avoid code bloat, use helper methods that create exceptions and initialize their properties.

Also, members that throw exceptions are not getting inlined. Moving the throw statement inside the builder might allow the member to be inlined.

**X DO NOT** throw exceptions from exception filter blocks.

When an exception filter raises an exception, the exception is caught by the CLR, and the filter returns false. This behavior is indistinguishable from the filter executing and returning false explicitly and is therefore very difficult to debug.

**X AVOID** explicitly throwing exceptions from finally blocks. Implicitly thrown exceptions resulting from calling methods that throw are acceptable.

**Exception and SystemException**

**X DO NOT** throw System.Exception or System.SystemException.

**X DO NOT** catch `System.Exception` or `System.SystemException` in framework code, unless you intend to rethrow.

**X AVOID** catching `System.Exception` or `System.SystemException`, except in top-level exception handlers.

**ApplicationException**

**X DO NOT** throw or derive from ApplicationException.

**InvalidOperationException**

**✓** **DO** throw an InvalidOperationException if the object is in an inappropriate state.

**ArgumentException, ArgumentNullException, and ArgumentOutOfRangeException**

**✓** **DO** throw ArgumentException or one of its subtypes if bad arguments are passed to a member. Prefer the most derived exception type, if applicable.

**✓** **DO** set the `ParamName` property when throwing one of the subclasses of `ArgumentException`.

**✓** **DO** use `value` for the name of the implicit value parameter of property setters.

**NullReferenceException, IndexOutOfRangeException, and AccessViolationException**

**X DO NOT** allow publicly callable APIs to explicitly or implicitly throw NullReferenceException, AccessViolationException, or IndexOutOfRangeException. These exceptions are reserved and thrown by the execution engine and in most cases indicate a bug.

Do argument checking to avoid throwing these exceptions. Throwing these exceptions exposes implementation details of your method that might change over time.

**StackOverflowException**

**X DO NOT** explicitly throw StackOverflowException. The exception should be explicitly thrown only by the CLR.

**X DO NOT** catch `StackOverflowException`.

It is almost impossible to write managed code that remains consistent in the presence of arbitrary stack overflows. The unmanaged parts of the CLR remain consistent by using probes to move stack overflows to well-defined places rather than by backing out from arbitrary stack overflows.

**OutOfMemoryException**

**X DO NOT** explicitly throw OutOfMemoryException. This exception is to be thrown only by the CLR infrastructure.

