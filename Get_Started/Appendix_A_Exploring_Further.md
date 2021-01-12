<h1 align="center">Appendix A: Exploring Further</h1>

## Values vs. References

- In [Chapter 2: Surveying JS](https://dev.to/rajat2502/you-don-t-know-js-get-started-chapter-2-surveying-js-notes-h85), we discussed about the different kinds of values: `primitives` and `objects`.

#### Reference
References are the idea that two or more variables are pointing at the same value, such that modifying this shared value would be reflected by an access via any of those references.

- In many languages, the developer can choose between assigning/passing a value as the value itself, or as a reference to the value. 
- In JS, however, this decision is entirely determined by the kind of value.

**Note:** Primitive values are always assigned/passed as value copies. For eg:

```
var myName = "Kyle";
var yourName = myName;

myName = "Frank";

console.log(myName);
// Frank
console.log(yourName);
// Kyle
```

- As you can notice, `yourName` wasn’t affected by the re-assignment of `myName` to "Frank", as they both hold different copies.

**Note:** Object values (arrays, objects, functions, etc.) are treated as references. For eg:

```
var myAddress = {
  street: "123 JS Blvd",
  city: "Austin",
  state: "TX",
};

var yourAddress = myAddress;
// I've got to move to a new house!

myAddress.street = "456 TS Ave";

console.log(yourAddress.street);
// 456 TS Ave
```

- Because the value assigned to myAddress is an object, it’s held/assigned by reference, and thus the assignment to the yourAddress variable is a copy of the reference, not the object value itself. That’s why the updated value assigned to the myAddress.street is reflected when we access yourAddress.street.


## So Many Function Forms

- Recall this snippet from [Chapter 2: Surveying JS](https://dev.to/rajat2502/you-don-t-know-js-get-started-chapter-2-surveying-js-notes-h85):

```
var awesomeFunction = function (coolThings) {
  // ..
  return amazingStuff;
};
```

- This function expression is referred to as an *anonymous function expression*, since it has no name identifier between the function keyword and the (..) parameter list.
- But when we perform `name inference` on an anonymous function it gives:

```
awesomeFunction.name;
// "awesomeFunction"
```

- `name inference` only happens in limited cases such as when the function expression is assigned (with = ).
- If you pass a function expression as an argument to a function call, for example, no name inference occurs; the name property will be an empty string, and the developer console will usually report **“(anonymous function)”**.
- Even if a name is inferred, it’s still an anonymous function. because the inferred name is a metadata and can't be used to refer to that function.

**Note:** An anonymous function doesn’t have an identifier to use to refer to itself from inside itself — for recursion, event unbinding, etc.

**Tip:** It is a good practice to use `named functions` as they improves the readability of the program.

- Here are some more declaration forms:

```
// generator function declaration
function *two() { .. }

// async function declaration
async function three() { .. }

// async generator function declaration
async function *four() { .. }

// named function export declaration (ES6 modules)
export function five() { .. }

// IIFE
(function(){ .. })();
(function namedIIFE(){ .. })();

// asynchronous IIFE
(async function(){ .. })();
(async function namedAIIFE(){ .. })();

// arrow function expressions
var f;
f = async (x) => {
  var y = await doSomethingAsync(x);
  return y * 2;
};
```

**Note:** Keep in mind that arrow function expressions are syntactically anonymous, meaning the syntax doesn’t provide a way to provide a direct name identifier for the function.

**Tip:** Since, arrow functions are anonymous functions, they should be used for everywhere. They have a specific purpose (i.e., handling the this keyword lexically).

## Coercive Conditional Comparison

- Here we will talk about, conditional expressions needing to perform coercion-oriented comparisons to make their decisions.

```
var x = "hello";
if (x) {
  // will run!
}

if (x == true) {
  // won't run
}

if (Boolean(x) == true) {
  // will run, as both have the same type
}

// which is the same as:
if (Boolean(x) === true) {
  // will run
}
```

- Since the `Boolean(..)` function always returns a value of type `boolean`, the `==` vs `===` in this snippet is irrelevant; they’ll both do the same thing. But the important part is to see that before the comparison, a coercion occurs, from whatever type x currently is, to boolean.

## Prototypal “Classes”

- In [Chapter 3: Digging to the Roots of JS](https://dev.to/rajat2502/you-don-t-know-js-get-started-chapter-3-digging-to-the-roots-of-js-notes-412n), we learned how different objects are linked together using prototype chain.
- Here, we will talk about **Prototypa; Classes**:

```
function Classroom() {
  // ..
}

Classroom.prototype.welcome = function hello() {
  console.log("Welcome, students!");
};

var mathClass = new Classroom();
mathClass.welcome();
// Welcome, students!
```

- All functions by default reference an empty object at a property named prototype.
- This is not the function’s prototype (where the function is prototype linked to), but rather the prototype object to link to when other objects are created by calling the function with the `new` keyword.
- This **“prototypal class”** pattern is now strongly discouraged, in favor of using ES6’s class mechanism:

```
class Classroom {
  constructor() {
    // ..
  }
  welcome() {
    console.log("Welcome, students!");
  }
}

var mathClass = new Classroom();
mathClass.welcome();
// Welcome, students!
```

- Under the covers, the same prototype linkage is wired up, but this class syntax fits the class-oriented design pattern much more cleanly than **“prototypal classes”**.


That's it for this chapter. I will be back with the notes of the next chapter. 

Till then, **Happy Coding!**

If you enjoyed reading these notes or have any suggestions or doubts, then do let me know your views in the comments. 
In case you want to connect with me, follow the links below:

[LinkedIn](https://www.linkedin.com/in/rajat2502) | [GitHub](https://github.com/rajat2502) | [Twitter](https://twitter.com/rajatverma2502)
