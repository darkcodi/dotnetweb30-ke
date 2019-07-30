# JavaScript: Arrays

 There exists a special data structure named `Array`, to store ordered collections.

There are two syntaxes for creating an empty array:

```javascript
let arr = new Array();
let arr = [];
```

Almost all the time, the second syntax is used. We can supply initial elements in the brackets:

```javascript
let fruits = ["Apple", "Orange", "Plum"];
```

Array elements are numbered, starting with zero.

We can get an element by its number in square brackets:

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits[0] ); // Apple
alert( fruits[1] ); // Orange
alert( fruits[2] ); // Plum
```

We can replace an element:

```javascript
fruits[2] = 'Pear'; // now ["Apple", "Orange", "Pear"]
```

…Or add a new one to the array:

```javascript
fruits[3] = 'Lemon'; // now ["Apple", "Orange", "Pear", "Lemon"]
```

The total count of the elements in the array is its `length`:

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits.length ); // 3
```

We can also use `alert` to show the whole array.

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits ); // Apple,Orange,Plum
```

An array can store elements of any type.

{% hint style="info" %}
Trailing comma

An array, just like an object, may end with a comma:

```javascript
let fruits = [
  "Apple",
  "Orange",
  "Plum",
];
```

The “trailing comma” style makes it easier to insert/remove items, because all lines become alike.
{% endhint %}

### Methods pop/push, shift/unshift

A [queue](https://en.wikipedia.org/wiki/Queue_%28abstract_data_type%29) is one of the most common uses of an array. In computer science, this means an ordered collection of elements which supports two operations:

* `push` appends an element to the end.
* `shift` get an element from the beginning, advancing the queue, so that the 2nd element becomes the 1st.

![](https://javascript.info/article/array/queue.png)

There’s another use case for arrays – the data structure named [stack](https://en.wikipedia.org/wiki/Stack_%28abstract_data_type%29).

It supports two operations:

* `push` adds an element to the end.
* `pop` takes an element from the end.

So new elements are added or taken always from the “end”.

A stack is usually illustrated as a pack of cards: new cards are added to the top or taken from the top:

![](https://javascript.info/article/array/stack.png)

**Methods that work with the end of the array:**

#### `pop`

Extracts the last element of the array and returns it:

```javascript
let fruits = ["Apple", "Orange", "Pear"];

alert( fruits.pop() ); // remove "Pear" and alert it

alert( fruits ); // Apple, Orange
```

#### `push`

Append the element to the end of the array:

```javascript
let fruits = ["Apple", "Orange"];

fruits.push("Pear");

alert( fruits ); // Apple, Orange, Pear
```

**Methods that work with the beginning of the array:**

#### `shift`

Extracts the first element of the array and returns it:

```javascript
let fruits = ["Apple", "Orange", "Pear"];

alert( fruits.shift() ); // remove Apple and alert it

alert( fruits ); // Orange, Pear
```

### `unshift`

Add the element to the beginning of the array:

```javascript
let fruits = ["Orange", "Pear"];

fruits.unshift('Apple');

alert( fruits ); // Apple, Orange, Pear
```

Methods `push` and `unshift` can add multiple elements at once:

```javascript
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

// ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
alert( fruits );
```

### [Internals](https://javascript.info/array#internals)

Remember, there are only 7 basic types in JavaScript. Array is an object and thus behaves like an object.

For instance, it is copied by reference:

```javascript
let fruits = ["Banana"]

let arr = fruits; // copy by reference (two variables reference the same array)

alert( arr === fruits ); // true

arr.push("Pear"); // modify the array by reference

alert( fruits ); // Banana, Pear - 2 items now
```

…But what makes arrays really special is their internal representation. The engine tries to store its elements in the contiguous memory area, one after another, and there are other optimizations as well, to make arrays work really fast.

But they all break if we quit working with an array as with an “ordered collection” and start working with it as if it were a regular object.

For instance, technically we can do this:

```javascript
let fruits = []; // make an array

fruits[99999] = 5; // assign a property with the index far greater than its length

