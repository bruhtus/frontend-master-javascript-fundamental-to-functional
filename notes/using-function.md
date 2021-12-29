# Using Functions

What's the function below return?
```javascript
function createSuspectObjects(name) {
  return {
    name: name,
    color: name.split(" ")[1],
    speak: function () {
      console.log("my name is ", name);
    }
  };
}

var suspects = ["Miss Scarlet", "Colonel Mustard", "Mr. White"];
```
with the function above, we're returning an object with three properties:
`name`, `color`, and `speak`.

Next, we'll take a look at this function below:
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
```
now, `speak` is a method inside an object which is an ES6 feature where we
can add method inside an object.

What we wanna do now is, we wanna initialize each suspect into an object.
Basically take a data and turned it into a class or an object.

> In javascript, class is just functions that return objects.

The task is, we want every suspects to have a function. For example, we
type `Miss Scarlet.speak()`, we want it to say "my name is Miss Scarlet".
So, how do we do it? We can do that with for-loop like this:
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

for (let i = 0; i < suspects.length; i++) {
  suspectsList.push(createSuspectObjects(suspects[i]));
};

console.log(suspectsList);
```
