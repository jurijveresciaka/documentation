JS
==

General
-------

Data types
^^^^^^^^^^

string
number
boolean
null
undefined
object
symbol

JS has typed values, not typed variables.

Bug - typeof(null) returns "null".

.. code-block:: javascript

    console.log(typeof(10));            // number
    console.log(typeof('Hallo world')); // string
    console.log(typeof(true));          // boolean
    console.log(typeof(null));          // object (known JS bug)
    console.log(typeof(a));             // undefined
    console.log(typeof({}));            // object

.. code-block::

    var a = { name: "Jurij Veresciaka" };
    console.log(a); // object

    var b = ["a", "b", "c"];
    console.log(b); // object

Use array for numerically positioned values and use objects for named properties.

.. code-block::

    var a = String(10);
    console.log(typeof(a)); // string

    var b = Number('10');
    console.log(typeof(b)); // number

    var c = Object('10');
    console.log(typeof(c)); // object

    var d = Boolean('10');
    console.log(typeof(d)); // boolean

ES6
^^^

.. code-block::

    "use strict";
    let a = 10;

Immediately invoked function expression (IIFEs)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block::

    (function IIFE() {
      console.log('Hallo World!!!');
    })();

.. code-block::

    var a = 1;

    (function IIFE() {
      var a = 9;

      console.log(a);
    })();

    console.log(a);

Module pattern
^^^^^^^^^^^^^^

.. code-block::

    function User() {
      var username, password;

      function doLogin(user, pw) {
        username = user;
        password = pw;

        console.log(username + ' ' + password);
      }

      var publicAPI = {
        login: doLogin
      };

      return publicAPI;
    }

    var jurij = User();

    jurij.login('Jurij', '123abc');
    jurij.login('Jurij', '123abc');

.. code-block::

    function foo() {
      console.log(this.bar);
    }

    var bar = 'global';

    var obj1 = {
      bar: "obj1",
      foo: foo
    }

    var obj2 = {
      bar: "obj2"
    }

    foo();          // "global"
    obj1.foo();     // "obj1"
    foo.call(obj2); // "obj2"
    new foo();      // undefined

.. code-block::

    var foo = {
      a: 42
    };

    var bar = Object.create(foo);

    bar.b = "hello world";

    bar.b; // "hello world"
    bar.a; // 42 <-- delegated to 'foo'