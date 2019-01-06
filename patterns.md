# Writing Maintianable and Readable Javascript: Design Patterns

  

Design patterns are reusable solutions to commonly occurring problems in software design. - Wikipedia

  

Reusing design patterns can speed up software development process by providing us with tested and proven solutions to common development problems while ensuring that we write readable, reusable and maintainable codes

  

Over the lifespan of Javascript many design patterns has been made and tested by a large number of developers using javascript. In this article we would explain the common design patterns used by javascript developers.  

Design patterns can be categorizied into creational patterns, structural patterns and behavioural patterns

## Creational Pattern
Creational patterns focus on optimizing new object creation so as to suite the situation we are working it. The basic method for object creation migth add some desgin complexities so these patterns help to remove such complexities.

Some of the patterns which under this category are:
 - Constructor pattern
 - Module pattern
 - Singleton pattern
 - Factory pattern
 - Prototype pattern

## Structural Pattern
Structural patterns are concerned with how objects are made up and simplify relationships between different objects. These patterns ensure that objects are structured in a manner that when one part of the system changes, the entire structure of the system doesn't need to do the same.
Patterns that belong to this category are:
-  Decorator
-  Facade
-  Flyweight

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

The  prototype pattern is  based on prototypal inheritance. We create objects which act as prototypes for other objects. The prototype object itself is effectively used as a blueprint for creating other objects

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
A module is a group of small independent components that we can reuse in our application. A component can be a function, class or even a variable. The module pattern helps us enscapsulate private   components and only return public APIs that have access to the private components.

In ES6 the export/import mechanism is used to implement modularity. The export keyword is used when we want to make a component accessible  somewhere, and the import is used to access what export has made available.

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
To use ES6 Modules you may to "use strict"     on a browser and set "--experimental-modules" flag on nodejs. You can also use transpilers or module bundlers to transpile to ES5 version to make them compaactible with modern browsers and stable versions of Nodejs.

### Singleton Pattern
The singleton pattern is a pattern used to restrict an object to a single instance. A sigleton creates an instance of an object if that object does not exist. If it exists it returns the existing instance.
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


