# Default Parameters

Below is an example of default parameters:
```JavaScript
const add = function (a, b = 2) {
  return a + b;
}

add(3);
```

Basically if we didn't pass the argument for a parameter in a function, then
the parameter will use the default argument.

Like the example above, we didn't pass an argument for `b` parameters in `add()`
function, so `add()` function will use `2` as argument for `b` parameters and
the result would be `5`.

If we pass the argument for `b` parameters like this:
```javascript
const add = function (a, b = 2) {
  return a + b;
}

add(3, 66);
```
the result would be `69` because `b` use `66` as an argument instead of `2`.

> Keep in mind that `arguments` keyword is only paying attention to the
> explicit values being passed into the function. So `arguments` keyword
> doesn't tell us about the parameters of a function, only the arguments
> that being passed to the function.

## ES5 Rewrite Exercise

How do we set a default parameter like below before this feature was available?
```javascript
const add = function (a, b = 2) {
  return a + b;
}

add(3);
```

### ES5 Rewrite Exercise Solution

```javascript
const add = function (a, b) {
  // if there's argument for b, then use that value.
  // if not, use 2 as value.
  b = b || 2;
  return a + b;
}

add(3);
```
