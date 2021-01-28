# Chapter 1: What's the Scope?

- While working with JS, have you ever thought, How does it know which variables are accessible by any given statement, and how does it handle two variables of the same name?
- The answers to questions like these take the form of well-defined rules called scope. In this book, we will dig deeper into all the aspects of scope.
- Let's first uncover how the JS engine processes our programs: 
- As we studied in the last book that JS is a compiled language and it is first parsed before the execution begins.
- The code author's decisions on where to place variables, functions, and blocks with respect to each other are analyzed according to the rules of scope, during the initial parsing/compilation phase.

### Compiled vs. Interpreted

- Code compilation is a set of steps that process the text of your code and turn it into a list of instructions the computer can understand. Typically, the whole source code is transformed at once, and those resulting instructions are saved as output that can later be executed.
- In case of interpretation, the source code is transformed line by line; each line or statement is executed before immediately proceeding to processing the next line of the source code.
- Here is an image showing the difference between the two: 

![image](https://user-images.githubusercontent.com/42200276/106129194-0ad25300-6186-11eb-9ca8-d0b7ebc32f88.png)

Let's now learn about the compilation of a program:

### Compiling Code

- Scope is primarily determined during compilation, so understanding how compilation and execution relate is key in mastering scope.
- There are mainly three stages of compilation:
  1. **Tokenizing/Lexing** 
  2. **Parsing**
  3. **Code Generation**
  
#### Tokenizing/Lexing 

Breaking up a string of characters into meaningful (to the language) chunks, called tokens. For eg:
```
  var a = 2;
```
This program would likely be broken up into the following tokens: `var` , `a` , `=` , `2` , and `;`. Whitespace may or may not be persisted as a token,     depending on whether it's meaningful or not. 

#### Parsing

Parsing is the process of taking a stream of tokens and turning it into a tree of nested elements, called as the **Abstract Syntax Tree** or **AST**. 

For example, the tree for `var a = 2;` might start with a top-level node called `VariableDeclaration` , with a child node called `Identifier` (whose value is a ), and another child called `AssignmentExpression` which itself has a child called `NumericLiteral` (whose value is 2 ).

#### Code Generation

Code geneation involves taking an AST and turing it into executable code. This part varies greatly depending on the language, the platform it's targeting, and other factors.

**NOTE**: The implementation details of a JS engine (utilizing system memory resources, etc.) is much deeper than we will dig here. We'll keep our focus on the observable behavior of our programs and let the JS engine manage those deeper system-level abstractions.

### Required: Two Phases

- The most important observation we can make about processing of JS programs is that it occurs in (at least) two phases: parsing/compilation first, then execution.
- The separation of a parsing/compilation phase from the subsequent execution phase is observable fact, There are three program characteristics you can observe to prove this to yourself: syntax errors, early errors, and hoisting.

### Syntax Errors from the Start

- Consider the program:

```
var greeting = "Hello";
console.log(greeting);
greeting = ."Hi";
// SyntaxError: unexpected token .
```

- When we try to execute this program it shows no output, but instead throws a `SyntaxError` about the unexpected . token right before the `"Hi"` string.
- Since, JS is a compiled language and not interpreted (line by line), the string was not printed, and the program was executed as a whole.

### Early Errors

- Now, consider:
```
console.log("Howdy");
saySomething("Hello", "Hi");
// Uncaught SyntaxError: Duplicate parameter name not
// allowed in this context
function saySomething(greeting, greeting) {
  "use strict";
  console.log(greeting);
}
```

- The `"Howdy"` message is not printed, despite being a well-formed statement. Instead, just like the snippet in the previous section, the SyntaxError here is thrown before the program is executed. 
- In this case, it's because strict-mode (opted in for only the saySomething(..) function here) forbids, among many other things, functions to have duplicate parameter names; this has always been allowed in non-strict-mode.
- Here also, we can observe that the code was first fully parsed and then only the execution began. Otherwise, the string `"Howdy"` would be printed.

### Hoisting

- Finally, consider:

```
function saySomething() {
  var greeting = "Hello";
  {
    greeting = "Howdy"; // error comes from here
    let greeting = "Hi";
    console.log(greeting);
  }
}
saySomething();
// ReferenceError: Cannot access 'greeting' before initialization
```

- 





























