# Objects and Arrays

## Assignment with Dots

An example:
```javascript
// this syntax
var person = {};
person.name = "Mrs. White";

// equivalent to this syntax
var person = {
  "name": "Mrs. White"
};
```

**Anything that ever use a dot in javascript is an object**.

Another example:
```javascript
var person = {};
person.name = "Mrs. White";
person.name; // this is gonna evaluate to a string that says Mrs. White.
// assignment will only happen if we explicitly do it with `=` (equal sign),
// otherwise it's a lookup.
```

## Access with Dots

One thing that can be a little bit confusing is about how our data is stored in
memory. It's pretty simple when we have a variable and we're storing a value
like this:
```javascript
var person = {};
person.name = "Mrs. White";
var who = person.name;
console.log(who)
```

the `who` variable is assigned to `"Mrs. White"`. Now, what happen if we
reassign `person.name` to "Mr. White" like this:
```javascript
var person = {};
person.name = "Mrs. White";
var who = person.name;
console.log(who);

person.name = "Mr.White";
console.log(who);
```

The `person.name` would be `"Mr. White"` but the `who` is still `"Mrs. White"`.
That was because `person.name` use primitive value.

> A primitive value is:
> - a string
> - a number
> - a boolean
> - a boolean
> - a null
> - a undefined
>
> A non-primitive value is:
> - an object
> - an array
> - a function
> - a promise

**Primitive value get pass by value, while non-primitive value get pass by
reference. So we have these pointers in memory for objects**.

> What it means to have a pointers in memory for objects?
>
> That means, if we have pass a primitive value, it gets its own spot in memory
> every single time. While with functions and objects, we're often sharing the
> same place in memory. So if changing the functions or objects, that can effect
> things in unusual ways if we are not planning for that.
>
> Basically if we pass a non-primitive value, we're not making a copy of that
> value, we're just use those value as a reference (or making a pointer). The
> non-primitive value is just sharing the instance of their objects or
> functions.
>
> If we expect the primitive value and non-primitive value to have the same
> behavior, we're gonna have something that we don't expect.
>
> It's recommended that we don't mutate our data structure and just copy them,
> then return the new copy. So that we don't have a side effect of our code
> being updated in various places.

**Mutating just means updating and changing, and then immutable means that we
can't update or change it**.

Now, what would happen if we do something like this:
```javascript
var person = {};
person.name = "Mrs. White";
var who = person.name;

person.name = "Mr.White";
who.story;
```

That will return `undefined` because we haven't defined it anywhere.

Now, what if the person is an array, like this:
```javascript
var person = [];
person.name = "Mrs. White";

var who = person.name;
console.log(who);
```

The output is still `"Mrs. White"`. Arrays are objects and because of that,
the rules are exactly the same.

**The reason that we used brackets is not because it's an array, but we also
used brackets with objects**.

Another example, what is the result of this:
```javascript
var person = [];
person.name = "Mrs. White";

var who = person.name;
console.log(who);

console.log(typeof person === "array");
```

The result is `false`, but if we use `object` instead of `array` like this:
```javascript
var person = [];
person.name = "Mrs. White";

var who = person.name;
console.log(who);

console.log(typeof person === "object");
```

The result is `true`.

> If you're surprised by this, is because people have been lying to you.

**Arrays are just objects, the only difference is that the arrays have some
methods on them (`array.push()`, `array.pop()`, `array.length`)**.

> If you're storing an array of functions, you're probably doing something
> wrong but it's possible.

We can also do something like this:
```javascript
var person = [];
person.name = "Mrs. White";

var who = person.name;

// add to the object with square brackets.
person[0] = "I was not in the Billiard room";

console.log(person.name);
console.log(person[0]);
```

In the example above, zero (0) is just a property. But, why can't we do
something like this `person.0`? Because it's not a string and that's why we
use brackets.

> We can only use dot notation with character that are not unusual. What unusual
> means, can we create a variable name starting with that character or contains
> that character? If we use a character that's unusual, we might get a syntax
> error.

Basically we use the brackets when we can't use the dot, but when we can't use
the dot? Pretty much when the value is not supposed to be a string literal.

