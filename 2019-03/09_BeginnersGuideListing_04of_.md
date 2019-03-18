---
title: Where do I start? Part 4: JavaScript OOP, Context and Class
published: false
description: A short blog with some list of links and guides for folks starting out.
tags: beginners, webdev, JavaScript
---

# Where do I start? Part 4: JavaScript Object-Oriented Programming, Context and Class
## Didn't you just write something about this last week?
No, I made a listing of resources for **JavaScript** without the trickiness of its implementation of **Object-Oriented Programming** included. Some of the resources cover it but not extensively, except for in the case of the Free Code Camp one I believe.
## What are we gonna learn about this time?
### Object-Oriented Programming
Yeah, I know I keep saying it but let's cover some vocab first. Last time, I mentioned **Objects** as being a data type but I didn't really address the difference between an object and the other data types, or primitives. In JavaScript, everything is an object and that leads to some interesting problems. Namely binding.
### Primitives
A primitive is an immutable or unchangeable data type that has no methods that mutate the primitive itself. Current year JavaScript has 6 kinds of primitives:
- strings
     - "hello"
- numbers
     - 123.456, 1, -12
- booleans
     - true, false
- null
     - null pointer reference, a reference that points to nothing 
- undefined
     - default primitive value assigned to a variable when it's not defined
- symbols
     - I could write a blog about these, I probably will. For now, they are used as dynamically produced distinct anonymous values. It's okay if you don't get it. 

There are sub-categories like integers and such but that's not that important at the moment.
#### If primitives are immutable, how come I can do this?
```JavaScript
     let greeting = "hello";
     greeting += " and goodbye"; // greeting equals "hello and goodbye" now
```
In this snippet, you're not actually changing the string primitive "hello" into "hello and goodbye" you're changing the **assigned** value the variable _greeting_ has.

### What makes Objects so special?
Objects are typically used to group together related information. Be they values, functions, or otherwise. It's a data structure. Often objects are used to create abstractions of real-world things and concepts like shoes or dates. You may also hear words like dictionaries or hashes thrown around. These are all objects. The important through-line is that they all have key-value pairs.
#### Key-Value pairs     
Yes, key-value pairs. Objects have attributes that have different values and the keys are used to access the value whatever it may be in relation to the object. Ergo the name key-value pair. For example:

```javascript
     // initializing a shoe object
     const shoe = {};
     // it's looking lonely let's give it a type or something
     shoe.type = "sneakers";
     // what's it made of ?
     shoe.materials = ["nubuck", "rubber", "EVA"];     
     // and you can nest objects inside of objects indefinitely, you might not want to nest them too deeply
     shoe.company = {
          name: "Anon shoe Corp",
          address: "123 None of your business Ave."
     }
     // and who makes them
     shoe['getCompany'] = function() {
          return this.company.name;
     }

     console.log(shoe.type); // prints out "sneakers"
     console.log(shoe['materials']); //prints out ["nubuck", "rubber", "EVA"];
```
I'm swapping on purpose between the object.key and the object["key"] notations. They mean the same thing but have different uses. If you are iterating through an object with a for-in loop you had better use the square bracket object['key'] notation inside the loop, but you won't need the quotes because for-in supplies you with the key as a string. Bracket notation uses the literal key as a string to access the value. On the other hand, if you know the name of the key and it isn't something like, "I have spaces", you can assign or access its value with dot notation.

### You said something about context, right?
Yes, but first I'll show you some code and explain as we go.
```javascript
     function greetings (greeting) {
          // the this keyword refers to the object that the function resides inside or its context
          return greeting +" "+ this.name;
     }
     console.log(greetings("Hello")); // "Hello undefined"

     const James = {
          name: "James Walker"
     }

     console.log(greetings.call(James, "Hello")); // "Hello James Walker"
```
The **this** keyword refers to the context the function is being invoked in. By context, I mean where the function resides or what it's bound to when called/executed. On the first invocation of greetings we get "Hello undefined" because the context of this first invocation is global. There is no value assigned to this name property globally so by default it's undefined. After we make another object that can provide context, we bind the function to that object to give it a defined execution context. **Call** is one of three special methods that explicitly bind the greetings function to the James object which provides it context for the name property. So when it's invoked in that context, it returns "Hello James Walker". The first argument is always the invocation context followed by the remaining arguments that need to be passed. In other words **this** in that execution context is the James object so _this.name_ on the second invocation is basically _James.name_.


