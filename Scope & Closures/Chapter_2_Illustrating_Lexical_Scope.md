# Chapter 2: Illustrating Lexical Scope

- In this chapter we will discuss about how our program is handled by the JS Engine and how the JS Engine actually works.
- We will see different metaphors to illustrate scope.

### Marbles, and Buckets, and Bubbles... Oh My!

- Let's say we have marbles of three different colors Red, Blue and Green. To sort all the marbles we will drop the red marbles into the red bucket, blue into a blue bucket, and green into a green bucket.
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
- References (non-declarations) to variables/identifiers are allowed if here's a matching declaration either in the current scope, or any scope above/outside the current scope, but not with declarations from lower/nested scopes.
- An expression in the RED(1) bucket only has access to RED(1) marbles, not BLUE(2) or GREEN(3). An expression in the BLUE(2) bucket can reference either BLUE(2) or RED(1) marbles, not GREEN(3). And an expression in the GREEN(3) bucket has access to RED(1), BLUE(2), and GREEN(3) marbles.



















