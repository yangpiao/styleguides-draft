# CSS & SASS Style Guide

## General

- All code should have proper and consistent indentation.

- Put one rule per line. Use enough whitespaces and line breaks for readability. Compression is the build tool's job, not yours.

  ```scss
  // avoid
  .selector { color: white; background-color: black; }
  .parent-1 .child-1, .parent-2, .child-2 { /* rules */ }

  // recommmend
  .selector {
    color: white;
    background-color: black;
  }

  .parent-1 .child-1,
  .parent-2, .child-2 {
    /* rules */
  }
  ```

- Use variables and mixins if the code is supposed to be reusable.

- Do not use Compass mixins for simple things like `border-radius`, `box-shadow`, etc. Do not write vendor prefixes (`-webkit-`, `-moz-`, `-o-`, and `-ms-`) yourself. Vendor prefixes are not required anymore for some properties, and `autoprefixer` will take care of prefixes while building.

  ```scss
  // avoid
  .selector {
    @include border-radius(4px);
    -webkit-transform: translateX(42em);
    -moz-transform: translateX(42em);
    -o-transform: translateX(42em);
    -ms-transform: translateX(42em);
    transform: translateX(42em);
  }

  // recommmend
  .selector {
    border-radius: 4px;
    transform: translateX(42em);
  }
  ```

- Break down styles into small chunks and use `@import`s.

- Put nested selectors at the end of rules.

  ```scss
  // avoid
  .parent {
    color: black;
    .child {
      color: blue;
    }
    background-color: white;
  }

  // recommend
  .parent {
    color: black;
    background-color: white;

    .child {
      color: blue;
    }
  }
  ```

## Specificity

- Avoid styling ID selectors.

  ```scss
  // avoid
  #main-menu {
    // rules
  }

  // recommmend
  .menu {
    // rules
  }
  ```

- Do not put tag name before class or ID selector.
  ```scss
  // avoid
  div.control-group {
    // ...
  }

  // recommend
  .control-group {
    // ...
  }
  ```

- Avoid using `!important`. Overwrite styles by specifying a selector with higher specificity.

- When styling elements (tags), make sure the styles are general enough.

  ```scss
  // general styles
  a {
    color: $link-color;
  }
  h1 {
    font-size: 32px;
    font-weight: bold;
  }

  // generally, adding margin or padding to all `div`s is not a good idea
  .component div {
    margin-bottom: 5px;
  }
  ```

- Avoid too many nested levels: if the level's more than **3**, you should refactor your code. The code is hard to read. The file size is much bigger. And it adds unnecessary overhead for others to overwrite some styles.

  ```scss
  // avoid - this is from our code base, and it should be refactored.
  .module-page {
    // ...
    .tabs-left {
      // ...
      div.tab-content {
        // ...
        .tab-pane.active {
          // ...
          .table-tpauploadnewcreative {
            // ...
            .control-group {
              // ...
              .controls {
                margin-left: 0;
              }
            }
          }
        }
      }
    }
  }

  // recommend
  .level-1 {
    .level-2 {
      .level-3 {
        // stop right here!
      }
    }
  }
  ```
