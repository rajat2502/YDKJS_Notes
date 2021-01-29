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

- The noted ReferenceError occurs from the line with the statement `greeting = "Howdy"`. 
- What's happening is that the greeting variable for that statement belongs to the declaration on the next line, `let greeting = "Hi"`, rather than to the previous var greeting = "Hello" statement.
- Here also, we can notice that the JS engine could only know, at the line that error is thrown, that the next statement would declare a block-scoped variable of the same name ( greeting ) is if the JS engine had already processed this code in an earlier pass, and already set up all the scopes and their variable associations.

### Compiler Speak

- Let's now learn how the JS engine identifies the variables and determines their scopes as the program is compiled.
- Let's first see an example:

```
var students = [
  { id: 14, name: "Kyle" },
  { id: 73, name: "Suzy" },
  { id: 112, name: "Frank" },
  { id: 6, name: "Sarah" },
];

function getStudentName(studentID) {
  for (let student of students) {
    if (student.id == studentID) {
      return student.name;
    }
  }
}

var nextStudent = getStudentName(73);

console.log(nextStudent);
// Suzy
```

- All occurrences of variables/identifiers in a program serve in one of two "roles": either they're the target of an assignment or they're the source of a value.
- If a variable is being assigned a value, then it is a **target** otherwise a **source** of value.

### Targets

- In the above code, since the `students` and `nextStudent` variables are assigned a value so they are both targets.
- There are three other target assignment operations in the code that are perhaps less obvious. One of them:

```
for (let student of students) {
```

This statement assigns a value to `student` for each element of the array `students`.

Another target reference:

```
getStudentName(73);
```

Here, the arguement `73` is assigned to the parameter `studentID`.

The last target reference in the program is:

```
function getStudentName(studentID) {
```

A `function` declaration is a special case of a target reference. Here the identifier `getStudentName` is assigned a function as a value.

So, we have identified all the targets in the program, let's now identify the sources!

### Sources

- The sources are as follows:

```
for (let student of students)
```

Here the `student` is a target but the array `students` is a source reference.

```
if (student.id == studentID)
```

In thi statement, both the `student` and `studentID` are source reference.

```
return student.name;
```

`student` is also a source reference in the `return` statement.

In `getStudentName(73)`, `getStudentName` is a source reference (which we hope resolves to a function reference value). In `console.log(nextStudent)`, `console` is a source reference, as is `nextStudent`.

**NOTE:** In case you were wondering, `id`, `name`, and `log` are all properties, not variable references.

### Cheating: Runtime Scope Modifications

- Scope is determined as the program is compiled, and should not generally be affected by runtime conditions.
- However, in non-strict-mode, there are technically still two ways to cheat this rule, modifying a program's scopes during runtime.
- The first way is to use the `eval(..)` function that receives a string of code to compile and execute on the fly during the program runtime. If that string of code has a `var` or `function` declaration in it, those declarations will modify the current scope that the `eval(..)` is currently executing in:

```
function badIdea() {
eval("var oops = 'Ugh!';");
console.log(oops);
}

badIdea(); // Ugh!
```

- If the `eval(..)` function was not present, the program would throw an error that the variable `oops` was not defined. But eval(..) modifies the scope of the `badIdea()` function at runtime.
- The second way to cheat is the `with` keyword, which essentially dynamically turns an object into a local scope — its properties are treated as identifiers in that new scope's block:

```
var badIdea = { oops: "Ugh!" };

with (badIdea) {
  console.log(oops); // Ugh!
}
```

- The global scope was not modified here, but badIdea was turned into a scope at runtime rather than compile time, and its property oops becomes a variable in that scope.

**NOTE:** At all costs, avoid `eval(..)` (at least, `eval(..)` creating declarations) and `with`. Again, neither of these cheats is available in strict-mode, so if you just use strict-mode (you should!) then the temptation goes away!

### Lexical Scope

- JS's scope is determined at compile time, the term for this kind of scope is **lexical scope**.
- "Lexical" is associated with the "lexing" stage of compilation, as discussed earlier in this chapter.

**NOTE:** It's important to note that compilation doesn't actually do anything in terms of reserving memory for scopes and variables.

That's it for this chapter. I will be back with the notes of the next chapter. 

Till then, **Happy Coding!**

If you enjoyed reading these notes or have any suggestions or doubts, then do let me know your views in the comments. 
In case you want to connect with me, follow the links below:

[LinkedIn](https://www.linkedin.com/in/rajat2502) | [GitHub](https://github.com/rajat2502) | [Twitter](https://twitter.com/rajatverma2502)
