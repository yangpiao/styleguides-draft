# JavaScript & Angular Style Guide

## Contents

1. [JavaScript](#javascript)
2. [Angular](#angular)
  1. [Modules](#modules)
  2. [Controllers](#controllers)
  3. [Services](#services)
  4. [Directives](#directives)
  5. [Filters](#filters)
  6. [Miscellaneous](#miscellaneous)
  7. [References](#references)

## JavaScript

- `jshint` covers most of common cases. Just run `grunt jshint:dev` if you don't want to run the whole build task.

- Put variable declarations at the top of their scope to avoid hoisting problem.

- Use the literal syntax for varable creation.

  ```js
  // avoid
  var obj = new Object();
  var arr = new Array();
  var str = new String();

  // recommend
  var obj = {};
  var arr = [];
  var str = '';
  ```

- Understand what are truey and falsy when dealing with conditional statements. Check this out: [JS Equality Table](http://dorey.github.io/JavaScript-Equality-Table/).

- If the function has too many parameters, consider using one object parameter.

  ```js
  // avoid
  method(id, name/*, and 3 other parameters */);

  // recommend
  method({
    id: id,
    name: name,
    // other parameters
  });
  ```

- Use ES5 features when possible. They're all supported by modern browsers. [ES5 compatibility table](http://kangax.github.io/compat-table/es5/).

## Angular

Based on Angular 1.2, the version we're using now.

### Modules

- Use unique names with separators for sub-modules. Unique names help avoid module name collisions. Separators help define modules and their submodule hierarchy.

- Try to create small modules that encapsulate one responsibility. Avoid huge modules.

### Controllers

- Do not put any DOM related code in controllers. Refactor DOM access into a directive.

- Put only presentational logic in a controller. Avoid business logic (delegate to services). This helps keeping controllers lean and simple.

- Keep controllers focused on a relative small view. If the controller gets too big (e.g., 500+ lines), consider breaking it down.

- If a controller needs a dependency resolved before other logic, resolve it in routing resolves, not in the controller itself. Create a `resolve` property on each controller and reference the property in router.

  ```js
  // avoid
  function SomeCtrl(dataService) {
    var vm = this;
    dataService.getData().then(function(model) {
      // all other logic relies on `model`
      vm.model = model;
    });
  }

  // recommend
  function SomeCtrl(model) {
    var vm = this;
    vm.model = model;
  }
  SomeCtrl.resolve = {
    model: resolveModel
  };
  function resolveModel(dataService) {
    return dataService.getData();
  }
  resolveModel.$inject = ['dataService'];

  // in the router
  $routeProvider.when('/', {
    templateUrl: '',
    controller: 'SomeCtrl',
    controllerAs: 'vm',
    resolve: SomeCtrl.resolve
  });
  ```

- It's highly recommended to use `controllerAs` syntax. Instead of binding variables and methods on `$scope`, bind them to `this` (controllers are classes). This avoids a lot of nested scope issues. Treat `$scope` as a special case and limit its use to publishing / subscribing events and `$watch`.

  Bound to `$scope`:

  ```js
  function MainCtrl($scope) {
    $scope.name = '';
    $scope.editable = true;
  }
  ```

  ```html
  <div ng-controller="MainCtrl">
    <div ng-if="editable">
      <!-- doesn't work properly -->
      <input type="text" ng-model="name">
    </div>
  </div>
  ```

  Bound to `this`:
  
  ```js
  function MainCtrl() {
    this.name = '';
    this.editable = true;
  }
  ```

  ```html
  <div ng-controller="MainCtrl as vmMain">
    <div ng-if="vmMain.editable">
      <!-- no issue -->
      <input type="text" ng-model="vmMain.name">
    </div>
  </div>
  ```

- Put all members bound to `$scope` / `this` together at the top to improve readability. This makes it easier for people to identify which members is being used in the view.

  ```js
  // avoid
  function SomeCtrl() {
    this.someMethod = function() {
    };

    function helperFn() {
    }
    // and some other 100 lines of code
    // which makes it hard to find this method
    this.otherMethod = function() {
    };
  }

  // recommend
  function SomeCtrl() {
    this.someMethod = someMethod;
    this.otherMethod = otherMethod;

    function someMethod() {
    }

    function otherMethod() {
    }

    function helperFn() {
    }
    // ...
  }
  ```

### Services

- Angular services can be defined using `service()` or `factory()`. They are basically the same thing. The only difference is that in a `service` function members are bound to `this`, while a `factory` function simply returns an object. Use `factory()` only for consistency.

- Put accessible members together at the top for readability.

### Directives

- Restrict to elements (`restrict: 'E'`) and attributes (`restrict: 'A'`, `'EA'` for both) when declaring directives. It makes more sense to use `<turn-directive></turn-directive>` or `<div turn-directive></div>` than `<div class="turn-diretive"></div>`.

- Add `turn-` prefix to the name of a directive.

### Miscellaneous

- Use constants for values that do not change and do not come from another service.

- Do not bind any variable or method to `$rootScope`. `$rootScope` should not be used as a shared data store - use services.

- Events make it harder to locate code and debug. Use services, directive, and `$watch` over events, unless it's impossible to do so. `$rootScope.$broadcast` should only publish events that are global and universal accross the whole app. It's not for cross-controller communication.

- Use `$scope.$digest` over `$scope.$apply` where it makes sense. When using `$scope.$digest` only child scopes will update. `$scope.$apply` will call `$rootScope.$digest`.

- Use `$window`, `$document`, `$timeout`, and `$interval` instead of `window`, `document`, `setTimeout`, and `setInterval`.

- If you have `Array#filter` in your code, consider creating an Angular filter for it.

- Return promises for asynchronous functions instead of passing a callback function.

- Use jsDoc syntax to document modules and methods.

### References

- [Airbnb JavaScript Style Guide (ES5)](https://github.com/airbnb/javascript/tree/master/es5)
- [Angular 1 Style Guide by John Papa](https://github.com/johnpapa/angular-styleguide/tree/master/a1)
- [Angular Style Guide by Todd Motto](https://github.com/toddmotto/angular-styleguide)
