<h1 align="center">Chapter 3: Digging to the Roots of JS</h1>

- Programs are essentially built to process data and make decisions on that data.
- The patterns used to step through the data have a big impact on the program’s readability.

## Iteration

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

#### Map

- A Map data structure uses objects as keys, associating a value (of any type) with that object.

```
// given two DOM elements, `btn1` and `btn2`
var buttonNames = new Map();
buttonNames.set(btn1, "Button 1");
buttonNames.set(btn2, "Button 2");

for (let [btn, btnName] of buttonNames) {
  btn.addEventListener("click", function onClick() {
    console.log(`Clicked ${btnName}`);
  });
}
```

- In the `for..of` loop over syntax (called the default map iteration, we use the **[btn,btnName]** ("*array destructuring*") to break down each consumed tuple into the respective key/value pairs ( btn1 / "Button 1" and btn2 / "Button 2" ).
- We can call `values()` to get a values-only iterator:

```
for (let btnName of buttonNames.values()) {
  console.log(btnName);
}
// Button 1
// Button 2
```

- Or if we want the index and value in an array iteration, we can make an entries iterator with the entries() method:

```
var arr = [10, 20, 30];
for (let [idx, val] of arr.entries()) {
  console.log(`[${idx}]: ${val}`);
}
// [0]: 10
// [1]: 20
// [2]: 30
```

- For the most part, All built-in iterables in JS have three iterator forms available: **keys-only** ( keys() ), **values-only** ( values() ), and **entries** ( entries() ).

## Closure

- Closure is when a function remembers and continues to access variables from outside its scope, even when the function is executed in a different scope.
- Closure is part of the nature of a function. Objects don’t get closures, functions do.
- To observe a closure, you must execute a function in a different scope than where that function was originally defined.

```
function greeting(msg) {
  return function who(name) {
    console.log(`${msg}, ${name}!`);
  };
}

var hello = greeting("Hello");
var howdy = greeting("Howdy");

hello("Kyle");
// Hello, Kyle!
hello("Sarah");
// Hello, Sarah!
howdy("Grant");
// Howdy, Grant!
```

- First the `greeting(..)` outer function is executed, creating an instance of the inner function `who(..)`, that function closes over the variable `msg`. The instance of the inner function is assigned to the variables named `hello` and `howdy` respectively.
- Since the inner function instances are still alive (assigned to hello and howdy , respectively), their closures are still preserving the `msg` variables.
- These closures are not snapshots but actual variables. Hence, we can make changes to it using the inner function. 

```
function counter(step = 1) {
  var count = 0;
  return function increaseCount() {
    count = count + step;
    return count;
  };
}

var incBy1 = counter(1);

incBy1(); // 1
incBy1(); // 2
```

**Note**: It’s not necessary that the outer scope be a function—it usually is, but not always—just that there be at least one variable in an outer scope accessed from an inner function:

```
for (let [idx, btn] of buttons.entries()) {
  btn.addEventListener("click", function onClick() {
    console.log(`Clicked on button (${idx})!`);
  });
}
```

## this Keyword

- **Scope** is static and contains a fixed set of variables available at the moment and location you define a function.
- **Execution Context** is dynamic, entirely dependent on how it is called (regardless of where it is defined or even called from).
- `this` is not a static/fixed characteristic of function, it is defined each time the function is called.

```
function classroom(teacher) {
  return function study() {
    console.log(`${teacher} says to study ${this.topic}`);
  };
}
var assignment = classroom("Kyle");
```
The outer `classroom(..)` function makes no reference to a `this` keyword, so it’s just like any other function we’ve seen so far. But the inner `study()` function does reference `this` , which makes it a *this-aware* function. In other words, it’s a function that is dependent on its execution context.

- Since no `topic` was defined in the `global` object, calling `assignment()` prints:

```
assignment()
// Kyle says to study undefined
```

Now consider:

```
var homework = {
  topic: "JS",
  assignment: assignment,
};
homework.assignment();
// Kyle says to study JS
```

Here, the this for that function call will be the `homework` object. Hence, `this.topic` resolves to "JS" in this case.

**Note**: The benefit of `this-aware` functions and their *dynamic context* is the ability to more flexibly re-use a single function with data from different objects.

## Prototypes

- A prototype is a characteristic of an object.
- The prototype can be thought of as a linkage between two objects and this linkage occurs when an object is created.
- A series of objects linked together via prototypes is called the **prototype chain.**
- The purpose of this prototype linkage (i.e., from an object B to another object A) is so that accesses against B for properties/methods that B does not have, are delegated to A to handle.

```
var homework = {
  topic: "JS",
};
```

- The `homework` object has only a single property, however its default prototype linkage connects to the `Object.prototype` object, which has common built-in methods on it like `toString()`, `valueOf()`, etc. For eg:

```
homework.toString();
// [object Object]
```

### Object Linkage

- To define Object prototype linkage, create the object using the `Object.create(..)`:

```
var homework = {
  topic: "JS",
};

var otherHomework = Object.create(homework);
otherHomework.topic;
// "JS"
```

- The figure shows how the objects are linked in a prototype chain:
<img align="center" src="https://user-images.githubusercontent.com/42200276/103455627-abaf2900-4d14-11eb-83a2-8fce05e477b6.png" />

**Tip**: `Object.create(null)` creates an object that is not prototype linked anywhere, so it’s purely just a standalone object; in some circumstances, that may be preferable.

**Note**: 
```
homework.topic;
// "JS"
otherHomework.topic;
// "JS"

otherHomework.topic = "Math";
otherHomework.topic; // "Math"

homework.topic;
// "JS" -- not "Math"
```
The assignment to `topic` creates a property of that name directly on `otherHomework`; there’s no effect on the `topic` property on `homework`.


### this Revisited

























