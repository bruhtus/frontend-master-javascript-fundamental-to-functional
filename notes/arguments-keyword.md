# Arguments Keyword

Before the spread operator, we had to rely on this arguments keyword to do stuff
like that. Below is the example of arguments keyword:
```javascript
const createTuple = (a, b, c, d) => {
  console.log(arguments);
  return [[a, c], [b, d]];
};

createTuple('It', 'be', 'could', 'anyone', 'no one');
```

The snippet above will throw an error because arrow function doesn't have an
arguments and it's not gonna work as intended.

> So what arguments keyword do is referencing all the arguments as pseudo array.
> Pseudo array is an object that looks like an array but it's actually an
> object.  That means we don't have access to our handy array methods such as
> `.push()`, `.pop()`, `.forEach()`, `.slice()`, and stuff like that.

Now, let's try with the `function` keyword instead of arrow function:
```javascript
const createTuple = function (a, b, c, d) {
  console.log(arguments);
  // ['It', 'be', 'could', 'anyone', 'no one']
  return [[a, c], [b, d]];
};

createTuple('It', 'be', 'could', 'anyone', 'no one');
```

**The `arguments` keyword only has anything to do with what is passed on the
function**.
