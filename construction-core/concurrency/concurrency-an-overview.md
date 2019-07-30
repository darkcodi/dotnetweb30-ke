# Concurrency: An Overview

### Introduction to Concurrency

**Concurrency**: Doing more than one thing at a time.

Examples: End-user applications use concurrency to respond to user input while writing to a database. Server applications use concurrency to respond to a second request while finishing the first request.

**Multithreading**: A form of concurrency that uses multiple threads of execution.

**Parallel Processing**: Doing lots of work by dividing it up among multiple threads that run concurrently.

Parallel processing is one type of multithreading, and multithreading is one type of concurrency.

**Asynchronous Programming**: A form of concurrency that uses futures or callbacks to avoid unnecessary threads.

A **future** \(or promise\) is a type that represents some operation that will complete in the future. The modern future types in .NET are Task and Task&lt;TResult&gt;.

**Reactive Programming:** A declarative style of programming where the application reacts to events.

### Introduction to Asynchronous Programming

Modern asynchronous .NET applications use two keywords: **async** and **await**. The async keyword is added to a method declaration, and its primary purpose is to enable the await keyword within that method. An async method should return Task&lt;TResult&gt;. if it returns a value, or Task if it does not return a value.

When you await a task, a context is captured when the await decides to pause the method. This context is the current **SynchronizationContext** unless it is null, in which case the context is the current TaskScheduler. The method resumes executing within that captured context. Usually, this context is the UI context \(if you’re on the UI thread\), an ASP.NET request context \(if you’re processing an ASP.NET request\), or the thread pool context \(most other situations\).

You can avoid this default behavior by awaiting the result of the ConfigureAwait extension method and passing false for the continueOnCapturedContext parameter.

For ASP.NET Core:

ConfigureAwait only has effects on code running in the context of a SynchronizationContext which ASP.NET Core doesn't have, so the call to ConfigureAwait\(false\) is redundant and does nothing.

### Introduction to Multithreaded Programming

A **thread** is an independent executor.

Each thread has its own independent stack but shares the same memory with all the other threads in a process.

Every .NET application has a **thread pool**. The thread pool maintains a number of worker threads that are waiting to execute whatever work you have for them to do.

### Collections for Concurrent Applications

**Concurrent collections** allow multiple threads to update them simulatenously in a safe way. Most concurrent collections use snapshots to allow one thread to enumerate the values while another thread may be adding or removing values.

An **immutable collection** cannot actually be modified; instead, to modify an immutable collection, you create a new collection that represents the modified collection.