For example, the property name of `person.name` is `name` which is a valid
variable name. Basically if it's a valid variable name, it probably could
be used with a dot notation. If it's not, then it gets caught up in our parser.

Now, what about this:
```javascript
var person = [];

person.name = "Mrs. White";
person[plea] = "I would never!";
console.log(person[plea]);
```

That will give an error.

**When we use the brackets, we don't assume that it's a string. So, it could be
a variable name, it could be an expression, we could also call a function (not
a good idea but still valid)**.

To fix the error, we can do define the `plea` with something like this:
```javascript
var person = [];
var plea = "wouldShe";

person.name = "Mrs. White";
person[plea] = "I would never!";
console.log(person[plea]);
```

If we take a look at the property with this:
```javascript
console.log(Object.keys(person));
```

We'll notice that all the property name would be like this:
```sh
# `name` is the property name of `person.name`.
# `wouldShe` is the property name of `plea`.
["name", "wouldShe"]
```

Notice that the property name is `wouldShe` instead of `plea`. If we want it to
be `plea`, what might we need to change? Put a quote around `plea` like this:
```javascript
var person = [];
var plea = "wouldShe";

person.name = "Mrs. White";
person["plea"] = "I would never!";
console.log(Object.keys(person));
```

and the results would be something like this:
```sh
["name", "plea"]
```

If we create something with a brackets, can we look it up with a dot like this:
```javascript
var person = [];
var plea = "wouldShe";

person.name = "Mrs. White";
person["plea"] = "I would never!";
console.log(person.plea);
```

The answer is yes, we can look it up `person["plea"]` with `person.plea` and
the result would be something like this:
```sh
# similar when we use `console.log(person["plea"]);`
"I would never!"
```

## Invalid Character

**A piece of advice, just try not to use invalid character as property names**.

An example of using invalid character:
```javascript
var box = {};

box["material"] = "cardboard";
box[0] = "meow";

// basically don't forget to put the quote.
box["^&*"] = "nanimo";

var test = box["^&*"];
```

We can also put anything that can be evaluated in the brackets like this:
```javascript
var x = {};
x[2 + 2] = true;
console.log(x);
```

and the result would be something like this:
```javascript
[object Object] {
  4: true
}
```

And that's why we don't need to put quotes around `0` in `box[0]` above,
because it's seeing that as something that need to be evaluated rather than
something that need to be coerced directly into a string.

## Game Characters Exercise

We're going to create a Clue game and represent it as an object in array.

The data for Clue game (Clue game is a board game):
- Characters.
- Weapons.
- Rooms.

> I have no idea what Clue game is.

Here's the solution:
```javascript
var game = {};

game.murderer = "??";

// in this case, why would we choose an array instead of an object?
// because of the structure of the data, since this is a collection
// of things that are the same, which is a weapons.
game["weapons"] = ["lasers", "angry cats", "dish soap"];

// we can also make an array of objects.
// an object has a key an value.
// property name and key is the same thing.
// make a property name or a key that is consistent among our objects.
// consistent property name or key make it easier to organize our data
// (we don't have to remember the specific things that stored there).
game["weapons"] = [
  {type: "lasers", location: "lab"},
  {type: "angry cats", location: "garden"},
  {type: "dish soap", location: "kitchen"}
];

game.name = [];
game.name[0] = "Miss Scarlet";
// we can't push to an object, we can only push to an array
// `.push()` means to put the content in the back of array,
// basically append the array content.
// the result would be ["Miss Scarlet", "Mr. Green"].
game.name.push("Mr. Green");
```

## Object Review

Type             | Dots | Brackets |
--               | --   | --       |
strings          | yes  | yes      |
numbers          | no   | yes      |
quotations       | no   | yes      |
variables        | no   | yes      |
weird characters | no   | yes      |
expressions      | no   | yes      |

## ES6 Destructuring (Objects and Arrays)

Two things that we need to talk about when we are thinking about destructuring
objects and arrays is:
- The target.
- The source.

**Destructuring is a simplified way of defining variables and taking them
outside of an object or an array**.

