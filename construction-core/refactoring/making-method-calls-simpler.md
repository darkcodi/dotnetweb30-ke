# Making Method Calls Simpler

If you understand what a program is doing, you should not be afraid to use **Rename Method** to pass on that knowledge. You can \(and should\) also rename variables and classes. On the whole these renamings are fairly simple text replacements, so I haven't added extra refactorings for them. 

Parameters themselves have quite a role to play with interfaces. **Add Parameter** and **Remove Parameter** are common refactorings. Programmers new to objects often use long parameter lists, which are typical of other development environments. Objects allow you to keep parameter lists short, and several more involved refactorings give you ways to shorten them. 

If you are passing several values from an object, use **Preserve Whole Object** to reduce all the values to a single object. If this object does not exist, you can create it with **Introduce Parameter Object**. 

If you can get the data from an object to which the method already has access, you can eliminate parameters with **Replace Parameter with Method**. If you have parameters that are used to determine conditional behavior, you can use **Replace Parameter with Explicit Methods**. You can combine several similar methods by adding a parameter with **Parameterize Method**. 

One of the most valuable conventions I've used over the years is to clearly separate methods that change state \(modifiers\) from those that query state \(queries\). I don't know how many times I've got myself into trouble, or seen others get into trouble, by mixing these up. So whenever I see them combined, I use **Separate Query from Modifier** to get rid of them. 

Good interfaces show only what they have to and no more. You can improve an interface by hiding things. Of course all data should be hidden \(I hope I don't need to tell you to do that\), but also any methods that can should be hidden. When refactoring you often need to make things visible for a while and then cover them up with **Hide Method** and **Remove Setting Method**. 

Constructors are a particularly awkward feature of Java and C++, because they force you to know the class of an object you need to create. Often you don't need to know this. The need to know can be removed with **Replace Constructor with Factory Method**. 

Casting is another bane of the Java programmer's life. As much as possible try to avoid making the user of a class do downcasting if you can contain it elsewhere by using **Encapsulate Downcast**. 

Exception-handling mechanism makes error handling easier. Programmers who are not used to this often use error codes to signal trouble. You can use **Replace Error Code with Exception** to use the new exceptional features. But sometimes exceptions aren't the right answer; you should test first with **Replace Exception with Test**.

