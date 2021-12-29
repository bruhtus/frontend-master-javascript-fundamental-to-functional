# List Transformations

List transformations is one of the core things that we'll be doing in functional
utility method, which is take a list or collection data in different
arrangements and then extract data from them (similar to destructuring, but
also by looping through it and using various logic to get what we need).

## Nested Data Structures

Here's an example of nesting objects:
```javascript
const game = {};

game["suspects"] = [];

// we can use push like this
game.suspects.push({
  name: "Rusty",
  color: "orange"
});

// or the bracket with number like this
game.suspects[1] = {
  name: "Miss Scarlet",
  color: "red"
};

console.log(game["suspects"]);

// the representation of those object is something like this:
// const game = {
//  "suspects": [
//    {
//      name: "Rusty",
//      color: "orange"
//    },
//    {
//      name: "Miss Scarlet",
//      color: "red"
//    }
//  ]
// };
```

## Looping Exercise part 1

Now, our exercise is to loop through the `suspects` array that we've created in
previous section.

We can do that with something like this:
```javascript
const game = {
 "suspects": [
   {
     name: "Rusty",
     color: "orange"
   },
   {
     name: "Miss Scarlet",
     color: "red"
   }
 ]
};

function foo() {
  for (let i = 0; i < game.suspects.length; i++) {
    console.log(game.suspects[i]);
  }
}

foo();
```

- Why do we use this kind of loop with an array? Would we use this with an object?

> This kind of loop referencing to `(let i = 0; i < game.suspects.length; i++)`.
> Array have numerical value associated with them, so they map well onto the
> the way that loop iterate.
>
> That loop has nothing to do with arrays, we have specific for-loop for object
> like this:
> for (let key in obj) {
>   obj[key]
> };

- Why do we need to use brackets in `game.suspects[i]`?

> Because `i` is not a property of the object `game.suspect` so we need brackets
> to evaluate `i` as a variable.

- What's the give away that `i` is a variable?

> `let`.

## Looping Exercise part 2

Next exercise is to loop through all the properties of the `suspects` objects
in the `suspects` array and mark them if we think they're guilty.

We can do that with something like this:
```javascript
const game = {
 "suspects": [
   {
     name: "Rusty",
     color: "orange"
   },
   {
     name: "Miss Scarlet",
     color: "red"
   }
 ]
};

function foo() {
  for (let i = 0; i < game.suspects.length; i++) {
    console.log(game.suspects[i]);
  }
}

function fooLoop() {
  for (let i = 0; i < game.suspects.length; i++) {
    console.log("Outer loop");
    for (let key in game.suspects[i]) {
      console.log("Inner loop");
      // for now we'll assume that it's Rusty because we don't have enough clue.
      if (game.suspects[i][key] === "Rusty") {
        console.log("Found them!");
      } else {
        console.log("Next time!");
      }
    }
  }
}

fooLoop()
```

## Looping Exercise part 3

Next exercise is to destructuring the nested data structure below into two
variables, one variable is contain `red` and another variable contain `orange`:
```javascript
var suspects = [
  {
    name: "Rusty",
    color: "orange"
  },
  {
    name: "Miss Scarlet",
    color: "red"
  }
];

const [{color: firstColor}, {color: secondColor}] = suspects;
console.log(firstColor);
console.log(secondColor);
```
