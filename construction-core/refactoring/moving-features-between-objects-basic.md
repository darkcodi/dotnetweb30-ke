# Moving Features Between Objects \(basic\)

### Move Method

Moving methods is the bread and butter of refactoring. By moving methods around, I can make the classes simpler and they end up being a more crisp implementation of a set of responsibilities.

If I am not sure whether to move a method, I go on to look at other methods. Moving other methods often makes the decision easier. Sometimes the decision still is hard to make. Actually it is then no big deal. If it is difficult to make the decision, it probably does not matter that much. Then I choose according to instinct; after all, I can always change it again later.

#### Mechanics

* Examine all features used by the source method that are defined on the source class. Consider whether they also should be moved.
* Check the sub- and superclasses of the source class for other declarations of the method.
* Declare the method in the target class.
* Copy the code from the source method to the target. Adjust the method to make it work in its new home.
* Compile the target class.
* Determine how to reference the correct target object from the source.
* Turn the source method into a delegating method.
* Compile and test.
* Decide whether to remove the source method or retain it as a delegating method.
* If you remove the source method, replace all the references with references to the target method.
* Compile and test.

### Move Field

Moving state and behavior between classes is the very essence of refactoring. As the system develops, you find the need for new classes and the need to shuffle responsibilities around. A design decision that is reasonable and correct one week can become incorrect in another. 

I consider moving a field if I see more methods on another class using the field than the class itself. This usage may be indirect, through getting and setting methods. I may choose to move the methods; this decision based on interface. But if the methods seem sensible where they are, I move the field. 

Another reason for field moving is when doing **Extract Class**. In that case the fields go first and then the methods.

#### Mechanics

* If the field is public, use **Encapsulate Field**.
* Compile and test.
* Create a field in the target class with getting and setting methods.
* Compile the target class.
* Determine how to reference the target object from the source.
* Remove the field on the source class.
* Replace all references to the source field with references to the appropriate method on the target.
* Compile and test.





