# JavaScript: Functions, Execution Context and Variables scopes

### Variable Scoping

в JS область видимости - это текущий контекст в коде.

* глобальная область видимости
* локальная область видимости \(функция\)
* блочная область видимости для переменных \(let, const\)

**LexicalEnvironment**

Все переменные внутри функции – это свойства специального внутреннего объекта LexicalEnvironment. При запуске функция создает объект LexicalEnvironment, записывает туда аргументы, функции и переменные.

* Каждая функция при создании получает ссылку \[\[Scope\]\] на объект с переменными, в контексте которого была создана.
* При запуске функции создаётся новый объект с переменными LexicalEnvironment. Он получает ссылку на внешний объект переменных из \[\[Scope\]\].
* При поиске переменных он осуществляется сначала в текущем объекте переменных, а потом – по этой ссылке.

### Context of calling

> Context - это не scope, а то, куда ссылается `this`

```text
- при вызове функции через new создается новый объект и ```this``` ссылается на него
```

### **this**

> Значение this называется контекстом вызова и будет определено в момент вызова функции.

* this - текущий объект при вызове «через точку» и новый объект при конструировании через new.
* Если одну и ту же функцию запускать в контексте разных объектов, она будет получать разный this
* потеря контекста

  ```text
  const user = {
    name: "Вася",
    hi: function() { alert(this.name); },
    bye: function() { alert("Пока"); }
  };

  user.hi(); // Вася (простой вызов работает)

  // а теперь вызовем user.hi или user.bye в зависимости от имени
  (user.name == "Вася" ? user.hi : user.bye)(); // undefined
  ```

### Functions

Functions are the main “building blocks” of the program. They allow the code to be called many times without repetition.

A function declaration looks like this:

```javascript
function name(parameters, delimited, by, comma) {
  /* code */
}
```

![](../../.gitbook/assets/image%20%2864%29.png)

```javascript
function showMessage() {
  alert( 'Hello everyone!' );
}

showMessage();
showMessage();
```

* Values passed to a function as parameters are copied to its local variables. A variable declared inside a function is only visible inside that function. 

  ```javascript
  function showMessage() {
    let message = "Hello, I'm JavaScript!"; // local variable

    alert( message );
  }

  showMessage(); // Hello, I'm JavaScript!

  alert( message ); // <-- Error! The variable is local to the function
  ```

* A function may access outer variables. But it works only from inside out. 

  ```javascript
  let userName = 'John';

  function showMessage() {
    let message = 'Hello, ' + userName;
    alert(message);
  }

  showMessage(); // Hello, John
  ```

  The function has full access to the outer variable. It can modify it as well.

  ```javascript
  let userName = 'John';

  function showMessage() {
    userName = "Bob"; // (1) changed the outer variable

    let message = 'Hello, ' + userName;
    alert(message);
  }

  alert( userName ); // John before the function call

  showMessage();

  alert( userName ); // Bob, the value was modified by the function
  ```

  The code outside of the function doesn’t see its local variables.

  ```javascript
  let userName = 'John';

  function showMessage() {
    let userName = "Bob"; // declare a local variable

    let message = 'Hello, ' + userName; // Bob
    alert(message);
  }

  // the function will create and use its own userName
  showMessage();

  alert( userName ); // John, unchanged, the function did not access the outer variable
  ```

* A function can return a value. If it doesn’t, then its result is `undefined`.

  ```javascript
  function showMovie(age) {
    if ( !checkAge(age) ) {
      return;
    }

    alert( "Showing you the movie" ); // (*)
    // ...
  }
  ```

  ```javascript
  function sum(a, b) {
    return a + b;
  }

  let result = sum(1, 2);
  alert( result ); // 3
  ```

To make the code clean and easy to understand, it’s recommended to use mainly local variables and parameters in the function, not outer variables.

 We can pass arbitrary data to functions using parameters \(also called _function arguments_\) .

```javascript
function showMessage(from, text) { // arguments: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```

When the function is called in lines `(*)` and `(**)`, the given values are copied to local variables `from` and `text`. Then the function uses them.

Here’s one more example: we have a variable `from` and pass it to the function. Please note: the function changes `from`, but the change is not seen outside, because a function always gets a copy of the value:

```javascript
function showMessage(from, text) {

  from = '*' + from + '*'; // make "from" look nicer

  alert( from + ': ' + text );
}

let from = "Ann";

showMessage(from, "Hello"); // *Ann*: Hello

// the value of "from" is the same, the function modified a local copy
alert( from ); // Ann
```

It is always easier to understand a function which gets parameters, works with them and returns a result than a function which gets no parameters, but modifies outer variables as a side-effect.

If a parameter is not provided, then its value becomes `undefined`.

For instance, the aforementioned function `showMessage(from, text)` can be called with a single argument:

```javascript
showMessage("Ann");
```

That’s not an error. Such a call would output `"Ann: undefined"`. There’s no `text`, so it’s assumed that `text === undefined`.

If we want to use a “default” `text` in this case, then we can specify it after `=`:

```javascript
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```

Function naming:

* A name should clearly describe what the function does. When we see a function call in the code, a good name instantly gives us an understanding what it does and returns.
* A function is an action, so function names are usually verbal.
* There exist many well-known function prefixes like `create…`, `show…`, `get…`, `check…` and so on. Use them to hint what a function does.

Functions are the main building blocks of scripts. Now we’ve covered the basics, so we actually can start creating and using them. But that’s only the beginning of the path. We are going to return to them many times, going more deeply into their advanced features.

