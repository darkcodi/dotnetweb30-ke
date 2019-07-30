# Dispose and Finalizable patterns

For the majority of the objects that your app creates, you can rely on .NET's garbage collector to handle memory management. However, when you create objects that include unmanaged resources, you must explicitly release those resources when you finish using them in your app. The most common types of unmanaged resource are objects that wrap operating system resources, such as files, windows, network connections, or database connections. Although the garbage collector is able to track the lifetime of an object that encapsulates an unmanaged resource, it doesn't know how to release and clean up the unmanaged resource.

If your types use unmanaged resources, you should do the following:

* Implement the [dispose pattern](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/dispose-pattern). This requires that you provide an [IDisposable.Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) implementation to enable the deterministic release of unmanaged resources. A consumer of your type calls [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) when the object \(and the resources it uses\) is no longer needed. The [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) method immediately releases the unmanaged resources.
* Provide for your unmanaged resources to be released in the event that a consumer of your type forgets to call [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose). There are two ways to do this:

  * Use a safe handle to wrap your unmanaged resource. This is the recommended technique. Safe handles are derived from the [System.Runtime.InteropServices.SafeHandle](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.interopservices.safehandle) class and include a robust [Finalize](https://docs.microsoft.com/en-us/dotnet/api/system.object.finalize) method. When you use a safe handle, you simply implement the [IDisposable](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable) interface and call your safe handle's [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.interopservices.safehandle.dispose) method in your [IDisposable.Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) implementation. The safe handle's finalizer is called automatically by the garbage collector if its [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) method is not called _**\(better solution for most cases\)**_.

    —or—

  * Override the [Object.Finalize](https://docs.microsoft.com/en-us/dotnet/api/system.object.finalize) method. Finalization enables the non-deterministic release of unmanaged resources when the consumer of a type fails to call [IDisposable.Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) to dispose of them deterministically. However, because object finalization can be a complex and error-prone operation, we recommend that you use a safe handle instead of providing your own finalizer.



  **Implementing a Dispose method**

  * **The Dispose\(\) overload**

    ```csharp
    public void Dispose()
    {
       // Dispose of unmanaged resources.
       Dispose(true);
       // Suppress finalization.
       GC.SuppressFinalize(this);
    }
    ```

    The `Dispose` method performs all object cleanup, so the garbage collector no longer needs to call the objects' [Object.Finalize](https://docs.microsoft.com/en-us/dotnet/api/system.object.finalize) override. Therefore, the call to the [SuppressFinalize](https://docs.microsoft.com/en-us/dotnet/api/system.gc.suppressfinalize) method prevents the garbage collector from running the finalizer. If the type has no finalizer, the call to [GC.SuppressFinalize](https://docs.microsoft.com/en-us/dotnet/api/system.gc.suppressfinalize) has no effect. Note that the actual work of releasing unmanaged resources is performed by the second overload of the `Dispose` method.

  * **The Dispose\(Boolean\) overload**

    In the second overload, the _disposing_ parameter is a [Boolean](https://docs.microsoft.com/en-us/dotnet/api/system.boolean) that indicates whether the method call comes from a [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) method \(its value is `true`\) or from a finalizer \(its value is `false`\).

    The body of the method consists of two blocks of code:

    * A block that frees unmanaged resources. This block executes regardless of the value of the `disposing` parameter.
    * A conditional block that frees managed resources. This block executes if the value of `disposing` is `true`. The managed resources that it frees can include.

    If the method call comes from a finalizer \(that is, if _disposing_ is `false`\), only the code that frees unmanaged resources executes. Because the order in which the garbage collector destroys managed objects during finalization is not defined, calling this `Dispose`overload with a value of `false` prevents the finalizer from trying to release managed resources that may have already been reclaimed.  


    ```csharp
    protected virtual void Dispose(bool disposing)
    {
       //if already was disposed - don't do anything. 
       //Microsoft guidline recuires, that multiple dispose calls won't case Exceptions
       if (disposed) 
          return; 
   
       if (disposing) {
          // Free any other managed objects here.
          //
       }
   
       // Free any unmanaged objects here.
       //
       disposed = true;
    }
    ```

Implementation Samples:

Base class

```csharp
using System;

class BaseClass : IDisposable
{
   // Flag: Has Dispose already been called?
   bool disposed = false;
   
   // Public implementation of Dispose pattern callable by consumers.
   public void Dispose()
   { 
      Dispose(true);
      GC.SuppressFinalize(this);           
   }
   
   // Protected implementation of Dispose pattern.
   protected virtual void Dispose(bool disposing)
   {
      if (disposed)
         return; 
      
      if (disposing) {
         // Free any other managed objects here.
         //
      }
      
      // Free any unmanaged objects here.
      //
      disposed = true;
   }

   ~BaseClass()
   {
      Dispose(false);
   }
}
```

DerivedClass

```csharp
using System;

class DerivedClass : BaseClass
{
   // Flag: Has Dispose already been called?
   bool disposed = false;
   
   // Protected implementation of Dispose pattern.
   protected override void Dispose(bool disposing)
   {
      if (disposed)
         return; 
      
      if (disposing) {
         // Free any other managed objects here.
         //
      }
      
      // Free any unmanaged objects here.
      //
      disposed = true;
      
      // Call the base class implementation.
      base.Dispose(disposing);
   }

   ~DerivedClass()
   {
      Dispose(false);
   }
}
```

