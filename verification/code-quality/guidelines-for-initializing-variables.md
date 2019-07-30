# Guidelines for initializing variables

* Initialize each variable as it’s declared Initializing variables as they’re declared is an inexpensive form of defensive programming. It’s a good insurance policy against initialization errors.
* Initialize each variable close to where it’s first used
* Use final or const when possible
* Pay special attention to counters and accumulators The variables i, j, k, sum, and total are often counters or accumulators. A common error is forgetting to reset a counter or an accumulator before the next time it’s used.
* Initialize a class’s member data in its constructor
* Check the need for reinitialization Ask yourself whether the variable will ever need to be reinitialized, either because a loop in the routine uses the variable many times or because the variable retains its value between calls to the routine and needs to be reset between calls. If it needs to be reinitialized, make sure that the initialization statement is inside the part of the code that’s repeated.
* Use the compiler setting that automatically initializes all variables
* Take advantage of your compiler’s warning messages
* Check input parameters for validity

