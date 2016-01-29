## Types and Casting

- [10.1](#10.1) <a name="10.1"></a> Use the `String` function to convert a value to a string.

  ESLint rules: [`no-implicit-coercion`](http://eslint.org/docs/rules/no-implicit-coercion.html), [`no-new-wrappers`](http://eslint.org/docs/rules/no-new-wrappers.html)

  ```js
  let number = 15;

  // bad
  let badStringNumOne = number + '';
  let badStringNumTwo = new String(number);

  // good
  let goodStringNum = String(number);
  ```

- [10.2](#10.2) <a name="10.2"></a> Use the `Number` function for type casting and `Number.parseInt` for parsing strings. Always include the radix parameter when using `Number.parseInt`.

  > Why? Forgetting to include the radix when your string starts with `0` or `0x` will result in it being parsed as an octal or hexadecimal number, respectively (which is not usually what you want). Providing a radix forces you to specify the way in which the string is parsed.

  ESLint rules: [`radix`](http://eslint.org/docs/rules/radix.html), [`no-implicit-coercion`](http://eslint.org/docs/rules/no-implicit-coercion.html), [`no-new-wrappers`](http://eslint.org/docs/rules/no-new-wrappers.html)

  ```js
  let input = '43';

  // bad
  let badOne = new Number(input);
  let badTwo = +input;
  let badThree = input >> 0;
  let badFour = Number.parseInt(input);
  let badFive = parseInt(input);

  // good
  let goodOne = Number(input);
  let goodTwo = Number.parseInt(input, 10);
  ```

- [10.3](#10.3) <a name="10.3"></a> Use the `Boolean` function for casting to a boolean value. Never use double negation (`!!`), the `Boolean` constructor, or other "clever" techniques for getting a boolean value.

  ESLint rules: [`no-implicit-coercion`](http://eslint.org/docs/rules/no-implicit-coercion.html), [`no-new-wrappers`](http://eslint.org/docs/rules/no-new-wrappers.html), [`no-extra-boolean-cast`](http://eslint.org/docs/rules/no-extra-boolean-cast.html)

  ```js
  let collection = [];

  // bad
  let badOne = !!collection.length;
  let badTwo = new Boolean(collection.length);
  let badThree = ~collection.indexOf('foo');

  // good
  let good = Boolean(collection.length); // or, just use `collection.length`
  ```

- [10.4](#10.4) <a name="10.4"></a> Use `===` and `!==` over `==` and `!=`. The only exception to this rule is `== null`, which is allowed in order to check whether a reference is either `null` or `undefined`.

  > Why? `==` and `!=` perform type coercion, which can result in some unexpected comparions (for example, `[] == false` and `3 == '03'` evaluate to `true`). `===` and `!==` test for strict equality, which is almost always what you want.

  ESLint rule: [`eqeqeq`](http://eslint.org/docs/rules/eqeqeq.html)

  ```js
  // bad
  if (badValue == 3) {}

  // good
  if (goodValue === 3) {}
  ```

- [10.5](#10.5) <a name="10.5"></a> Use shorthand boolean comparisons.

  > **Note**: remember that `false`, `undefined`, `null`, `''`, `0`, and `NaN` evaluate to `false`, and all other values evaluate to `true`.

  ```js
  let name = '';
  let collection = [];

  // bad
  if (name !== '') {}
  if (collection.length > 0) {}

  // good
  if (name) {}
  if (collection.length) {}
  ```

- [10.6](#10.6) <a name="10.6"></a> Use the following patterns for type checking:

  ```js
  // String
  typeof something === 'string';

  // Number
  typeof something === 'number';

  // Boolean
  typeof something === 'boolean';

  // Object
  something != null && typeof something === 'object';

  // Array
  Array.isArray(something);

  // Null
  something === null;

  // Undefined
  something === undefined;

  // Null or Undefined
  something == null;
  ```

[↑ scrollTo('#table-of-contents')](#table-of-contents)