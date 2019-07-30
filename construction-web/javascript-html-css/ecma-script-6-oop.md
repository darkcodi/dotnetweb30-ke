# Ecma script 6: OOP

#### ES6 Class Definition

You’re ready to define your first class in ES6. Let’s create a Vehicle class now.

```text
class Vehicle {
 
}
console.log(typeof Vehicle);
 
// function
```

 After we create our class here, we actually log out the `typeof` `Vehicle` of our class. Wait a minute, it says it’s a function. Why isn’t it a class? Well, this shows that in fact using the `class` keyword does not really give you access to an actual _class type_ in JavaScript. You can almost think of it as an ES5 constructor function with much prettier syntax.

#### Instantiating an Object from an ES6 Class

Now that we have a class, we can now instantiate an object. We do this by making use of the `new` keyword like many other object oriented programming languages. This is how we, “new up” an object.

```text
class Vehicle {
 
}
let vehicle = new Vehicle();
 
console.log(typeof vehicle);  // object
console.log(vehicle instanceof Vehicle);  // true
```

So even though the “class” itself is a function, when we instantiate an object from that class, we do get an actual object. In addition to this, if we test that the `vehicle`is an instance of `Vehicle`, we do get back a `true` statement. This shows us that we can determine the class of an instantiated object by making use of the `instanceof`keyword.

#### Creating an ES6 Method Inside a Class

So far our class is 100% empty. Let’s change that by adding a method to our class.

```text
class Vehicle {
    displayType() {
        console.log('Car');
    }
}
 
let vehicle = new Vehicle();
vehicle.displayType();  // Car
```

Adding a method to an ES6 class is great, because just like you can use a shorthand to declare a function inside an object literal without the function keyword in ES6, you can also use this shorthand syntax when creating a method inside a class. It’s a very nice and clean syntax. In addition, if your editor supports it, you will also see a nice autocomplete feature for your methods once they are declared.

#### Adding a method to a class = Adding a function to the Prototype

Adding a method to a class is like adding a function to the prototype object. This just further shows that setting up a constructor function in ES5 and adding functions to the prototype is still happening behind the scenes in ES6. The class keyword just makes things much easier for us. Observe this example code to see this idea in action.

```text
class Vehicle {
    displayType() {
        console.log('Car');
    }
}
 
let vehicle = new Vehicle();
console.log(vehicle.displayType === Vehicle.prototype.displayType);
 
// true
```

#### ES6 Constructor Function

Constructors are a key concept of classes in any object oriented language. ES6 now has support for creating a constructor function inside your class. As a quick review, the concept of a constructor function in general is that of a function which _automatically runs_ anytime an object is instantiated from that class. This is commonly used to set up some default data or initialize needed variables. We’ll add a constructor to our Vehicle class right here.

```text
class Vehicle {
    constructor() {
        console.log('Running Automatically')
    }
 
    displayType() {
        console.log('Car');
    }
}
 
let vehicle = new Vehicle();
 
// Running Automatically
```

 When we inspect the console, we see _Running Automatically_. notice all we did was new up an object. We never actually call the constructor itself since it is automatic. Note there is no comma after the closing curly brace of the constructor. Since we are used to working with object literals where every key value pair is separated by a comma, you might be tempted to add one between methods in a class. Don’t do it! You’ll throw an unexpected token error if you do.

#### Assigning a class to a variable

You may be familiar with assigning functions to variables and passing them around as first class citizens. You can do the same type of thing with a class in ES6. Let’s see how that works.

```text
let somevariable = class Vehicle {
    constructor() {
        console.log('Running Automatically')
    }
 
    displayType() {
        console.log('Car');
    }
}
 
new somevariable();
 
// Running Automatically
```

#### Inheritance with extends and super in ES6

Let’s now create a class that inherits from another class. To do this, we make use of the `extends` keyword just like other object oriented languages. This allows the child class to inherit all of the behavior of the parent class. We can extend our Vehicle class by building a Tesla class to test out the functionality of **extends**.

```text
class Vehicle {
    constructor() {
        console.log('Start me up');
    }
}
 
class Tesla extends Vehicle {
}
 
let model3 = new Tesla();
 
// Start me up
```

Notice that the Tesla class is 100% empty, there is nothing between the curly braces. When we run the code however, we get the message from the constructor of the parent class of Vehicle. So even though Tesla has no constructor or methods in it, it does extend Vehicle which does have a constructor. In ES6 when working with classes, that constructor does get called when the child class is instantiated. Let’s see another example of this, but this time we will pass in an argument to the constructor in the parent class.

```text
class Vehicle {
    constructor(color) {
        console.log(`The car is ${color}`);
    }
}
 
class Tesla extends Vehicle {
}
 
let model3 = new Tesla('Blue');
 
// The car is Blue
```

#### Calling a Parent Constructor with super\(\)

What happens if a parent has a constructor, and the child class also has a constructor? In this case you make use of the `super();` language construct. Let’s see an example here.

```text
class Vehicle {
    constructor() {
        console.log('The Base Vehicle.');
    }
}
 
class Tesla extends Vehicle {
    constructor() {
        super();
        console.log('The Tesla Vehicle.')
    }
}
 
let model3 = new Tesla();
 
// The Base Vehicle.
// The Tesla Vehicle.
```

 By calling **super\(\)** in the Tesla child class, the JavaScript engine knows that it should instantiate the parent class of Vehicle and call it’s constructor. This is why we see the output of both classes in the console. In fact, if the child class has a constructor, you _must_ call `super()` in the child constructor. If you do not, you will get an error of “Derived constructor must call super\(\)”.

#### ES6 Method Override

