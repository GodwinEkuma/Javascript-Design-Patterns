
 
# Writing Maintainable and Readable Javascript: Design Patterns 
 

Design patterns are reusable solutions to commonly occurring problems in software design. - Wikipedia 

Reusing design patterns can speed up the software development process by providing us with tested and proven solutions to common development problems while ensuring that we write readable, reusable and maintainable codes 

Over the lifespan of Javascript, many design patterns have been made and tested by a large number of developers using javascript. In this article, we would explain the common design patterns used by javascript developers. 

Design patterns can be categorized into creational patterns, structural patterns, and behavioral patterns 

## Creational Pattern 

Creational patterns focus on optimizing new object creation so as to suit the situation we are working it. The basic method for object creation might add some design complexities so these patterns help to remove such complexities. 

Some of the patterns which under this category are: 
- Constructor pattern 
- Module pattern 
- Singleton pattern 
- Factory pattern 
- Prototype pattern 
 
## Structural Pattern 
Structural patterns are concerned with how objects are made up and simplify relationships between different objects. These patterns ensure that objects are structured in a manner that when one part of the system changes, the entire structure of the system doesn't need to do the same. 
Patterns that belong to this category are: 
 - Decorator 
- Facade 
- Flyweight 
 
## Behavioural Pattern 
Behavioral design patterns are concerned with the assignment of responsibilities between objects and how objects communicate. 
Some behavioral patterns include: 
- Mediator 
- Observer 
- Command. 
 
#### Note: Most of the examples used in this article are based on ES6 
 
### Constructor Pattern 
Constructors are functions used to create a new instance of an object - both preparing the object for use and accepting arguments which the constructor can use to set the values of member properties and methods when the object is first created. 
 
 

``` 
class Car { 
	constructor(model, year, miles){ 
	this.model = model; 
	this.year = year; 
	this.miles = miles 
	} 
	toString(){ 
	return this.model + " has done " + this.miles + " miles"; 
	} 
} 
// Usage: 
 
let civic = new Car( "Honda Civic", 2009, 20000 ); 
let mondeo = new Car( "Ford Mondeo", 2010, 5000 ); 
 
console.log( civic.toString() ); 
console.log( mondeo.toString() ); 
``` 
 
 

### Proptotype Pattern 
The prototype pattern is based on prototypal inheritance. We create objects which act as prototypes for other objects. The prototype object itself is effectively used as a blueprint for creating other objects 
``` 
class Animal { 
	 
	constructor(name) { 
	this.speed = 0; 
	this.name = name; 
	} 
	 
	run(speed) { 
	this.speed += speed; 
	alert(`${this.name} runs with speed ${this.speed}.`); 
	} 
	 
	stop() { 
	this.speed = 0; 
	alert(`${this.name} stopped.`); 
	} 
} 
 
// Inherit from Animal 
class Rabbit extends Animal { 
	hide() { 
	alert(`${this.name} hides!`); 
	} 
} 

let rabbit = new Rabbit("White Rabbit"); 
rabbit.run(5); // White Rabbit runs with speed 5. 
rabbit.hide(); // White Rabbit hides! 
``` 
 

### Module Pattern 

A module is a group of small independent components that we can reuse in our application. A component can be a function, class or even a variable. The module pattern helps us encapsulate private components and only return public APIs that have access to the private components. 

In ES6 the export/import mechanism is used to implement modularity. The export keyword is used when we want to make a component accessible somewhere, and the import is used to access what export has made available. 
 
```
// car.js 
class Car { 
	constructor(model, year, miles){ 
	this.model = model; 
	this.year = year; 
	this.miles = miles 
	} 
	toString(){ 
	return this.model + " has done " + this.miles + " miles"; 
	} 
} 
export default Car 
 
 
// Usage: 
// main.js 
import Car from './car.js' 
let civic = new Car( "Honda Civic", 2009, 20000 ); 
let mondeo = new Car( "Ford Mondeo", 2010, 5000 ); 
 
console.log( civic.toString() ); 
console.log( mondeo.toString() ); 
```
To use ES6 Modules you may to "use strict" on a browser and set "--experimental-modules" flag on nodejs. You can also use transpilers or module bundlers to transpile to ES5 version to make them compatible with modern browsers and stable versions of Nodejs. 
 
 

### Singleton Pattern 
The singleton pattern is a pattern used to restrict an object to a single instance. A singleton creates an instance of an object if that object does not exist. If it exists it returns the existing instance. 
```
class Car { 
	constructor(model, year, miles){ 
		if(Car.exists){ 
		return Car.instance 
		} 
		this.model = model; 
		this.year = year; 
		this.miles = miles; 
		Car.exists = true; 
		Car.instance = this; 
		return this 
	} 
	toString(){ 
		return this.model + " has done " + this.miles + " miles"; 
	} 
} 
// Usage: 
 
let civic = new Car( "Honda Civic", 2009, 20000 ); 
let mondeo = new Car( "Ford Mondeo", 2010, 5000 ); 
 
console.log( civic.toString() ); // Honda Civic has done 20000 miles 
console.log( mondeo.toString() ); // Honda Civic has done 20000 miles 
``` 