fruits.age = 25; // create a property with an arbitrary name
```

The ways to misuse an array:

* Add a non-numeric property like `arr.test = 5`.
* Make holes, like: add `arr[0]` and then `arr[1000]` \(and nothing between them\).
* Fill the array in the reverse order, like `arr[1000]`, `arr[999]` and so on.

Please think of arrays as special structures to work with the _ordered data_. They provide special methods for that. Arrays are carefully tuned inside JavaScript engines to work with contiguous ordered data, please use them this way. And if you need arbitrary keys, chances are high that you actually require a regular object `{}`.

### [Performance](https://javascript.info/array#performance)

Methods `push/pop` run fast, while `shift/unshift` are slow.![](https://javascript.info/article/array/array-speed.png)

Why is it faster to work with the end of an array than with its beginning? Let’s see what happens during the execution:

```text
fruits.shift(); // take 1 element from the start
```

It’s not enough to take and remove the element with the number `0`. Other elements need to be renumbered as well.

The `shift` operation must do 3 things:

1. Remove the element with the index `0`.
2. Move all elements to the left, renumber them from the index `1` to `0`, from `2` to `1` and so on.
3. Update the `length` property.

![](https://javascript.info/article/array/array-shift.png)

**The more elements in the array, the more time to move them, more in-memory operations.**

The similar thing happens with `unshift`: to add an element to the beginning of the array, we need first to move existing elements to the right, increasing their indexes.

And what’s with `push/pop`? They do not need to move anything. To extract an element from the end, the `pop`method cleans the index and shortens `length`.

The actions for the `pop` operation:

```text
fruits.pop(); // take 1 element from the end
```

![](https://javascript.info/article/array/array-pop.png)

**The `pop` method does not need to move anything, because other elements keep their indexes. That’s why it’s blazingly fast.**

The similar thing with the `push` method.

Technically, because arrays are objects, it is also possible to use `for..in`:

```javascript
let arr = ["Apple", "Orange", "Pear"];

for (let key in arr) {
  alert( arr[key] ); // Apple, Orange, Pear
}
```

But that’s actually a bad idea. There are potential problems with it:

1. The loop `for..in` iterates over _all properties_, not only the numeric ones.

   There are so-called “array-like” objects in the browser and in other environments, that _look like arrays_. That is, they have `length` and indexes properties, but they may also have other non-numeric properties and methods, which we usually don’t need. The `for..in` loop will list them though. So if we need to work with array-like objects, then these “extra” properties can become a problem.

2. The `for..in` loop is optimized for generic objects, not arrays, and thus is 10-100 times slower. Of course, it’s still very fast. The speedup may only matter in bottlenecks. But still we should be aware of the difference.

Generally, we shouldn’t use `for..in` for arrays.

### [new Array\(\)](https://javascript.info/array#new-array)

There is one more syntax to create an array:

```javascript
let arr = new Array("Apple", "Pear", "etc");
```

It’s rarely used, because square brackets `[]` are shorter. Also there’s a tricky feature with it.

If `new Array` is called with a single argument which is a number, then it creates an array _without items, but with the given length_.

Let’s see how one can shoot themself in the foot:

```javascript
let arr = new Array(2); // will it create an array of [2] ?

alert( arr[0] ); // undefined! no elements.

alert( arr.length ); // length 2
```

In the code above, `new Array(number)` has all elements `undefined`.

To evade such surprises, we usually use square brackets, unless we really know what we’re doing.

### [toString](https://javascript.info/array#tostring)

Arrays have their own implementation of `toString` method that returns a comma-separated list of elements.

For instance:

```javascript
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true
```

Also, let’s try this:

```javascript
alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```

Arrays do not have `Symbol.toPrimitive`, neither a viable `valueOf`, they implement only `toString`conversion, so here `[]` becomes an empty string, `[1]` becomes `"1"` and `[1,2]` becomes `"1,2"`.

### [Summary](https://javascript.info/array#summary)

Array is a special kind of object, suited to storing and managing ordered data items.

* The declaration:

  ```javascript
  // square brackets (usual)
  let arr = [item1, item2...];

  // new Array (exceptionally rare)
  let arr = new Array(item1, item2...);
  ```

  The call to `new Array(number)` creates an array with the given length, but without elements.

* The `length` property is the array length or, to be precise, its last numeric index plus one. It is auto-adjusted by array methods.
* If we shorten `length` manually, the array is truncated.

We can use an array as a deque with the following operations:

* `push(...items)` adds `items` to the end.
* `pop()` removes the element from the end and returns it.
* `shift()` removes the element from the beginning and returns it.
* `unshift(...items)` adds `items` to the beginning.

To loop over the elements of the array:

* `for (let i=0; i<arr.length; i++)` – works fastest, old-browser-compatible.
* `for (let item of arr)` – the modern syntax for items only,
* `for (let i in arr)` – never use.

