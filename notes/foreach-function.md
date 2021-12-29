# forEach Function

Now, we're going to implement looping with `_.each`. Below is an example
of `_.each`:
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

_.each(suspects, function (name) {
  suspectsList.push(createSuspectObjects(name));
});
```
`_.each` take two arguments, the first argument is a list, and the second
argument is a callback function (we also call this the iterator function).

> We call it the iterator function because iterator is related to things that
> can be looped through.

Basically callback function in `_.each` is gonna called on each item on the list
`suspects`.

Definition of `_.each()` or `forEach`:
- Iterates over a list of elements, passing the values to a function.
- Each invocation of `iterator`, which is the function, is called with three
arguments: `element`, `index`, `list`. If `list` is a javascript object,
`iterator`'s argument will be `value`, `key`, and `list`.

Overview:
```javascript
_.each(
  ["observatory", "ballroom", "library"],
  function (value, index, list){...}
);

["observatory", "ballroom", "library"].forEach(
  function (value, index, list){...}
)
```

> We're kind of abstracting a loop into a function. So instead of using our
> for-loop, we're using `each` and `each` is a function.
>
> The reason we want to do that is because it prevents errors and more readable
> (is tho? hmm).
>
> The reason we implementing `_.each()` before is because using `.forEach()` might
> be a lot harder to write than just passing two arguments. Because once we put
> `.forEach()` means that the method on the array and for it to be a method on
> array, we have to get into prototype and object and object oriented stuff which
> is beyond the scope of this course.

- What is `each` in `_.each()` do?

> Looping through list.

- What is the difference between `forEach()` and `_.each()`?

> `forEach()` is called on array itself, while `_.each()` is taking the array as
> argument.

- What is the underscore in `_.each()` means?

> That's the underscore library.

> `_` is an object, how do we know it's an object? Because it has a dot in it.

## `forEach()` and `_.each()` Exercise

Complete the rest of the function below so that it works as described in
previous section:
```javascript
const _ = {};
let nickname_list = ["Sally", "Georgie", "Porgie"];

function foo(name, i, list) {
  if (list[i + 1]) {
    console.log(name, "is younger than", list[i + 1]);
  } else {
    console.log(name, "is the oldest");
  }
}

_.each = function (list, callback) {
  // TODO
}

_.each(nickname_list, foo);
```

## `forEach()` and `_.each()` Exercise Solution

```javascript
const _ = {};
let nickname_list = ["Sally", "Georgie", "Porgie"];

function foo(name, i, list) {
  if (list[i + 1]) {
    console.log(name, "is younger than", list[i + 1]);
  } else {
    console.log(name, "is the oldest");
  }
}

_.each = function (list, callback) {
  if (Array.isArray(list)) {
    // loop through array
    for (let i = 0; i < list.length; i++) {
      callback(list[i], i, list);
    }

  } else {
    // loop through object
    for (let key in list) {
      callback(list[key], key, list);
    }
  }
}

_.each(nickname_list, foo);
```
