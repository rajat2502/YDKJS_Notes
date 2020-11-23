<h1 align="center">Chapter 2: Surveying JS</h1>

**Best way to learn JS is to practice it!**

### Each File is a Program

- Almost every Web Application has a bunch of JS files.
- In JS, every single file is its own separate program. So, if somehow one file fails, it won't affect the execution of the other files.
- The only way multiple JS files act as a single program is by sharing their state via the **"global scope"**.
- Since ES6, JS started supporting **Modules** format.

### Values

- Fundamental unit of information in a program is **Value**.
- Values come in two forms in JS: **Primitive** and **Objects**.

#### Strings

- Strings are ordered collection of characters.

```
console.log("Hello World");
```

- In this code, *Hello World* is the string.
- Strings can be defined using both *Single-Quotes* or *Double-Quotes*. The choice of which to use is yours. Just make sure to choose one and use it consistently in your program. 
- We can also use the *backtick-character* to define a string. However, this choice is not merely stylistic; there’s a behavioral difference as well. For example:

```
console.log("My name is ${ firstName }.");
// My name is ${ firstName }.

console.log('My name is ${ firstName }.');
// My name is ${ firstName }.

console.log(`My name is ${ firstName }.`);
// My name is Rajat.
```

- In the above code snippet, we assumed that we have already declared a variable named **firstName** with the value **Rajat**. 
- The use of backtick declaration to place the value of a variable in a string is known as **Interpolation**.

#### Other primitive datatypes

- Booleans and numbers are also used in a JS program.

```
while (false) {
console.log(3.141592);
}
```

- The code inside of the while loop is never executed as the condition always remains false.
- **Math.PI** should be used for getting the value of mathematical PI.
- **Bigint** is a primitive type that is used to store large whole numbers (larger than: (2^53) - 1).
- In addition to strings, numbers and booleans, two other primitive values in JS programs are **null** and **undefined**. While there are many differences between them, for most parts both serve the purpose of emptiness of a value. **However, it’s safest and best to use only undefined as the single empty value.**
- Another primitive data-type is **Symbol**. You won’t encounter direct usage of symbols very often in typical JS programs. They’re mostly used in low-level code such as in libraries and frameworks.

#### Arrays And Objects

- Besides primitives, the other value type in JS is an object value.
- Arrays are a special type of object that’s comprised of an ordered and numerically indexed list of data. For eg:

```
names = [ "One", "Two", "Three", "Four" ];
names.length;
// 4
names[0];
// One
names[1];
// Two
```

- JS arrays can hold any datatype, either primitive or object. Even functions are values that can be held in arrays or objects.
- Objects are more general: an unordered, keyed collection of any various values. For eg:

```
name = {
  first: "Kyle",
  last: "Simpson",
  age: 39,
  specialties: ["JS", "Table Tennis"],
};
console.log(`My name is ${name.first}.`);
```

- Here, `name` is an object with keys like `first`, `last`, `age` and `specialties`.
- We can also use the the following syntax to access a value of object:

```
name["first"]
```

#### Value Type Determination

- The `typeof` operator tells the built-in type of the value (i.e, primitive or object).

```
typeof 42; // number
typeof "abc"; // string
typeof true; // boolean
typeof undefined; // undefined
typeof null; // object
typeof { a: 1 }; // object
typeof [1, 2, 3]; // object
typeof function hello() {}; // function
```

- Note that, `typeof` returns the type of `null`, `array` as object and `function` as `function`.

### Declaring and Using Variables

- Variables are like containers for values. There are many types of variable declaration in JS, and each one of them have their own different meanings. For eg:

```
var name = "Kyle";
var age;
```

- The `var` keyword declares a variable to be used in the program, and optionally allows initial value assignment.
- Similarly, the `let` keyword can be used to declare variables as:

```
let name = "Kyle";
let age;
```

- `let` allows a more limited access to the variable than var. This is called **block scoping** as opposed to regular or function scoping.
- Another type of declaration is using the `const` keyword. A variable declared using this keyword is similar to `let`, with addition that it must be given a value at the moment it’s declared, and cannot be re-assigned a different value later.

```
const myBirthday = true;
let age = 39;
if (myBirthday) {
  age = age + 1;
  // OK!
  myBirthday = false; // Error!
}
```

**Tip: If you stick to using const only with primitive values, you avoid any confusion of re-assignment (not allowed) vs. mutation (allowed)! That’s the safest and best way to use const .**

### Functions

- In JS, the term function take the broader meaning of a **Procedure**. A procedure is a collection of statements that can be invoked one or more times, may be provided some inputs, and may give back one or more outputs. A function declaration in JS looks like:

```
function greetHello(name) {
  const msg = `Hello ${name}`;
  return msg;
}
```

- This function is a *statement* and not an expression. The association between the identifier `awesomeFunction` and the function value happens during the compile phase of the code, before that code is executed.
- A function expression can be defined as:

```
// let awesomeFunction = ..
// const awesomeFunction = ..
var awesomeFunction = function (coolThings) {
  // ..
  return amazingStuff;
};
```

- This function is an `expression` that is assigned to the variable `awesomeFunction`. Contrary to a function statement, a function expression is not associated with its identifier until that statement during runtime. 
- In JS, functions are a special type of object. They are treated as Values.
- A function may or may not have a parameter.
- Functions can also return values. You can only return a single value, but if you want to return multiple values, then you can wrap up them into a single object/array.
- Since functions are values, they can be assigned as properties on objects:

```
var whatToSay = {
  greeting() {
    console.log("Hello!");
  },
  question() {
    console.log("What's your name?");
  },
  answer() {
    console.log("My name is Kyle.");
  },
};
whatToSay.greeting();
// Hello!
```

#### Comparisions


































































