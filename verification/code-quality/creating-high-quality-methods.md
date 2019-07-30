# Creating high quality methods

Here’s a summary list of the valid reasons for creating a method:

* Reduce complexity
* Introduce an intermediate, understandable abstraction
* Avoid duplicate code
* Support subclassing
* Hide sequences
* Improve portability
* Simplify complicated boolean tests
* Improve performance

In addition, many of the reasons to create a class are also good reasons to create a method:

* Isolate complexity
* Hide implementation details
* Limit effects of changes
* Hide global data
* Make central points of control
* Facilitate reusable code
* Accomplish a specific refactoring

Namings

* Describe everything the method does
* Avoid meaningless, vague, or wishy-washy verbs Some verbs are elastic, stretched to cover just about any meaning. Method names like HandleCalculation\(\), PerformServices\(\), OutputUser\(\), ProcessInput\(\), and DealWithOutput\(\) don’t tell you what the routines do.
* Don’t differentiate method names solely by number
* Use opposites precisely \(add/remove, increment/decrement, open/close\)

Parameters

* Put parameters in input-modify-output order Instead of ordering parameters randomly or alphabetically, list the parameters that are input-only first, input-and-output second, and output-only third.
* If several methods use similar parameters, put the similar parameters in a consistent order
* Use all the parameters
* Put status or error variables last
* Don’t use method parameters as working variables
* Limit the number of a routine’s parameters to about seven
* Consider an input, modify, and output naming convention for parameters

