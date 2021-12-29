# Functional Utilities

## Currying

Currying is when you create a function that can later be called multiple times
with different arguments.

Here's an example of currying:
```javascript
// run this in browser console while accessing lodash.com.
function abc(a, b, c) {
  return [a, b, c];
}

var curried = _.curry(abc);

curried(1)(2)(3);
// the output is [1, 2, 3].

curried(1, 2)(3);
// the output is also [1, 2, 3].
```

So what curry does in example above, is allows us to call a function up to
three times with different value.

In general, curry allows us to break up an arguments passed by the number of
arguments.

> Currying doesn't return anything. It just waits until it gets all of the
> arguments and then it runs the function.
>
> So we can imagine that the `curried` function has in its internal saved a
> copy of the original function and it's just kind of waiting as you add
> arguments. The `curried` function accumulating that.
>
> But, keep in mind that every time we call a `curried` function and it hasn't
> met all of the required arguments, it has to return a function every time.

### Currying Exercise

Implement `curry()` that only takes up to 2 arguments.

#### Currying Exercise Solution

```javascript
const _ = {};

_.curry = function (fn) {
  return function (arg) {
    return function (arg2) {
      return fn(arg, arg2);
    };
  };
}

function ab(a, b) {
  return [a, b];
}

let curried = _.curry(ab);

curried(1)(2);
```

## Composing

Composing is when we take two functions and combine them.

Here's an example of composing:
```javascript
// run this in browser console while accessing underscore.org.
function consider(name) {
  return `I think it could be... ${name}`;
}

function exclaim(statement) {
  return `${statement.toUpperCase()}!`;
}

// the order does matter, but it depends on how the internal of `_.compose()`
// function works.
// in this case, underscore module execute the second function first and then
// the first function.
const blame = _.compose(consider, exclaim);

blame('me');
// the output is 'I think it could be... ME!'.
```

### Composing Exercise

Implement our own compose function.

#### Composing Exercise Solution

```javascript
const _ = {};

_.compose = function (fn, fn2) {
  return function () {
    // if we have access to `arguments` keyword, we can do something like this.
    const result = fn2.apply(this, arguments);
    return fn(result);
  };
}

// an alternative with arrow function.
// _.compose = (fn, fn2) => {
//   return (arg) => {
//     const result = fn(arg);
//     return fn(result);
//   };
// }

function consider(name) {
  return `I think it could be... ${name}`;
}

function exclaim(statement) {
  return `${statement.toUpperCase()}!`;
}

const blame = _.compose(consider, exclaim);

blame('me');
```