### Execution Context

A property of an execution context \(global, function or eval\) that, in non–strict mode, is always a reference to an object and in strict mode can be any value.

```javascript
this
```

#### Global context

In the global execution context \(outside of any function\), `this` refers to the global object whether in strict mode or not.

```javascript
// In web browsers, the window object is also the global object:
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```

{% hint style="info" %}
 You can always easily get the global object using the global [`globalThis`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis) property, regardless of the current context in which your code is running.
{% endhint %}

#### Function context

 Inside a function, the value of `this` depends on how the function is called.

Since the following code is not in [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode), and because the value of `this` is not set by the call, `this` will default to the global object, which is [`window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) in a browser. 

```javascript
function f1() {
  return this;
}

// In a browser:
f1() === window; // true 

// In Node:
f1() === global; // true
```

In strict mode, however, if the value of `this` is not set when entering an execution context, it remains as `undefined`, as shown in the following example**:**

```javascript
function f2() {
  'use strict'; // see strict mode
  return this;
}

f2() === undefined; // true
```

{% hint style="info" %}
 In the second example, `this` should be [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined), because `f2` was called directly and not as a method or property of an object \(e.g. `window.f2()`\). This feature wasn't implemented in some browsers when they first started to support [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode). As a result, they incorrectly returned the `window` object.
{% endhint %}

### Variables scopes

The scope of a variable is the region of your program source code in which it is defined. A global variable has global scope; it is defined everywhere in your JavaScript code. On the other hand, variables declared within a function are defined only within the body of the function. They are local variables and have local scope.

Within the body of a function, a local variable takes precedence over a global variable with the same name. If you declare a local variable or function parameter with the same name as a global variable, you effectively hide the global variable:

```javascript
var scope = "global"; // Declare a global variable
function checkscope() {
 var scope = "local"; // Declare a local variable with the same name
 return scope; // Return the local value, not the global one
}
checkscope() // => "local"
```

Although you can get away with not using the var statement when you write code in the global scope, you must always use var to declare local variables. Consider what happens if you don’t:

```javascript
scope = "global"; // Declare a global variable, even without var.
function checkscope2() {
 scope = "local"; // Oops! We just changed the global variable.
 myscope = "local"; // This implicitly declares a new global variable.
 return [scope, myscope]; // Return two values.
}
checkscope2() // => ["local", "local"]: has side effects!
scope // => "local": global variable has changed.
myscope // => "local": global namespace cluttered up
```

Function definitions can be nested. Each function has its own local scope, so it is possible to have several nested layers of local scope. For example:

```javascript
var scope = "global scope"; // A global variable
function checkscope() {
 var scope = "local scope"; // A local variable
 function nested() {
 var scope = "nested scope"; // A nested scope of local variables
 return scope; // Return the value in scope here
 }
 return nested();
}
checkscope() // => "nested scope"
```

### Function Scope and Hoisting

#### Function hoisting <a id="function-hoisting"></a>

> Hoisting is JavaScript's default behavior of moving declarations to the top.

* Variables and constants declared with let or const are not hoisted!
* function declaration, var - hoisted

In some C-like programming languages, each block of code within curly braces has its own scope, and variables are not visible outside of the block in which they are declared. This is called block scope, and JavaScript does not have it. Instead, JavaScript uses function scope: variables are visible within the function in which they are defined and within any functions that are nested within that function. In the following code, the variables i, j, and k are declared in different spots, but all have the same scope—all three are defined throughout the body of the function:

```javascript
function test(o) {
 var i = 0; // i is defined throughout function
 if (typeof o == "object") {
 var j = 0; // j is defined everywhere, not just block
 for(var k=0; k < 10; k++) { // k is defined everywhere, not just loop
 console.log(k); // print numbers 0 through 9
 }
 console.log(k); // k is still defined: prints 10
 }
 console.log(j); // j is defined, but may not be initialized
}
```

JavaScript’s function scope means that all variables declared within a function are visible throughout the body of the function. Curiously, this means that variables are even visible before they are declared. This feature of JavaScript is informally known as hoisting: JavaScript code behaves as if all variable declarations in a function \(but not any associated assignments\) are “hoisted” to the top of the function. Consider the following code:

```javascript
var scope = "global";
function f() {
 console.log(scope); // Prints "undefined", not "global"
 var scope = "local"; // Variable initialized here, but defined everywhere
 console.log(scope); // Prints "local"
}
```

You might think that the first line of the function would print “global”, because the var statement declaring the local variable has not yet been executed. Because of the rules of function scope, however, this is not what happens. The local variable is defined throughout the body of the function, which means the global variable by the same name is hidden throughout the function. Although the local variable is defined throughout, it is not actually initialized until the var statement is executed. Thus, the function above is equivalent to the following, in which the variable declaration is “hoisted” to the top and the variable initialization is left where it is:

```javascript
function f() {
 var scope; // Local variable is declared at the top of the function
 console.log(scope); // It exists here, but still has "undefined" value
 scope = "local"; // Now we initialize it and give it a value
 console.log(scope); // And here it has the value we expect
}
```

In programming languages with block scope, it is generally good programming practice to declare variables as close as possible to where they are used and with the narrowest possible scope. Since JavaScript does not have block scope, some programmers make a point of declaring all their variables at the top of the function, rather than trying to declare them closer to the point at which they are used. This technique makes their source code accurately reflect the true scope of the variables.