### Array

An example of array destructuring of a variable declaration:
```javascript
// the name doesn't have anything to do with the order.
const [second, first] = [true, false];

// we can also do this
// let [second, first] = [true, false];

// or this
// var [second, first] = [true, false];

console.log(first);
console.log(second);
```

When we have more variable on the left than the array item on the right like
this:
```javascript
const [second, first, third] = [true, false];
console.log(first);
console.log(second);
console.log(third);
```
the result of `third` would be `undefined`, while the result of `first` and
`second` respectively would be `false` and `true`.

#### Const

**We use `const` when we don't want the variable name to be reassigned to
something else (it'll throw an error if we reassign the same variable)**.

Let's say we assigned the value of `c` like this:
```javascript
const c = 3;
```
and then we try to reassigned the variable `c` to another value like this:
```javascript
c = 69;
```
that will throw an error because we can't reassigned the variable `c` because
we use `const`.

Now, what happen if we do something like this:
```javascript
const j = { x: 1 };
j.x = 3
console.log(j.x);
```
That won't throw an error and the output is `3`. Why can we do that? It's
because we didn't reassigned the variable `j`, we're just reassigned the
property name `x` on `j`. With that in mind, we can still add new property
on `j` like this:
```javascript
j.y = 69;
```
but what we can't do is assign `j` to different object like this:
```javascript
j = { x: 69 };
```
that will throw an error.

#### Let

**We use `let` when we want the variable name to be reassigned to
something else, but `let` has implication for its scope**.

### Object

An example of object destructuring of a variable declaration:
```javascript
// the name have to match the variable because object don't have an order.
// but the order of the variable (on the left) is not matter.
const {second, first} = {first: 0, second: 1};

// we can also do something like this
// let {first, second} = {first: 0, second: 1};

// and this
// var {first, second} = {first: 0, second: 1};

console.log(first);
console.log(second);
```

> When ever we start thinking objects have an order or should have an order,
> we should be using an array. And if we expecting an order from an object,
> that's a bad expectation because it's not guaranteed.

## Destructuring Challenge

The challenge is:
1. Create an object that looks like this:
```json
{ "name": "Rusty", "room": "kitchen", "weapon": "candlestick" }
```

2. Extract the weapon and room using destructuring technique.

### Destructuring Challenge Solution

1. Create an object:

```javascript
// this is basically equivalent to
// const obj = { "name": "Rusty", "room": "kitchen", "weapon": "candlestick" };
// const name = obj.name;
// const room = obj.room;
// const weapon = obj.weapon;
const obj = {
  "name": "Rusty",
  "room": "kitchen",
  "weapon": "candlestick"
};
console.log(obj);
```

2. Extract the weapon and room using destructuring technique:

```javascript
const { name, weapon } = obj;
console.log(name);
console.log(weapon);
```

### Destructuring Examples

1. Destructuring an array

```javascript
var [a, b] = [1, 2];
console.log(a, b);
// 1
// 2
```

2. Omit certain values in array

```javascript
var [a, ,b] = [1, 2, 3];
console.log(a, b);
// 1
// 3
```

3. Combine with spread operator (accumulates the rest of values) in array

```javascript
var [a, ...b] = [1, 2, 3];
console.log(a, b);
// 1
// [2, 3]
```

4. Swap variables without temp in array

```javascript
var a = 1, b = 2;
[b, a] = [a, b];
console.log(a, b);
// 2
// 1
```

5. Advantage deep arrays

```javascript
// make a nested array is not recommended, unless we make tree data
// structure or something like that.
// we better off use nested object instead of nested array.
var [a, [b, [c, d]]] = [1, [2, [[[3, 4], 5], 6]]];
console.log("a:", a, "b:", b, "c:", c, "d:", d);
// "a:"
// 1
// "b:"
// 2
// "c:"
// [[3, 4], 5]
// "d:"
// 6
```

6. Destructuring an object

```javascript
var {user: x} = {user: 69};
console.log(x);
// 69
```

7. Fail-save destructuring an object

```javascript
var {user: x} = {user1: 69};
console.log(x);
// undefined
```
