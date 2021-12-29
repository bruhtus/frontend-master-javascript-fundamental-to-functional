# Array-like Object

Array-like object is an object that looks like an array but we can't use
array method such as `.push()`, `.join()`, `.length`, etc. We need to convert the
array-like object into an actual array.

One of the example of array-like object is `arguments` keyword.

Here's an example of how to turn array-like object into an actual array:
```javascript
const constructArr = function () {
  // what this does is take an array-like object and turn it into an array.
  const arr = Array.prototype.slice.call(arguments);

  // before push: ['was', 'it', 'in']
  arr.push('the billiards room?');
  // after push: ['was', 'it', 'in', 'the billiards room?']
  return arr.join(' ');
  // the return value: 'was it in the billiards room?'
};

constructArr('was', 'it', 'in');
```

## `Array.from()` in ES6

Before ES6, we need to use something like `Array.prototype.slice.call()`. Now,
in ES6 we have something called `Array.from()` which does exactly the same as
`Array.prototype.slice.call()` which is turn array-like object into an actual
array.

Here's the snippet before if we replace `Array.prototype.slice.call()` with
`Array.from()`:
```javascript
const constructArr = function () {
  // what this does is take an array-like object and turn it into an array.
  const arr = Array.from(arguments);

  // before push: ['was', 'it', 'in']
  arr.push('the billiards room?');
  // after push: ['was', 'it', 'in', 'the billiards room?']
  return arr.join(' ');
  // the return value: 'was it in the billiards room?'
};

constructArr('was', 'it', 'in');
```

## Implement `_.from()` Exercise

We're going to implement our own `from` method.

> Before `from` existed as part of ES6 spec, we had to use method like `from`
> that essentially did the `Array.prototype.slice.call()` under the hood for us
> without us having to think about it every time.


### Implement `_.from()` Exercise Solution

```javascript
const from = arr => {
  return Array.prototype.slice.call(arr);
};
```
