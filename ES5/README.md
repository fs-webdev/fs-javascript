JavaScript
==========

Code can and should not be submitted that does not meet these criteria:

## Table of Contents

  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Functions](#functions)
  1. [Variables](#variables)
  1. [Hoisting](#hoisting)
  1. [Blocks](#blocks)
  1. [Ternarys](#ternarys)
  1. [Whitespace](#whitespace)
  1. [Commas](#commas)
  1. [Semicolons](#semicolons)
  1. [Naming Conventions](#naming-conventions)
  1. [Performance](#performance)
  1. [Frontier](#frontier)

## Objects

  - Use the literal syntax for object creation.

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

**[⬆ back to top](#table-of-contents)**

## Arrays

  - Use the literal syntax for array creation.

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

**[⬆ back to top](#table-of-contents)**

## Functions

  - Function expressions:

    ```javascript
    // anonymous function expression
    var anonymous = function() {
      return true;
    };

    // named function expression
    var named = function named() {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

**[⬆ back to top](#table-of-contents)**

## Variables

  - Always use `var` to declare variables. Not doing so will result in global variables.

    ```javascript
    // bad
    nowGlobalVar = true;

    // good
    var myScopedVar = true;
    ```

  - Use one `var` declaration per variable. It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs.

    ```javascript
    // bad
    var coolItem = 1,
        coolerItem = 'abcd',
        coolestItem = $('myItem');

    // bad
    // Adding another item to the list can result in an error
    var coolItem = 1,
        coolerItem = 'abcd',
        coolestItem = $('myItem');
        coolesterItem = true;

    // good
    var coolItem = 1;
    var coolerItem = 'abcd';
    var coolestItem = $('myItem');
    ```

**[⬆ back to top](#table-of-contents)**

## Hoisting

  - Variable declarations get hoisted to the top of their scope, their assignment does not.

    ```javascript
    // we know this wouldn't work (assuming there is no
    // notDefined global variable)
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // creating a variable declaration after you reference
    // the variable will work due to variable hoisting.
    // Note: the assignment value of `true` is not hoisted.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // The interpreter is hoisting the variable declaration
    // to the top of the scope, which means our example could
    // be rewritten as:
    function example() {
      var declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }
    ```

  - Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function() {
        console.log('anonymous function expression');
      };
    }
    ```

  - Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // the same is true when the function name is the same
    // as the variable name.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      }
    }
    ```

  - Function declarations hoist their name and the function body.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/)

**[⬆ back to top](#table-of-contents)**

## Blocks

  - Use braces with all multi-line blocks.

    ```javascript
    // bad
    if (condition)
      statement;

    // bad
    if (condition)
      statement;
    else
      statement;

    // bad
    // code that requires an 'else' should be on multiple lines.
    if (condition) statement;
    else statement;

    // bad
    // code that contains more than one statement should not
    // be on a single line.
    if (condition) { statement; statement; }

    // good
    if (condition) {
       statement;
    }

    // good
    if (condition) {
      statement;
    } else {
      statement;
    }

    // good
    // single-statement, single line, no braces
    if (condition) statement;

    // good
    // mult-statement, multi-line, braces
    if (condition) {
      statement;
      statement;
    }
    ```

**[⬆ back to top](#table-of-contents)**   

## Ternarys

  - Use ternarys for variable assignment.

    ```javascript
    // bad
    // determines a course of action. Use an 'if' statement instead
    (condition) ? funcOne() : funcTwo();

    // good
    var myVar (condition) ? 'on' : 'off';
    ```

**[⬆ back to top](#table-of-contents)**    

## Whitespace

  - Use soft tabs set to 2 spaces.

    ```javascript
    // bad
    function() {
    ∙∙∙∙var name;
    }

    // bad
    function() {
    ∙var name;
    }

    // good
    function() {
    ∙∙var name;
    }
    ```
  - Use Unix line endings (LF) not Windows line endings (CRLF).

  - Line up the equal signs of var statments.

    ```javascript
    var coolItem      = 1;
    var coolerItem    = "abcd";
    var coolestItem   = $("#my-id");
    var coolesterItem = $(".my-class");
    ```

    **Note:** Currently under review.

**[⬆ back to top](#table-of-contents)**

## Commas

  - Trailing commas: **Nope.**

    ```javascript
    // bad
    var foo = [ 1, 2, 3, ];

    var bar = { a: 1, b: 2, c: 3, };

    // good
    var foo = [ 1, 2, 3 ];

    var bar = { a: 1, b: 2, c: 3 };
    ```

**[⬆ back to top](#table-of-contents)**

## Semicolons

  - Lines missing a semicolon may cuase accidental code execution.

    ```javascript
    // bad
    // when minified, JavaScript will attempt to run 'foo'
    // with your IIFE as a parameter
    var foo = function() {
      // ...
    }
    (function() {
      // ...
    })();

    // good
    var foo = function() {
      // ...
    }; // note the ending semicolon
    (function() {
      // ...
    })();
    ````

**[⬆ back to top](#table-of-contents)**

## Naming Conventions

  - Avoid single letter names. Production code will already be minified so be descriptive with your naming.

    ```javascript
    // bad
    function q() {
      // ...
    }

    // good
    function query() {
      // ...
    }
    ```

  **Note:** Counters and iterators inside loops are an exception.

  - Use camelCase when naming objects, functions, and instances.

    ```javascript
    // bad
    var OBj = {};
    var this_is_my_object = {};
    function c() {}
    var u = { name: 'John' };

    // good
    var obj = {};
    var thisIsMyObject = {};
    function thisIsMyFunction() {}
    var user = { name: 'John' };
    ```

  - Use all uppercase with underscores for naming constants.

    ```javascript
    // bad
    var myConst = true;

    // bad
    var MY-CONST = true

    // good
    var MY_CONST = true;
    ```

  - Name your functions. This is helpful for stack traces.

    ```javascript
    // bad
    var log = function(msg) {
      console.log(msg);
    };

    // good
    var log = function log(msg) {
      console.log(msg);
    };
    ```

  - Follow conventions for naming standard objects.

    * `ex` - Exception. Used in `catch()` statements.
    * `evt` - Event. Used in `on` handlers.
    * `xhr` - xmlHttpRequest. Convention for ajax response objects.
    * `i`, `j` - Counters used in loops.
    * `$var` - Shortcut to jQuery objects.
    * `el` - HTML Element. The first var usually passed to a control.
    * `config` - Config object. The second var usually passed to a control.

**[⬆ back to top](#table-of-contents)**

## Performance

  - Optimize `for` loops. At the very least, cache the `length` parameter of a collection.

    ```javascript
    // bad
    var myArray = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
    for (var i = 0; i < myArray.length; i++) {
      // ...
    }

    // good
    var myArray = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
    for (var i = 0, len = myArray.length; i < len; i++) {
      // ...
    }
    ```

  - Cache frequently used items (such as regex and HTML Nodes from jQuery).

    ```javascript
    // bad
    var myArray = [ 'one', 'two', 'three', 'four', 'five' ];
    for (var i = 0; i < 10; i++) {
      myArray[i].match(/two/);
    }

    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    var regex = /two/;
    var myArray = [ 'one', 'two', 'three', 'four', 'five' ];
    for (var i = 0; i < 10; i++) {
      myArray[i].match(regex);
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

  - Minimize browser reflow events. Changes to the DOM should be reduced as much as possible.

    * Try to use `innerHTML` to write to the DOM only once
    * Try using DOM fragments instead of actually altering live DOM nodes
    * Try setting class names instead of setting styles via the `style` property
    * Avoid accessing the width, height, and position of elements a lot

**[⬆ back to top](#table-of-contents)**

## Frontier

  - Avoid URLs in JavaScript. These should be passed in via the `config` object. This allows us to create URLs that work in development, staging, and production.
  - Avoid hardcoded i18n strings in the JavaScript. These should be passed in via the `config` object.

**[⬆ back to top](#table-of-contents)**
