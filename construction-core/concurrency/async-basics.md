# Async basics

### Pausing for a Period of Time

**Problem**: You need to \(asynchronously\) wait for a period of time. This can be useful when unit testing or implementing retry delays. This solution can also be useful for simple time‐ outs.

**Solution**: Task.Delay\(TimeSpan delay\)

### Reporting progress

**Problem:** You need to respond to progress while an asynchronous operation is executing.

**Solution:** Use the provided IProgress&lt;T&gt; and Progress&lt;T&gt; types. Your async method should take an IProgress&lt;T&gt; argument; the T is whatever type of progress you need to report.

![](../../.gitbook/assets/image%20%282%29.png)

![](../../.gitbook/assets/image%20%289%29.png)

### Waiting for a Set of Tasks to Complete

**Problem:** You have several tasks and need to wait for them all to complete.

**Solution:** Use the Task.WhenAll method.This method takes several tasks and returns a task that completes when all of those tasks have completed.

### Waiting for Any Task to Complete

**Problem**: You have several tasks and need to respond to just one of them completing. For example, you could request stock quotes from multiple web services simultaneously, but you only care about the first one that responds.

**Solution:** Use the Task.WhenAny method. This method takes a sequence of tasks and returns a task that completes when any of the tasks complete. The result of the returned task is the task that completed.

### Processing Tasks as They Complete

**Problem**: You have a collection of tasks to await, and you want to do some processing on each task after it completes. However, you want to do the processing for each one as soon as it completes, not waiting for any of the other tasks.

**Solution:** The easiest solution is to restructure the code by introducing a higher-level async method that handles awaiting the task and processing its result. Once the processing is factored out, the code is significantly simplified

![](../../.gitbook/assets/image%20%28161%29.png)

### Avoiding Context for Continuations

**Problem:** When an async method resumes after an await, by default it will resume executing within the same context. This can cause performance problems if that context was a UI context and a large number of async methods are resuming on the UI context.

**Solution**: To avoid resuming on a context, await the result of ConfigureAwait and pass false for its continueOnCapturedContext parameter.

### Handling Exceptions from async Task

**Problem:** Exception handling is a critical part of any design. It’s easy to design for the success case but a design is not correct until it also handles the failure cases. Fortunately, handling exceptions from async Task methods is straightforward.

**Solution**: Exceptions can be caught by a simple try/catch, just like you would for synchronous code/ Exceptions raised from async Task methods are placed on the returned Task. They are only raised when the returned Task is awaited.

### Handling Exceptions from async Void Methods

**Problem:** You have an async void method and need to handle exceptions propagated out of that method.

**Solution**: There is no good solution. If at all possible, change the method to return Task instead of void. In some situations, this isn’t possible, so you can provide a Task-returning overload of your Execute method as such.

If you must use an async void method, consider wrapping all of its code in a try block and handling the exception directly. There is another solution. When an async void method propagates an exception, that exception is raised on the SynchronizationContext that was active at the time the async void method started executing. If your execution environment provides a SynchronizationContext, then it usually has a way to handle these top-level exceptions at a global scope. For example, ASP.NET has Application\_Error.

