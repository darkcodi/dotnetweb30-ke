# Organizing Data \(basic\)

### Encapsulate Field

If I move data around, I have to change all the references to the data in a single cycle to keep the code working. For data with a very small scope of access, such as a temporary variable in a small function, this isn’t a problem. But as the scope grows, so does the difficulty, which is why global data is such a pain.

So if I want to move widely accessed data, often the best approach is to first encapsulate it by routing all its access through functions. That way, I turn the difficult task of reorganizing data into the simpler task of reorganizing functions.

Encapsulating data is valuable for other things too. It provides a clear point to monitor changes and use of the data; I can easily add validation or consequential logic on the updates. It is my habit to make all mutable data encapsulated like this and only accessed through functions if its scope is greater than a single function. The greater the scope of the data, the more important it is to encapsulate. My approach with legacy code is that whenever I need to change or add a new reference to such a variable, I should take the opportunity to encapsulate it. That way I prevent the increase of coupling to commonly used data.

Keeping data encapsulated is much less important for immutable data. When the data doesn’t change, I don’t need a place to put in validation or other logic hooks before updates. I can also freely copy the data rather than move it—so I don’t have to change references from old locations, nor do I worry about sections of code getting stale data. Immutability is a powerful preservative.

#### Mechanics

* Create encapsulating functions to access and update the variable.
* Run static checks.
* For each reference to the variable, replace with a call to the appropriate encapsulating function. Test after each replacement.
* Restrict the visibility of the variable
* Test
* If the value of the variable is a record, consider **Encapsulate Record**

### Encapsulate Collection

Access to a collection variable may be encapsulated, but if the getter returns the collection itself, then that collection’s membership can be altered without the enclosing class being able to intervene.

To avoid this, I provide collection modifier methods — usually **add** and **remove~** —on the class itself. This way, changes to the collection go through the owning class, giving me the opportunity to modify such changes as the program evolves.

#### Mechanics

* Apply Encapsulate Variable \(132\) if the reference to the collection isn’t already encapsulated
* Add functions to add and remove elements from the collection
* If there is a setter for the collection, use **Remove Setting Method** if possible. If not, make it take a copy of the provided collection
* Run static checks
* Find all references to the collection. If anyone calls modifiers on the collection, change them to use the new add/remove functions. Test after each change
* Modify the getter for the collection to return a protected view on it, using a readonly proxy or a copy
* Test

