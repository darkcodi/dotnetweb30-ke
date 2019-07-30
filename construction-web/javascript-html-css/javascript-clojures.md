# JavaScript: Closure

{% hint style="success" %}
  A _closure_ is the combination of a function and the lexical environment within which that function was declared. This environment consists of any local variables that were in-scope at the time the closure was created. 
{% endhint %}

Like most modern programming languages, JavaScript uses lexical scoping. This means that functions are executed using the variable scope that was in effect when they were defined, not the variable scope that is in effect when they are invoked. In order to implement lexical scoping, the internal state of a JavaScript function object must include not only the code of the function but also a reference to the current scope chain_._ This combination of a function object and a scope \(a set of variable bindings\) in which the function’s variables are resolved is called a **closure** in the computer science literature. 

{% hint style="info" %}
This is an old term that refers to the fact that the function’s variables have bindings in the scope chain and that therefore the function is “closed over” its variables.
{% endhint %}

Technically, all JavaScript functions are closures: they are objects, and they have a scope chain associated with them. Most functions are invoked using the same scope chain that was in effect when the function was defined, and it doesn’t really matter that there is a closure involved. Closures become interesting when they are invoked under a different scope chain than the one that was in effect when they were defined. This happens most commonly when a nested function object is returned from the function within which it was defined. There are a number of powerful programming techniques that involve this kind of nested function closures, and their use has become relatively common in JavaScript programming. Closures may seem confusing when you first encounter them, but it is important that you understand them well enough to use them comfortably.

```javascript
var scope = "global scope"; // A global variable
function checkscope() {
 var scope = "local scope"; // A local variable
 function f() { return scope; } // Return the value in scope here
 return f();
}
checkscope() // => "local scope"
```

The checkscope\(\) function declares a local variable and then defines and invokes a function that returns the value of that variable. It should be clear to you why the call to checkscope\(\) returns “local scope”. Now let’s change the code just slightly.

```javascript
var scope = "global scope"; // A global variable
function checkscope() {
 var scope = "local scope"; // A local variable
 function f() { return scope; } // Return the value in scope here
 return f;
}
checkscope()() // What does this return?
```

In this code, a pair of parentheses has moved from inside checkscope\(\) to outside of it. Instead of invoking the nested function and returning its result, checkscope\(\) now just returns the nested function object itself.

Remember the fundamental rule of lexical scoping: JavaScript functions are executed using the scope chain that was in effect when they were defined. The nested function f\(\) was defined under a scope chain in which the variable scope was bound to the value “local scope”. That binding is still in effect when f is executed, wherever it is executed from. So the last line of code above returns “local scope”, not “global scope”. This, in a nutshell, is the surprising and powerful nature of closures: they capture the local variable \(and parameter\) bindings of the outer function within which they are defined.

