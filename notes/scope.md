# Scope

Scope is the area where a variable has access to some value. When we're defining
variables, we know that there's something like global variable and local
variable.

Global variable is available throughout the entire code base, usually we declare
that by not putting `var`, `let`, and `const` in front of the variable (usually
not a good idea). Or we could attach it directly to window object like this
`window.VARIABLE`.

Local variable is only available inside of functions or inside of blocks, and
there're some tricky rules when certain variables have access to certain values
and not.

## Function Scope

Function scope means that the variables inside of a function only had access to
the values defined there or in the parent function (we can only look up).

A local function scope variables are not available anywhere outside that
function, regardless of the context it's called in. Here's an example:
```javascript
var ACTUAL = null;

function firstFn() {
  var localToFirstFn = 'first';
  secondFn();
}

function secondFn() {
  ACTUAL = localToFirstFn;
}

firstFn();
console.log(ACTUAL);
```
even tho `secondFn()` is called inside of `firstFn()`, but `secondFn()`
didn't have access to `localToFirstFn` variable and this will throw an
error.

> Why `secondFn()` didn't look `localToFirstFn` variable inside of `firstFn()`
> function? Because `firstFn()` and `secondFn()` has different scope.
> `firstFn()` is not a parent scope of `secondFn()`, because `secondFn()` is not
> defined inside of `firstFn()` function. We just calling the `secondFn()`
> inside of `firstFn()` function which is a different thing.
>
> And because we haven't define `localToFirstFn` in the parent scope of
> `secondFn()` and `firstFn()` (they both has the same parent scope), that will
> cause an error.

**The look up order for variable is not by line, but by scope order. The current
block scope, and then the parent scope**.

## Block Scope

Block is something inside the curly parentheses `{}` and we can create a block
scope with `let`.

What block scope variable does basically the variable only exist inside of the
block. Here's an example:
```javascript
var ACTUAL = null;

var fn = function () {
  var where = 'outer';
  {
    let where = 'inner';
  }
  var ACTUAL = where;
};

// the output would be 'outer'.
fn();
```

If we used `var` instead of `let` like this:
```javascript
var ACTUAL = null;

var fn = function () {
  var where = 'outer';
  {
    var where = 'inner';
  }
  var ACTUAL = where;
};

// the output would be 'inner' because we're just re-defining the previous
// variable.
fn();
```

## Inner and Outer Scope Share The Same Name

If an inner and an outer variable share the same name, and the name is
referenced in the inner scope, the inner scope variable masks the variable
from the outer scope with the same name. **This renders the outer scope
variables inaccessible from anywhere within the inner function block**.

Here's an example:
```javascript
var ACTUAL = null;
var sameName = 'outer';

function fn() {
  var sameName = 'inner';
  ACTUAL = sameName;
}

fn();
// the output would be 'inner'.
console.log(ACTUAL);
```

If an inner and an outer variable share the same name, the name is referenced
in the outer scope, the outer scope value will be used. Basically it's the
opposite of what we've done before.

Here's an example:
```javascript
var ACTUAL = null;
var sameName = 'outer';

function fn() {
  var sameName = 'inner';
}

fn();
ACTUAL = sameName;
// the output would be 'outer'.
console.log(ACTUAL);
```

## New Variable Scope is Created for Every Function Call

A new variable scope is created for every call to a function, like example below:
```javascript
var ACTUAL = null;

function fn() {
  // the `||` symbol here means `or`. if `innerCounter` already have a value
  // we'll use that value. but if `innerCounter` doesn't have a value or
  // undefined, we'll use `10` as value.
  var innerCounter = innerCounter || 10;

  innerCounter = innerCounter + 1;
  ACTUAL = innerCounter;
}

fn();
// the output is `11`.
console.log(ACTUAL);
fn();
// the output is still `11`.
console.log(ACTUAL);
```

So, what happen is whenever we call a function, we create a brand new
function scope.

**Every time we call a function, a brand new scope is created which is
separate from previous scope**.

Another example with uninitialized string variables:
```javascript
var ACTUAL = null;

function fn() {
  var localVariable;
  if ( localVariable === undefined ) {
    // the variable will be initialized for the first time during the first
    // call.
    ACTUAL = 'alpha';

  } else if (localVariable === 'initialized') {
    // the variable already been initialized by previous call.
    ACTUAL = 'omega';

  }

  // now that ACTUAL has been set, we will initialized localVariable to refer to
  // a string.
  localVariable = 'initialized';
}

fn();
// the output is `alpha`.
console.log(ACTUAL);
fn();
// the output is still `alpha`.
console.log(ACTUAL);
```

## Inner Function can Access Local Scope Variables and Parent Scope Variables

An inner function can access both its local scope variables and variables in its
parent scope, as long as the local scope variables and parent scope variables
have different name.

Here's an example:
```javascript
var ACTUAL = null;
var outerName = 'outer';

function fn() {
  var innerName = 'inner';
  ACTUAL = innerName + outerName;
}

fn();
// the output is `innerouter`.
console.log(ACTUAL);
```

## Inner Function Retains Access to a Variable in Parent Scope Variable

Between calls to an inner function, that inner function retains access to
a variable in parent scope (or outer scope). Modifying those variables has
a lasting effect between calls to the inner function.

Here's an example:
```javascript
var ACTUAL = null;
var outerCounter = 10;

function fn() {
  // because we define the variable outside the function scope,
  // the increment value is not disappear.
  outerCounter = outerCounter + 1;
  ACTUAL = outerCounter;
}

fn();
// the result is `11`.
console.log(ACTUAL);
fn();
// the result is `12`.
console.log(ACTUAL);
```

> If we put `var` in `outerCounter = outerCounter + 1;` like this
> `var outerCounter = outerCounter + 1;`, that will initializing
> another variable in function scope instead of referencing the parent
> scope.
>
> The second `outerCounter` in `var outerCounter = outerCounter + 1`
> become `undefined` and `undefined + 1` result in `NaN` (Not a Number).

## Retaining Access to Variables from a Parent Scope

The rule about retaining access to variables from a parent scope still
applies, even after the parent function call (that created the parent
scope) has returned.

Here's an example:
```javascript
function outerFn() {
  var counterInOuterScope = 10;

  function innerIncrementingFn() {
    counterInOuterScope = counterInOuterScope + 1;
    ACTUAL = counterInOuterScope;
  }

  innerIncrementingFn();
  // the output is `11`.
  console.log(ACTUAL);

  innerIncrementingFn();
  // the output is `12`.
  console.log(ACTUAL);

  // we save a reference to the newly created inner function for later,
  // by assigning it to the global scope (window).
  window.retainedInnerFn = innerIncrementingFn;
  // if we put the parentheses in `innerIncrementingFn` above, that would
  // be running the function and `window.retainedInnerFn` will take the
  // results of that function.
  // we only want that function, not the result of that function.
}

// calling the `outerFn()` function.
outerFn();

// calling the `innerIncrementingFn()` function.
window.retainedInnerFn();

// the output is `13`.
console.log(ACTUAL);
```

Because the `innerIncrementingFn()` called twice inside of outerFn()` function,
the `counterInOuterScope` variable already incremented twice before we call
`window.retainedInnerFn()` function (which is basically the global version of
`innerIncrementingFn()` local function in `outerFn()` function). That's why the
final result of `ACTUAL` is 13.
