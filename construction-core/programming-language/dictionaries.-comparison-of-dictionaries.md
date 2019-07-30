# Dictionaries. Comparison of Dictionaries

Dictionaries represent a collection of keys and values.

### Dictionary&lt;TKey, TValue&gt;

The `Dictionary<TKey,TValue>` generic class provides a mapping from a set of keys to a set of values. Each addition to the dictionary consists of a value and its associated key. **Retrieving a value by using its key is very fast, close to O\(1\)**, because the `Dictionary<TKey,TValue>` class is implemented as a hash table.

Every key in a `Dictionary<TKey,TValue>` must be unique according to the dictionary's equality comparer. A key cannot be `null`, but a value can be, if its type `TValue` is a reference type.

 The Dictionary is the fastest class for associative lookups/inserts/deletes because **it uses a hash table under the covers**. Because the keys are hashed, **the key type should correctly implement `GetHashCode()` and `Equals()`** appropriately or you should provide an external `IEqualityComparer` to the dictionary on construction. The insert/delete/lookup time of items in the dictionary is amortized constant time - O\(1\) - which means no matter how big the dictionary gets, the time it takes to find something remains relatively constant. This is highly desirable for high-speed lookups. The only **downside** is that the dictionary, by nature of using a hash table, is unordered, so **you cannot easily traverse the items in a Dictionary in order**.

A `Dictionary<TKey,TValue>` can support multiple readers concurrently, as long as the collection is not modified. Even so, enumerating through a collection is intrinsically not a thread-safe procedure. For thread-safe alternatives, see the `ConcurrentDictionary<TKey,TValue>` class or `ImmutableDictionary<TKey,TValue>` class.

### SortedDictionary&lt;TKey, TValue&gt;

Represents a collection of key/value pairs that are sorted on the key.

The `SortedDictionary<TKey,TValue>` generic class is a binary search tree with O\(log n\) retrieval, where n is the number of elements in the dictionary. 

The **SortedDictionary uses a binary tree under the covers to maintain the items in order by the key**. As a consequence of sorting, **the type used for the key must correctly implement IComparable** so that the keys can be correctly sorted. 

### SortedList&lt;TKey, TValue&gt;

Represents a collection of key/value pairs that are sorted by key based on the associated `IComparer<T>` implementation.

The `SortedList<TKey,TValue>` generic class is an array of key/value pairs with O\(log `n`\) retrieval, where n is the number of elements in the dictionary. In this, it is similar to the `SortedDictionary<TKey,TValue>` generic class. The two classes have similar object models, and both have O\(log `n`\) retrieval. 

SortedList, like SortedDictionary, **uses a key to sort key-value pairs**. Unlike SortedDictionary, however, **items in a SortedList are stored as sorted array of items**. This means that insertions and deletions are linear - O\(n\) - because deleting or adding an item may involve shifting all items up or down in the list. Lookup time, however is O\(log n\) because the SortedList can use a binary search to find any item in the list by its key. 

Where the two classes differ is in memory use and speed of insertion and removal:

* `SortedList<TKey,TValue>` uses less memory than `SortedDictionary<TKey,TValue>`.
* `SortedDictionary<TKey,TValue>` has faster insertion and removal operations for unsorted data, O\(log `n`\) as opposed to O\(`n`\) for `SortedList<TKey,TValue>`.
* If the list is populated all at once from sorted data, `SortedList<TKey,TValue>` is faster than `SortedDictionary<TKey,TValue>`.

If you are going to load the SortedList up-front, the insertions will be slower, but because array indexing is faster than following object links, lookups are marginally faster than a SortedDictionary. Once again I'd use this in situations where you want fast lookups and want to maintain the collection in order by the key, and where insertions and deletions are rare. 

A `SortedList<TKey,TValue>` can support multiple readers concurrently, as long as the collection is not modified. Even so, enumerating through a collection is intrinsically not a thread-safe procedure. 

### ConcurrentDictionary&lt;TKey, TValue&gt;

Represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently.

All operations on the `ConcurrentDictionary<TKey,TValue>` class are atomic and are thread-safe with regards to all other operations.  The only exceptions are the methods that accept a delegate, that is, `AddOrUpdate` and `GetOrAdd`. For modifications and write operations to the dictionary, `ConcurrentDictionary<TKey,TValue>` uses fine-grained locking to ensure thread safety. \(Read operations on the dictionary are performed in a lock-free manner.\) However, delegates for these methods are called outside the locks to avoid the problems that can arise from executing unknown code under a lock. Therefore, the code executed by these delegates is not subject to the atomicity of the operation.

