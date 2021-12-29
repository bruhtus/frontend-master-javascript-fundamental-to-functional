# ES6 Arrow Functions

Example of ES6 arrow functions:
```javascript
var nameImprover = (name, adj) => {
  return `Col ${name} Mc ${adj} pants`;
};

$('body').hide();

// we don't have to wrap our parameters in parentheses if it's only one.
// if the function body only has one line, we don't need to put it in brackets.
myArr.forEach(val => console.log(val));

$('button').on('click', () => {
  console.log('Don\'t press my button!');
});
```

Arrow functions do not have their own value for `this` and they inherit the
value `this` from the parent scope. Another thing is that, arrow functions
doesn't have it's own value for the arguments keyword.

Another thing is that, arrow function doesn't have its own value for the
arguments keyword. So the arguments keyword, at call time, gets bound to all
the arguments that are being passed into the function.

> If we're trying to return something from an arrow function, just write an
> explicit `return` sometimes arrow function will return something and the other
> times it won't. That has something to do with whether or not something is a
> statement and we have to understand deeply what a statement is and that's
> complicated.

## Projecting Exercise

**Projecting is basically when we take a value out of data structure and turn it
into another data structure and turn it into another data structure**.

The data structure:
```javascript
const videoData = [
    {
        name: 'Miss Scarlet',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Mrs. White',
        present: false,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Reverend Green',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Rusty',
        present: false,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Colonel Mustard',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Professor Plum',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    }
];
```

The task is filter and then map the data structure above to get the names
of the final suspects to send back to the team.

### Projecting Exercise Solution

```javascript
const videoData = [
    {
        name: 'Miss Scarlet',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Mrs. White',
        present: false,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Reverend Green',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Rusty',
        present: false,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Colonel Mustard',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    },
    {
        name: 'Professor Plum',
        present: true,
        rooms: [
            {kitchen: false},
            {ballroom: false},
            {conservatory: false},
            {'dining room': false},
            {'billiard room': false},
            {library: false}
        ]
    }
];

const _ = {};

_.filter =  (arr, callback) => {
  const storage = [];

  for (let i = 0; i < arr.length; i++) {
    if (callback(arr[i], i, arr) === true) {
      storage.push(arr[i]);
    }
  }

  return storage;
}

_.map = function (list, callback) {
  let storage = [];

  for (let i = 0; i < list.length; i++) {
    storage.push(callback(list[i], i, list));
  }

  return storage;
}

const suspects = _.filter(videoData, (suspectObject) => {
  return suspectObject.present;
});

const suspectsName = _.map(suspects, suspect => {
  return suspect.name;
});

console.log(suspectsName);
```
