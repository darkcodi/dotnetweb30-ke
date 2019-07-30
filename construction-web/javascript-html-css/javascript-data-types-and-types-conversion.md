# JavaScript: Data types and types conversion

## Data types

A variable in JavaScript can contain any data. Programming languages that allow such things are called “dynamically typed”, meaning that there are data types, but variables are not bound to any of them.

There are seven basic data types in JavaScript.

* `number` for numbers of any kind: integer or floating-point.
* `string` for strings. A string may have one or more characters, there’s no separate single-character type.
* `boolean` for `true`/`false`.
* `null` for unknown values – a standalone type that has a single value `null`.
* `undefined` for unassigned values – a standalone type that has a single value `undefined`.
* `object` for more complex data structures.
* `symbol` for unique identifiers.

### [A number](https://javascript.info/types#a-number)

 The _number_ type represents both integer and floating point numbers. 

There are many operations for numbers, e.g. multiplication `*`, division `/`, addition `+`, subtraction `-`, and so on.

Besides regular numbers, there are so-called “special numeric values” which also belong to this data type: `Infinity`, `-Infinity` and `NaN`.

 `NaN` is sticky. Any further operation on `NaN` returns `NaN`

`Infinity` represents the mathematical [Infinity](https://en.wikipedia.org/wiki/Infinity) ∞. It is a special value that’s greater than any number.

```javascript
alert( 1 / 0 ); // Infinity
alert( Infinity ); // Infinity
alert( "not a number" / 2 ); // NaN, such division is erroneous
alert( "not a number" / 2 + 5 ); // NaN
```

{% hint style="info" %}
**Mathematical operations are safe**

Doing maths is “safe” in JavaScript. We can do anything: divide by zero, treat non-numeric strings as numbers, etc.

The script will never stop with a fatal error \(“die”\). At worst, we’ll get `NaN` as the result.
{% endhint %}

### [A string](https://javascript.info/types#a-string)

A string in JavaScript must be surrounded by quotes. In JavaScript, there are 3 types of quotes:

1. Double quotes: `"Hello"`.
2. Single quotes: `'Hello'`.
3. Backticks: ```Hello```.

```javascript
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed ${str}`;
alert( "the result is ${1 + 2}" ); // the result is ${1 + 2} (double quotes do nothing)
```

The expression inside `${…}` is evaluated and the result becomes a part of the string. We can put anything in there: a variable like `name` or an arithmetical expression like `1 + 2` or something more complex.

Please note that this can only be done in backticks. Other quotes don’t have this embedding functionality!

{% hint style="info" %}
**There is no** _**character**_ **type.**

In some languages, there is a special “character” type for a single character. For example, in the C language and in Java it is `char`.

In JavaScript, there is no such type. There’s only one type: `string`. A string may consist of only one character or many of them.
{% endhint %}

### [A boolean \(logical type\)](https://javascript.info/types#a-boolean-logical-type)

 The boolean type has only two values: `true` and `false`.

Boolean values also come as a result of comparisons:

```javascript
let isGreater = 4 > 1;

alert( isGreater ); // true (the comparison result is "yes")
```

### [The “null” value](https://javascript.info/types#the-null-value)

The special `null` value does not belong to any of the types described above.

It forms a separate type of its own which contains only the `null` value:

```javascript
let age = null;
```

In JavaScript, `null` is not a “reference to a non-existing object” or a “null pointer” like in some other languages.

It’s just a special value which represents “nothing”, “empty” or “value unknown”.

The code above states that `age` is unknown or empty for some reason.

### [The “undefined” value](https://javascript.info/types#the-undefined-value)

The special value `undefined` also stands apart. It makes a type of its own, just like `null`.

The meaning of `undefined` is “value is not assigned”.

```javascript
let y;

alert(y); // shows "undefined"

let x = 123;

x = undefined;

alert(x); // "undefined"
```

 …But we don’t recommend doing that. Normally, we use `null` to assign an “empty” or “unknown” value to a variable, and we use `undefined` for checks like seeing if a variable has been assigned.

### [Objects](https://javascript.info/types#objects-and-symbols)

 The `object` type is special. All other types are called “primitive” because their values can contain only a single thing \(be it a string or a number or whatever\). In contrast, objects are used to store collections of data and more complex entities.

```javascript
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30        // by key "age" store value 30
};
```

### [Symbols](https://javascript.info/types#objects-and-symbols)

 The `symbol` type is used to create unique identifiers for objects. “Symbol” value represents a unique identifier. Upon creation, we can give symbol a description \(also called a symbol name\), mostly useful for debugging purposes.

Symbols are guaranteed to be unique. Even if we create many symbols with the same description, they are different values. The description is just a label that doesn’t affect anything.

For instance, here are two symbols with the same description – they are not equal:

```javascript
// id is a new symbol
let id = Symbol();

// id is a symbol with the description "id"
let id = Symbol("id");

let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

## The typeof operator

