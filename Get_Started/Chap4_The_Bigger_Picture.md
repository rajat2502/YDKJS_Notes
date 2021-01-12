<h1 align="center">Chapter 4: The Bigger Picture</h1>

- This chapter divides the organization of JS into three main pillars:
  - **Pillar 1: Scope and Closure**
  - **Pillar 2: Prototypes**
  - **Pillar 3: Types and Coercion**

## Pillar 1: Scope and Closure

- The organization of variables into units of scope (functions, blocks) is one of the most foundational characteristics of any language. Scopes are like buckets while variables are like the marbles that are put into the buckets.
- The scope model of a language is like the rules that help you determine which color marbles go in which matching-color buckets.

#### **Lexical Scope:** 
It is a type of convention used in many programming languages that sets the scope of a variable so that it can only be called from within the block of code in which it is defined.

- JS is lexically scoped.
- Many people claim that JS is not lexically scoped because of its two characteristics that are not present in other languages:
  - **Hoisting:** All variables declared anywhere in scope are treated as if they’re declared at the beginning of the scope.
  - **var-declared variables**: `var-declared variables` are function scoped, even if they appear inside a block.
  
- Neither hoisting nor function-scoped var are sufficient to back the claim that JS is not lexically scoped.

#### Closures

- Closure is a natural result of lexical scope when the language has functioned as first-class values, as JS does. 
- When a function makes reference to variables from an outer scope, and that function is passed around as a value and executed in other scopes, it maintains access to its original scope variables; this is closure.
- We will dive deeper into `Scope and Closure` in the Book 2 of this series.

## Pillar 2: Prototypes

- We covered **Prototypes** in detail in the [last chapter](https://dev.to/rajat2502/you-don-t-know-js-get-started-chapter-3-digging-to-the-roots-of-js-notes-412n).
- JavaScript is one of the very few languages where we have the option to create objects directly and explicitly, without first defining their structure in a class.
- We will cover more about Prototypes, objects, and classes in Book 3 of this series.

## Pillar 3: Types and Coercion

- JS developers should learn more about types and should learn more about how JS manages type conversions.
- No JS program will do anything useful if it doesn’t properly leverage JS’s value types, as well as the conversion (coercion) of values between types.
- We will learn more about Types and Coercion in Book 4 of this series.

That's it for this chapter. With that, we have covered the first Book of the series "You Don't Know JS Yet". 

Now you’ve got a broader perspective on what’s left to explore in JS, and the right attitude to approach the rest of your journey.

I will be back with the notes of the first chapter of Book 2.

Till then, **Happy Coding!**

If you enjoyed reading these notes or have any suggestions or doubts, then do let me know your views in the comments. 
In case you want to connect with me, follow the links below:

[LinkedIn](https://www.linkedin.com/in/rajat2502) | [GitHub](https://github.com/rajat2502) | [Twitter](https://twitter.com/rajatverma2502)
