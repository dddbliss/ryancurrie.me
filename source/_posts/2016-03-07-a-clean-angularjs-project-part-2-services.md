---
layout: post
title: 'A Clean AngularJS Project: Part 2 - Services'
date: 2016-03-07T16:06:31.000Z
comments: true
description: 'A Clean AngularJS Project: Part 2 - Services'
keywords: ''
categories:
  - angularjs
tags:
  - angularjs
---

To continue the discussion from [Part 1][blog-part1] on starting with a clean [AngularJS][angularjs] project, we wanted to discuss the style we chose for services.

--------------------------------------------------------------------------------

> A note on the difference between a `service` and a `factory`. A `service` is instantiated with a `new` keyword, and uses the `this` keyword for public methods and variables. They are similar to `factory`, so similar that it is recommended to use `factory` for consistency.

# Part 2: Services

We wanted our services to be clean, useful, and provide the main consumer of our data. Since we mainly use RESTful Web Services, we focus most of our code on Services that will use [ngResource[angular-ngresource] and make use of $resource.

First, our code style, again adapted from the wonderful [Angular 1 Styleguide][angular-sg] by John Papa.

```js
angular
    .module('app')
    .factory('dataService', dataService);

// inject dependencies on this line
dataService.$inject = ['$log'];

function dataService($log) {
    var someValue = '';

    var service = {
        // these methods are implemented below
        save: save,
        validate: validate,
        // additional value from above
        someValue: someValue
    };

    return service;

    function save() {
        // implement save functionality down here.
    };

    function validate() {
        // implement validate functionality down here.
    };
}
```

--------------------------------------------------------------------------------

# Using $resource for easy RESTful services

To make using $resource easy, we usually wrap our services so they return $resource objects. This gives us access to the wonderful `$resource.$get()`, `$resource.$query()`, `$resource.$save()`, `$resource.$delete()` functions inside our Controllers.

```js
angular
    .module('app')
    .factory('dataService', dataService);

// inject dependencies on this line
dataService.$inject = ['$resource'];

function dataService($log) {
    var service = $resource('/api/entity/:id', { id: '@_id' }, {
      update: {
        method: 'PUT' // this method issues a PUT request
      }
    });

    return service;
}
```

Here we have defined an additional `$update()` member we can call on our items for a PUT operation. We decided are okay with being able to save an object from a service outside of the service, as long as the business logic resides inside the service.

[blog-part1]: /2016/03/a-clean-angularjs-project-part-1-controllers/
[angularjs]: https://angularjs.org/
[angular-ngresource]: https://docs.angularjs.org/api/ngResource
[angular-sg]: https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md
