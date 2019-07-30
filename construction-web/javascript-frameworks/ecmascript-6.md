# EcmaScript 6

{% page-ref page="../javascript-html-css/ecma-script-6-oop.md" %}

ECMAScript 6 is also known as ES6 and ECMAScript 2015. 

Some of the new features in ES6:

* JavaScript `let`
* JavaScript `const`
* JavaScript Arrow Functions
* JavaScript Classes
* Default parameter values
* `Array.find()`
* `Array.findIndex()`
* Exponentiation \(`**`\) \(EcmaScript 2016\)

###  `let`

The `let` statement allows you to declare a variable with block scope. 

### `const`

The `const` statement allows you to declare a constant \(a JavaScript variable with a constant value\).

Constants are similar to let variables, except that the value cannot be changed.

### Arrow Functions

Arrow functions allows a short syntax for writing function expressions.

You don't need the `function` keyword, the `return` keyword, and the **curly brackets**.

```javascript
// ES5
var x = function(x, y) {
   return x * y;
}

// ES6
const x = (x, y) => x * y;
```

Arrow functions do not have their own `this`. They are not well suited for defining **object methods**.

Arrow functions are not hoisted. They must be defined **before** they are used.

Using `const` is safer than using `var`, because a function expression is always constant value.

You can only omit the `return` keyword and the curly brackets if the function is a single statement. Because of this, it might be a good habit to always keep them:

```javascript
const x = (x, y) => { return x * y };
```

### Classes

ES6 introduced classes.

A class is a type of function, but instead of using the keyword `function` to initiate it, we use the keyword `class`, and the properties is assigned inside a`constructor()` method.

Use the keyword `class` to create a class, and always add a constructor method.

The constructor method is called each time the class object is initialized.

```javascript
class Car {
  constructor(brand) {
    this.carname = brand;
  }
}
```

Now you can create objects using the Car class \(create an object called "mycar" based on the Car class\): 

```javascript
class Car {
  constructor(brand) {
    this.carname = brand;
  }
}
mycar = new Car("Ford");
```

### Default Parameter Values

ES6 allows function parameters to have default values.

```javascript
function myFunction(x, y = 10) {
  // y is 10 if not passed or undefined
  return x + y;
}
myFunction(5); // will return 15
```

### Array.find\(\)

The `find()` method returns the value of the first array element that passes a test function.

This example finds \(returns the value of \) the first element that is larger than 18:

```javascript
var numbers = [4, 9, 16, 25, 29];
var first = numbers.find(myFunction);

function myFunction(value, index, array) {
  return value > 18;
}
```

Note that the function takes 3 arguments:

* The item value
* The item index
* The array itself

### Array.findIndex\(\)

The `findIndex()` method returns the index of the first array element that passes a test function.

This example finds the index of the first element that is larger than 18:

```javascript
var numbers = [4, 9, 16, 25, 29];
var first = numbers.findIndex(myFunction);

function myFunction(value, index, array) {
  return value > 18;
}
```

Note that the function takes 3 arguments:

* The item value
* The item index
* The array itself

