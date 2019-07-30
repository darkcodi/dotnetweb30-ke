# Composing Methods \(basic\)

### Extract Method

Extract Function is one of the most common refactorings.

If you have to spend effort looking at a fragment of code and figuring out what it’s doing, then you should extract it into a function and name the function after the “what.” Then, when you read it again, the purpose of the function leaps right out at you, and most of the time you won’t need to care about how the function fulfills its purpose \(which is the body of the function\).

#### Mechanics

* Create a new function, and name it after the intent of the function \(name it by what it does, not by how it does it\).
* Copy the extracted code from the source function into the new target function.
* Scan the extracted code for references to any variables that are local in scope to the source function and will not be in scope for the extracted function. Pass them as parameters.
* Compile after all variables are dealt with.
* Replace the extracted code in the source function with a call to the target function.
* Test.
* Look for other code that’s the same or similar to the code just extracted, and consider using **Replace Inline Code with Function Call** to call the new function.

### Inline Method

 this is inverse of: **Extract Method**

One of the themes of this book is using short functions named to show their intent, because these functions lead to clearer and easier to read code. But sometimes, I do come across a function in which the body is as clear as the name. Or, I refactor the body of the code into something that is just as clear as the name. When this happens, I get rid of the function. Indirection can be helpful, but needless indirection is irritating.

I also use **Inline Function** is when I have a group of functions that seem badly factored. I can inline them all into one big function and then reextract the functions the way I prefer.

I commonly use Inline Function when I see code that’s using too much indirection — when it seems that every function does simple delegation to another function, and I get lost in all the delegation. Some of this indirection may be worthwhile, but not all of it. By inlining, I can flush out the useful ones and eliminate the rest.

#### Mechanics

* Check that this isn’t a polymorphic method
* If this is a method in a class, and has subclasses that override it, then I can’t inline it
* Find all the callers of the function
* Replace each call with the function’s body
* Test after each replacement
* Remove the function definition

### Inline Temp

Variables provide names for expressions within a function, and as such they are usually a Good Thing. But sometimes, the name doesn’t really communicate more than the expression itself. At other times, you may find that a variable gets in the way of refactoring the neighboring code. In these cases, it can be useful to inline the variable.

#### Mechanics

* Check that the righthand side of the assignment is free of side effects
* If the variable isn’t already declared immutable, do so and test
* This checks that it’s only assigned to once
* Find the first reference to the variable and replace it with the righthand side of the assignment
* Test
* Repeat replacing references to the variable until you’ve replaced all of them
* Remove the declaration and assignment of the variable
* Test

### Replace Temp with Query

Using functions instead of variables also allows me to avoid duplicating the calculation logic in similar functions. Whenever I see variables calculated in the same way in different places, I look to turn them into a single function.

Only some temporary variables are suitable for **Replace Temp with Query**. The variable needs to be calculated once and then only be read afterwards. In the simplest case, this means the variable is assigned to once, but it’s also possible to have several assignments in a more complicated lump of code—all of which has to be extracted into the query.

Furthermore, the logic used to calculate the variable must yield the same result when the variable is used later—which rules out variables used as snapshots with names like _oldAddress_.

#### Mechanics

* Check that the variable is determined entirely before it’s used, and the code that calculates it does not yield a different value whenever it is used
* If the variable isn’t readonly, and can be made readonly, do so
* Test
* Extract the assignment of the variable into a function
* Test
* Use **Inline Variable** to remove the temp

### Split Temporary Variable

You have a temporary variable assigned to more than once, but is not a loop variable nor a collecting temporary variable. Make a separate temporary variable for each assignment.

Temporary variables are made for various uses. Some of these uses naturally lead to the temp's being assigned to several times. Loop variables \[Beck\] change for each run around a loop \(such as the i in for \(int i=0; i&lt;10; i++\). Collecting temporary variables \[Beck\] collect together some value that is built up during the method.

Many other temporaries are used to hold the result of a long-winded bit of code for easy reference later. These kinds of variables should be set only once. That they are set more than once is a sign that they have more than one responsibility within the method. Any variable with more than one responsibility should be replaced with a temp for each responsibility. Using a temp for two different things is very confusing for the reader.

#### Mechanics

* Change the name of a temp at its declaration and its first assignment. 
* Declare the new temp as final. 
* Change all references of the temp up to its second assignment. 
* Declare the temp at its second assignment.
* Compile and test. 
* Repeat in stages, each stage renaming at the declaration, and changing references until the next assignment.