The `typeof` operator returns the type of the argument. It’s useful when we want to process values of different types differently or just want to do a quick check.

It supports two forms of syntax:

1. As an operator: `typeof x`.
2. As a function: `typeof(x)`.

In other words, it works with parentheses or without them. The result is the same.

The call to `typeof x` returns a string with the type name:

```javascript
typeof undefined // "undefined"

typeof 0 // "number"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

typeof Math // "object"  (1)

typeof null // "object"  (2)

typeof alert // "function"  (3)
```

The `typeof` operator allows us to see which type is stored in a variable.

* Two forms: `typeof x` or `typeof(x)`.
* Returns a string with the name of the type, like `"string"`.
* For `null` returns `"object"` – this is an error in the language, it’s not actually an object.

## Type Conversions

Most of the time, operators and functions automatically convert the values given to them to the right type.

For example, `alert` automatically converts any value to a string to show it. Mathematical operations convert values to numbers.

### [ToString](https://javascript.info/type-conversions#tostring)

String conversion happens when we need the string form of a value.

For example, `alert(value)` does it to show the value.

We can also call the `String(value)` function to convert a value to a string:

```javascript
let value = true;
alert(typeof value); // boolean

value = String(value); // now value is a string "true"
alert(typeof value); // string
```

String conversion is mostly obvious. A `false` becomes `"false"`, `null` becomes `"null"`, etc.

### [ToNumber](https://javascript.info/type-conversions#tonumber)

Numeric conversion happens in mathematical functions and expressions automatically.

For example, when division `/` is applied to non-numbers:

```javascript
alert( "6" / "2" ); // 3, strings are converted to numbers
```

We can use the `Number(value)` function to explicitly convert a `value` to a number:

```javascript
let str = "123";
alert(typeof str); // string

let num = Number(str); // becomes a number 123

alert(typeof num); // number
```

Explicit conversion is usually required when we read a value from a string-based source like a text form but expect a number to be entered.

If the string is not a valid number, the result of such a conversion is `NaN`. For instance:

```javascript
let age = Number("an arbitrary string instead of a number");

alert(age); // NaN, conversion failed
```

Numeric conversion rules:

| Value | Becomes… |
| :--- | :--- |
| `undefined` | `NaN` |
| `null` | `0` |
| `true and false` | `1` and `0` |
| `string` | Whitespaces from the start and end are removed. If the remaining string is empty, the result is `0`. Otherwise, the number is “read” from the string. An error gives `NaN`. |

{% hint style="danger" %}
**Addition ‘+’ concatenates strings**

Almost all mathematical operations convert values to numbers. A notable exception is addition `+`. If one of the added values is a string, the other one is also converted to a string.

Then, it concatenates \(joins\) them:

```text
alert( 1 + '2' ); // '12' (string to the right)
alert( '1' + 2 ); // '12' (string to the left)
```

This only happens when at least one of the arguments is a string. Otherwise, values are converted to numbers.
{% endhint %}

### [ToBoolean](https://javascript.info/type-conversions#toboolean)

Boolean conversion is the simplest one.

It happens in logical operations \(later we’ll meet condition tests and other similar things\) but can also be performed explicitly with a call to `Boolean(value)`.

The conversion rule:

* Values that are intuitively “empty”, like `0`, an empty string, `null`, `undefined`, and `NaN`, become `false`.
* Other values become `true`.

For instance:

```javascript
alert( Boolean(1) ); // true
alert( Boolean(0) ); // false

alert( Boolean("hello") ); // true
alert( Boolean("") ); // false
```

{% hint style="warning" %}
**Please note: the string with zero `"0"` is `true`**

Some languages \(namely PHP\) treat `"0"` as `false`. But in JavaScript, a non-empty string is always `true`.

```text
alert( Boolean("0") ); // true
alert( Boolean(" ") ); // spaces, also true (any non-empty string is true)
```
{% endhint %}

### [Summary](https://javascript.info/type-conversions#summary)

The three most widely used type conversions are to string, to number, and to boolean.

**`ToString`** – Occurs when we output something. Can be performed with `String(value)`. The conversion to string is usually obvious for primitive values.

**`ToNumber`** – Occurs in math operations. Can be performed with `Number(value)`.

The conversion follows the rules:

| Value | Becomes… |
| :--- | :--- |
| `undefined` | `NaN` |
| `null` | `0` |
| `true / false` | `1 / 0` |
| `string` | The string is read “as is”, whitespaces from both sides are ignored. An empty string becomes `0`. An error gives `NaN`. |

**`ToBoolean`** – Occurs in logical operations. Can be performed with `Boolean(value)`.

Follows the rules:

| Value | Becomes… |
| :--- | :--- |
| `0`, `null`, `undefined`, `NaN`, `""` | `false` |
| any other value | `true` |

Most of these rules are easy to understand and memorize. The notable exceptions where people usually make mistakes are:

* `undefined` is `NaN` as a number, not `0`.
* `"0"` and space-only strings like `" "` are true as a boolean.

