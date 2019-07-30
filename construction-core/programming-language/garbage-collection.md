# Garbage collection

In the common language runtime \(CLR\), the garbage collector serves as an automatic memory manager. It provides the following benefits:

* Enables you to develop your application without having to free memory.
* Allocates objects on the managed heap efficiently.
* Reclaims objects that are no longer being used, clears their memory, and keeps the memory available for future allocations. Managed objects automatically get clean content to start with, so their constructors do not have to initialize every data field.
* Provides memory safety by making sure that an object cannot use the content of another object.

After the garbage collector is initialized by the CLR, it allocates a segment of memory to store and manage objects. This memory is called the managed heap, as opposed to a native heap in the operating system.  
There is a managed heap for each managed process. All threads in the process allocate memory for objects on the same heap.  
The heap can be considered as the accumulation of two heaps: the [large object heap](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/large-object-heap) and the small object heap.  
The [large object heap](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/large-object-heap) contains very large objects that are 85,000 bytes and larger. The objects on the large object heap are usually arrays. It is rare for an instance object to be extremely large.

### Generations <a id="generations"></a>

The heap is organized into generations so it can handle long-lived and short-lived objects. Garbage collection primarily occurs with the reclamation of short-lived objects that typically occupy only a small part of the heap. There are three generations of objects on the heap:

* **Generation 0**. This is the youngest generation and contains short-lived objects. An example of a short-lived object is a temporary variable. Garbage collection occurs most frequently in this generation.

  Newly allocated objects form a new generation of objects and are implicitly generation 0 collections, unless they are large objects, in which case they go on the large object heap in a generation 2 collection.

  Most objects are reclaimed for garbage collection in generation 0 and do not survive to the next generation.

* **Generation 1**. This generation contains short-lived objects and serves as a buffer between short-lived objects and long-lived objects.
* **Generation 2**. This generation contains long-lived objects. An example of a long-lived object is an object in a server application that contains static data that is live for the duration of the process.

### GC Triggers

Garbage collection occurs when one of the following conditions is true:

* The system has low physical memory. This is detected by either the low memory notification from the OS or low memory indicated by the host.
* The memory that is used by allocated objects on the managed heap surpasses an acceptable threshold. This threshold is continuously adjusted as the process runs.
* The [GC.Collect](https://docs.microsoft.com/en-us/dotnet/api/system.gc.collect) method is called. In almost all cases, you do not have to call this method, because the garbage collector runs continuously. This method is primarily used for unique situations and testing.

Garbage collections occur on specific generations as conditions warrant. Collecting a generation means collecting objects in that generation and all its younger generations. A generation 2 garbage collection is also known as a full garbage collection, because it reclaims all objects in all generations \(that is, all objects in the managed heap\).

### Large Objects

If an object is greater than or equal to 85,000 bytes, it’s considered a large object. This number was determined by performance tuning. When an object allocation request is for 85,000 or more bytes, the runtime allocates it on the large object heap.  
Small objects are always allocated in generation 0 and, depending on their lifetime, may be promoted to generation 1 or generation2. Large objects are always allocated in generation 2.  
When a garbage collection is triggered, the GC traces through the live objects and compacts them. But because compaction is expensive, the GC _sweeps_ the LOH; it makes a free list out of dead objects that can be reused later to satisfy large object allocation requests. Adjacent dead objects are made into one free object.  
.NET Core and .NET Framework \(starting with .NET Framework 4.5.1\) include the [GCSettings.LargeObjectHeapCompactionMode](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.gcsettings.largeobjectheapcompactionmode#System_Runtime_GCSettings_LargeObjectHeapCompactionMode) property that allows users to specify that the LOH should be compacted during the next full blocking GC. And in the future, .NET may decide to compact the LOH automatically. This means that, if you allocate large objects and want to make sure that they don’t move, you should still pin them.

Allocations on the large object heap impact performance in the following ways.

* Allocation cost.

  The CLR makes the guarantee that the memory for every new object it gives out is cleared. This means the allocation cost of a large object is completely dominated by memory clearing \(unless it triggers a GC\). If it takes 2 cycles to clear one byte, it takes 170,000 cycles to clear the smallest large object. Clearing the memory of a 16MB object on a 2GHz machine takes approximately 16ms. That's a rather large cost.

* Collection cost.

  Because the LOH and generation 2 are collected together, if either one's threshold is exceeded, a generation 2 collection is triggered. If a generation 2 collection is triggered because of the LOH, generation 2 won't necessarily be much smaller after the GC. If there's not much data on generation 2, this has minimal impact. But if generation 2 is large, it can cause performance problems if many generation 2 GCs are triggered. If many large objects are allocated on a very temporary basis and you have a large SOH, you could be spending too much time doing GCs. In addition, the allocation cost can really add up if you keep allocating and letting go of really large objects.

* Array elements with reference types.

  Very large objects on the LOH are usually arrays \(it's very rare to have an instance object that's really large\). If the elements of an array are reference-rich, it incurs a cost that is not present if the elements are not reference-rich. If the element doesn’t contain any references, the garbage collector doesn’t need to go through the array at all. 

### Monitoring Application’s Memory Usage

#### Memory Performance Counters <a id="memory-performance-counters"></a>

You can use performance counters to gather performance data. For instructions, see [Runtime Profiling](https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/runtime-profiling). The .NET CLR Memory category of performance counters, as described in [Performance Counters in the .NET Framework](https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/performance-counters), provides information about the garbage collector.

#### Debugging with SOS <a id="debugging-with-sos"></a>

You can use the [Windows Debugger \(WinDbg\)](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index) to inspect objects on the managed heap.  
To install WinDbg, install Debugging Tools for Windows from the [Download Debugging Tools for Windows](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/debugger-download-tools) page.

#### Garbage Collection ETW Events <a id="garbage-collection-etw-events"></a>

Event tracing for Windows \(ETW\) is a tracing system that supplements the profiling and debugging support provided by the .NET Framework. Starting with the .NET Framework 4, [garbage collection ETW events](https://docs.microsoft.com/en-us/dotnet/framework/performance/garbage-collection-etw-events) capture useful information for analyzing the managed heap from a statistical point of view. For example, the `GCStart_V1` event, which is raised when a garbage collection is about to occur, provides the following information:

* Which generation of objects is being collected.
* What triggered the garbage collection.
* Type of garbage collection \(concurrent or not concurrent\).

ETW event logging is efficient and will not mask any performance problems associated with garbage collection. A process can provide its own events in conjunction with ETW events. When logged, both the application's events and the garbage collection events can be correlated to determine how and when heap problems occur. For example, a server application could provide events at the start and end of a client request.

#### The Profiling API <a id="the-profiling-api"></a>

The common language runtime \(CLR\) profiling interfaces provide detailed information about the objects that were affected during garbage collection. A profiler can be notified when a garbage collection starts and ends. It can provide reports about the objects on the managed heap, including an identification of objects in each generation. For more information, see [Profiling Overview](https://docs.microsoft.com/en-us/dotnet/framework/unmanaged-api/profiling/profiling-overview).  
Profilers can provide comprehensive information. However, complex profilers can potentially modify an application's behavior.

#### Application Domain Resource Monitoring <a id="application-domain-resource-monitoring"></a>

Starting with the .NET Framework 4, Application domain resource monitoring \(ARM\) enables hosts to monitor CPU and memory usage by application domain. For more information, see [Application Domain Resource Monitoring](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/app-domain-resource-monitoring).

