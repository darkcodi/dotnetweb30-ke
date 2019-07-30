# JavaScript: Operators

* _An operand_ – is what operators are applied to. For instance, in the multiplication of `5 * 2` there are two operands: the left operand is `5` and the right operand is `2`. Sometimes, people call these “arguments” instead of “operands”.
* An operator is _unary_ if it has a single operand. For example, the unary negation `-` reverses the sign of a number:
*  An operator is _binary_ if it has two operands. 

### [String concatenation, binary +](https://javascript.info/operators#string-concatenation-binary)

Usually, the plus operator `+` sums numbers.

But, if the binary `+` is applied to strings, it merges \(concatenates\) them:

```javascript
let s = "my" + "string";
alert(s); // mystring
```

Note that if one of the operands is a string, the other one is converted to a string too.

```javascript
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

However, note that operations run from left to right. If there are two numbers followed by a string, the numbers will be added before being converted to a string:

```javascript
alert(2 + 2 + '1' ); // "41" and not "221"
```

Other arithmetic operators work only with numbers and always convert their operands to numbers.

For instance, subtraction and division:

```javascript
alert( 2 - '1' ); // 1
alert( '6' / '2' ); // 3
```

### [Numeric conversion, unary +](https://javascript.info/operators#numeric-conversion-unary)

 The plus `+` exists in two forms: the binary form that we used above and the unary form.  The unary plus or, in other words, the plus operator `+` applied to a single value, doesn’t do anything to numbers. But if the operand is not a number, the unary plus converts it into a number.

```javascript
// No effect on numbers
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

// Converts non-numbers
alert( +true ); // 1
alert( +"" );   // 0
```

The binary plus would add them as strings:

```javascript
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
```

If we want to treat them as numbers, we need to convert and then sum them:

```javascript
let apples = "2";
let oranges = "3";

// both values converted to numbers before the binary plus
alert( +apples + +oranges ); // 5

// the longer variant
// alert( Number(apples) + Number(oranges) ); // 5
```

### [Operator precedence](https://javascript.info/operators#operator-precedence)

 If an expression has more than one operator, the execution order is defined by their _precedence_, or, in other words, the default priority order of operators.

| Precedence | Name | Sign |
| :--- | :--- | :--- |
| … | … | … |
| 16 | unary plus | `+` |
| 16 | unary negation | `-` |
| 14 | multiplication | `*` |
| 14 | division | `/` |
| 13 | addition | `+` |
| 13 | subtraction | `-` |
| … | … | … |
| 3 | assignment | `=` |
| … | … | … |

As we can see, the “unary plus” has a priority of `16` which is higher than the `13` of “addition” \(binary plus\). That’s why, in the expression `"+apples + +oranges"`, unary pluses work before the addition.

### [Assignment](https://javascript.info/operators#assignment)

Let’s note that an assignment `=` is also an operator. It is listed in the precedence table with the very low priority of `3`.

That’s why, when we assign a variable, like `x = 2 * 2 + 1`, the calculations are done first and then the `=` is evaluated, storing the result in `x`.

```javascript
let x = 2 * 2 + 1;

alert( x ); // 5
```

It is possible to chain assignments:

```javascript
let a, b, c;

a = b = c = 2 + 2;

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Chained assignments evaluate from right to left. First, the rightmost expression `2 + 2` is evaluated and then assigned to the variables on the left: `c`, `b` and `a`. At the end, all the variables share a single value.

{% hint style="info" %}
T**he assignment operator `"="` returns a value**

An operator always returns a value. That’s obvious for most of them like addition `+` or multiplication `*`. But the assignment operator follows this rule too.

The call `x = value` writes the `value` into `x` _and then returns it_.

Here’s a demo that uses an assignment as part of a more complex expression:

```javascript
let a = 1;
let b = 2;

let c = 3 - (a = b + 1);

alert( a ); // 3
alert( c ); // 0
```
{% endhint %}

### [Remainder %](https://javascript.info/operators#remainder)

The result of `a % b` is the remainder of the integer division of `a` by `b`.

```javascript
alert( 5 % 2 ); // 1 is a remainder of 5 divided by 2
alert( 8 % 3 ); // 2 is a remainder of 8 divided by 3
alert( 6 % 3 ); // 0 is a remainder of 6 divided by 3
```

