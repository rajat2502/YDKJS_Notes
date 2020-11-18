<h1 align="center">Chapter 1: What Is JavaScript?</h1>

- JavaScript is not the script part of Java.
- The official name of the language specified by TC39 and formalized by the ECMA standards body is **ECMAScript**.
- **TC39** - the technical steering committee that manages JS, comprises of around 50-100 people from different companies like Mozilla, Google, Apple and Samsung.
- **ECMA** - the standards organization.
- All tc39 proposals can be found here: https://github.com/tc39/proposals
- **v8 engine** - Chrome's JS Engine
- **SpiderMonkey engine** - Mozilla’s JS engine

<br/>

### The Web Rules Everything About (JS)

- The array of environments that runs JS are constantly expanding.
- But, the one environment that rules JS is the web.

<br/>

### Not All (Web) JS...

- Various JS environments (like browser JS engines, Node.js, etc.) add APIs into the global scope of your JS programs that give you environment-specific capabilities, like being able to pop an alert-style box in the user’s browser.
- These are not mentioned in the actual JS specifications.
- Some exmaples of such APIs are: fetch(..), getCurrentLocation(..), getUserMedia(..) and fs.write(..).
- Even **console.log() and all other console methods** are not specified in the JS specifications but are used in almost every JS environments.
- Most of the cross-browser differences people complain about with **JS is so inconsistent!** claims are actually due to differences in how those environment behaviours work, not in how the JS itself works.

<br/>

### It’s Not Always JS

- **console/REPL (Read-Evaluate-Print-Loop)** are not JS enviornments, they are developer tools.
- Their primary purpose is to make life easier for developers.
- We shouldn’t expect such tools to always adhere strictly to the way JS programs are handled, because that’s not the purpose of these tools.

<br/>

### Many Faces

- Typical paradigm-level code categories includes:
  - **Procedural** - follows a top-down, linear approach thorugh a pre-determined set of operations.
  - **Object Oriented** - collects logic and data into units called classes.
  - **Functional** - organizes code into functions.

<br/>

#### Paradigms are orientations that guide the programmers to approach the solutions to their problems.
- C is procedural, Java and C++ are Object-oriented while Haskell is FP.
- Some languages support code that comes from mix and match of more than one paradigm, these languages are called as **"multi-paradigm languages"**.
- **JavaScript is most definitely a multi-paradigm language.**

<br/>

## Backwards & Forwards

- JavaScript practice the **Preservation of backwards compatibility**.
- **Backwards Compatibility**: It means that once something is accepted as *valid JS*, there will not be any future change to the language that causes that code to become *Invalid JS*.
- **TC39** members often proclaim that: **“we don’t break the web!”**.
- **forwards compatibility**: Being forwards-compatible means that including a new addition to the language in a program would not cause that program to break if it were run in an older JS engine.
- **JS is not forwards-compatible**.
- **HTML and CSS** are forwards-compatible, for instance, if you take out a code from 2020 and try to run it in an older browser, it will just skip the unrecognized HTML/CSS but it will not break the page (though the page may not look the same). They are not backwards-compatible.

<br/>

### Jumping the Gaps

- Since JS is not forward-compatible, there will always be some code that is *valid JS*, but is not working in an older browser or environment.
- Due to this, JS developers need to take special care to address this gap. For new and incompatible syntax, the solution is **transpiling**.
- **Transpiling**: to convert newer JS syntax version to an equivalent older syntax that the old browsers and environments support.
- The most common transpiler is **[Babel](https://babeljs.io/)**.
- It’s strongly recommended that developers use the latest version of JS so that their code is clean and communicates its ideas most effectively.

<br/>

### Filling the Gaps

- It the forwards-compatibility issue is not because of a new-syntax but because of an API method that was recently added, the solution is to define the recently added API that acts as if the older environment had already had it natively defined.
- This pattern is called a **polyfill**.
- Example:

```
// getSomeRecords() returns us a promise for some
// data it will fetch
var pr = getSomeRecords();
// show the UI spinner while we get the data
startSpinner();
pr.then(renderRecords).catch(showError).finally(hideSpinner);
// render if successful
// show an error if not
// always hide the spinner
```
This code uses an ES2019 feature and so it would not work in a pre-ES2019 environment, as, the **finally(..)** method would not exist, and an error would occur.

To make it work, we can define the finally(..) method, as:

```
if (!Promise.prototype.finally) {
  Promise.prototype.finally = function f(fn) {
    return this.then(
      function t(v) {
        return Promise.resolve(fn()).then(function t() {
          return v;
        });
      },
      function c(e) {
        return Promise.resolve(fn()).then(function t() {
          throw e;
        });
      }
    );
  };
}
```
<br/>

**Warning**: *This is only a simple illustration of a basic (not entirely spec-compliant) polyfill for finally(..). Don’t use this polyfill in your code; always use a robust, official polyfill wherever possible, such as the collection of polyfills/shims in ES-Shim.*

<br/>

### What’s in an Interpretation?

- Code wriiten in JS: is it an **interpreted script** or **compiled program**?
- The real reason that matters to have a clear picture of whether JS is interpreted or compiled relates to the nature of how errors are handled in it.
- Historically, Interpreted or Scripting languages were executed in generally a top-down and line-by-line fashion.

![image](https://user-images.githubusercontent.com/42200276/99537054-2fb18980-29d1-11eb-8825-1c46b838ab9a.png)

- Some languages go through a processing step (typically Parsing) before their execution. This parsing creates an Abstract Syntax Tree (AST) of the whole program.

![image](https://user-images.githubusercontent.com/42200276/99537130-4821a400-29d1-11eb-8b80-44fe10a25042.png)

- In JS, source code is parsed before it is executed.
- So JS is a parsed language, but is it compiled? The Answer is very close to YES than NO.
- The parsed JS is converted into binary form and that binary form is executed.
- Hence, **JS is a compiled language**. So, due to this fact, we are informed about the errors in our code even before it gets executed.

<br/>

### Web Assembly (WASM)

- In 2013, ASM.js was introduced as one way of addressing the pressures on the runtime performance of JS.
- ASM.js intended to provide a path for non-JS programs (C, etc.) to be converted to a form that could run in the JS engine.
- After several years, another set of engineers released **Web Assembly**.
- WASM is a representation format more akin to Assembly that can be processed by a JS engine by skipping the parsing/compilation that the JS engine normally does.
- The parsing/compilation of a WASM-targeted program happen ahead of time (AOT); what’s distributed is a binary-packed program ready for the JS engine to execute with very minimal processing.

<br/>

### Strictly Speaking

- With the release of ES5(2009), JS added "strict mode" as an opt-in mechanism for encouraging better JS programs.
- It should be thought of as a guide to the best way to do things so that the JS engine has the best chance of optimizing and efficiently running the code.

<br/>

Strict mode is switched on per file with a special pragma (nothing allowed before it except comments/whitespace):

```
// only whitespace and comments are allowed
// before the use-strict pragma
"use strict";
// the rest of the file runs in strict mode
```

- Strict mode can alternatively be turned on the per-function scope
- Interestingly, if a file has strict mode turned on, the function-level strict mode pragmas are disallowed. So you have to pick one or the other.
