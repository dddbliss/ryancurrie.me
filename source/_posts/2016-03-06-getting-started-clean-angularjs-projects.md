---
layout: post
title: "A Clean AngularJS Project: Part 1 - Controllers"
permalink: getting-started-angularjs-project
date: 2016-03-06 18:38:04
comments: true
description: "Getting started with a clean AngularJS project structure"
keywords: "angularjs javascript styleguide structure project structure"
categories:
- angularjs
tags:
- angularjs
---

When starting on a new [AngularJS][angularjs] project, it is important early on to choose how you want to organize yourself before your project grows out of control.

Just recently, while on a new work project, our team ran into this issue in a big way. Being a team that was new to [AngularJS][angularjs], we ran with it head first and dove in. After about 3 months we quickly found ourselves running into issues with module dependencies being all over the place, poorly structured folders, badly written javascript, and generally a large confusing "ball of mud."

So, we stepped back, and reviewed the situation.

***

## Part 1: Controllers

We quickly identified that we were not all coding in a similar fashion. Being a .NET team, we usually all code C# in a similar fashion naturally, but we never stopped and asked ourselves about Javascript and how we should code it.

So we took a pointer from the wonderfully opinionated [Angular 1 Style Guide][angular-sg] by John Papa.

For Controllers, we style a controller like:

{% highlight javascript %}
angular
    .module('app')
    .controller('DashboardController', DashboardController);

// inject needed depencies and services
DashboardController.$inject = ['$log'];

function DashboardController($log) {
  var vm = this;

  // bindable members that can be bound at top.
  vm.complexAction = complexAction;
  vm.simpleAction = function() {
    // implement here if only one line of code.
  }
  vm.list = [];

  constructor();

  function constructor() {

  }

  function complexAction() {
    // implement down here if
    // it is more then one line.
  }
}
{% endhighlight %}

We also remember the following about Controllers when we use them:

* Always use the `controllerAs` syntax when using a Controller.
* When possible, defer logic to a factory or service.

[angularjs]: https://angularjs.org
[angular-sg]: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md
