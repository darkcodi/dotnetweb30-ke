# Building enumerable types

Exposes the enumerator, which supports a simple iteration over a collection of a specified type.

`IEnumerable<T>` is the base interface for collections in the `System.Collections.Generic` namespace such as `List<T>`, `Dictionary<TKey,TValue>`, and `Stack<T>` and other generic collections such as `ObservableCollection<T`&gt; and `ConcurrentStack<T>`. Collections that implement `IEnumerable<T>` can be enumerated by using the `foreach` statement.

When you implement `IEnumerable<T>`, you must also implement `IEnumerator<T>` or, for C\# only, you can use the `yield` keyword. Implementing `IEnumerator<T>` also requires `IDisposable` to be implemented, which you will see in this example.

`IEnumerable<T>` contains a single method that you must implement when implementing this interface; `GetEnumerator`, which returns an `IEnumerator<T>` object. The returned `IEnumerator<T>` provides the ability to iterate through the collection by exposing a `Current` property.

Implementing `IEnumerator<T>` interface requires implementing the nongeneric `IEnumerator` interface. The `MoveNext()` and `Reset()` methods do not depend on `T`, and appear only on the nongeneric interface. The `Current` property appears on both interfaces, and has different return types. Implement the nongeneric `Current` property as an explicit interface implementation. This allows any consumer of the nongeneric interface to consume the generic interface.

In addition, `IEnumerator<T>` implements `IDisposable`, which requires you to implement the `Dispose()` method. This enables you to close database connections or release file handles or similar operations when using other resources. If there are no additional resources to dispose of, provide an empty `Dispose()` implementation.

```csharp
public class List : IEnumerable
{
    private object[] _objects;
 
    public List()
    {
        _objects = new object[100];
    }
 
    public void Add(object obj)
    {
        _objects[_objects.Count] = obj;
    }
 
    public IEnumerator GetEnumerator()
    {
        return new ListEnumerator();
    } 
 
    public class ListEnumerator : IEnumerator
    {
        private int _currentIndex = -1; 
     
        public bool MoveNext()
        {
            _currentIndex++;
     
            return (_currentIndex < _objects.Count); 
        }
     
        public object Current
        { 
            get
            {
                try
                {
                    return _objects[_currentIndex];
                }
                catch (IndexOutOfRangeException)
                {
                    throw new InvalidOperationException();
                }
        }
     
        public void Reset()
        {
            _currentIndex = -1;
        }
        
        public void Dispose()
        {
        }
    }
}
```