### [Exponentiation \*\*](https://javascript.info/operators#exponentiation)

For a natural number `b`, the result of `a ** b` is `a` multiplied by itself `b` times.

```javascript
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

The operator works for non-integer numbers as well.

```javascript
alert( 4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root, that's maths)
alert( 8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

### [Increment/decrement](https://javascript.info/operators#increment-decrement)

* **Increment** `++` increases a variable by 1:

  ```javascript
  let counter = 2;
  counter++;      // works the same as counter = counter + 1, but is shorter
  alert( counter ); // 3
  ```

* **Decrement** `--` decreases a variable by 1:

  ```javascript
  let counter = 2;
  counter--;      // works the same as counter = counter - 1, but is shorter
  alert( counter ); // 1
  ```

{% hint style="warning" %}
Increment/decrement can only be applied to variables. Trying to use it on a value like `5++` will give an error.
{% endhint %}

The operators `++` and `--` can be placed either before or after a variable.

* When the operator goes after the variable, it is in “postfix form”: `counter++`.
* The “prefix form” is when the operator goes before the variable: `++counter`.

Both of these statements do the same thing: increase `counter` by `1`.

* If the result of increment/decrement is not used, there is no difference in which form to use:

  ```javascript
  let counter = 0;
  counter++;
  ++counter;
  alert( counter ); // 2, the lines above did the same
  ```

* If we’d like to increase a value _and_ immediately use the result of the operator, we need the prefix form:

  ```javascript
  let counter = 0;
  alert( ++counter ); // 1
  ```

* If we’d like to increment a value but use its previous value, we need the postfix form:

  ```javascript
  let counter = 0;
  alert( counter++ ); // 0
  ```

{% hint style="info" %}
I**ncrement/decrement among other operators**

The operators `++/--` can be used inside expressions as well. Their precedence is higher than most other arithmetical operations.

For instance:

```javascript
let counter = 1;
alert( 2 * ++counter ); // 4
```

Compare with:

```javascript
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

We advise a style of “one line – one action”:

```javascript
let counter = 1;
alert( 2 * counter );
counter++;
```
{% endhint %}

### [Bitwise operators](https://javascript.info/operators#bitwise-operators)

Bitwise operators treat arguments as 32-bit integer numbers and work on the level of their binary representation.

The list of operators:

* AND \( `&` \)
* OR \( `|` \)
* XOR \( `^` \)
* NOT \( `~` \)
* LEFT SHIFT \( `<<` \)
* RIGHT SHIFT \( `>>` \)
* ZERO-FILL RIGHT SHIFT \( `>>>` \)

### [Modify-in-place](https://javascript.info/operators#modify-in-place)

This notation can be shortened using the operators `+=` and `*=`:

```javascript
let n = 2;
n += 5; // now n = 7 (same as n = n + 5)
n *= 2; // now n = 14 (same as n = n * 2)

alert( n ); // 14
```

Short “modify-and-assign” operators exist for all arithmetical and bitwise operators: `/=`, `-=`, etc.

Such operators have the same precedence as a normal assignment, so they run after most other calculations:

```javascript
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (right part evaluated first, same as n *= 8)
```

### [Comma](https://javascript.info/operators#comma)

 The comma operator allows us to evaluate several expressions, dividing them with a comma `,`. Each of them is evaluated but only the result of the last one is returned.

```javascript
let a = (1 + 2, 3 + 4);

alert( a ); // 7 (the result of 3 + 4)
```

{% hint style="info" %}
**Comma has a very low precedence**

Please note that the comma operator has very low precedence, lower than `=`, so parentheses are important in the example above.

Without them: `a = 1 + 2, 3 + 4` evaluates `+` first, summing the numbers into `a = 3, 7`, then the assignment operator `=` assigns `a = 3`, and the rest is ignored. It’s like `(a = 1 + 2), 3 + 4`.
{% endhint %}

Sometimes, people use it in more complex constructs to put several actions in one line.

For example:

```javascript
                            // three operations in one line
for (a = 1, b = 3, c = a * b; a < 10; a++) {
 ...
}
```

Such tricks are used in many JavaScript frameworks. That’s why we’re mentioning them. But usually they don’t improve code readability so we should think well before using them.

