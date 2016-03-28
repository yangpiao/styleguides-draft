# JavaScript & Angular Style Guide

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
