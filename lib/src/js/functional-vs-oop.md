# Functional vs Object oriented programming

## Functional concepts

### Pure functions
* No side effects.
* Given an input, produce same output.
* Do not mutate or use any external data that lives outside the function. e.g. mutating a global var or `window` object.

```
var num = 1;

// Pure function
function pure(a, b) {
  return a + b;
}

// Impure function
function impure(a) {
  a = a + 1; // mutates arguments
  var c = num + a; // uses external data
  num = 2; // mutates external data
}

```

### Immutable data
* Functional code is considered stateless. Mutuating data breaks this promise.
* Never mutate existing data, instead use functions to create new instances from existing ones, thus keeping the `state` of your program `pure`.
* Use JS functionality like `const`, `Object.freeze` to lock primitives, arrays and objects.

```
// Impure 
const arr = [1, 2, 3, 4];
arr.push(5); // mutating original data
const obj = { num: 1 };
obj['foo'] = 'joe'; 
```

```
// Pure
const data = Object.freeze([1,2,3]);

// Define pure functions to compute new data
function addOne = (val) => val + 1;

// Use JS APIs like `map` and pass functions as arguments to compute new data without mutating existing one
const newData = data.map(addOne);
```

### Functions as Arguments
* Ability to pass functions as arguments allows us to calculate new data or work on data without repeating code

```
const data = Object.freeze([1,2,3]);

// Define pure functions to compute new data
function addOne = (val) => val + 1;

// Use JS APIs like `map` and pass functions as arguments to compute new data without mutating existing one
const newData = data.map(addOne);
```

### Functions as return values
* Functions can be returned as a return value.
* Returned functions trap in-memory stack frames as 

```
const appendWeatherEmoji = (fixed) => (dynamic) => fixed + dynamic; // same as `function(fixed) { return function(dynamic) { return fixed + dynamic; } }`
const rain = appendWeatherEmoji(':-(');
const sun = appendWeatherEmoji(':-)');

console.log(rain('today')); // `:-( today`
```


## References

* https://probablydance.com/2016/02/27/functional-programming-is-not-popular-because-it-is-weird/