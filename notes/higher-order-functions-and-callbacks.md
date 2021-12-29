# Higher-order Functions and Callbacks

## Higher-order Functions

Higher-order functions in javascript is what enables us to do functional
programming techniques. Because a function in javascript is data, and that's
not true in other programming language that function can be data.

What function is data means, we can pass function around, we can return them
without invoking them and things like that. Just like we would do with an
object or primitive value.

### Takes a Function as an Input (Argument)

A higher-order function can take a function as an input, for example:
```javascript
element.addEventListener("change", () => {
  console.log("Our evidence is updated");
});
```

### Returns a Function as the Output

A higher-order function can also take a function as an output, for example:
```javascript
const newClue = (name) => {
  const length = name.length;

  return (weapon) => {
    let clue = length + weapon.length;
    return !!(clue % 1);
  };
};
```

## Callbacks

Callbacks are just functions that we pass to a functions. Here's an example
of callbacks:
```javascript
const ifElse = (condition, isTrue, isFalse) => {
  return condition ? isTrue() : isFalse();
};

ifElse(true,
  () => { return console.log(true); },
  () => { return console.log(false); }
);
```

## Passing a Function as Arguments to another Function

Here's an example of passing arguments to function:
```javascript
function increment(n) {
  return console.log(n + 1);
}

function square(n) {
  return console.log(n * n);
}

function doMathSoIDontHaveTo(n, func) {
  return func(n);
}

doMathSoIDontHaveTo(5, square);
doMathSoIDontHaveTo(4, increment);
```

### Exercise: Rewrite The Example into ES6

Rewrite the example above, which is this:
```javascript
function increment(n) {
  return console.log(n + 1);
}

function square(n) {
  return console.log(n * n);
}

function doMathSoIDontHaveTo(n, func) {
  return func(n);
}

doMathSoIDontHaveTo(5, square);
doMathSoIDontHaveTo(4, increment);
```
into ES6.

#### Solution: Rewrite The Example into ES6

```javascript
const increment = n => {
  return console.log(n + 1);
};

const square = n => {
  return console.log(n * n);
};

const doMathSoIDontHaveTo = (n, func) => {
  return func(n);
};

doMathSoIDontHaveTo(5, square);
doMathSoIDontHaveTo(4, increment);
```

## Passing a Function to Another Function and then Calling It with Arguments

Here's an example:
```javascript
const ifElse = (condition, isTrue, isFalse, param) => {
  return condition ? isTrue(param) : isFalse(param);
};

ifElse(true,
  parameter => { return console.log(true, parameter); },
  parameter => { return console.log(false, parameter); },
  'hello world'
);
```

Another example using the spread operator:
```javascript
const ifElse = (condition, isTrue, isFalse, ...args) => {
  console.log(args);
  return condition ? isTrue(...args) : isFalse(...args);
};

ifElse(true,
  (...parameter) => { return console.log(true, ...parameter); },
  (...parameter) => { return console.log(false, ...parameter); },
  'hello world 1',
  'hello world 2',
  'hello world 3',
);
```

### Before ES6

Before ES6 or spread operator exist, we need to do something like this to pass
a function to another function and then calling it with an arguments:
```javascript
// this will cause an error, because arrow function doesn't have arguments.
// const ifElse = (condition, isTrue, isFalse) => {
//   const args = [].slice.call(arguments,3);
//   return condition ? isTrue.apply(this, args) : isFalse.apply(this, args);
// };

function ifElse(condition, isTrue, isFalse) {
  const args = [].slice.call(arguments,3);
  console.log(args);
  return condition ? isTrue.apply(this, args) : isFalse.apply(this, args);
}

// still not sure how to log all the arguments.
const logTrue = (msgs) => { return console.log(msgs); };
const logFalse = (msgs) => { return console.log(msgs); };

ifElse(
  true,
  logTrue,
  logFalse,
  'hello world 1',
  'hello world 2',
  'hello world 3',
);
```

## `_.reduce()` Exercise

`_.reduce()` always returns one function. What `_.reduce()` does is loop
through the collection calling the callback function, and then based on
whatever the callback function returns, the result get passed on back and get
accumulated.

So as we looping through the call back function, we're gonna call the previous
value and the current value.

Now the task is to implement `_.reduce()` mechanism.

### `_.reduce()` Exercise Solution

```javascript
const _ = {};

_.reduce = function (list, callback, initial) {
  let accumulated = initial;

  for (let i = 0; i < list.length; i++) {
    if (i === 0 && accumulated === undefined) {
      accumulated = list[0];
      console.log('boom');

    } else {
      accumulated = callback(list[i], accumulated);

    }
  }

  return accumulated;
};

function sum(current_value, last_value) {
  return current_value + last_value;
}

_.reduce([1, 2, 3], sum, 0);
```

## Empty Room Exercise

There's some data like this:
```javascript
const newDevelopment = [
    {
        name: 'Miss Scarlet',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: true},
            {'dining room': true},
            {'billiard room': false},
            {library: true}
        ]
    },
    {
        name: 'Reverend Green',
        present: true,
        rooms: [
            {kitchen: true},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': true},
            {library: false}
        ]
    },
    {
        name: 'Colonel Mustard',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: true},
            {'dining room': false},
            {'billiard room': true},
            {library: false}
        ]
    },
    {
        name: 'Professor Plum',
        present: true,
        rooms: [
            {kitchen: true},
            {ballroom: false},
            {conservatory: false},
            {'dining room': true},
            {'billiard room': false},
            {library: false}
        ]
    }
];
```

We need to figure out which room no one was in.

### Empty Room Exercise Solution

```javascript
// run this in browser console while accessing lodash.com.
// this return empty array, and i'm not sure how to solve this.
const newDevelopment = [
    {
        name: 'Miss Scarlet',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: true},
            {'dining room': true},
            {'billiard room': false},
            {library: true}
        ]
    },
    {
        name: 'Reverend Green',
        present: true,
        rooms: [
            {kitchen: true},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': true},
            {library: false}
        ]
    },
    {
        name: 'Colonel Mustard',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: true},
            {'dining room': false},
            {'billiard room': true},
            {library: false}
        ]
    },
    {
        name: 'Professor Plum',
        present: true,
        rooms: [
            {kitchen: true},
            {ballroom: false},
            {conservatory: false},
            {'dining room': true},
            {'billiard room': false},
            {library: false}
        ]
    }
];

function notInRoom(suspect) {
  const emptyRooms = _.reduce(suspect.rooms, (room, memo) => {
    if (room === false) {
      memo.push(room);
    }

    return memo;
  }, []);

  return emptyRooms;
}

notInRooms = _.map(newDevelopment, notInRoom);

_.intersection(...notInRooms);
```
