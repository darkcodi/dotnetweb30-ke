# Task Parallelism

### Parallel Framework concepts and components

**PFX \(Parallel Framework\) Concepts**

There are two strategies for partitioning work among threads: data parallelism and task parallelism.

When a set of tasks must be performed on many data values, we can parallelize by having each thread perform the \(same\) set of tasks on a subset of values. This is called **data parallelism** because we are partitioning the data between threads. In contrast, with **task parallelism** we partition the tasks; in other words, we have each thread perform a different task.

**PFX Components**

PFX comprises two layers of functionality. The higher layer consists of two structured data parallelism APIs: [PLINQ](http://www.albahari.com/threading/part5.aspx#_PLINQ) and the [Parallel](http://www.albahari.com/threading/part5.aspx#_The_Parallel_Class) class. The lower layer contains the task parallelism classes — plus a set of additional constructs to help with parallel programming activities.

![](../../.gitbook/assets/image%20%28122%29.png)

PLINQ offers the richest functionality: it automates all the steps of parallelization — including partitioning the work into tasks, executing those tasks on threads, and collating the results into a single output sequence. It’s called declarative — because you simply declare that you want to parallelize your work, and let the Framework take care of the implementation details. In contrast, the other approaches are imperative, in that you need to explicitly write code to partition or collate. In the case of the Parallel class, you must collate results yourself; with the task parallelism constructs, you must partition the work yourself, too.

### Parallel LINQ

PLINQ automatically parallelizes local LINQ queries.

To use PLINQ, simply call AsParallel\(\) on the input sequence and then continue the LINQ query as usual.

![](../../.gitbook/assets/image%20%28130%29.png)

A side effect of parallelizing the query operators is that when the results are collated, it’s not necessarily in the same order that they were submitted.

If you need order preservation, you can force it by calling AsOrdered\(\) after AsParallel\(\). Calling AsOrdered incurs a performance hit with large numbers of elements because PLINQ must keep track of each element’s original position.

### Exception-Handling Tasks

When you wait for a task to complete, any unhandled exceptions are conveniently rethrown to the caller, wrapped in an [**AggregateException**](http://www.albahari.com/threading/part5.aspx#_Working_with_AggregateException) object.

You still need to exception-handle detached autonomous tasks \(unparented tasks that are not waited upon\) in order to prevent an unhandled exception taking down the application when the task drops out of scope and is garbage-collected.

For parented tasks, waiting on the parent implicitly waits on the [children](http://www.albahari.com/threading/part5.aspx#_Child_tasks) — and any child exceptions then bubble up:

```csharp
TaskCreationOptions atp = TaskCreationOptions.AttachedToParent;
var parent = Task.Factory.StartNew (() => 
{
  Task.Factory.StartNew (() =>   // Child
  {
      Task.Factory.StartNew (() => { throw null; }, atp);   // Grandchild
      }, atp);
  });
          
 // The following call throws a NullReferenceException (wrapped
 // in nested AggregateExceptions):
 parent.Wait();
```

### Continuation with Tasks

Sometimes it’s useful to start a task right after another one completes \(or fails\). The ContinueWith method on the Task class does exactly this.

![](../../.gitbook/assets/image%20%28151%29.png)

By default, a continuation is scheduled unconditionally — whether the antecedent completes, throws an exception, or is canceled. You can alter this behavior via a set of \(combinable\) flags included within the TaskContinuationOptions enum. The three core flags that control conditional continuation are:

```text
NotOnRanToCompletion = 0x10000,
NotOnFaulted = 0x20000,
NotOnCanceled = 0x40000,
```

### Canceling Tasks

You can optionally pass in a [cancellation token](http://www.albahari.com/threading/part3.aspx#_Cancellation_Tokens) when starting a task. This lets you cancel tasks via the cooperative cancellation pattern:

```text
var cancelSource = new CancellationTokenSource();
CancellationToken token = cancelSource.Token;
Task task = Task.Factory.StartNew (() => 
{
  // Do some stuff...
    token.ThrowIfCancellationRequested();  // Check for cancellation request
      // Do some stuff...
}, token);
...
cancelSource.Cancel();
```

### Working with AggregateException

An AggregateException has an InnerExceptions property containing each of the caught exception\(s\):

```text
try{  
    var query = from i in ParallelEnumerable.Range (0, 1000000) 
                select 100 / i;
    // Enumerate query
  ...
}
catch (AggregateException aex)
{
  foreach (Exception ex in aex.InnerExceptions)
      Console.WriteLine (ex.Message);
}
```

