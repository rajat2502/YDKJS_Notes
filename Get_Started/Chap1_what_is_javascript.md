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

- The array of enviornments that runs JS are constantly expanding.
- But, the one environment that rules JS is the web.

<br/>

### Not All (Web) JS...

- Various JS environments (like browser JS engines, Node.js, etc.) add APIs into the global scope of your JS programs that give you environment-specific capabilities, like being able to pop an alert-style box in the user’s browser.
- These are not mentioned in the actual JS specifications.
- Some exmaples of such APIs are: fetch(..), getCurrentLocation(..), getUserMedia(..) and fs.write(..).
- Even **console.log() and all other console methods** are not specified in the JS specifications but are used in almost every JS enviornments.
- Most of the cross-browser differences people complain about with **JS is so inconsistent!** claims are actually due to differences in how those environment behaviors work, not in how the JS itself works.

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

#### Paradigms are orientations that guides the programmers to approach the solutions to their problems.
- C is procedural, Java and C++ are Object oriented while Haskell is FP.
- Some languages support code that comes from mix and match of more than one paradigm, these languages are called as **"multi-paradigm languages"**.
- **JavaScript is most definitely a multi-paradigm language.**

<br/>

## Backwards & Forwards

- JavaScript practice the **Preservation of backwards compatibility**.
- **Backwards Compatibility**: It means that once something is accepted as *valid JS*, there will not be any future change to the language that causes that code to become *Invalid JS*.
- **TC39** members often proclaims that: **“we don’t break the web!”**.
- **forwards compatibility**: Being forwards-compatible means that including a new addition to the language in a program would not cause that program to break if it were run in an older JS engine.
- **JS is not forwards-compatible**.
- **HTML and CSS** are forwards-compatible, for instance, if you take out a code from 2020 and try to run it in an older browser, it will just skip the unrecognized HTML/CSS but it will not break the page (though the page may not look the same). They are not backwards-compatible.

<br/>

### Jumping the Gaps

- Since JS is not forward-compatible, there will always be some code that is *valid JS*, but is not working in an older browser or enviornment.
- Due to this, JS developers need to take special care to address this gap. For new and incompatible syntax, the solution is **transpiling**.
- **Transpiling**: to convert newer JS syntax version to an equivalent older syntax that the old browsers and enviornments supports.
- The most common transpiler is **[Babel](https://babeljs.io/)**.
- It’s strongly recommended that developers use the latest version of JS so that their code is clean and communicates its ideas most effectively.

<br/>

### Filling the Gaps

- 






