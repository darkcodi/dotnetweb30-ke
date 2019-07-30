# JavaScript: Variables

Variables are used to store this information.

A [variable](https://en.wikipedia.org/wiki/Variable_%28computer_science%29) is a “named storage” for data. We can use variables to store goodies, visitors, and other data.

To create a variable in JavaScript, use the `let` keyword.

![](../../.gitbook/assets/image%20%2816%29.png)

We can put any value in the box.

We can also change it as many times as we want:

```javascript
let message;

message = 'Hello!';

message = 'World!'; // value changed

alert(message);
```

When the value is changed, the old data is removed from the variable:

![](../../.gitbook/assets/image%20%2831%29.png)

We can also declare two variables and copy data from one into the other.



```javascript
let hello = 'Hello world!';

let message;

// copy 'Hello world' from hello into message
message = hello;

// now two variables hold the same data
alert(hello); // Hello world!
alert(message); // Hello world!
```

{% hint style="info" %}
There are two limitations on variable names in JavaScript:

1. The name must contain only letters, digits, or the symbols `$` and `_`.
2. The first character must not be a digit.
{% endhint %}

```javascript
let $ = 1; // declared a variable with the name "$"
let _ = 2; // and now a variable with the name "_"

alert($ + _); // 3
```

{% hint style="info" %}
**Case matters**

Variables named `apple` and `AppLE` are two different variables.
{% endhint %}

**Non-Latin letters are allowed, but not recommended**

It is possible to use any language, including cyrillic letters or even hieroglyphs, like this:

```javascript
let имя = '...';
let 我 = '...';
```

[Constants](https://javascript.info/variables#constants):  to declare a constant \(unchanging\) variable, use `const` instead of `let`:

```javascript
const myBirthday = '18.04.1982';
```

### [Summary](https://javascript.info/variables#summary)

We can declare variables to store data by using the `var`, `let`, or `const` keywords.

* `let` – is a modern variable declaration. The code must be in strict mode to use `let` in Chrome \(V8\).
* `var` – is an old-school variable declaration. Normally we don’t use it at all, but we’ll cover subtle differences from `let` in the chapter [The old "var"](https://javascript.info/var), just in case you need them.
* `const` – is like `let`, but the value of the variable can’t be changed.

Variables should be named in a way that allows us to easily understand what’s inside them.

