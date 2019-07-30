# Creating high quality classes

### Key points

*  **Good Abstraction** Abstraction is the ability to view a complex operation in a simplified form. A class interface provides an abstraction of the implementation that’s hidden behind the interface. The class’s interface should offer a group of routines that clearly belong together.
* **Provide services in pairs with their opposites** Most operations have corresponding, equal, and opposite operations. If you have an operation that turns a light on, you’ll probably need one to turn it off.
* **Move unrelated information to another class**
* **Make interfaces programmatic rather than semantic when possible**  Each interface consists of a programmatic part and a semantic part. The programmatic part consists of the data types and other attributes of the interface that can be enforced by the compiler. The semantic part of the interface consists of the assumptions about how the interface will be used, which cannot be enforced by the compiler. The semantic interface includes considerations such as “RoutineA must be called before RoutineB” or “RoutineA will crash if dataMember1 isn’t initialized before it’s passed to RoutineA.”
* **Beware of erosion of the interface’s abstraction under modification**  As a class is modified and extended, you often discover additional functionality that’s needed, that doesn’t quite fit with the original class interface, but that seems too hard to implement any other way.
* **Don’t add public members that are inconsistent with the interface abstraction** Each time you add a routine to a class interface, ask “Is this routine consistent with the abstraction provided by the existing interface?” If not, find a different way to make the modification and preserve the integrity of the abstraction.
* **Consider abstraction and cohesion together** Classes with strong cohesion tend to present good abstractions, although that relationship is not as strong.
* **Minimize accessibility of classes and members**
* **Don’t expose member data in public** Exposing member data is a violation of encapsulation and limits your control over the abstraction.
* **Avoid putting private implementation details into a class’s interface**
* **Don’t make assumptions about the class’s users**  A class should be designed and implemented to adhere to the contract implied by the class interface. It shouldn’t make any assumptions about how that interface will or won’t be used, other than what’s documented in the interface.
* **Avoid friend classes**  In a few circumstances such as the State pattern, friend classes can be used in a disciplined way that contributes to managing complexity. But, in general, friend classes violate encapsulation.
* **Don’t put a routine into the public interface just because it uses only public routines**
* **Favor read-time convenience to write-time convenience**  Code is read far more times than it’s written, even during initial development.
* **Move common interfaces, data, and behavior as high as possible in the inheritance tree**
* **Avoid deep inheritance trees**
* **Prefer polymorphism to extensive type checking** Frequently repeated case statements sometimes suggest that inheritance might be a better design choice
* **Make all data private, not protected**  When you inherit from an object, you obtain privileged access to that object’s protected routines and data. If the derived class really needs access to the base class’s attributes, provide protected accessor functions instead.

### Reasons to Create a Class

* Model real-world objects
* Model abstract objects  A good example is the classic Shape object. Circle and Square really exist, but Shape is an abstraction of other specific shapes.
* Reduce complexity  Create a class to hide information so that you won’t need to think about it.
* Isolate complexity  Complexity in all forms—complicated algorithms, large data sets, intricate communications protocols, and so on—is prone to errors. If an error does occur, it will be easier to find if it isn’t spread through the code but is localized within a class.
* Hide implementation details
* Limit effects of changes
* Hide global data  If you need to use global data, you can hide its implementation details behind a class interface.
* Streamline parameter passing  If you’re passing a parameter among several routines, that might indicate a need to factor those routines into a class that share the parameter as object data.
* Make central points of control
* Facilitate reusable code
* Plan for a family of programs  If you expect a program to be modified, it’s a good idea to isolate the parts that you expect to change by putting them into their own classes.
* Package related operations  In cases in which you can’t hide information, share data, or plan for flexibility, you can package sets of operations into classes.
* Accomplish a specific refactoring

### Avoid

* Avoid creating god classes
* Eliminate irrelevant classes  If a class consists only of data but no behavior, ask yourself whether it’s really a class and consider demoting it so that its member data just becomes attributes of one or more other classes.
* Avoid classes named after verbs  A class that has only behavior but no data is generally not really a class. Consider turning a class like DatabaseInitialization\(\) or StringBuilder\(\) into a routine on some other class.