### That's nice and all, but what if I want to write a piece of code that makes the objects instead of coding each one by hand?
We used to use classes for everything and there are cases where we still do but I'll show you this and then tell you why it's to be used sparingly. There's a famous example called the Gorilla Banana Problem.

```javascript
     // old-school ES5
     // creates an object with a constructor function
     function Vehicle(make, model, year) {
          this.make = make;
          this.model = model;
          this.year = year;
     }

     // The prototype refers to an object inside of vehicle, all objects have a prototype object inside and it's used to pass down attributes or make new ones
     // we then create another attribute with the key of getInfo and its value is a function that prints out information about the Object.
     Vehicle.prototype.getInfo = function() {
          console.log("This is a ", this.year, " ", this.make, " ", this.model);
     }

     // Bicycle subclass, Vehicle being the superclass or parent
     function Bicycle(make, model, year, speed) {
          // using call redefines the execution context to the Bicycle object, not the original Vehicle constructor
          Vehicle.call(this, make, model, year);
          this.speed = speed;
     }

     // es6 style
     // much closer to traditional OOP languages in the "new" es6 syntax
     class Vehicle {
          constructor(make, model, year) {
               this.make = make;
               this.model = model;
               this.year = year;
          }
          
          getInfo() {
               console.log("This is a ", this.year, " ", this.make, " ", this.model);
          }
     }

     // let's make a subclass
     class Bicycle extends Vehicle {
          constructor(make, model, year, speed) { 
               // super is used to pass arguments to the class Bicycle is derived from
               super(make, model, year);
               this.speed = speed;
          }
     }

     const bike = new Bicycle("BMX", "Stormbringer", 1999, 5);
     bike.getInfo(); // logs "This is a 1999 BMX Stormbringer"
```
Prototypes are objects that exist inside of all other objects as a sort of kernel. This kernel is where all your properties and functions reside. The prototype may also contain another prototype that it inherits functions and properties from ad infinitum. The access derived or sub-classes have is referred to as **inheritance** which is provided by the **prototype chain**. Prototype chain is just a reference to how all classes inherit from all the prototypes of their previous ancestors forming a chain or prototypal inheritance.

The second, ES6 version is written in a fashion anyone with some OOP language experience can recognize. This was part of the reason this syntax was implemented. It makes it easier for JavaScript folks to get to grips with OOP coding and it gives folks who don't know it so well a foothold if they already know an OOP language or two. Plus explaining what prototypes are and the **this** keyword means can get confusing. ES6 has made great progress in simplifying JavaScript syntax as a whole.

Long story short, prototypal inheritance was a necessary evil and even with the new conventions, it's still there beneath the surface. That being said, OOP is still prone to certain problems and is by no means a panacea. I will address these issues next time as well as some solutions and more resources.

### Parting words
Next time, I'll bring you some more resources and as always I am not infallible, please comment, critique, and reach out. I am just starting my career and would love to get better and provide more value to my fellow comrades-in-keyboards.

### Resource links
- **Videos**
     - Traversy Media
          - [JavaScript OOP Crash Course - 40 mins](https://www.youtube.com/watch?v=vDJpGenyHaA)
     - Programming with Mosh
          - [Object-Oriented Programming in JavaScript - 1hr](https://www.youtube.com/watch?v=PFmuCDHHpwk)
     - Academind
          - [Reference vs. Primitive Values/ types - 21 mins](https://www.youtube.com/watch?v=9ooYYRLdg_g)
- **Sites/ Reading Material**
     - MDN
          - [Object Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics)
          - [Object Prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
          - [Inheritance and Prototypes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
          
     - W3Schools
          - [JavaScript Objects](https://www.w3schools.com/js/js_object_definition.asp)
          - [This keyword](https://www.w3schools.com/js/js_this.asp)
          - [Object Prototypes](https://www.w3schools.com/js/js_object_prototypes.asp)