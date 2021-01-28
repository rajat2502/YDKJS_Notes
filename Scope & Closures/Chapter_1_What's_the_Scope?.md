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
  1. Tokenizing/Lexing: breaking up a string of characters into meaningful (to the language) chunks, called tokens. For eg:
  ```
  var a = 2;
  ```
  This program would likely be broken up into the following tokens: `var` , `a` , `=` , `2` , and `;`. Whitespace may or may not be persisted as a token, depending on whether it's meaningful or not. 
  2. Parsing
  3. Code Generation























