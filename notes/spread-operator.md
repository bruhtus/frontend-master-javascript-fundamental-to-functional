# Spread Operator

What the snippet below gonna return?
```javascript
const createTuple = (a, b, c, d) => {
  return [[a, c], [b, d]];
};

createTuple('It', 'be', 'could', 'anyone', 'no one');
```

That snippet returns
```javascript
['It', 'could']
['be', 'anyone']
```

> Something to note, we passed `no one` into `createTuple` function, but that
> wasn't picked up because we don't have a variable name that maps to that
> directly (we only give 4 parameters in `createTuple` function but we give
> 5 arguments for `createTuple` function).

Now, here's the spread operator:
```javascript
const createTuple = (a, b, c, ...d) => {
  return [[a, c], [b, d]];
};

createTuple('It', 'be', 'could', 'anyone', 'no one');
```

The snippet above will return:
```javascript
['It', 'could']
['be', ['anyone', 'no one']]
```
