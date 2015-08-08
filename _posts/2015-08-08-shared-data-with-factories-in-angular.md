---
layout: post
title:  "Shared data with factories in AngularJS"
date:   2015-08-08 16:36:55 UTC -7
categories: angular js factory
banner_image: 
comments: false
---

When using AngularJS, there will eventually come a time when you want to share data between controllers. Thanks to the fact that objects are passed by reference in JavaScript, this is deceptively easy.

Let's start with a basic Angular app with two controllers:

~~~ javascript
var app = angular.module("app", [])
  
  .controller("first", function() {
    var _this = this;
    _this.data1 = {
      test: 'initial text 1'
    };
  })

  .controller("second", function() {
    var _this = this;
    _this.data2 = {
      test: 'initial text 2'
    };
  });
~~~

In the example above, there is no way for either controller to see the changes that happen to `text` in the other controller. This is where a shared factory becomes useful. In the example below, I have added a shared factory to the Angular app. This factory returns an object that contains a data object.

~~~ javascript
var app = angular.module("app", [])

  .factory("sharedScope", function() {
    var _this = this;
    _this.data = {text: "init text from factory"};
    return _this;
  })

  .controller("first", function() {
    var _this = this;
    _this.data1 = {
      test: 'initial text 1'
    };
  })

  .controller("second", function() {
    var _this = this;
    _this.data2 = {
      test: 'initial text 2'
    };
  });
~~~

Now that we have our factory, it's time to wire it in to the controllers.

~~~ javascript
var app = angular.module("app", [])

  .factory("sharedScope", function() {
    var _this = this;
    _this.data = {text: "init text from factory"};
    return _this;
  })

  .controller("first", function(sharedScope) {
    var _this = this;
    _this.data1 = sharedScope.data;
  })               
  
  .controller("second", function(sharedScope) {
    var _this = this;
    _this.data2 = sharedScope.data;
});
~~~

By using the fact that JavaScript passes objects by reference, we now have a shared factory that both controllers can access and modify while retaining two-way data binding.

To play with this code, check out this [JSFiddle][fiddle].


[fiddle]: https://jsfiddle.net/UL54D/7/
