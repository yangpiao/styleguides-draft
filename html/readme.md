# HTML Style Guide

## General

- Make sure HTML code have proper indentation and ensure the validity.
- Use lowercase for elements and attributes.
- Quote attribute values and use double quotes.
- Do not use `style` attribute. Put styles in SCSS files.
- Avoid extremely long lines.
- Although some closing tags are optional, include them to avoid confusion.
  ```html
  <!-- avoid, although it's valid -->
  <ul>
    <li>Google
    <li>Facebook
  </ul>

  <!-- recommend -->
  <ul>
    <li>Google</li>
    <li>Facebook</li>
  </ul>
  ```

## Markup

- Keep markup as lean as possible. Avoid superfluous parent elemnts and meaningless elements purely for styling, unless it's impossible to follow the design with the markup. Consult teammates and Google / StackOverflow to see if that's really impossible.
  ```html
  <!-- avoid -->
  <span class="avatar">
    <img src="">
  </span>

  <!-- recommend -->
  <img class="avatar" src="">
  ```

- Choose elements based on semantics. Use them for what they're supposed to be used for (think about the meanings of `section`, `article`, `header`, `footer`, `nav`, `aside`, `ul`, `ol`, `dl`, `h[1-6]`, `table`, `p`, `a`, `button`, `label`, `strong`, `em`, `time`, and a lot more). 

  If there's no proper element to choose, use `div` (for block element) or `span` (for inline element) with meaningful `class`es.

- Do not use `<br>` to control vertical white space is not acceptable. It's used for creating a line break inside of a paragraph. Use CSS `margin` and `padding`.

- `span` should used for adding global attributes and additional styles to text content. Do not use it to control flow (wrapping block contents).
  ```html
  <!-- avoid (this is from our code base!) -->
  <span class="breadcrumb-wrapper">
    <ul class="breadcrumb inline-block">
    ... ...
    </ul>
  </span>

  <!-- recommend -->
  <nav class="breadcrumb-wrapper">
    <ul class="breadcrumb inline-block">
    ... ...
    </ul>
  </nav>
  ```
