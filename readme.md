# JavaScript: From Fundamentals to Functional JS, v2

> If it feels uncomfortable as the difficulty ramps up, that's good.
> That's where we we want to be. Just stick with it and see what's happens.
>
> Figure out what's missing and figure out how to measure our learning.
> "How do we know that we're learning".

> They say functional programming is about verbs (actions), and object-oriented
> programming is about the nouns (objects).
>
> If we're gonna build a house, in object-oriented programming, we would talk
> about the walls, doors, and windows. In functional programming, we'll talk
> about opening, closing, and applying material of the house.
>
> One of the core of functional programming is making pure function that
> doesn't have side effects, and in doing that make our code is a lot easier to
> test. That's one of the benefits over object-oriented programming.

## Contents

- [Objects and Arrays](./notes/object-array.md).
- [List Transformations](./notes/list-transformation.md).
- [Using Function](./notes/using-function.md)
- [forEach Function](./notes/foreach-function.md).
- [map Function](./notes/map-function.md).
- [filter Function](./notes/filter-function.md).
- [Function In-depth](./notes/function-in-depth.md).
- [ES6 Arrow Function](./notes/es6-arrow-function.md).
- [Spread Operator](./notes/spread-operator.md).
- [Arguments Keyword](./notes/arguments-keyword.md).
- [Default Parameters](./notes/default-parameters.md).
- [Array-like Object](./notes/array-like-object.md).
- [Scope](./notes/scope.md).
- [Higher-order Functions and Callbacks](./notes/higher-order-functions-and-callbacks.md).
- [Functional Utilities](./notes/functional-utilities.md).
- [Advance Scope](./notes/advance-scope.md).

## Extra Notes

- We can either change data or we can share data, but don't do both.

- Knowing how to read the documentation is important.

- We can put `debugger;` when running code in browser console, to stop
the code and open the debugging interface. Here's an example:
```javascript
const constructArr = function () {
  debugger;
  const arr = Array.from(arguments);

  arr.push('the billiards room?');
  return arr.join(' ');
};

constructArr('was', 'it', 'in');
```

- Functions are also objects.

- The appropriate time to use `let` is when we want to scope our variable
inside of a block that's not a function. But `var` do some funny thing
with hoisting (search for `javascript hoisting`), and `let` supposed to fix
that.

## Q&A

- What would happened to `person[plea]` if we skip `var plea = "wouldShe"`?

> It'll evaluate what's in the brackets first, and then it'll say `plea` is
> a variable (because there's no quotes around it or anything like that, and
> it's not a number). So, first it'll look in the scope for variable and
> look into any scope for a variable, and look into any scopes that it's
> connected to, and find that there's no plea.

- Can we put a function inside array brackets like `obj[function(){}] = false`?

> Yes we could, but it'll stringify that function. If we use
> `typeof Object.keys(obj)[0]`, it'll return `"string"`. So we can't call the
> function inside the brackets. And that's why it's not recommended to put a
> function inside brackets.
>
> But, if we call the function directly like this
> `obj[(function(){ return 3; })()] = false`, that means the function will
> return `3` and the brackets will evaluate `3`.

- What is the difference between arrays and objects?

> An array is a special kind of object, and the most special thing about array
> is the `.length` property which is a property that is computed as you add
> numerical index, and numerical index are different than properties on an
> array because an array captures that and will increment the length.
>
> Here's an example, let's say we add to and array (don't forget to defined x
> with something like `var x = [];`) `x["0"] = true;`. If we use
> `console.log(x.length);`, the result would be `1`, but if we do something
> like this `x.hello = "world"` and do `console.log(x.length)` again, it'll
> still return `1`.
>
> There's a special behavior for arrays with numerical index and there's method
> that we can use to take advantage of this.

- When are we creating an object and when are we creating properties?

> Whenever we create or assign a variable, it's always gonna be on the left like
> `var x = y;` and not `x = var y` or something. So, that's the hint.

- What is something that we want to consider when we're implementing `map`
instead of `each`?

> `map` return an array, so we only need to have a `return` statement at the end
> of the callback function.

## References

- [Frontend master course javascript fundamentals](https://frontendmasters.com/courses/js-fundamentals-functional-v2/).
- [Frontend master course javascript fundamentals slide day 1](https://slides.com/bgando/f2f-final-day-1).
- [Frontend master course javascript fundamentals slide day 2](https://slides.com/bgando/f2f-final-day-2).
- [Check property name in javascript](https://stackoverflow.com/a/23614729).
- [To test the javascript output (jsbin)](https://jsbin.com/nohorekoha/edit?js,console).
- [Javascript hoisting](https://www.geeksforgeeks.org/javascript-hoisting/).
