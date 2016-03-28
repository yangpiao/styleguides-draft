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

## JavaScript

- `jshint` covers most of common cases. Just run `grunt jshint:dev` if you don't want to run the whole build task.
- Put variable declarations at the top of their scope to avoid hoisting problem.
- Use the literal syntax for varable creation.
  ```js
  // avoid
  var obj = new Object();
  var arr = new Array();

  // recommend
  var obj = {};
  var arr = [];
  ```

- Use single quotes for strings.
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
### Controllers
### Services
### Directives
### Filters
### Miscellaneous
