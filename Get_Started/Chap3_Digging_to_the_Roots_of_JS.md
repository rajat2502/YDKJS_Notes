<h1 align="center">Chapter 3: Digging to the Roots of JS</h1>

- Programs are essentially built to process data and make decisions on that data.
- The patterns used to step through the data have a big impact on the program’s readability.

### Iteration

- The Iterator pattern suggests **standardized** approach to consuming data from a source one chunk at a time.
- The iterator pattern defines a data structure called an **iterator** that has a reference to an underlying data source (like the query result rows), which exposes a method like next() . Calling next() returns the next piece of data (i.e., a “record” or “row” from a database query).
- ES6 standardized a specific protocol for the iterator pattern directly in the language. The protocol defines a [**next()**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator/next) method whose return is an object called an *iterator* result; the object has value and done properties, where done is a boolean that is false until the iteration over the underlying data source is complete.
- The `next()` approach is so ES6 also included several APIs for standard consumption of the iterators.

### Consuming Iterators

- 
