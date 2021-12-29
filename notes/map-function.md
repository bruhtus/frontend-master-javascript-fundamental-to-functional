# `map` Functions

The key different between `map` and `each` is that `each` does
not return anything, the function does not return anything. And then `map`
always return an array.

> So even if we want to return something in the `each` callback function, we
can't. It doesn't work like that.

We use `map` to take list and transform the list into a new array. So we can
use it to just copy an array, if we wanted to. But, typically we're going to
use it to manipulate change, update it, and move it around however we want.

The general syntax for `_.map()` will look like this:
```javascript
// whatever this function returns, it's gonna go on the object.

// the only place the functions return something (at least in ES5) it's
// where we explicitly use `return`.

// we're not explicitly use `return`, so what's returning is `undefined` in
// this case. and so, we're gonna loop through and we're gonna have an array
// length three of undefined values.
_.map([1, 2, 3], function (v, i, list){
  console.log(v)
});
```

## `_.map()` Exercise Part 1

We have an array of weapons like below:
```javascript
const weapons = ['candlestick', 'lead pipe', 'revolver'];
```
we also have a `makeBroken` function like this:
```javascript
// takes an item and return a broken item by prepending the item with the word
// broken.
function makeBroken(item) {
  return `broken ${item}`;
}
```

So the task is, we need to make an array of broken weapons.

### `_.map()` Exercise Part 1 Solution

```javascript
const weapons = ['candlestick', 'lead pipe', 'revolver'];

function makeBroken(item) {
  return `broken ${item}`;
}

const brokenWeapons = _.map(weapons, makeBroken);

console.log(brokenWeapons);
```

## `_.map()` Vs `_.each()`

When we create `suspectsList` before, we need to use for-loop like
this:
```javascript
function createSuspectObjects(name) {
  return {
    name: name,
    color: name.split(" ")[1],
    speak() {
      console.log("my name is ", name);
    }
  };
}

var suspects = ["Miss Scarlet", "Colonel Mustard", "Mr. White"];
var suspectsList = [];

for (let i = 0; i < suspects.length; i++) {
  suspectsList.push(createSuspectObjects(suspects[i]));
};
```

Now, with `_.map()`, we can do that without the for-loop like this:
```javascript
function createSuspectObjects(name) {
  return {
    name: name,
    color: name.split(" ")[1],
    speak() {
      console.log("my name is ", name);
    }
  };
}

var suspects = ["Miss Scarlet", "Colonel Mustard", "Mr. White"];
var suspectsList = _.map(suspects, function (name) {
  return createSuspectObjects(name);
});

console.log(suspectsList);

// we can also loop through the `speak` like this
// _.each(suspects, function (suspects) {
//   suspect.speak
// });
```

Here's how we do that with `_.each()` instead of `_.map()`:
```javascript
function createSuspectObjects(name) {
  return {
    name: name,
    color: name.split(" ")[1],
    speak() {
      console.log("my name is ", name);
    }
  };
}

var suspects = ["Miss Scarlet", "Colonel Mustard", "Mr. White"];
var suspectsList = [];

_.each(suspects, function (suspect) {
  suspectsList.push(createSuspectObjects(suspect))
});

console.log(suspectsList);
```

## `_.map()` Exercise Part 2

Complete the rest of the function below using the `_.map()`:
```javascript
const _ = {};
let list = [1, 2, 3];

function foo(val) {
  return val + 1;
}

_.map = function (list, callback) {
  // TODO
}

_.map(list, foo);
```

### `_.map()` Exercise Part 2 solution

We can do it with for-loop like this:
```javascript
const _ = {};
let list = [1, 2, 3];

function foo(val) {
  return val + 1;
}

_.map = function (list, callback) {
  let storage = [];

  for (let i = 0; i < list.length; i++) {
    storage.push(callback(list[i], i, list));
  }

  return storage;
}

_.map(list, foo);
```

Or with `_.each()` like this:
```javascript
const _ = {};
let list = [1, 2, 3];

function foo(val) {
  return val + 1;
}

_.map = function (list, callback) {
  let storage = [];

  // there's still an error about `_.each()` is not a function
  // because we need to define `_.each()` as a function like `_.map()`
  // above.
  _.each(list, function (value, i, list) {
    storage.push(callback(value, i, list));
  });

  return storage;
}

_.map(list, foo);
```
