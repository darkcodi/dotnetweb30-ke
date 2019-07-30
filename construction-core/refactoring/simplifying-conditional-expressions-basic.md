# Simplifying Conditional Expressions \(basic\)

### Decompose Conditional Expression

One of the most common sources of complexity in a program is complex conditional logic. As I write code to do various things depending on various conditions, I can quickly end up with a pretty long function. Length of a function is in itself a factor that makes it harder to read, but conditions increase the difficulty. The problem usually lies in the fact that the code, both in the condition checks and in the actions, tells me what happens but can easily obscure why it happens.

As with any large block of code, I can make my intention clearer by decomposing it and replacing each chunk of code with a function call named after the intention of that chunk. With conditions, I particularly like doing this for the conditional part and each of the alternatives. This way, I highlight the condition and make it clear what I’m branching on. I also highlight the reason for the branching.

This is really just a particular case of applying Extract Function to my code, but I like to highlight this case as one where I’ve often found a remarkably good value for the exercise.

#### Mechanics

* Apply **Extract Function** on the condition and each leg of the conditional

### Consolidate Conditional Expression

Sometimes, I run into a series of conditional checks where each check is different yet the resulting action is the same. When I see this, I use and and or operators to consolidate them into a single conditional check with a single result. Consolidating the conditional code is important for two reasons. First, it makes it clearer by showing that I’m really making a single check that combines other checks.

The sequence has the same effect, but it looks like I’m carrying out a sequence of separate checks that just happen to be close together. The second reason I like to do this is that it often sets me up for Extract Function \(106\). Extracting a condition is one of the most useful things I can do to clarify my code. It replaces a statement of what I’m doing with why I’m doing it.

#### Mechanics

* Ensure that none of the conditionals have any side effects
* Take two of the conditional statements and combine their conditions using a logical operator
* Test
* Repeat combining conditionals until they are all in a single condition
* Consider using Extract Function \(106\) on the resulting condition

### Consolidate Duplicate Conditional Fragments

Code is easier to understand when things that are related to each other appear together. If several lines of code access the same data structure, it’s best for them to be together rather than intermingled with code accessing other data structures. At its simplest, I use Slide Statements to keep such code together. A very common case of this is declaring and using variables. Some people like to declare all their variables at the top of a function. I prefer to declare the variable just before I first use it.

Usually, I move related code together as a preparatory step for another refactoring, often an **Extract Function**. Putting related code into a clearly separated function is a better separation than just moving a set of lines together, but I can’t do the **Extract Function** unless the code is together in the first place.

#### Mechanics

* Identify the target position to move the fragment to. Examine statements between source and target to see if there is interference for the candidate fragment. Abandon action if there is any interference
* Cut the fragment from the source and paste into the target position
* Test

### Remove Control Flag

You have a variable that is acting as a control flag for a series of boolean expressions. Use a break or return instead

### Mechanics

* Find the value of the control flag that gets you out of the logic statement. 
* Replace assignments of the break-out value with a break or continue statement. 
* Compile and test after each replacement.

Another approach, also usable in languages without break and continue, is as follows:

* Extract the logic into a method.
* Find the value of the control flag that gets you out of the logic statement.
* Replace assignments of the break-out value with a return.
* Compile and test after each replacement. 

Even in languages with a break or continue, I usually prefer use of an extraction and of a return. The return clearly signals that no more code in the method is executed. If you have that kind of code, you often need to extract that piece anyway. 

Keep an eye on whether the control flag also indicates result information. If it does, you still need the control flag if you use the break, or you can return the value if you have extracted a method.

### Replace Conditional with Polymorphism

A common case for this is where I can form a set of types, each handling the conditional logic differently. I might notice that books, music, and food vary in how they are handled because of their type. This is made most obvious when there are several functions that have a switch statement on a type code. In that case, I remove the duplication of the common switch logic by creating classes for each case and using polymorphism to bring out the typespecific behavior.

Polymorphism is one of the key features of objectoriented programming—and, like any useful feature, it’s prone to overuse. I’ve come across people who argue that all examples of conditional logic should be replaced with polymorphism. I don’t agree with that view. Most of my conditional logic uses basic conditional statements—if/else and switch/case. But when I see complex conditional logic that can be improved as discussed above, I find polymorphism a powerful tool.

#### Mechanics

* If classes do not exist for polymorphic behavior, create them together with a factory function to return the correct instance.
* Use the factory function in calling code.
* Move the conditional function to the superclass.
* If the conditional logic is not a selfcontained function, use **Extract Function** to make it so.
* Pick one of the subclasses. Create a subclass method that overrides the conditional statement method. Copy the body of that leg of the conditional statement into the subclass method and adjust it to fit.
* Repeat for each leg of the conditional.
* Leave a default case for the superclass method. Or, if superclass should be abstract, declare that method as abstract or throw an error to show it should be the responsibility of a subclass.

