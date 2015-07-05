---
layout: post
title:  "The Joy and Sorrow of Ternary Operators"
date:   2015-07-04 16:08:49-7
categories:
- ternary
- debugging
- JavaScript
comments: true
---

A ternary operator is a shorthand way to write if/then/else statements. Ternary operators can be used as return statements, to assign a value to a variable, or to run functions based on a conditional.

You write a ternary in three steps. 

1. State your conditional.
2. Preface your then expression with the shorthand `?`.
3. Preface your else conditional with the shorthand ':'.

The following example:

~~~ javascript
function getBool(someValue) {
  if (someValue === true) {
    return true;
  } else {
    return false;
  }
}
~~~

Is the same as:

~~~ javascript
function getBool(someValue) {
  return someValue === true ? true : false;
}
~~~

Can you see how this would result in less lines of code? This is the greatest shortcut ever, right? Not so fast. Before you run off to change every if statement in your codebase into a ternary, you should realize the drawbacks. Ternary operators increase the complexity of your code. Instead of being able to easily follow the logic path you have dictated in your code, there is now one line that is doing many things. The simple example I provided above does not quite illustrate just how quickly the complexity can increase. Consider the following two code snippets that do the exact same operation.

Without ternary:

~~~ javascript
function deepEqual(thing1, thing2){
    if (thing1 === thing2){
      return true;
    }
    
    if (typeof thing1 !== "object" || typeof thing2 !== "object"){
      return false;
    } 
    
    return !!Object.keys(thing1).reduce(function(prev,curr){
      if (prev) { return deepEqual(thing1[curr], thing2[curr]); }
    }, true);
};
~~~

With ternary:

~~~ javascript
function deepEqual(thing1, thing2){
    return thing1 === thing2
      ? true : typeof thing1 !== "object" || typeof thing2 !== "object"
        ? false : !!Object.keys(thing1).reduce(function(prev,curr){
            if (prev) { return deepEqual(thing1[curr], thing2[curr]); }
          }, true);
};
~~~

### Did you just nest a ternary operator?!?

Yes, I did. While the return statement is technically now one line of code. It is definitely harder to read. However, the maintenance cost is much higher. If I wanted to swap out the reduce function or add any other steps in this process, I would have to spend the time to decipher the nested ternary to figure out at what step the new code needs to be inserted, not to mention the time spent debugging values through this statement.

In conclusion. Like all other shorthand code you may come across, ternary operators are not an end all, be all to all code situations. In my opinion, I would recommend that you take into consideration how often is the code maintained, how stable is the codebase, and what level are the other developers that will need to understand this code.

The nested ternary example is testable using the following object.

~~~ javascript
var obj = {here: {is: "an"}, object: 2};

console.log(deepEqual(obj, obj));
// → true
console.log(deepEqual(obj, {here: 1, object: 2}));
// → false
console.log(deepEqual(obj, {here: {is: "an"}, object: 2}));
// → true
~~~