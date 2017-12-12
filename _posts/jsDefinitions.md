---
layout: post
title: Archive of useful JS definitions
categories: setup
---
A list of useful JS definitions
<!--more-->

# Archive of useful JS definitions

## Javascript Paradigms
Javascript is a multi-paradigm language
  1. Prototypal inheritance (OOP)
  2. Functional programming 
  
## Functional Programming 
  * pure functions / function purity
  * avoid side-effects
  * examples include Haskell, Clojure, Elm
  * JS Features that support FP
    * first class functions
    * higher order functions
    * functions as arguments/values
    
## Pure function
Function that does not depend on nor modify the states of variables outside of its scope. That means pure functions always return the same result given the same parameters

## Higher order function
Function that takes in at least one function as argument, like callbacks, map...etc.

## First class function
Programming language that treats functions as any other value. Values in a language that are handled uniformly throughout (stored in data structure, passed in as arguments or used in control structures)

## Difference between classical and prototypal inheritance
  1. Class inheritance: instances inherit from classes and create sub-class relationships: hierachical class taxonomies. Instances are typically instantiated via constructor functions and 'new' keyword. (tight coupling or hierarchies) 
  2. Prototypal inheritance: instances inherit directly from other objects. Instances are typically instantiated via factory functions or 'Object.create()'. Instances may be composed from many different objects, allowing for easy selective inheritance.
  
## Prototypal Inheritance (object composition) 
  1. concatenative inheritance
  2. prototype delegation
  3. functional inheritance
  
## Concatenativve Inheritance
the process of inheriting features directly from one object to another by copying the source object properties and without retaining a reference between the two objects

{% highlight javascript %}
function foo(options = defaults) {
  const settings = {...defaults, ...options}
  return `${settings.bar}, ${settings.baz}`;
}

foo({bar: 'yay'});
{% endhighlight %}

Event emitter mixin
{% highlight javascript %}
import Events from 'eventemitter3';

cost obj = {};

Object.assign(obj, Events.prototype);
obj.on('event', payload => console.log(payload));
obj.emit('event', 'some data');
{% endhighlight %}

## Prototype
Is a working object instance. Objects inherit directly from other objects

## Prototype delegation
An object may have a link to a prototype for delegation. If a property is not found on the object, the lookup is delegated to the delegate prototype and its chain

example of prototype delegation with factory function

{% highlight javascript %}
const proto = {
  hello() {
    return `Hello, my name is ${this.name}`
  }
};
const greeter = name => Object.assign(Object.create(proto), {name});

const george = greeter('george');
const msg = george.hello(); // prototype delegation
console.log(msg);
{% endhighlight %}

One major drawback to delegation is that it’s not very good for storing state. If you try to store state as objects or arrays, mutating any member of the object or array will mutate the member for every instance that shares the prototype. In order to preserve instance safety, you need to make a copy of the state for each object

## Functional Inheritance
An object constructor function creates an empty object and adds it some methods before returning it. Inheritance is achieved in this object constructor function by getting the object through another object constructor function instead of creating an empty one.

The primary advantage of using functions for extension is that it allows you to use the function closure to encapsulate private data. In other words, you can enforce private state.

{% highlight javascript %}
// Base object constructor function
functiuon base(spec) {
  var that = {};
  that.name = spec. name;
  return that;
}

// construct a child object, inheriting from base
function child(spec) {
  var that base(spec);
  that.sayHello = () => `Hello, I am ${that.name}`
  return that;
}

// usage
var object = child({name: 'a functional object'});
console.log(object.sayHello());
{% endhighlight %}

Pros: 
  1. simplicity: a few steps are required to achieve inheritance ;
  2. “this”-free: you don’t have to care with the context variable “this”, meaning that you can freely pass any method of a   functional object as a callback parameter and everything will work as expected (see this script, for example) ;
  3. encapsulation: objects can have private (and even protected) members.
