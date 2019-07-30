# Basic Synchronization in C\#

### Synchronization Essentials

**Synchronization –** coordinating the actions of threads for a predictable outcome. Synchronization is particularly important when threads access the same data.

Synchronization constructs can be divided into four categories:

1.      Simple blocking methods. These wait for another thread to finish or for a period of time to elapse. Sleep, Join, and Task.Wait are simple blocking methods.

2.      Locking constructs. These limit the number of threads that can perform some activity or execute a section of code at a time. Exclusive locking constructs are most common — these allow just one thread in at a time, and allow competing threads to access common data without interfering with each other. The standard exclusive locking constructs are lock \(Monitor.Enter/Monitor.Exit\), Mutex, and SpinLock. The nonexclusive locking constructs are Semaphore, SemaphoreSlim, and the reader/writer locks.

3.      Signaling constructs. These allow a thread to pause until receiving a notification from another, avoiding the need for inefficient polling. There are two commonly used signaling devices: event wait handles and Monitor’s Wait/Pulse methods. Framework 4.0 introduces the CountdownEvent and Barrier classes.

4.       Nonblocking synchronization constructs. These protect access to a common field by calling upon processor primitives. The CLR and C\# provide the following nonblocking constructs: Thread.MemoryBarrier, Thread.VolatileRead, Thread.VolatileWrite, the volatile keyword, and the Interlocked class.

### Locking

Exclusive locking is used to ensure that only one thread can enter particular sections of code at a time. The two main exclusive locking constructs are lock and Mutex. Of the two, the lock construct is faster and more convenient. Mutex, though, has a niche in that its lock can span applications in different processes on the computer.

**A Comparison of Locking Constructs**

| **Construct** | **Purpose** | **Cross-process?** |
| :--- | :--- | :--- |
| [lock](http://www.albahari.com/threading/part2.aspx#_Locking) \(Monitor.Enter / Monitor.Exit\) | Ensures just one thread can access a resource, or section of code at a time | - |
| [Mutex](http://www.albahari.com/threading/part2.aspx#_Mutex) | -\|\|- | Yes |
| [SemaphoreSlim](http://www.albahari.com/threading/part2.aspx#_Semaphore) \(introduced in Framework 4.0\) | Ensures not more than a specified number of concurrent threads can access a resource, or section of code | - |
| [Semaphore](http://www.albahari.com/threading/part2.aspx#_Semaphore) | -\|\|- | Yes |
| [ReaderWriterLockSlim](http://www.albahari.com/threading/part4.aspx#_Reader_Writer_Locks)\(introduced in Framework 3.5\) | Allows multiple readers to coexist with a single writer | - |
| [ReaderWriterLock](http://www.albahari.com/threading/part4.aspx#_Reader_Writer_Locks)\(effectively deprecated\) | -\|\|- | - |

C\#’s lock statement is in fact a syntactic shortcut for a call to the methods Monitor.Enter and Monitor.Exit, with a try/finally block.

Choosing the Synchronization Object - any object visible to each of the partaking threads can be used as a synchronizing object, subject to one hard rule: it must be a reference type.

When to Lock? As a basic rule, you need to lock around accessing any writable shared field.

### Thread Safety

A program or method is **thread-safe** if it has no indeterminacy in the face of any multithreading scenario. Thread safety is achieved primarily with locking and by reducing the possibilities for thread interaction.

Locking can be used to convert thread-unsafe code into thread-safe code.

Enumerating .NET collections is thread-unsafe in the sense that an exception is thrown if the list is modified during enumeration. Rather than locking for the duration of enumeration, in this example we first copy the items to an array.

Static members

For instance, imagine if the static property on the DateTime struct, DateTime. Now, was not thread-safe, and that two concurrent calls could result in garbled output or an exception. The only way to remedy this with external locking might be to lock the whole type itself — lock\(typeof\(DateTime\)\) — before calling DateTime.Now. For this reason, static members on the DateTime struct have been carefully programmed to be thread-safe. This is a common pattern throughout the .NET Framework: static members are thread-safe; instance members are not.

### Signaling with Event Wait Handles

Event wait handles are used for signaling. **Signaling** is when one thread waits until it receives notification from another. Event wait handles are the simplest of the signaling constructs, and they are unrelated to C\# events.

They come in three flavors: [AutoResetEvent](http://www.albahari.com/threading/part2.aspx#_AutoResetEvent), [ManualResetEvent](http://www.albahari.com/threading/part2.aspx#_ManualResetEvent), and \(from Framework 4.0\) [CountdownEvent](http://www.albahari.com/threading/part2.aspx#_CountdownEvent). The former two are based on the common EventWaitHandle class, where they derive all their functionality.

**A Comparison of Signaling Constructs**

| **Construct** | **Purpose** | **Cross-process?** |
| :--- | :--- | :--- |
| [AutoResetEvent](http://www.albahari.com/threading/part2.aspx#_AutoResetEvent) | Allows a thread to unblock once when it receives a signal from another | Yes |
| [ManualResetEvent](http://www.albahari.com/threading/part2.aspx#_ManualResetEvent) | Allows a thread to unblock indefinitely when it receives a signal from another \(until reset\) | Yes |
| [ManualResetEventSlim](http://www.albahari.com/threading/part2.aspx#_ManualResetEvent)\(introduced in Framework 4.0\) | -\|\|- | - |
| [CountdownEvent](http://www.albahari.com/threading/part2.aspx#_CountdownEvent) \(introduced in Framework 4.0\) | Allows a thread to unblock when it receives a predetermined number of signals | - |
| [Barrier](http://www.albahari.com/threading/part4.aspx#_The_Barrier_Class) \(introduced in Framework 4.0\) | Implements a thread execution barrier | - |
| [Wait and Pulse](http://www.albahari.com/threading/part4.aspx#_Signaling_with_Wait_and_Pulse) | Allows a thread to block until a custom condition is met | - |

### Synchronization Context

An alternative to [locking manually](http://www.albahari.com/threading/part2.aspx#_Locking) is to lock declaratively. By deriving from ContextBoundObject and applying the \[Synchronization\] attribute, you instruct the CLR to apply locking automatically.

The CLR ensures that only one thread can execute code in safeInstance at a time. It does this by creating a single synchronizing object — and [locking](http://www.albahari.com/threading/part2.aspx#_Locking) it around every call to each of safeInstance's methods or properties. The scope of the lock —the safeInstance object — is called a synchronization context.