When you extend a class, all methods and properties get passed down to the child instance. What about a situation where you want to apply different behavior to a method that gets inherited? This is pretty easy. All you need to do is redefine the method in the child class with the behavior you would like. Here is an example.

```text
class Vehicle {
    getPropulsion() {
        return 'Gas Powered';
    }
}
 
class Tesla extends Vehicle {
    getPropulsion() {
        return 'Electric Powered';
    }
}
 
let model3 = new Tesla();
 
let poweredby = model3.getPropulsion();
console.log(poweredby);
 
// Electric Powered
```

Even though the prototype gets overridden here, you do not need to specify any special type of syntax to do so. Just re create the method in question in the child class, and it will just work.

#### Calling super\(\) in a method

We learned that if the child class has a constructor we must call super\(\). In addition to this, you can also make use of a call to super\(\) in a method of the child class. Let’s see an example of calling super\(\) in a method here.

```text
class Vehicle {
    getPropulsion() {
        return 'Gas Powered';
    }
}
 
class Tesla extends Vehicle {
    getPropulsion() {
        return 'Hybrid is ' + super.getPropulsion() + ' and Electric Powered';
    }
}
 
let model3 = new Tesla();
 
let poweredby = model3.getPropulsion();
console.log(poweredby);
 
// Hybrid is Gas Powered and Electric Powered

```

 By calling `super.getPropulsion()`, the JavaScript engine will look up the prototype chaine for a `getPropulsion()` method, and locates it in the Vehicle class \(or constructor function\). We can achieve a similar result using Object Literals in combination with the Object.setPrototypeOf\(\) method. The example would translate to this code you see here.

```text
let vehicle = {
    getPropulsion() {
        return 'Gas Powered';
    }
};
 
let Tesla = {
    getPropulsion() {
        return 'Hybrid is ' + super.getPropulsion() + ' and Electric Powered';
    }
};
 
Object.setPrototypeOf(Tesla, vehicle);
 
let poweredby = Tesla.getPropulsion();
console.log(poweredby);
 
// Hybrid is Gas Powered and Electric Powered
```

#### Properties for Class Instances

So far we have covered a good deal of information about using the class keyword in ES6, but we haven’t yet touched on using properties. Let’s investigate them now. We’ll set up some example code then discuss how it works.

```text
class Vehicle {
    constructor() {
        this.kindof = 'Car';
    }
}
 
class Tesla extends Vehicle {
    constructor() {
        super();
    }
}
 
let car = new Tesla();
console.log(car.kindof);
 
// Car
```

Here we have a class of `Vehicle`, and in the constructor we are setting `this.kindof`to a simple string value of ‘Car’. The constructor method in `Vehicle` is very much like the way you would specify a constructor function in ES5 which you would “new up”. Many times you would accept values and set them via the `this` keyword when working like this.

Next we have our `Tesla` class which extends `Vehicle`. All we do in this class is to define a constructor which calls `super()`.

Finally, we new up a new instance of `Tesla` and assign it to `car`. We then log out `car.kindof` and find the result of ‘Car’. The takeaway is that we initialize values in the constructor using the `this` keyword as we did in ES5.

**Accessing this across constructors**

In the following example, we show how you can access properties held in the `this`object across constructors. You’ll see we again make use of `this.kindof` in the constructor of the `Vehicle` class. We also access `this.kindof` in the constructor of the child class of `Tesla`. We take this opportunity to mutate the value held in `this.kindof` and we can see the results when we log out the value. As always, make sure to call `super()` in the constructor of the child class.

```text
class Vehicle {
    constructor() {
        this.kindof = 'Car';
    }
}
 
class Tesla extends Vehicle {
    constructor() {
        super();
        this.kindof = 'Electric ' + this.kindof;
    }
}
 
let car = new Tesla();
console.log(car.kindof);
 
// Elcectric Car
```

#### Static Methods and Properties in ES6

First we will look at an example of a static method. Notice the method declaration of getDefaultEngine\(\) is prefixed with the `static` keyword. If you are familiar with the general concepts of object oriented programming, you know that if a method is static, you can call it right from the class without having to create an instance of the class first. That is exactly what we do here. We call getDefaultEngine\(\) right from the Vehicle class with no need of the `new` keyword. By declaring a method as static, the method gets attached directly to `Vehicle`.

```text
class Vehicle {
    static getDefaultEngine() {
        return 'Gas';
    }
}
let engine = Vehicle.getDefaultEngine();
console.log(engine);
 
// Gas
```

**No static keyword for class properties**

As it turns out, in ES6 you can apply the static keyword to methods but you can not do the same for properties. If you want to set a static property on a class in ES6, it actually works like it did in ES5. Here is an example of pseudo static property in ES6.

```text
class Vehicle {
 
}
Vehicle.color = 'Red';
console.log(Vehicle.color);
 
// Red
```

#### ES6 Getters and Setters

In ES6 during your method definitions inside of a class, you can set up getter and setter methods quite easily. All you need to do is prefix the method you want to be a getter with the keyword of `get`. Conversely, if you need to set up a setter method, you would prefix with the `set` keyword. In this example of getters and setters below, we set up a class of Square. By using the keywords of get and set, we give ourselves the ability to retrieve the height or area of a square by simply typing `square.height` or `square.area`. To set a new height for the square, we simply do something like `square.height = 25;`

#### Classes as first class citizens

In ES6, classes are first class citizens. In other words, they can be passed around in your scripts just like you would pass variables, objects, and functions. Let’s see how it works.

```text
lass Vehicle {
    constructor() {
        console.log('moving forward');
    }
}
 
function move() {
    console.log('finished moving');
}
 
move(new Vehicle());
 
// moving forward
// finished moving
```

