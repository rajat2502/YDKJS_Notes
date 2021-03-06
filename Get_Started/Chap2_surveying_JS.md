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

- `==` is generally referred to as the *loose-equality* operator.
- `===` equality comparison is often described as, “checking both the value and the type”. For eg:

```
3 === 3.0 // true
null === null // true
3 === "3" // false
```

- `===` disallows any sort of type conversion (aka, **“coercion”**) in its comparison, where other JS comparisons do allow coercion.
- The `===` operator is designed to lie in two cases of special values: NaN and -0. Consider:

```
NaN === NaN; // false
0 === -0; // true
```

- In first case, it says that, an occurence of `NaN` is not equal to any other occurence of `NaN`. In case of 0, the === operator lies and says it’s equal to the regular 0 value.
- So, for such comparisions involving NaN use the `Number.isNaN(..)` utility, and For -0 comparison, use the `Object.is(..)` utility.
- The `Object.is(..)` utility can also be used for NaN comparisions. It is a really-really-strict comparison!
- Object values comparision is even more complicated:

```
[ 1, 2, 3 ] === [ 1, 2, 3 ];  // false
{ a: 42 } === { a: 42 }       // false
(x => x * 2) === (x => x * 2) // false
```

- The `===` operator uses identity equality for object values.
- In JS, all object values are held by reference, are assigned and passed by reference-copy, and are compared by reference (identity) equality.

```
var x = [ 1, 2, 3 ];
// assignment is by reference-copy, so
// y references the *same* array as x,
// not another copy of it.
var y = x;
y === x;            // true
y === [ 1, 2, 3 ];  // false
x === [ 1, 2, 3 ];  // false
```

- JS doesn’t provide structural equality comparison because it’s almost intractable to handle all the corner cases!

#### Coercive Comparisons

- Coercion means a value of one type being converted to its respective representation in another type.
- The `==` operator performs an equality comparison similarly to how the `===` performs it. In fact, both operators consider the type of the values being compared. And if the comparison is between the same value type, both `==` and `===` do exactly the same thing, no difference whatsoever. If the value types being compared are different, the `==` differs from `===` in that it allows coercion before the comparison.
- Instead of **“loose equality,”** the == operator should be described as **“coercive equality”**. Consider the following examples:

```
42 == "42";
1 == true;
```

- In both cases, the value types are different so coercion is appplied and once they are of the same type then only the values are compared.
- The relational comparison operators (>, <, >=, <=) also work like `==` operator. For eg:

```
var arr = ["1", "10", "100", "1000"];
for (let i = 0; i < arr.length && arr[i] < 500; i++) {
  // will run 3 times
}
```

- These relational operators typically use numeric comparisons, except in the case where both values being compared are already strings; in this case, they use alphabetical (dictionary-like) comparison of the strings:

```
var x = "10";
var y = "9";
x < y;      // true, watch out!
```

### How We Organize in JS

- Two of the most used patterns are: **classes** and **modules**.

#### Classes

- A class in a program is a definition of a *type* of custom data structure that includes both data and behaviors that operate on that data.

```
class Page {
  constructor(text) {
    this.text = text;
  }
  print() {
    console.log(this.text);
  }
}

class Notebook {
  constructor() {
    this.pages = [];
  }
  addPage(text) {
    var page = new Page(text);
    this.pages.push(page);
  }
  print() {
    for (let page of this.pages) {
      page.print();
    }
  }
}

var mathNotes = new Notebook();
mathNotes.addPage("Arithmetic: + - * / ...");
mathNotes.addPage("Trigonometry: sin cos tan ...");
mathNotes.print();

// Arithmetic: + - * / ...
// Trigonometry: sin cos tan ...
```

- In `Page` class, the data `text` is stored in property `this.text` and the behavior is `print()`.
- In `Notebook` class, the data `pages` is an array of `Page` instances and the behaviours are `print()` and `addPage(..)`.

#### Class Inheritance

```
class Publication {
  constructor(title, author, pubDate) {
    this.title = title;
    this.author = author;
    this.pubDate = pubDate;
  }
  print() {
    console.log(`
Title: ${this.title}
By: ${this.author}
${this.pubDate}
`);
  }
}
```

- This Publication class defines a set of common behavior that any publication might need.

```
class Book extends Publication {
  constructor(bookDetails) {
    super(bookDetails.title, bookDetails.author, bookDetails.publishedOn);
    this.publisher = bookDetails.publisher;
    this.ISBN = bookDetails.ISBN;
  }
  print() {
    super.print();
    console.log(`
Publisher: ${this.publisher}
ISBN: ${this.ISBN}
`);
  }
}
```

- The `Book` class use the `extends` clause to extend the general definition of Publication to include additional behavior. This behavior is called `Inheritance`.

#### Modules

- The `Modules` pattern have the same goal i.e. to group data and behavior, but it has certain differences from `classes`. An example of `classic-modules` is:

```
function Publication(title, author, pubDate) {
  var publicAPI = {
    print() {
      console.log(`
Title: ${title}
By: ${author}
${pubDate}
`);
    },
  };
  return publicAPI;
}

function Book(bookDetails) {
  var pub = Publication(
    bookDetails.title,
    bookDetails.author,
    bookDetails.publishedOn
  );
  var publicAPI = {
    print() {
      pub.print();
      console.log(`
Publisher: ${bookDetails.publisher}
ISBN: ${bookDetails.ISBN}
`);
    },
  };
  return publicAPI;
}
```

- The class form stores methods and data on an object instance, which must be accessed with the `this.` prefix. With modules, the methods and data are accessed as identifier variables in scope, without any this. prefix.

#### ES Modules

- ESMs are always file-based; one file, one module.
- They have to be exported from one file to be used into another.
