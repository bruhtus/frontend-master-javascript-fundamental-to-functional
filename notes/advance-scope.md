# Advance Scope

## Closure

**Closure is a function inside of a function that creates scope isolation**.

A closure happens when we put a functions inside of a function and we can
take advantage of that by returning a function that retains access to its
parent function even after the function inside a parent function has been
executed.

We can use a closure to kind of hide away functionality that we don't want
people to mess with.

Let's say we have `myAlert()` function like this:
```javascript
function myAlert() {
  const x = "Help! I think I found a Clue";

  function alerter() {
    // `alert()` function will pop-up a window.
    alert(x);
  }

  alerter();
}

myAlert();
```

Another example of `myAlert()` function:
```javascript
function myAlert() {
  const x = "Help! I think I found a Clue";

  function alerter() {
    // `alert()` function will pop-up a window.
    alert(x);
  }

  // will run alerter after 1000 seconds.
  setTimeout(alerter, 1000);
  console.log("What happens first? This log or alert pop-up?")
  // spoiler: the log first.
}

myAlert();
```

Another example of `myAlert()` function:
```javascript
function myAlert() {
  const x = "Help! I think I found a Clue";
  let count = 0;

  function alerter() {
    // `alert()` function will pop-up a window.
    alert(`${x} ${++count}`);
  }

  // return the function body, not running the function.
  return alerter;
}

// save the result of `myAlert()` function in `funcAlert`.
const funcAlert = myAlert();

// save the result of `myAlert()` function in `funcAlert2`.
const funcAlert2 = myAlert();

funcAlert();
// this will show a pop-up window with output 'Help! I think I found a clue'.
```

Now, what happens if we call `funcAlert()` again like this:
```javascript
function myAlert() {
  const x = "Help! I think I found a Clue";
  let count = 0;

  function alerter() {
    // `alert()` function will pop-up a window.
    alert(`${x} ${++count}`);
  }

  // return the function body, not running the function.
  return alerter;
}

// save the result of `myAlert()` function in `funcAlert`.
const funcAlert = myAlert();

// save the result of `myAlert()` function in `funcAlert2`.
const funcAlert2 = myAlert();

funcAlert();
funcAlert();
```

Does that start again? or Does that keep adding?

So, when we call `myAlert()` function, we created one execution context. And
then when we call `funcAlert()`, we're creating some child execution context
(which is `alerter()`) but we're not re-creating the parent execution context.
Which means we're actually retaining access to count.

If we called the `funcAlert2()` like this:
```javascript
function myAlert() {
  const x = "Help! I think I found a Clue";
  let count = 0;

  function alerter() {
    // `alert()` function will pop-up a window.
    alert(`${x} ${++count}`);
  }

  // return the function body, not running the function.
  return alerter;
}

// save the result of `myAlert()` function in `funcAlert`.
const funcAlert = myAlert();

// save the result of `myAlert()` function in `funcAlert2`.
const funcAlert2 = myAlert();

funcAlert();
funcAlert();

funcAlert2();
```

That will start the count at `1` because we're initializing a new `myAlert()`.
`funcAlert` and `funcAlert2` is separate.

### Closure Demonstration

Here's the example for closure:
```javascript
function newClue(name) {
  const length = name.length;

  // we return a function here.
  return function (weapon) {
    let clue = length + weapon.length;
    // this will return truthy.
    return !!(clue % 2);
  };
}

// we passed the name here.
const didGreenDoItWithA = newClue('Green');

// this will return a function that expecting a `weapon`.
didGreenDoItWithA;

// we passed the weapon name here.
didGreenDoItWithA('candlestick');
```

Another example:
```javascript
function countClues() {
  var n = 0;

  // return an object that has a two function in it.
  return {
    count: function () { return ++n; },
    reset: function () { return n = 0; }
  };
}

// initialize `counter` with the object that has two function in it.
const counter = countClues();

// initialize `counter2` with the object that has two function in it.
const counter2 = countClues();

// the output is `1`.
counter.count();

// the output is `2`.
counter.count();

// the output is `3`.
counter.count();
// and keep going.

// the output is `1`.
counter2.count();
// it's different instance of `countClues()` function.
```

Another usual example:
```Javascript
function makeTimer() {
  console.log('initialized');

  let elapsed = 0;
  console.log(elapsed);

  function stopwatch() {
    console.log('stopwatch');
    return elapsed;
  }

  function increase() {
    return elapsed++;
  }

  // keep running every 1000 ms.
  setInterval(increase, 1000);

  return stopwatch;
}

// initialize `timer`.
let timer = makeTimer();

// check what `timer` holds.
timer;

// call `timer`.
timer();
```

### Closure Recipe

#### Create a Closure

> This is just the general guide, closure come in different ways.

1. Create a parent function.
2. Define some variables in parent scope that can be accessed by child
function.
3. Define a function inside parent function.
4. Return that function from inside the parent function.

#### Execution of Closure

1. Call the parent function and save it to a variable because it's returning
a function that we'll call later.
2. [Optional] Check what that variable holds as its value.
3. Call that variable.