### Factory Pattern 

The factory pattern abstracts object creation by providing an interface, where we can specify the type of factory object to be created. 

The Factory pattern can be especially useful when applied to the following situations: 

- When our object or component setup involves a high level of complexity, e.g. if it strongly depends on dynamic factors or application configuration. 
- When we need to easily generate different instances of objects depending on the environment we are in 
- When we're working with many small objects or components that share the same properties 
- When composing objects with instances of other objects that need only satisfy an API contract (aka, duck typing) to work. This is useful for decoupling.

``` 

// A class for defining new cars
class Car {
 constructor(doors, state, color) {
 this.doors = doors || 4;
 this.state = state || "brand new";
 this.color = color || "silver";
 }

 props(){
 return `I am a ${this.state} ${this.color} car and I have ${this.doors} doors`
 }
}

// A class for defining new trucks
class Truck {
 constructor(state, wheelSize, color) {
 this.state = state || "used";
 this.wheelSize = wheelSize || "large";
 this.color = color || "blue";
 }

 props(){
 return `I am a ${this.state} ${this.color} truck and I have a ${this.wheelSize} wheels`
 }
}

// Define a factory

class VehicleFactory {
 constructor(options) {
 
 let vehicle;
 switch (options.type) {
 case "car":
 vehicle = new Car(options.doors, options.state, options.color)
 break;
 case "truck":
 vehicle = new Truck(options.state, options.wheelSize, options.color);
 break;
 }
 return vehicle;
 }
 
}

// Usage

let options1 = {
 type: "car",
 color: "yellow",
 doors: 6
}
let options2 = {
 type: "truck",
 state: "like new",
 color: "red",
 wheelSize: "small"
}

let car = new VehicleFactory(options1);
let truck = new VehicleFactory(options2);

console.log(car.state) // brand new
console.log(car.color) // yellow
console.log(car.props()) // I am a brand new yellow car and I have 6 doors
console.log(truck.state) // used
console.log(truck.color)// red
console.log(truck.props())// I am a used red truck and I have a small wheels
```

### Facade Pattern
The Facade pattern simplifies and hides the underlying complexity of a large abody of code by providing a cleaner and easy to use interface.

``` 
class TaskService {
 constructor(data){
 this.name = data.name;
 this.priority = data.priority;
 this.project = data.project;
 this.user = data.user;
 this.completed = data.completed;
 }

 complete() {
 this.completed = true;
 console.log('completing task: ' + this.name);
 }

 setCompleteDate() {
 this.completedDate = new Date();
 console.log(this.name + ' completed on ' + this.completedDate);
 }

 notifyCompletion() {
 console.log('Notifying ' + this.user + ' of the completion of ' + this.name);
 }
 save () {
 console.log('saving Task: ' + this.name);
 }
}

class TaskServiceFacade extends TaskService{
 constructor(data){
 super(data)
 }
 completeAndNotify(){
 this.complete();
 this.setCompleteDate();
 this.notifyCompletion();
 this.save();
 }
}

let mytask = new TaskServiceFacade({
 name: 'MyTask',
 priority: 1,
 project: 'Courses',
 user: 'Jon',
 completed: false
})
console.log(mytask.completeAndNotify())
// completing task: MyTask

// MyTask completed on Sun Jan 06 2019 09:54:33 GMT+0100 (West Africa Standard Time)

// Notifying Jon of the completion of MyTask

// saving Task: MyTask
```

### Decorator Pattern
The decorator pattern is a structural pattern that focuses on adding new functionality to a class. The idea was that the decoration_itself wasn't essential to the base functionality of the class, otherwise, it would be baked into the superclass itself. 
```
// The constructor to decorate
class MacBook {
 
  cost () {
    return 997;
  };
  screenSize () { 
    return 11.6; 
  };
 
}
 
// Decorator 1
function macbookDecorator(macbook){
  macbook.discount = function(){
    return macbook.cost() * 0.1
  }
  return macbook;
}

// Decorator 2
function macbookDecorator2( macbook ) {
 
  var v = macbook.cost();
  macbook.cost = function() {
    return v + 75;
  };
 return macbook;
}

 // usage
const decorator1 = macbookDecorator(new MacBook());

console.log(decorator1.cost()); // 997
console.log(decorator1.discount()); // 99.7

const decorator2 = macbookDecorator2(new MacBook());

console.log(decorator2.cost()); 1072

```

### Conclusion
To design better software it is important to know design patterns as they can be very helpful in solving common problems. But, this is a very vast subject and it is simply not possible to include everything about them in a short article. To dive deeper, I would recommend the following :
- #### [Practical Design Patterns in JavaScript](https://www.pluralsight.com/courses/javascript-practical-design-patterns)
- #### [Learning JavaScript Design Patterns by Addy Osmani](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)
