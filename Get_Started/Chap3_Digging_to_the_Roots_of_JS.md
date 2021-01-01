<h1 align="center">Chapter 3: Digging to the Roots of JS</h1>

- Programs are essentially built to process data and make decisions on that data.
- The patterns used to step through the data have a big impact on the program’s readability.

### Iteration

- The Iterator pattern suggests **standardized** approach to consuming data from a source one chunk at a time.
- The iterator pattern defines a data structure called an **iterator** that has a reference to an underlying data source (like the query result rows), which exposes a method like next() . Calling next() returns the next piece of data (i.e., a “record” or “row” from a database query).
- ES6 standardized a specific protocol for the iterator pattern directly in the language. The protocol defines a [**next()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator/next) method whose return is an object called an *iterator* result; the object has value and done properties, where done is a boolean that is false until the iteration over the underlying data source is complete.
- The `next()` approach is so ES6 also included several APIs for standard consumption of the iterators.

### Consuming Iterators

- `for..of` loop:

```
// given an iterator of some data source:
var it = /* .. */;

// loop over its results one at a time
for (let val of it) {
  console.log(`Iterator value: ${val}`);
}
// Iterator value: ..
// Iterator value: ..
// ..
```

So, as you can notice the above code prints all the iterator values one by one.

- The `...` or **spread** operator can also be used to consume the iterators. For eg:

```
// An Array spread: spread an iterator into an array, 
// with each iterated value occupying an array element position.
var vals = [ ...it ];

// OR

// A function call spread: spread an iterator into a function, 
// call with each iterated value occupying an argument position.
doSomethingUseful( ...it );
```

#### Iterables

- The iterator-consumption protocol is technically defined for **consuming iterables**; an iterable is a value that can be iterated over.
- ES6 defined the basic data structure/collection types in JS as iterables. This includes strings, arrays, maps, sets, and others. 

```
// an array is an iterable
var arr = [10, 20, 30];
for (let val of arr) {
  console.log(`Array value: ${val}`);
}
// Array value: 10
// Array value: 20
// Array value: 30
```
- Since, arrays are iterables we can *`shallow-copy`* them using the `...` operator. For eg:

```
var arrCopy = [ ...arr ];
```

- We can also iterate strings as:

```
var greeting = "Hello world!";
var chars = [...greeting];
chars;
// [ "H", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d", "!" ]
```














