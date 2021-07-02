# Chapter 2: Illustrating Lexical Scope

- In this chapter, we will discuss how our program is handled by the JS Engine and how the JS Engine works.

### Marbles, and Buckets, and Bubbles... Oh My!

- Let's say we have marbles of three different colors Red, Blue, and Green. To sort all the marbles we will drop the red marbles into the red bucket, blue into a blue bucket, and green into a green bucket.
- Now if we need a red marble we know the red bucket is where to get it from.
- Now apply this analogy to scope and variables, the marbles are the variables and the bucket are the scopes.
- Let's understand this with the help of an example:

```
// outer/global scope: RED

var students = [
  { id: 14, name: "Kyle" },
  { id: 73, name: "Suzy" },
  { id: 112, name: "Frank" },
  { id: 6, name: "Sarah" },
];

function getStudentName(studentID) {
  // function scope: BLUE
  for (let student of students) {
    // loop scope: GREEN
    if (student.id == studentID) {
      return student.name;
    }
  }
}

var nextStudent = getStudentName(73);
console.log(nextStudent); // Suzy

```
- As you can see that we have designated three scope colors with code comments: RED (outermost global scope), BLUE (scope of function), and GREEN (scope inside the for loop).
- Now let's see the boundaries of these scope buckets by drawing colored bubbles:

<div align="center"><img src="https://user-images.githubusercontent.com/42200276/124065686-e50eea00-da54-11eb-8ac5-d4b7686bc61d.png" /></div>


- Bubble 1 (RED): surround global scope, holds three identifiers: `students`, `getStudentName` and `nextStudent`.
- Bubble 2 (BLUE): surround scope of function `getStudentName(..)`, holds one identifier: `studentID`.
- Bubble 3 (GREEN): surround the scope of the for-loop, holds one identifier: `student`.

**NOTE**: Scope bubbles are determined using compilation. Each marble is colored based on which bucket it's declared in, not the color of the scope it may be accessed from.

- Scopes can nest inside each other, to any depth of nesting as your program needs.
- References (non-declarations) to variables/identifiers are allowed if there's a matching declaration either in the current scope, or any scope above/outside the current scope, but not with declarations from lower/nested scopes.
- An expression in the RED(1) bucket only has access to RED(1) marbles, not BLUE(2) or GREEN(3). An expression in the BLUE(2) bucket can reference either BLUE(2) or RED(1) marbles, not GREEN(3). And an expression in the GREEN(3) bucket has access to RED(1), BLUE(2), and GREEN(3) marbles.

### Nested Scope

- Scopes are lexically nested to any arbitrary depth as the program defines.
- In the above example, the function scope for `getStudentName(..)` is nested inside the global scope. The block scope of the `for` loop is similarly nested inside that function scope.
- Any time an identifier reference cannot be found in the current scope, the next outer scope in the nesting is consulted; that process is repeated until an answer is found or there are no more scopes to consult.

### Undefined Mess

- If the variable is a source, an unresolved identifier lookup is considered an undeclared (unknown, missing) variable, which always results in a `ReferenceError` being thrown. 
- If the variable is a target, and the code at that moment is running in strict-mode, the variable is considered undeclared and similarly throws a `ReferenceError`.
- The error message for an undeclared variable condition, in most JS environments, will look like, "Reference Error: XYZ is not defined."
- "Not defined" means "not declared" or "undeclared".
- "Undefined" means that the variable was found, but it has no other value at the moment. So it defaults to the `undefined` value.
- To perpetuate the confusion even further, JS's typeof operator returns the string "undefined" for variable references in either state:

```
var studentName;

typeof studentName; // "undefined"
typeof doesntExist; // "undefined"
```

- So, we as developers have to pay close attention to not mix up which kind of "undefined" we're dealing with.

### Global... What!?

- If the variable is a target and the program is not in strict-mode, the engine creates an accidental global variable to fulfill that target assignment. For Example:

```
function getStudentName() {
  // assignment to an undeclared variable :(
  nextStudent = "Suzy";
}

getStudentName();
console.log(nextStudent);
// "Suzy" -- oops, an accidental-global variable!
```

- This is another reason why we should use strict-mode. It prevents us from such incidents by throwing a `ReferenceError`.
