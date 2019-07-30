# JavaScript: Control and Loop constructions

The control structures within JavaScript allow the program flow to change within a unit of code or function. These statements can determine whether or not given statements are executed, as well as repeated execution of a block of code.

Most of the statements enlisted below are so-called conditional statements that can operate either on a statement or a block of code enclosed with braces \({ and }\). The same structures utilize Booleans to determine whether or not a block gets executed, where any defined variable that is neither zero nor an empty string is treated as true.

### if

The if statement is straightforward — if the given expression is true, the statement or statements will be executed. Otherwise, they are skipped.

```javascript
if (a === b) {
  document.body.innerHTML += "a equals b";
}
```

The if statement may also consist of multiple parts, incorporating else and else if sections. These keywords are part of the if statement, and identify the code blocks that are executed, if the preceding condition is false.

```javascript
if (a === b) {
  document.body.innerHTML += "a equals b";
} else if (a === c) {
  document.body.innerHTML += "a equals c";
} else {
  document.body.innerHTML += "a does not equal either b or c";
}
```

### while

The syntax of the while statement is very much like the syntax for the if statement:

```javascript
while(this condition is true) {
    carry out these statements ...
}
```

### do ... while

The do ... while structure is similar in operation to while, but with one important difference. Here’s the syntax:

```javascript
do {
    ... these statements ...
} while(this condition is true)
```

The only real difference here is that, since the while clause appears _after_ the braces, the list of conditional statements is executed once _before_ the while clause is evaluated. The statements in a do ... while clause will therefore always be executed at least once.

### for

The for loop is another loop similar in operation to while, but with a more comprehensive syntax. With the for loop, you can specify an initial condition, a test condition \(to end the loop\), and a means of changing a counter variable for each pass through the loop, all in one statement. Have a look at the syntax:

```javascript
for(x=0; x<10; x++) {
    ... execute these statements ...
}
```

You can interpret this as follows:

* For x initially set to zero, and while x is less than 10, and incrementing x by 1 on each pass through the loop, carry out the conditional statements.

### Looping Through Objects with for ... in

The for ... in loop is a special sort of loop intended for stepping through the properties of an object. 

```javascript
var days = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
        var message = "";
        for (i in days) {
            message += 'Day ' + i + ' is ' + days[i] + '\n';
        }
        alert(message);
```

### Leaving a Loop with break

The break command works within a loop pretty much as it does in a switch statement: it kicks you out of the loop and returns operation to the line of code immediately after the closing brace.

Here’s an example:

```javascript
var count = 10;
var sum = 0;
while(count > 0) {
    sum = sum + count;
    if(sum > 42) break;
    count--;
}
alert(sum);
```



