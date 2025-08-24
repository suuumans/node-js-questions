# Solutions to JavaScript Practice Questions

## Solution 1
*Reference: [Question 1](js-questions.md#question-1)*

### Q. What is JavaScript and what are its key features?

JavaScript is a high-level, interpreted programming language primarily used for creating dynamic and interactive web applications. It was originally developed by Brendan Eich at Netscape in 1995 and has since become the cornerstone of front-end web development, while also extending to server-side (via Node.js), mobile apps, and even desktop applications. What makes JavaScript truly powerful is its ability to manipulate the Document Object Model (DOM) in browsers, enabling real-time updates without page reloads.

Key features include:
- **Dynamic Typing**: Variables don't need explicit type declarations; types are determined at runtime, which speeds up development but requires careful handling to avoid errors.

- **Object-Oriented and Functional Paradigms**: It supports prototypes for inheritance, closures, and higher-order functions, allowing for flexible and modular code.

- **Asynchronous Programming**: Built-in support for callbacks, Promises, and async/await makes it ideal for handling non-blocking operations like API calls or event handling.

- **Event-Driven**: JavaScript thrives in environments like browsers where it responds to user interactions (e.g., clicks, scrolls) via event listeners.

- **Cross-Platform**: Runs on any device with a JavaScript engine, such as V8 in Chrome or SpiderMonkey in Firefox.

- **Extensive Ecosystem**: With libraries like React, Vue, and Angular, it's evolved into a full-stack language.



## Solution 2
*Reference: [Question 2](js-questions.md#question-2)*
### Q. What is the difference between JavaScript and Java?

This is a common misconception due to the similar names, but JavaScript and Java are fundamentally different languages with distinct origins and uses. JavaScript was named "JavaScript" as a marketing ploy to capitalize on Java's popularity in the 90s, but that's where the similarity ends.

- **Syntax and Paradigm**: Java is a statically-typed, class-based object-oriented language, requiring compilation to bytecode. JavaScript is dynamically-typed, prototype-based, and interpreted (or just-in-time compiled in modern engines).

- **Execution Environment**: Java runs on the Java Virtual Machine (JVM), making it platform-independent but requiring a runtime. JavaScript primarily runs in browsers or Node.js environments without needing a separate VM.

- **Use Cases**: Java is often used for enterprise-level backend systems, Android apps, and large-scale applications (e.g., via Spring framework). JavaScript dominates web development, both client-side (interactivity) and server-side (Node.js for APIs).

- **Typing and Error Handling**: Java enforces strict types at compile-time, catching errors early. JavaScript's loose typing allows more flexibility but can lead to runtime errors if not managed well.

- **Concurrency**: Java uses multi-threading for parallelism, while JavaScript is single-threaded with an event loop for concurrency.

In short, if you're building a robust backend service, Java might be your go-to, but for web interactivity, JavaScript is unmatched. They're like distant cousins—sharing some syntax inspirations but living in different worlds.



## Solution 3
*Reference: [Question 3](js-questions.md#question-3)*

### Q. What are the primitive data types in JavaScript?

JavaScript has seven primitive data types, which are the building blocks of the language. Primitives are immutable and passed by value, unlike objects which are passed by reference. According to the [ECMAScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures) specification, they are:

1. **String**: Represents a sequence of characters, e.g., `"Hello, World!"`.
2. **Number**: Represents both integer and floating-point numbers, e.g., `42` or `3.14`.
3. **BigInt**: Represents integers with arbitrary precision, e.g., `9007199254740991n`.
4. **Boolean**: Represents a logical entity and can have two values: `true` and `false`.
5. **Undefined**: A variable that has been declared but not assigned a value is of type `undefined`.
6. **Null**: Represents the intentional absence of any object value.
7. **Symbol**: Introduced in ES6, represents a unique and immutable value, often used as object property keys.



## Solution 4
*Reference: [Question 4](js-questions.md#question-4)*

### Q. What is the difference between == and === operators?

The `==` (loose equality) and `===` (strict equality) operators both compare values, but the key difference lies in type coercion. The key differences between them are:

1. **Type Coercion**:
   - **`==` (Loose Equality)**: Performs type coercion before comparison. If types differ, JavaScript converts one to match the other. For example, "5" == 5 returns `true` because the string is coerced to a number. This can lead to unexpected results, like `false == 0` being `true`.
   
   - **`===` (Strict Equality)**: Compares both value and type without coercion. So, `"5" === 5` is `false` because one is a string and the other a number. It's safer and more predictable.



2. **Use Cases**:
   - Use `==` when you want to compare values for equality, regardless of their type.
   - Use `===` when you want to ensure that both the value and type are the same.

### Examples:

```javascript
console.log(5 == '5');   // true (type coercion occurs)
console.log(5 === '5');  // false (different types)

console.log(null == undefined);  // true (type coercion occurs)
console.log(null === undefined); // false (different types)
```

In general, it's recommended to use `===` to avoid unexpected behavior due to type coercion.



## Solution 5
*Reference: [Question 5](js-questions.md#question-5)*

### Q. What does NaN stand for, and how can you check if a value is NaN?

NaN stands for "Not a Number," which is a special value in the Number type representing an invalid or unrepresentable numeric result, like the square root of a negative number or 0 / 0.

To check if a value is NaN, you can use the `isNaN()` function or the `Number.isNaN()` method. However, it's important to note that `isNaN()` has some quirks, as it will coerce non-numeric values to numbers before checking. Therefore, it's generally recommended to use `Number.isNaN()` for a more reliable check.

### Examples:

```javascript
console.log(isNaN(NaN));          // true
console.log(isNaN('Hello'));      // true (coerced to NaN)
console.log(isNaN(42));           // false

console.log(Number.isNaN(NaN));          // true
console.log(Number.isNaN('Hello'));      // false (no coercion)
console.log(Number.isNaN(42));           // false
```

In summary, NaN is a unique value in JavaScript that indicates an invalid number, and you can use `Number.isNaN()` for accurate checks.



## Solution 6
*Reference: [Question 6](js-questions.md#question-6)*

### Q. What is the difference between undefined and null?

Both represent absence of value, but they serve different purposes:

- **Undefined**: Indicates a variable has been declared but not assigned a value, or a missing object property or function argument. It's the default for uninitialized variables (e.g., `let x; console.log(x); // undefined`). It's a primitive type.

- **Null**: An intentional assignment meaning "no value" or "empty object reference." It's often used to explicitly clear a variable (e.g., `let y = null;`). Interestingly, `typeof null` returns `"object"` due to a historical bug in JavaScript.

**Key difference**: Undefined is automatic (absence by default), null is deliberate (absence by choice). In JSON, null is supported, but undefined isn't. For best practices, use null for intentional resets and check with strict equality to avoid mixing them up.



### Examples:

```javascript
let a;
console.log(a);          // undefined (not initialized)
console.log(typeof a);   // "undefined"

let b = null;
console.log(b);          // null (intentionally empty)
console.log(typeof b);   // "object"
```

In summary, use `undefined` when a variable has not been assigned a value, and use `null` when you want to explicitly indicate no value.



## Solution 7
*Reference: [Question 7](js-questions.md#question-7)*

### Q. How do you check if a variable is undefined?

To check if a variable is undefined:

**Use strict equality**: `if (variable === undefined) { ... }`. This is precise and avoids coercion.

**Alternatively**, `typeof variable === "undefined"`, which works even if the variable isn't declared (avoids ReferenceError).

Avoid loose checks like if `(!variable)` because falsy values (e.g., 0, "") would also trigger it.

In modern code, optional chaining (`?`) or nullish coalescing (`??`) can handle undefined gracefully, like `value ?? 'default`'. This ensures code resilience, especially in APIs where data might be missing.



## Solution 8
*Reference: [Question 8](js-questions.md#question-8)*

### Q. What is the typeof operator, and what values does it return?

The `typeof` operator is used to determine the type of a given variable or value in JavaScript. It returns a string indicating the type of the unevaluated operand.

### Possible return values:

- `"undefined"`: If the variable is not assigned a value.
- `"boolean"`: If the variable is a boolean.
- `"number"`: If the variable is a number.
- `"bigint"`: If the variable is a bigint.
- `"symbol"`: If the variable is a symbol.
- `"string"`: If the variable is a string.
- `"object"`: If the variable is an object (including arrays and null).
- `"function"`: If the variable is a function.

### Examples:

```javascript
console.log(typeof undefined);    // "undefined"
console.log(typeof true);         // "boolean"
console.log(typeof 42);           // "number"
console.log(typeof 42n);         // "bigint"
console.log(typeof Symbol());    // "symbol"
console.log(typeof "Hello");     // "string"
console.log(typeof { name: "Alice" }); // "object"
console.log(typeof [1, 2, 3]);   // "object" (arrays are objects)
console.log(typeof null);        // "object" (historical bug)
console.log(typeof function() {}); // "function"
```

In summary, the `typeof` operator is a useful tool for checking the type of a variable or value in JavaScript.



## Solution 9
*Reference: [Question 9](js-questions.md#question-9)*

### Q. Explain type coercion in JavaScript with examples.

Type coercion in JavaScript refers to the automatic or implicit conversion of values from one data type to another. This can happen in various scenarios, such as during comparisons, arithmetic operations, or when using certain operators. JavaScript is a loosely typed language, which means it allows for flexible type conversions, but this can sometimes lead to unexpected results.

### Examples:

1. **String and Number Coercion**:
   ```javascript
   console.log("5" + 3); // "53" (string concatenation)
   console.log("5" - 3); // 2 (string is coerced to number)
   ```

2. **Boolean Coercion**:
   ```javascript
   console.log(true + 1); // 2 (true is coerced to 1)
   console.log(false + 1); // 1 (false is coerced to 0)
   ```

3. **Equality Coercion**:
   ```javascript
   console.log(0 == "0"); // true (string is coerced to number)
   console.log(0 === "0"); // false (no coercion, different types)
   ```

4. **Null and Undefined Coercion**:
   ```javascript
   console.log(null == undefined); // true (both are treated as "empty")
   console.log(null === undefined); // false (different types)
   ```

In summary, while type coercion can be useful, it can also lead to bugs if not properly understood. It's often recommended to use strict equality (`===`) to avoid unintended coercion.



## Solution 10
*Reference: [Question 10](js-questions.md#question-10)*

### Q. What are falsy values in JavaScript?

Falsy values are values that evaluate to `false` when encountered in a Boolean context. In JavaScript, the following values are considered falsy:

1. `false`: The Boolean value false.
2. `0`: The number zero.
3. `-0`: The negative zero.
4. `0n`: The BigInt zero.
5. `""`: An empty string.
6. `null`: Represents the intentional absence of any object value.
7. `undefined`: A variable that has been declared but has not yet been assigned a value.
8. `NaN`: Represents a value that is not a number.

### Examples:

```javascript
if (!false) {
    console.log("This is false");
}

if (!0) {
    console.log("This is zero");
}

if (!"") {
    console.log("This is an empty string");
}

if (!null) {
    console.log("This is null");
}

if (!undefined) {
    console.log("This is undefined");
}

if (!NaN) {
    console.log("This is NaN");
}
```

In summary, falsy values are those that evaluate to false in a Boolean context, and they can lead to unexpected behavior if not properly understood.


# Variable Scope and Declarations



## Solution 11
*Reference: [Question 11](js-questions.md#question-11)*

### Q. What are the differences between var, let, and const?

In JavaScript, var, let, and const are used for variable declarations, but they differ significantly in scope, hoisting behavior, and mutability—key to writing bug-free, maintainable code.

- **Scope**: 
  - `var` is function-scoped or globally-scoped, meaning it is accessible within the function it was declared in or globally if declared outside a function.
  - `let` and `const` are block-scoped, meaning they are only accessible within the block (enclosed by `{}`) they were declared in.
  
- **Hoisting**:
  - `var` declarations are hoisted to the top of their containing function or global scope, meaning they can be referenced before their declaration (but will be `undefined` until the declaration is reached).
  - `let` and `const` declarations are also hoisted, but they are not initialized, leading to a "temporal dead zone" where they cannot be accessed until the declaration is encountered.

- **Mutability**:
  - Variables declared with `var` and `let` can be reassigned.
  - Variables declared with `const` cannot be reassigned, making them immutable (though the contents of objects or arrays declared with `const` can still be modified).

- **Global Object**:
  - Variables declared with `var` in the global scope become properties of the global object (e.g., `window` in browsers).

  - Variables declared with `let` and `const` do not create properties on the global object.

- **Best Practices**:
  - Use `let` and `const` instead of `var` to avoid issues with scope and hoisting.
  - Prefer `const` for variables that should not be reassigned, and use `let` for those that will be.
  - Use `const` for objects and arrays that should not be modified.

**Examples**:

```javascript
// var example
var x = 10;
if (true) {
    var x = 20; // same variable
    console.log(x); // 20
}
console.log(x); // 20

// let example
let y = 10;
if (true) {
    let y = 20; // different variable
    console.log(y); // 20
}
console.log(y); // 10

// const example
const z = 10;
if (true) {
    const z = 20; // different variable
    console.log(z); // 20
}
console.log(z); // 10
```
In summary, prefer `let` and `const` for better scoping and immutability, and avoid `var` to prevent potential pitfalls.



## Solution 12
*Reference: [Question 12](js-questions.md#question-12)*

### Q. What is hoisting in JavaScript?

Hoisting in JavaScript is the language’s way of moving certain declarations to the top of their scope before any code runs. This happens during the compilation phase, so when execution begins, JavaScript already “knows” about your variables and functions — even if they’re written further down in the code.

- **Variable Hoisting**: Variables declared with `var` are hoisted to the top of their function or global scope, meaning they can be referenced before their declaration (but will be `undefined` until the declaration is reached). Variables declared with `let` and `const` are also hoisted, but they are not initialized, leading to a "temporal dead zone" where they cannot be accessed until the declaration is encountered.

- **Function Hoisting**: Function declarations are hoisted completely, meaning you can call a function before it is defined in the code. However, function expressions (including arrow functions) are not hoisted in the same way, and attempting to call them before their definition will result in an error.

- **Example**:
```javascript
// Variable Hoisting
console.log(a); // undefined
var a = 5;
console.log(a); // 5

console.log(c); // ReferenceError: Cannot access 'c' before initialization
const c = 15;
console.log(c); // 15

// function Hoisting
fn(); // Works!
function fn() { console.log('Hoisted!'); }
```



## Solution 13
*Reference: [Question 13](js-questions.md#question-13)*

### Q. What is the temporal dead zone (TDZ)?

The temporal dead zone (TDZ) is a behavior in JavaScript that occurs when a variable is accessed before it has been declared. This is particularly relevant for variables declared with `let` and `const`, which are block-scoped and not initialized until their declaration is reached.

In the TDZ, any attempt to access the variable before its declaration will result in a `ReferenceError`. This is because, unlike `var`, which is hoisted and initialized to `undefined`, `let` and `const` are not initialized at all until their declaration is encountered.

- Introduced in ES6 to fix var's issues.
- Applies to `let`, `const`, and classes (not `var` or functions).
- TDZ ends at the declaration, even if initialization happens later (e.g., `let x; console.log(x); // undefined` is fine after declaration).

**Example**:

```javascript
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
const b = 10;
```



## Solution 14
*Reference: [Question 14](js-questions.md#question-14)*

### Q. Explain block scope vs function scope.

Scope determines variable accessibility and lifetime in JavaScript, with two main types:

- **Function Scope**: Variables declared with `var` are scoped to the nearest function (or global if none). They persist until the function ends and are inaccessible outside. Nested functions create closures, capturing outer scopes.

- **Block Scope**: Introduced in ES6 with `let` and `const`, confines variables to the nearest block (delimited by {}). Ideal for loops, conditionals, or try-catch to avoid leakage.

**Example**:
```javascript
function example() {
    var a = 1;
    let b = 2;
    const c = 3;

    if (true) {
        var a = 4; // same variable
        let b = 5; // different variable
        const c = 6; // different variable
        console.log(a); // 4 (block scope)
        console.log(b); // 5 (block scope)
        console.log(c); // 6 (block scope)
    }

    console.log(a); // 4 
    console.log(b); // 2 (function scope)
    console.log(c); // 3 (function scope)
}
```
In summary, prefer `let` and `const` for better scoping and immutability, and avoid `var` to prevent potential pitfalls.



## Solution 15
*Reference: [Question 15](js-questions.md#question-15)*

### Q. What is global scope, and how can variables leak into it?

Global scope refers to the outermost scope in a JavaScript program, where variables are accessible from anywhere in the code. Variables declared outside of any function or block are in the global scope.

Variables can leak into the global scope in several ways:

1. **Implicit Global Variables**: If you assign a value to a variable without declaring it with `var`, `let`, or `const`, it becomes a global variable.
   ```javascript
   function leak() {
       a = 10; // Implicitly global
   }
   leak();
   console.log(a); // 10
   ```

2. **Global Object Properties**: In browsers, global variables are properties of the `window` object. You can create global variables by attaching them to `window`.
   ```javascript
   function createGlobal() {
       window.b = 20;
   }
   createGlobal();
   console.log(b); // 20
   ```

3. **Function Scope Leakage**: If a variable is declared with `var` inside a function, it is function-scoped. However, if you forget to use `var`, `let`, or `const`, it will leak to the global scope.
   ```javascript
   function leakVar() {
       var c = 30; // Function-scoped
       d = 40; // Implicitly global
   }
   leakVar();
   console.log(c); // ReferenceError
   console.log(d); // 40
   ```

To avoid leaking variables into the global scope, always use `var`, `let`, or `const` when declaring variables.



## Solution 16
*Reference: [Question 16](js-questions.md#question-16)*

### Q. What happens if you declare a variable without var, let, or const?

If you declare a variable without using `var`, `let`, or `const`,  (e.g., `x = 5;`) it becomes an implicit global variable. This means it is accessible from anywhere in your code, which can lead to unintended consequences and bugs.

**Example**:
```javascript
function implicitGlobal() {
    x = 5; // Implicitly global
}
implicitGlobal();
console.log(x); // 5
```

In the example above, the variable `x` is declared without any keyword, making it a global variable. This can cause conflicts if other parts of the code use the same variable name.

To avoid this issue, always use `var`, `let`, or `const` when declaring variables.



## Solution 17
*Reference: [Question 17](js-questions.md#question-17)*

### Q. Can you redeclare variables declared with let or const?

No, you cannot redeclare variables declared with `let` or `const` within the same scope. Attempting to do so will result in a `SyntaxError`.

**Example**:
```javascript
let a = 1;
const b = 2;

let a = 3; // SyntaxError: Identifier 'a' has already been declared
const b = 4; // SyntaxError: Identifier 'b' has already been declared
```

However, shadowing in inner scopes is allowed (e.g., nested blocks). This enforces intentionality, reducing bugs in complex codebases.

**Example**:
```javascript
let a = 1;
const b = 2;

if (true) {
    let a = 3; // Different variable
    const b = 4; // Different variable
    console.log(a); // 3
    console.log(b); // 4
}

console.log(a); // 1
console.log(b); // 2
```



## Solution 18
*Reference: [Question 18](js-questions.md#question-18)*

### Q. What is variable shadowing?

Variable shadowing occurs when an inner scope declares a variable with the same name as an outer one, "hiding" the outer variable temporarily. This can lead to confusion and bugs if not managed carefully.

**Example**:
```javascript
let a = 1;

if (true) {
    let a = 2; // Shadowing outer 'a'
    console.log(a); // 2
}

console.log(a); // 1
```



## Solution 19
*Reference: [Question 19](js-questions.md#question-19)*

### Q. What is an Immediately Invoked Function Expression (IIFE)?

An IIFE, or Immediately Invoked Function Expression, is a JavaScript function that runs as soon as it is defined. It is a common design pattern used to create a new scope and avoid polluting the global namespace.

**Example**:
```javascript
(function() {
    let a = 1;
    console.log(a); // 1
})();
```
Benefits of IIFE is that it creates a new scope, preventing variables from leaking into the global scope and avoiding potential naming conflicts. This is particularly useful in modular programming and when working with asynchronous code.



## Solution 20
*Reference: [Question 20](js-questions.md#question-20)*

### Q. What does 'use strict' mode do in JavaScript?

`'use strict'` is a directive introduced in ECMAScript 5 that enables strict mode in JavaScript. When a script or function is executed in strict mode, it operates under a stricter set of rules, which helps catch common coding mistakes and "unsafe" actions.

Some key features of strict mode include:

1. **Elimination of `this` coercion**: In strict mode, if a function is called without an explicit `this` value, `this` will be `undefined` instead of the global object.

2. **Prevention of variable leakage**: Variables must be declared with `var`, `let`, or `const`. Assigning a value to an undeclared variable will throw an error.

3. **Read-only properties**: Attempting to write to a read-only property will throw an error.

4. **No duplicate parameter names**: Functions cannot have duplicate parameter names.

**Example**:
```javascript
'use strict';

x = 1; // ReferenceError

function strictFunction() {
    // ...
}
```