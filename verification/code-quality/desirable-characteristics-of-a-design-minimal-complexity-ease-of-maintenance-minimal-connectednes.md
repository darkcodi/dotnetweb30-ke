# Desirable characteristics of a design \(minimal complexity, ease of maintenance, minimal connectednes

### Minimal complexity

The primary goal of design should be to minimize complexity. Avoid making “clever” designs. Clever designs are usually hard to understand. Instead make “simple” and “easy-to-understand” designs.

### Ease of maintenance

Ease of maintenance means designing for the maintenance programmer. Continually imagine the questions a maintenance programmer would ask about the code you’re writing.

### Loose coupling

Loose coupling means designing so that you hold connections among different parts of a program to a minimum. Use the principles of good abstractions in class interfaces, encapsulation, and information hiding to design classes with as few interconnections as possible.

### Extensibility

Extensibility means that you can enhance a system without causing violence to the underlying structure. You can change a piece of a system without affecting other pieces.

### Reusability

Reusability means designing the system so that you can reuse pieces of it in other systems.

### High fan-in

High fan-in refers to having a high number of classes that use a given class. High fan-in implies that a system has been designed to make good use of utility classes at the lower levels in the system.

### Low-to-medium fan-out

Low-to-medium fan-out means having a given class use a low-to-medium number of other classes. High fan-out \(more than about seven\) indicates that a class uses a large number of other classes and may therefore be overly complex. Researchers have found that the principle of low fan-out is beneficial whether you’re considering the number of routines called from within a routine or the number of classes used within a class.

### Portability

Portability means designing the system so that you can easily move it to another environment.

### Leanness

Leanness means designing the system so that it has no extra parts. Extra code has to be developed, reviewed, tested, and considered when the other code is modified.

### Stratification

Stratification means trying to keep the levels of decomposition stratified so that you can view the system at any single level and get a consistent view. Design the system so that you can view it at one level without dipping into other levels.

For example, if you’re writing a modern system that has to use a lot of older, poorly designed code, write a layer of the new system that’s responsible for interfacing with the old code. Design the layer so that it hides the poor quality of the old code, presenting a consistent set of services to the newer layers. Then have the rest of the system use those classes rather than the old code.

### Standard techniques

The more a system relies on exotic pieces, the more intimidating it will be for someone trying to understand it the first time. Try to give the whole system a familiar feeling by using standardized, common approaches.

