# Chapter 3: The Scope Chain

- The connections between scopes that are nested in the other scopes is called the scope chain.
- The scope chain is **directed**, meaning the lookup moves upward only.

### "Lookup" Is (Mostly) Conceptual

- We described runtime access to a variable as a *lookup* in the last chapter, in which the JavaScript Engine first checks if the variable is present in the current scope before moving upward up the chain of nested scopes (towards the global scope) until the variable is found, if at all.
- The lookup stops as soon as the first matching named declartion in a scope is found.
- The scope of a variable is usually decided during the initial compilation process. It will not change based on anything that can happen later during runtime.
- Since the scope is known from compilation, this information would likely be stored with each variable's entry in the AST, which means that the *Engine* doesn't need to lookup through bunch of scopes to figure out which scope a variable comes from.
- Avoiding the need of lookup is a key optimization benefit of lexical scope.

**Note**: Consider the following scenario: we have numerous files and we are unable to locate the declaration of a specific variable in one of them. It's not always an error if no declaration is found. That variable could be declared in the shared global scope by another file (programme) in the runtime.

- So the ultimate determination whether the variable was declared in some scope may need to be deferred to the runtime.
- Let's understand this with the *Marble and Buckets* analogy that we discussed in the last chapter:

> Any reference to a variable that's initially undeclared is left as an uncolored marble during that file's compilation; this color cannot be determined until other relevant file(s) have been compiled and the application runtime commences. That deferred lookup will eventually resolve the color to whichever scope the variable is found in (likely the global scope).

### Shadowing

- If all variables have different names it wouldn't matter if  all of them were just declared in the global scope.
- Having different lexical scopes starts to matter more when you have two or more variables, each in different scopes, with the same lexical names.
- Let's consider an example:

```js
var studentName = "Suzy";

function printStudent(studentName) {
  studentName = studentName.toUpperCase();
  console.log(studentName);
}

printStudent("Frank");
// FRANK
printStudent(studentName);
// SUZY
console.log(studentName);
// Suzy
```

- The `studentName` declaration on line 1, creates a new variable in the global scope. 
- All the three `studentName` references in the `printStudent` function refers to a different local scoped variable and not the global scoped `studentName` variable. This behaviour is called **Shadowing**.
- So, we can say that in the above example, the local scoped variable shadows the global scoped variable.

**Note**: It's lexically impossible to reference the global studentName anywhere inside of the printStudent(..) function (or from any nested scopes).

### Global Unshadowing Trick

- It is possible to access a global variable from a scope where that variable as been shadowed, but not through a typical lexical identifier reference.
- In the global scope, `var` and `function` declarations also expose themselves as properties (of the same name as the identifier) on the global object—essentially an object representation of the global scope. Consider the program:

```js
var studentName = "Suzy";

function printStudent(studentName) {
  console.log(studentName);
  console.log(window.studentName);
}

printStudent("Frank");
// "Frank"
// "Suzy"
```

- So, as we can notice using `window.variableName` we can still access the globally scoped shadowed variable in a function.

**Note**: 
- The `window.studentName` is a mirror of the global `studentName` variable, not a separate snapshot copy. Changes to one are still seen from the other, in either direction.
- This trick only works for accessing a global scope variable and not a shadowed variable from a nested scope, and even then, only one that was declared with `var` or `function`.

**Warning**: Just because you can doesn't mean you should. Don't shadow a global variable that you need to access, and conversely, avoid using this trick to access a global variable that you've shadowed.

### Copying Is Not Accessing

- Consider the example:

```js
var special = 42;

function lookingFor(special) {
  var another = {
    special: special,
  };

  function keepLooking() {
    var special = 3.141592;
    console.log(special);
    console.log(another.special); // Ooo, tricky!
    console.log(window.special);
  }
  keepLooking();
}

lookingFor(112358132134);
// 3.141592
// 112358132134
// 42
```

- So, we noticed that we were able to copy the `special` variable passed as a parameter to the `lookingFor` function in the `keepLooking` function. Does that mean we accessed a shadowed variable?  
- No! `special: special` is copying the value of the `special` parameter variable into another container (a property of the same name). This doesn't mean that we are accessing the parameter `special`. It means we are accessing the copy of the value it had at that moment, by way of another container. We cannot reassign the `special` parameter to a different value from inside `keepLooking` function.
- What if I'd used objects or arrays as the values instead of the numbers ( 112358132134 , etc.)? Would us having references to objects instead of copies of primitive values "fix" the inaccessibility? No. Mutating the contents of the object value via a reference copy is **not** the same thing as lexically accessing the variable itself. We still can't reassign the `special` parameter.

### Illegal Shadowing

- Not all combinations of declaration shadowing are allowed. `let` can shadow `var`, but `var` can't shadow `let`. Consider the example:

```js
function something() {
  var special = "JavaScript";
  {
    let special = 42; // totally fine shadowing
    // ..
  }
}

function another() {
  // ..
  {
    let special = "JavaScript";
    {
      var special = 42;
      // ^^^ Syntax Error
      // ..
    }
  }
}
```

- Notice in the `another()` function, the inner var `special` declaration is attempting to declare a function-wide `special`, which in and of itself is fine (as shown by the `something()` function).
- The syntax error description in this case indicates that `special` has already been defined.
- The real reason it's raised as a `SyntaxError` is because the `var` is basically trying to "cross the boundary" of (or hop over) the `let` declaration of the same name, which is not allowed.
- That boundary-crossing prohibition effectively stops at each function boundary, so this variant raises no exception:

```js
function another() {
  // ..
  {
    let special = "JavaScript";
    ajax("https://some.url", function callback() {
      // totally fine shadowing
      var special = "JavaScript";
      // ..
    });
  }
}
```

### Function Name Scope

- A function declaration looks like:

```js
function askQuestion() {
  // ..
}
```

- While function expression looks like:

```js
var askQuestion = function(){
  //..
};
```

- A function expression, takes in a function as a value, due to this, the function itself will not "hoist".
- Now let's consider a named function expression:

```js
var askQuestion = function ofTheTeacher() {
  // ..
};
```

- We know `askQuestion` can be accessed in the outer scope, but what about `ofTheTeacher` identifier? `ofTheTeacher` is declared as an identifier inside the function itself:

```js
var askQuestion = function ofTheTeacher() {
  console.log(ofTheTeacher);
};

askQuestion();
// function ofTheTeacher()...
console.log(ofTheTeacher);
// ReferenceError: ofTheTeacher is not defined
```

### Arrow Functions

- Here is how an arrow function is declared:

```js
var askQuestion = () => {
  // ..
};
```

- The arrow function doesn't need the word `function` to define it.

### Backing Out

- When a function (declaration or expression) is defined, a new scope is created. The positioning of scopes nested inside one another creates a natural scope hierarchy throughout the program, called the scope chain.
- Each new scope offers a clean slate, a space to hold its own set of variables. When a variable name is repeated at different levels of the scope chain, shadowing occurs, which prevents access to the outer variable from that point inward.
