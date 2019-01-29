---
layout: post
title:      "Rock This Way"
date:       2019-01-25 12:08:51 -0500
permalink:  rock_this_way
---

the concept of "this" in JavaScript can be very confusing, one that in practice is fairly abstract, and a lot of the times the code will simply function as intended without a thorough understanding of what is happening behind the scenes.  It is only when things go wrong (or when asked by a tech coach... yikes!)  that it can be difficult to troubleshoot or explain fundamentally what JS is doing and what "this" actually is being referred to.  So, let's break it down:
In JS "this" can simply be defined as the object the method is being called on.  Sounds easy enough right?  Well, it is not hard to overlook some of the technical concepts being used in this statement. 
let’s start off easy.  When defined outside a function "this" will refer to the global object.
```
let x = this
console.log(x)
> window
```
if we ran this in console, we would see the Window object logged.  This shows that outside any of our defined objects when referring to "this" it will refer to the global scope/object.

To further our understanding, we must grasp a couple fundamentals to JS to fully explain "this"; Functions are objects, a method is a value of an object that points to a function, and classes are basically object-creating functions with some quality of life improvements.
Before we dive into functions being objects lets define a method.   A method is a property of an object that points to a function.  For instance, if we took an object a, and gave it 2 properties, one a string and one a function, the property pointing to the function would be a method and the other would just be a property:
```
let a = {}
a = { b: function() {return this}, c: "just a string" }   // here b is a method of a, while c is just a property of a.

a.b()        // we execute a.b()
> a          // a's method b returns the value of a, if we look back to	our original definition of "this" it fits		  // nicely… the code would really return {b: ƒ}, the value of a.  For brevity I will be returning
  // variables not values
```
Great! Some solid footing to dive down the "this" rabbit hole.  The distinction between a method and a function is very important to retain.  We now know that a method comes with the implication that it is a property of a parent object that's pointing to a function.    So, what happens when we refer to "this" in regular function one that at first glance has no parent object?  The blanket answer is the global scope object, when working with the browser the window.  In other words, when a function is not a method (i.e. not a property of a parent object) "this" will refer to window, the global object in web development.  Let’s look at an example:
```
function a() { return this } // here we declare a as a function in the global scope
a()
> window // if we executed a we would return window which is the global scope object.
```
This seems fairly intuitive but things go awry and need special attention when using "this" in nested functions within methods.  Regardless of where a function (again not a method) is defined, its value of "this" will always return window.  Let's take this example:
```
a = {
  b: function() {
    return function() {      // here we have b, a method of a which returns a function that returns the value 
     return this                 // "this" in that function’s scope                 
  } 
 }
}

a.b()()                                  // here we execute the object a's method b, and then additionally we execute
                                            // the nested function returned by b()
> window                             //  window will return which is counter intuitive, but if we hold true to our 
                                            // assertation that "this" defined within a function refers to window.
```
**Disclaimer** the following is only my understanding of the advanced workings of JS but it helps me conceptualize "this" when being referred to in a function.  Here is when the concept of all functions are objects comes to play.
If all functions are objects than we can assume (and be correct) that when defining a function, we are using actually the following syntax to create actual objects:
```
var sum = new Function('a', 'b', 'return a + b')

// essentially the equation above and below are the same (more advanced but closures are different)

var sum = function(a, b) {
  return a + b
}
```
Looking a bit into the above example we can see that when we create a function, we are really creating a new function object from the global Function class.  Function is therefore technically a class method, an object creating function, of the global scope object (window) that points to a class:
```
Function === window.Function

> true           // this snippet demonstrates the class Function and window.Function point to the same  
                     // thing.
```
Whenever we create a function, we are really executing a class method within the global object to create a function object, therefore when we refer to "this" it is the object that the method is defined in, the window!

When working in class definitions or functions, it is helpful to know the arrow functions will retain the value of this from the scope that they are defined in.  Arrow functions really come to the rescue by following normal variable look up rules when referring to this.  That is to say in arrow functions "this" becomes a var, and when not scoped in the current block (the actual arrow function) it will look for "this" outside its scope and find it.  Arrow functions perform as though the "this" reference from the scope it is being defined in is passed down as an argument to be used within that arrow functions scope.  In short, the “this” in an arrow function with be the “this” in the function/object it is encapsulated in.


