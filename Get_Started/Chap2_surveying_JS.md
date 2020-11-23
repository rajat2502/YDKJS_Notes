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

















