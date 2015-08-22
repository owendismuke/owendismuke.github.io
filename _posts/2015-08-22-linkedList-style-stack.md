---
layout: post
title:  "Implementing a Linked List Style Containerless Stack"
date:   2015-08-22 11:45:55 UTC -7
categories: javascript linked list stack
banner_image: 
comments: false
---
A stack is a commonly used structure within the programming world. In essence, it is a Last In, First Out (LIFO) list of tasks to be handled. During an exercise on stack creation in JavaScript, I was struck with a thought. Can I bring into play a stack without using a storage array or object as a container? Well, yes.

Given the simple stack constructor below, let's refactor to get rid of the container.

~~~ javascript
function Stack() {
  this._storage = [];
  this._length = 0;
};

Stack.prototype.push = function(value) {
  this._storage[this._length++] = value;
};

Stack.prototype.pop = function() {
  if (this._length <= 0) { return; }
  var temp = this._storage[--this._length];
  delete this._storage[this._length];
  return temp;
};

Stack.prototype.size = function() {
  return this._length;
};
~~~

In this instance, our `Stack` constructor is using array `this._storage` as a container. To push and pop, we are adding to and deleting from this container. To refactor this container out in a linked list style, we need to remember two important facts:

  - Items in a (singly) linked list are nodes with a reference to the next node.
  - JavaScript has the fun feature of passing objects by reference. 

With these facts in mind, let's refactor our Stack constructor with our list head.

~~~ javascript
function Stack() {
  this._head;
  this._length = 0;
};
~~~

Next, we need to add a function to our prototype to make our nodes.

~~~ javascript
Stack.prototype.node = function(value, next) {
  return {
    value: value,
    next: next
  };
};
~~~

With the ability to create a node, it is time to turn our attention to `push` and `pop`. In our new `push` function, we need to create a new head node with the value passed in and a link to the previous head.

~~~ javascript
Stack.prototype.push = function(value) {
  this._head = this.node(value, this._head);
  this._length++;
};
~~~

When refactoring `pop`, we don't want to return the entire head node as all we care about is the stored value. 

~~~ javascript
Stack.prototype.pop = function() {
  var oldHead;

  if (this._length > 0) {
    oldHead = this._head.value;
    this._head = this._head.next;
    this._length--;
  }

  return oldHead;
};
~~~

The `size` function remains the same, so we are done refactoring. Our linked list style node stack is now ready for use :)

~~~ javascript
function Stack() {
  this._head;
  this._length = 0;
};

Stack.prototype.push = function(value) {
  this._head = this.node(value, this._head);
  this._length++;
};

Stack.prototype.pop = function() {
  var oldHead;

  if (this._length > 0) {
    oldHead = this._head.value;
    this._head = this._head.next;
    this._length--;
  }

  return oldHead;
};

Stack.prototype.size = function() {
  return this._length;
};

Stack.prototype.node = function(value, next) {
  return {
    value: value,
    next: next
  };
};
~~~