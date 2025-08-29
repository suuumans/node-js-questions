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


# Functions in JavaScript

## Solution 21
*Reference: [Question 21](js-questions.md#question-21)*

### Q. What is a function in JavaScript, and how do you define one?

A function in JavaScript is a reusable block of code that performs a specific task, encapsulating logic for modularity and abstraction. Functions are first-class citizens, meaning they can be assigned to variables, passed as arguments, returned from other functions, and even have properties—enabling paradigms like functional programming.

Functions can be defined in several ways:

- **Function Declarations**: These are the most common way to define a function. They are hoisted, meaning they can be called before they are defined in the code.
  ```javascript
  function add(a, b) {
      return a + b;
  }
  ```

- **Function Expressions**: These involve creating a function and assigning it to a variable. They are not hoisted, so they cannot be called before they are defined.
  ```javascript
  const add = function(a, b) {
      return a + b;
  };
  ```

- **Arrow Functions**: Introduced in ES6, arrow functions provide a more concise syntax for writing function expressions. They do not have their own `this` context.
  ```javascript
  const add = (a, b) => a + b;
  ```

Functions can be invoked with (), and they support parameters, returns, and scopes. They can be called multiple times with different arguments, making code more reusable and organized.



## Solution 22
*Reference: [Question 22](js-questions.md#question-22)*

### Q. What is the difference between function declarations and function expressions?

Function declarations and expressions both define functions, but they differ in hoisting, naming, and use cases, impacting code organization and debugging.
- **Function Declarations**:
  - Syntax: `function name() { ... }`
  - Fully hoisted (declaration and body), callable before definition.
  - Named, aiding stack traces.
  - Best for standalone utilities.

  ```javascript
  console.log(calculateArea(5)); // 'Declared!' (hoisted)
  function calculateArea(radius) {
      return Math.PI * radius * radius;
  }
  ```

- **Function Expressions**:
  - Syntax: `const name = function() { ... };` (or anonymous).
  - Only the variable is hoisted (as `undefined` for `var`, TDZ for `let`/`const`), so invocation before assignment errors.
  - Can be anonymous, but naming helps debugging (e.g., `const named = function namedFn() { ... };`).
  - Ideal for IIFEs, callbacks, or conditional definitions.

  ```javascript
  console.log(calculateArea(5)); // TypeError or ReferenceError
  const calculateArea = function(radius) {
    return Math.PI * radius * radius;
  };
  ```
In summary, function declarations are hoisted and can be called before their definition, while function expressions are not hoisted in the same way and cannot be called before they are defined.


## Solution 23
*Reference: [Question 23](js-questions.md#question-23)*

### Q. What are arrow functions, and how do they differ from regular functions?

Arrow functions are a more concise syntax for writing function expressions in JavaScript. They differ from regular functions in several key ways:

- **Syntax**: Arrow functions use a shorter syntax, omitting the `function` keyword and using the `=>` (fat arrow) notation.
   ```javascript
   const add = (a, b) => a + b;
   ```

- **Lexical `this`**: Arrow functions do not have their own `this` context. Instead, they inherit `this` from the surrounding lexical scope, making them ideal for use in callbacks and methods where you want to preserve the context.
   ```javascript
   function Counter() {
       this.count = 0;
       setInterval(() => {
           this.count++;
           console.log(this.count); // Lexical scoping of `this`
       }, 1000);
   }
   ```

- **No `arguments` object**: Arrow functions do not have their own `arguments` object. If you need to access arguments, you must use rest parameters or rely on the outer function's `arguments`.

   ```javascript
   // Simple arrow function
   const greet = (name) => `Hello ${name}!`;
   console.log(greet('John')); // Hello John!

   // Arrow function with multiple parameters
   const multiply = (a, b) => a * b;
   console.log(multiply(2, 3)); // 6

   // Arrow function with rest parameters
   const joinWords = (...words) => words.join(' ');
   console.log(joinWords('Hello', 'there', 'friend')); // Hello there friend
   ```

- **Cannot be used as constructors**: Arrow functions cannot be used with the `new` keyword, as they do not have a `[[Construct]]` method.
   ```javascript
   const Person = (name) => {
       this.name = name;
   };
   const john = new Person('John'); // TypeError
   ```

## Solution 24
*Reference: [Question 24](js-questions.md#question-24)*

### Q. Explain the 'this' keyword in JavaScript.

The `this` keyword in JavaScript refers to the context in which a function is called. Its value can change depending on how a function is invoked. Here are some key points about `this`:

1. **Global Context**: In the global execution context (outside of any function), `this` refers to the global object. In browsers, this is the `window` object.
   ```javascript
   console.log(this); // Window object
   ```

2. **Function Context**: Inside a regular function, `this` refers to the object that called the function. If the function is called as a method of an object, `this` refers to that object.
   ```javascript
   const obj = {
       name: 'John',
       greet: function() {
           console.log(this.name);
       }
   };
   obj.greet(); // John
   ```

3. **Arrow Functions**: Arrow functions do not have their own `this` context. Instead, they inherit `this` from the surrounding lexical scope.
   ```javascript
   const obj = {
       name: 'John',
       greet: function() {
           const arrow = () => console.log(this.name);
           arrow();
       }
   };
   obj.greet(); // John
   ```

4. **Event Handlers**: In event handlers, `this` refers to the element that triggered the event.
   ```javascript
   const button = document.querySelector('button');
   button.addEventListener('click', function() {
       console.log(this); // button element
   });
   ```

5. **Explicit Binding**: You can explicitly set the value of `this` using `call()`, `apply()`, or `bind()`.


## Solution 25
*Reference: [Question 25](js-questions.md#question-25)*

### Q. What are the differences between call(), apply(), and bind()?

`call()`, `apply()`, and `bind()` are methods available on all JavaScript functions that allow you to explicitly set the value of 'this' within a function, but they have different use cases and syntax:

- `call()` invokes a function with a specified `this` value and individual arguments.
- `apply()` invokes a function with a specified `this` value and an array of arguments.
- `bind()` creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

- **call():**
    - Invokes a function with a specified 'this' value and arguments provided individually
    - Syntax: `function.call(thisArg, arg1, arg2, ...)`.
    - Executes the function immediately
    ```typescript
    function greet(greeting) {
        return `${greeting}, ${this.name}`;
        }
    
        const person = { name: 'John' };
    ```

- **apply():**
    - Similar to call(), but accepts arguments as an array
    - Syntax: `function.apply(thisArg, [argsArray])`
    - Executes the function immediately
    - Useful when arguments are already in an array
    ```javascript
    function introduce(greeting, message) {
        return `${greeting}, ${this.name}. ${message}`;
    }

    const person = { name: 'John' };
    console.log(introduce.apply(person, ['Hello', 'How are you?'])); // "Hello, John. How are you?"
    ```

- **bind():**
    - Creates a new function with a bound 'this' value without executing it
    - Syntax: `function.bind(thisArg, arg1, arg2, ...)`
    - Does not execute the function immediately, returns a bound function that can be called later
    - Arguments can be partially applied
    ```javascript
    function calculateTax(rate) {
        return this.amount * rate;
    }

    const product = { amount: 100 };
    const calculateProductTax = calculateTax.bind(product);
    console.log(calculateProductTax(0.1)); // 10

    // Partial application
    const calculateProductTaxAt20Percent = calculateTax.bind(product, 0.2);
    console.log(calculateProductTaxAt20Percent()); // 20
    ```

**Examples of `call()`, `apply()`, and `bind()` together**:
   ```javascript
   // Example with a calculator object
   const calculator = {
       multiply: function(a, b) {
           return a * b;
       },
       sum: function(...numbers) {
           return numbers.reduce((total, num) => total + num, 0);
       }
   };

   // 1. call() - calls a function with a given 'this' and arguments passed individually
   const numbers = {
       numbers: [5, 6],
       getProduct() {
           return this.numbers[0] * this.numbers[1];
       }
   };
   console.log(numbers.getProduct.call({ numbers: [10, 2] })); // 20

   // 2. apply() - same as call(), but arguments passed as an array
   const prices = [10.5, 9.99, 8.75, 12.99];
   console.log(calculator.sum.apply(null, prices)); // 42.23

   // 3. bind() - creates a new function with a fixed 'this' value
   const discountCalculator = {
       discount: 0.1,
       calculateFinal(price) {
           return price - (price * this.discount);
       }
   };

   const calculate20PercentDiscount = discountCalculator.calculateFinal.bind({ discount: 0.2 });
   console.log(calculate20PercentDiscount(100)); // 80
   ```

This method is particularly useful for borrowing methods from other objects and working with callbacks.

## Solution 26
*Reference: [Question 26](js-questions.md#question-26)*

### Q. What are higher-order functions? Provide an example.

Higher-order functions (HOFs) are functions that either take one or more functions as arguments or return a function as their result. They are a powerful concept in JavaScript that enables functional programming patterns like composition, abstraction, and behavior parameterization.

Examples -  map(), filter(), and reduce() are all higher-order functions.
Custom example:
```javascript
// Array.map() is a built-in higher-order function
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// Custom higher-order function example
function createMultiplier(factor) {
  // Returns a new function
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

## Solution 27
*Reference: [Question 27](js-questions.md#question-27)*

### Q. What is currying in JavaScript?

Currying is a functional programming technique in which a function is transformed into a sequence of functions, each taking a single argument. Instead of taking all arguments at once, a curried function takes one argument and returns a new function that takes the next argument, and so on, until all arguments are provided.

- It transforms a function with multiple arguments into a sequence of functions.
- Each returned function takes exactly one argument.
- It allows for partial application of function arguments.
- It increases code reusability and composability.

Example:
```javascript
// Non-curried function
function add(a, b, c) {
  return a + b + c;
}

// Curried version
function curriedAdd(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

// Using the curried function
console.log(curriedAdd(1)(2)(3)); // 6

// Partial application
const addOne = curriedAdd(1);
const addOneAndTwo = addOne(2); // 3
console.log(addOneAndTwo(3)); // 6

// With ES6 arrow functions, the syntax becomes more concise
const arrowCurriedAdd = a => b => c => a + b + c;
console.log(arrowCurriedAdd(1)(2)(3)); // 6
```

## Solution 28
*Reference: [Question 28](js-questions.md#question-28)*

### Q. What is a pure function?

A pure function is a fundamental concept in functional programming that has two main characteristics:
1. **Deterministic:** Given the same inputs, a pure function always returns the same output.

2. **No side effects:** A pure function doesn't modify external state, mutate arguments, or perform operations that affect anything outside its scope (like I/O operations, DOM manipulations, or network requests).

**Key benefits of pure functions:**
- Predictability and easier debugging
- Testability (no external dependencies to mock)
- Memoization potential (caching results)
- Safe for parallelization and concurrency
- Referential transparency (can be replaced with their return values)

```javascript
// Pure function
function add(a, b) {
  return a + b;
}

// Pure function
function calculateArea(radius) {
  return Math.PI * radius * radius;
}

// Pure function for data transformation
function mapUserNames(users) {
  return users.map(user => user.name);
}
```
**Example of an impure function**:
```javascript
// Impure (depends on external state)
let total = 0;
function addToTotal(value) {
  total += value; // Side effect: modifies external state
  return total;
}

// Impure (performs I/O)
function logMessage(message) {
  console.log(message); // Side effect: I/O operation
}

// Impure (mutates input)
function addItemToCart(cart, item) {
  cart.push(item); // Side effect: mutates the input array
  return cart;
}
```

## Solution 29
*Reference: [Question 29](js-questions.md#question-29)*

### Q. How do default parameters work in functions?

Default parameters allow named parameters to be initialized with default values if no value or `undefined` is passed. This feature helps to make functions more flexible and easier to use. This feature was introduced in ES6 (ECMAScript 2015) and helps make functions more robust and flexible.

**Key aspects of default parameters:**
- They provide fallback values when arguments are omitted or undefined
- They are evaluated at call time, not when the function is defined
- They can be expressions, not just simple values
- They can refer to previous parameters in the same function signature

Example:
```javascript
function multiply(a, b = 1) {
  return a * b;
}

console.log(multiply(5, 2)); // 10
console.log(multiply(5));    // 5 (b is 1 by default)
```

**More complex examples:**
```javascript
// Default parameters can be expressions
function calculateTax(amount, taxRate = amount * 0.1) {
  return amount + taxRate;
}

console.log(calculateTax(100));     // 110
console.log(calculateTax(100, 20)); // 120

// Default parameters can reference previous parameters
function createUser(name, role = 'user', permissions = getDefaultPermissions(role)) {
  return { name, role, permissions };
  
  function getDefaultPermissions(role) {
    return role === 'admin' ? ['read', 'write', 'delete'] : ['read'];
  }
}

console.log(createUser('John'));                // { name: 'John', role: 'user', permissions: ['read'] }
console.log(createUser('Admin', 'admin'));      // { name: 'Admin', role: 'admin', permissions: ['read', 'write', 'delete'] }
console.log(createUser('Jane', 'editor', []));  // { name: 'Jane', role: 'editor', permissions: [] }
```
Default parameters are particularly useful when creating flexible utility functions and APIs, reducing the need for extensive parameter checking within function bodies.

## Solution 30
*Reference: [Question 30](js-questions.md#question-30)*

### Q. What are rest parameters, and how are they used?

Rest parameters allow a function to accept an indefinite number of arguments as an array. This feature was introduced in ES6 (ECMAScript 2015) and provides a more flexible way to work with function arguments.

**Key aspects of rest parameters:**
- They are defined using the `...` syntax before the last parameter in a function signature.
- They collect all remaining arguments into an array.
- They can be used in combination with other named parameters.

Example:
```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3));       // 6
console.log(sum(1, 2, 3, 4, 5)); // 15
console.log(sum());              // 0
```

**More complex examples:**
```javascript
// Rest parameters can be used with other named parameters
function concatenateStrings(separator, ...strings) {
  return strings.join(separator);
}

console.log(concatenateStrings(', ', 'apple', 'banana', 'cherry')); // "apple, banana, cherry"

// Rest parameters can be useful for variadic functions
function logMessages(...messages) {
  messages.forEach(msg => console.log(msg));
}

logMessages('Hello', 'World', 'This', 'is', 'JavaScript');
```
Rest parameters are particularly useful when creating functions that need to handle a variable number of arguments without explicitly defining each one.


# Arrays in JavaScript

## Solution 31
*Reference: [Question 31](js-questions.md#question-31)*

### Q. How do you create an array in JavaScript?

Creating an array in JavaScript is straightforward and flexible, as arrays are dynamic, resizable, and can hold mixed types. They're zero-indexed and inherit from Array.prototype, offering built-in methods.

Ways to create:
- **Literal Syntax**: Most common and performant for simple initialization.
```javascript
const arr = [1, 'two', true]; // Mixed types allowed
```

- **Array Constructor**: Useful for pre-allocating length or from arguments.
```javascript

const empty = new Array(5); // [ <5 empty items> ] – sparse array
const fromArgs = new Array(1, 2, 3); // [1, 2, 3]
```

- **Array.of()**: ES6 method; handles single numeric arg differently from constructor.
```javascript
const single = Array.of(5); // [5] vs. new Array(5) which is sparse
```

- **Array.from()**: ES6; creates from array-like (e.g., NodeList, strings) or iterables, with optional mapping.
```javascript
const fromString = Array.from('hello'); // ['h', 'e', 'l', 'l', 'o']
const mapped = Array.from({length: 3}, (_, i) => i * 2); // [0, 2, 4]
```
Arrays aren't truly arrays but objects with numeric keys— `typeof [] === 'object', but Array.isArray([]) === true.`



## Solution 32
*Reference: [Question 32](js-questions.md#question-32)*

### Q. What is the difference between push() and concat()?

Both `push()` and `concat()` add elements to arrays, but they differ in mutability, return values, and handling multiple additions—key for immutable patterns in functional programming.

- **`push()`**: Mutates the original array by appending one or more elements; returns the new length.     
  - Ideal for in-place modifications, but avoid in pure functions to prevent side effects.

```javascript
// push() - adds elements to the end of an array and returns the new length
const numbers = [1, 2, 3];
const length = numbers.push(4, 5);
console.log(numbers); // [1, 2, 3, 4, 5]
console.log(length);  // 5
```

- **`concat()`**: Non-mutating; returns a new array by merging the original with arguments (elements or arrays).
  - Handles arrays as spreads; great for immutability.

```javascript
// concat() - combines arrays and/or values and returns a new array
const originalArray = [1, 2, 3];
const newArray = originalArray.concat([4, 5], 6);
console.log(originalArray); // [1, 2, 3] - unchanged
console.log(newArray);      // [1, 2, 3, 4, 5, 6]
```

Key differences:
1. **Mutability**: `push()` modifies the original array (mutating method), while `concat()` returns a new array without modifying the original (non-mutating).
2. **Return value**: `push()` returns the new length of the array, while `concat()` returns a new array.
3. **Array flattening**: `concat()` flattens arrays one level deep, while `push()` adds arrays as elements.

```javascript
// Demonstrating array flattening difference
const arr1 = [1, 2];
arr1.push([3, 4]);
console.log(arr1); // [1, 2, [3, 4]]

const arr2 = [1, 2];
const arr3 = arr2.concat([3, 4]);
console.log(arr3); // [1, 2, 3, 4]
```

## Solution 33
*Reference: [Question 33](js-questions.md#question-33)*

### Q. Explain the difference between splice() and slice().

Both `splice()` and `slice()` manipulate arrays by modifying their contents, but they differ in mutability, return values, and handling removals—key for immutable patterns in functional programming.

```javascript
// splice() - changes the contents of an array by removing, replacing, or adding elements
const months = ['Jan', 'Feb', 'Apr', 'May'];
const removed = months.splice(2, 0, 'Mar'); // Insert at index 2, remove 0 elements
console.log(months); // ['Jan', 'Feb', 'Mar', 'Apr', 'May']
console.log(removed); // [] (nothing was removed)

// Remove and replace elements
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'];
const removedDays = days.splice(2, 2, 'Wednesday', 'Thursday');
console.log(days); // ['Mon', 'Tue', 'Wednesday', 'Thursday', 'Fri']
console.log(removedDays); // ['Wed', 'Thu'] (removed elements)

// slice() - returns a shallow copy of a portion of an array
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
const sliced = animals.slice(1, 4);
console.log(animals); // ['ant', 'bison', 'camel', 'duck', 'elephant'] (unchanged)
console.log(sliced); // ['bison', 'camel', 'duck']
```
Key differences:
1. **Mutability**: `splice()` modifies the original array, while `slice()` creates a new array without modifying the original.
2. **Parameters**:
  - `splice(start, deleteCount, ...items)` - start index, number of elements to delete, and elements to insert
  - `slice(start, end)` - start index (inclusive) and end index (exclusive)
3. **Return value**: `splice()` returns an array of removed elements, while `slice()` returns a new array with extracted elements.
4. **Negative indices**: Both support negative indices to count from the end of the array.

I find the mnemonic "splice = surgery" helpful for remembering that splice() modifies the array, while "slice = sampling" suggests taking a non-destructive view.

## Solution 34
*Reference: [Question 34](js-questions.md#question-34)*

### Q. What are the different ways to iterate over an array?

JavaScript offers multiple iteration methods, from imperative to declarative, balancing readability, performance, and control flow—essential for processing large datasets efficiently.

1. **forEach()**: Executes a provided function once for each array element.
   ```javascript
   const numbers = [1, 2, 3];
   numbers.forEach((num) => console.log(num)); // 1 2 3
   ```

2. **for...of**: Iterates over iterable objects (including arrays) and provides a simpler syntax.
   ```javascript
   const numbers = [1, 2, 3];
   for (const num of numbers) {
       console.log(num); // 1 2 3
   }
   ```

3. **map()**: Creates a new array populated with the results of calling a provided function on every element.
   ```javascript
   const numbers = [1, 2, 3];
   const doubled = numbers.map((num) => num * 2);
   console.log(doubled); // [2, 4, 6]
   ```

4. **filter()**: Creates a new array with all elements that pass the test implemented by the provided function.
   ```javascript
   const numbers = [1, 2, 3, 4, 5];
   const evens = numbers.filter((num) => num % 2 === 0);
   console.log(evens); // [2, 4]
   ```

5. **reduce()**: Executes a reducer function on each element, resulting in a single output value.
   ```javascript
   const numbers = [1, 2, 3];
   const sum = numbers.reduce((acc, num) => acc + num, 0);
   console.log(sum); // 6
   ```

6. **for Loop**: A traditional way to iterate over arrays using a counter.
   ```javascript
   const numbers = [1, 2, 3];
   for (let i = 0; i < numbers.length; i++) {
       console.log(numbers[i]); // 1 2 3
   }
   ```

For performance `for` is the fastest, followed by `for...of`, then `forEach`, with `map/filter/reduce` being slower due to function calls and creating new arrays. Choose based on readability vs. performance needs.

## Solution 35
*Reference: [Question 35](js-questions.md#question-35)*

### Q. What do map(), filter(), and reduce() do? Provide examples.

These three methods are the cornerstone of functional programming in JavaScript, enabling powerful data transformations:

- **`map()`**: Creates a new array by applying a function to each element of the original array.

  ```javascript
  const numbers = [1, 2, 3, 4, 5];

  // Double each number
  const doubled = numbers.map(num => num * 2);
  console.log(doubled); // [2, 4, 6, 8, 10]

  // Format array of objects
  const users = [
    { id: 1, name: 'Alice' },
    { id: 2, name: 'Bob' }
  ];
  const usernames = users.map(user => user.name);
  console.log(usernames); // ['Alice', 'Bob']
  ```

- **`filter()`**: creates a new array containing only elements that pass a test function.

  ```javascript
  const numbers = [1, 2, 3, 4, 5];

  // Keep only even numbers
  const evens = numbers.filter(num => num % 2 === 0);
  console.log(evens); // [2, 4]

  // Filter array of objects
  const users = [
    { id: 1, name: 'Alice', age: 25 },
    { id: 2, name: 'Bob', age: 30 },
    { id: 3, name: 'Charlie', age: 35 }
  ];
  const adults = users.filter(user => user.age >= 30);
  console.log(adults); // [{ id: 2, name: 'Bob', age: 30 }, { id: 3, name: 'Charlie', age: 35 }]
  ```

- **`reduce()`**: reduces an array to a single value by applying a function to each element and accumulating the result.

  ```javascript
  const numbers = [1, 2, 3, 4, 5];

  // Sum all numbers
  const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
  console.log(sum); // 15

  // Find maximum value
  const max = numbers.reduce((max, num) => num > max ? num : max, numbers[0]);
  console.log(max); // 5

  // Group objects by property
  const transactions = [
    { id: 1, type: 'debit', amount: 100 },
    { id: 2, type: 'credit', amount: 50 },
    { id: 3, type: 'debit', amount: 200 },
    { id: 4, type: 'credit', amount: 150 }
  ];

  const grouped = transactions.reduce((groups, transaction) => {
    const type = transaction.type;
    if (!groups[type]) {
      groups[type] = [];
    }
    groups[type].push(transaction);
    return groups;
  }, {});

  console.log(grouped);
  // {
  //   debit: [
  //     { id: 1, type: 'debit', amount: 100 },
  //     { id: 3, type: 'debit', amount: 200 }
  //   ],
  //   credit: [
  //     { id: 2, type: 'credit', amount: 50 },
  //     { id: 4, type: 'credit', amount: 150 }
  //   ]
  // }
  ```

These methods can be chained for complex data transformations:

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Calculate sum of squares of even numbers
const sumOfSquaresOfEvens = numbers
  .filter(num => num % 2 === 0)  // Get even numbers: [2, 4, 6, 8, 10]
  .map(num => num * num)         // Square them: [4, 16, 36, 64, 100]
  .reduce((sum, square) => sum + square, 0); // Sum: 220

console.log(sumOfSquaresOfEvens); // 220
```

## Solution 36
*Reference: [Question 36](js-questions.md#question-36)*

### Q. What is the difference between find() and filter()?

- `find()` returns the first element that matches the condition, or undefined if none is found.
- `filter()` returns an array of all elements that match the condition.

Example
```javascript
const numbers = [5, 12, 8, 130, 44];

// find() returns the first element that satisfies the condition
const found = numbers.find(num => num > 10);
console.log(found); // 12

// filter() returns an array of all elements that satisfy the condition
const filtered = numbers.filter(num => num > 10);
console.log(filtered); // [12, 130, 44]
```

**Key differences:**
1. **Return value**:
  - `find()` returns the first matching element itself (or `undefined` if none found)
  - `filter()` returns a new array containing all matching elements (or empty array if none found)
2. **Performance**:
  - `find()` stops iterating once it finds a match
  - `filter()` always iterates through the entire array
3. **Use cases**:
  - Use `find()` when you need just one result (like finding a user by ID)
  - Use `filter()` when you need all matching elements (like getting all active users)

## Solution 37
*Reference: [Question 37](js-questions.md#question-37)*

### Q. How do you check if an array includes a specific value?

JavaScript provides several methods to check if an array includes a specific value. Also there is a method to check if an array includes a specific value, which is `Array.includes(value)`.

```javascript
const fruits = ['apple', 'banana', 'orange', 'mango'];

// 1. includes() method (ES6) - most straightforward
const hasApple = fruits.includes('apple');
console.log(hasApple); // true

// includes() with fromIndex parameter (start searching from index 2)
console.log(fruits.includes('apple', 2)); // false

// 2. indexOf() method - returns index or -1
const bananaIndex = fruits.indexOf('banana');
console.log(bananaIndex); // 1
console.log(fruits.indexOf('grape')); // -1

const hasGrape = fruits.indexOf('grape') !== -1;
console.log(hasGrape); // false

// 3. some() method - for more complex conditions
const hasM = fruits.some(fruit => fruit.startsWith('m'));
console.log(hasM); // true
```
For primitive values, `includes()` is generally preferred as it's more readable and handles edge cases like `NaN` correctly. For complex conditions or finding objects, `some()` provides more flexibility.

## Solution 38
*Reference: [Question 38](js-questions.md#question-38)*

### Q. How does the sort() method work, and how do you sort an array of numbers correctly?

The sort() method sorts elements of an array in place and returns the sorted array. It's a mutating method, meaning it modifies the original array.
`sort(compareFn)` mutates the array, sorting in-place by string conversion default—hence numbers sort lexicographically unless compareFn provided.
  - Without compareFn: Converts to strings, Unicode order (e.g., [10, 2].sort() => [10, 2]).
  
  - With compareFn(a, b): Negative if a < b, positive if a > b, zero if equal.

**For numbers**:
```javascript
const numbers = [10, 2, 5, 1, 100];

// Ascending order
numbers.sort((a, b) => a - b);
console.log(numbers); // [1, 2, 5, 10, 100]

// Descending order
numbers.sort((a, b) => b - a);
console.log(numbers); // [100, 10, 5, 2, 1]
```
**By default**, it converts elements to strings and sorts them based on UTF-16 code units:
```javascript
// Default sort converts to strings (lexicographic sorting)
const fruits = ['banana', 'cherry', 'apple'];
fruits.sort();
console.log(fruits); // ['apple', 'banana', 'cherry']

// PROBLEM: Default sort doesn't work as expected for numbers
const numbers = [10, 2, 5, 1, 100];
numbers.sort();
console.log(numbers); // [1, 10, 100, 2, 5] (incorrect numeric sorting)
```
**Sorting objects by property:**
```javascript
const products = [
  { name: 'Laptop', price: 1200 },
  { name: 'Phone', price: 800 },
  { name: 'Tablet', price: 300 }
];

// Sort by price (ascending)
products.sort((a, b) => a.price - b.price);
console.log(products);
/* [
  { name: 'Tablet', price: 300 },
  { name: 'Phone', price: 800 },
  { name: 'Laptop', price: 1200 }
] */

// Case-insensitive string sorting
const names = ['David', 'alice', 'Bob'];
names.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
console.log(names); // ['alice', 'Bob', 'David']
```

**Important notes about `sort()`:**
- It modifies the original array (mutating method)
- The time and space complexity is not guaranteed and varies by browser
- Modern browsers typically use Timsort (O(n log n))

## Solution 39
*Reference: [Question 39](js-questions.md#question-39)*

### Q. What are flat() and flatMap() methods?

The flat() method flattens an array by one level, while the flatMap() method applies a function to each element of an array and flattens the result. They are both useful in flattening nested arrays.

**`flat()`**: The `flat()` method creates a new array with all sub-array elements concatenated recursively up to the specified depth.

```javascript
const nestedArray = [1, 2, [3, 4, [5, 6]]];

// Default depth is 1
const flattened = nestedArray.flat();
console.log(flattened); // [1, 2, 3, 4, [5, 6]]

// Specify depth to flatten deeper nested arrays
const fullyFlattened = nestedArray.flat(2);
console.log(fullyFlattened); // [1, 2, 3, 4, 5, 6]

// Use Infinity to flatten all nested arrays regardless of depth
const deeplyNested = [1, [2, [3, [4, [5]]]]];
console.log(deeplyNested.flat(Infinity)); // [1, 2, 3, 4, 5]

// flat() also removes empty slots in arrays
const sparseArray = [1, 2, , 4, 5];
console.log(sparseArray.flat()); // [1, 2, 4, 5]
```

**`flatMap()`**: The `flatMap()` method combines `map()` and `flat()` operations with depth 1, providing better performance than calling them separately:

```javascript
const sentences = ['Hello world', 'JavaScript is fun'];

// Split each sentence into words and flatten the result
const words = sentences.flatMap(sentence => sentence.split(' '));
console.log(words); // ['Hello', 'world', 'JavaScript', 'is', 'fun']

// Equivalent to:
// sentences.map(sentence => sentence.split(' ')).flat();

// flatMap() is useful for adding or removing items during mapping
const numbers = [1, 2, 3, 4];

// Generate [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
const repeated = numbers.flatMap(num => Array(num).fill(num));
console.log(repeated); // [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]

// Filter out odd numbers while mapping even numbers to their doubles
const evenDoubles = numbers.flatMap(num => 
  num % 2 === 0 ? [num * 2] : []
);
console.log(evenDoubles); // [4, 8]
```
Both methods create new arrays without modifying the original, following JavaScript's functional programming patterns.

## Solution 40
*Reference: [Question 40](js-questions.md#question-40)*

### Q. What are the ways to copy an array without mutating the original?

JavaScript offers several ways to create copies of arrays without modifying the original.

```javascript
const original = [1, 2, 3, 4, 5];

// 1. Spread operator (ES6) - most common and concise
const copy1 = [...original];

// 2. Array.from() method (ES6)
const copy2 = Array.from(original);

// 3. slice() method (no arguments copies the entire array)
const copy3 = original.slice();

// 4. concat() with an empty array
const copy4 = [].concat(original);

// 5. map() method
const copy5 = original.map(x => x);

// 6. Array.of() with spread
const copy6 = Array.of(...original);

// 7. JSON methods (deep copy, but limited to JSON-serializable data)
const copy7 = JSON.parse(JSON.stringify(original));

console.log(original); // [1, 2, 3, 4, 5] (unchanged)
```

**Important considerations for array copying:**
1. **Shallow vs. Deep Copying**:
  - Most methods above create shallow copies (nested objects/arrays share references)
  - For deep copying of complex nested structures, use:
    - Recursive functions
    - `JSON.parse(JSON.stringify())` (with limitations)

    ```javascript
    // Shallow copy example with nested objects
      const users = [{ name: 'Alice' }, { name: 'Bob' }];
      const shallowCopy = [...users];

      // Modifying the nested object affects both arrays
      shallowCopy[0].name = 'Alicia';
      console.log(users[0].name); // 'Alicia' (also changed)

      // Deep copy example
      const deepCopy = JSON.parse(JSON.stringify(users));
      deepCopy[1].name = 'Bobby';
      console.log(users[1].name); // 'Bob' (unchanged)
    ```
    
- **Performance considerations**:
  - Spread operator and `slice()` are generally the most performant
  - `JSON.parse(JSON.stringify())` is significantly slower and has limitations (doesn't preserve functions, dates, undefined, etc.)

The spread operator ([...array]) is typically the preferred method due to its readability and performance characteristics.

## Solution 41
*Reference: [Question 41](js-questions.md#question-41)*

### Q. How do you create an object in JavaScript?

In JavaScript, objects are collections of key-value pairs and can be created in several ways, each with specific advantages. Creating objects in JavaScript is versatile, as everything except primitives is an object under the hood. 

**Primary ways to create**:

- **Object Literal**: The most concise and efficient for static objects; preferred in modern code for readability.

  ```javascript
  const person = {
    name: 'Alice',
    age: 30,
    greet() { return `Hello, ${this.name}!`; }
  };
  console.log(person.greet()); // 'Hello, Alice!'
  ```
- **Object Constructor**: Similar to the object literal, but with a constructor function. Using `new Object()`; less common but useful for dynamic creation.

  ```javascript
  function Person(firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.greet = function() {
      return `Hello, I'm ${this.firstName}`;
    };
  }

  const john = new Person("John", "Doe", 30);
  console.log(john.greet()); // 'Hello, I'm John'
  ```

- **Classes**: Introduced in ES6, classes are a syntactic sugar for creating object constructors. They provide a more structured and readable way to define and work with objects.

  ```javascript
  class Person {
    constructor(firstName, lastName, age) {
      this.firstName = firstName;
      this.lastName = lastName;
      this.age = age;
    }
    
    greet() {
      return `Hello, I'm ${this.firstName}`;
    }
  }

  const jane = new Person("Jane", "Smith", 28);
  console.log(jane.greet()); // 'Hello, I'm Jane'
  ```

- **Object.create()**: Creates an object with a specified prototype and properties. Useful for prototypal inheritance.

  ```javascript
  const personProto = {
    greet() {
      return `Hello, I'm ${this.firstName}`;
    }
  };

  const suman = Object.create(personProto);
  suman.firstName = "Suman";
  suman.lastName = "Sarkar";
  console.log(suman.greet()); // 'Hello, I'm Suman'
  ```

- **Factory functions**: Functions that return objects. Commonly used for creating multiple instances of the same object type.

  ```javascript
  function createPerson(firstName, lastName, age) {
    return {
      firstName,
      lastName,
      age,
      greet() {
        return `Hello, I'm ${firstName}`;
      }
    };
  }

  const sarah = createPerson("Sarah", "Wilson", 32);
  console.log(sarah.greet()); // 'Hello, I'm Sarah'
  ```
Each approach has specific use cases: literals for simple objects, constructors and classes for creating multiple similar objects, Object.create() for explicit prototype relationships, and factory functions for encapsulation without using 'new'.

## Solution 42
*Reference: [Question 42](js-questions.md#question-42)*

### Q. What is the difference between dot notation and bracket notation for accessing properties?

Both dot notation and bracket notation allow you to access object properties, but they have important differences.

- **Dot notation (obj.prop):** Cleaner for static, valid identifiers (no numbers/spaces/special chars start). Faster lookup in engines like V8.
  - Pros: Readable, concise.
  - Cons: Can't use variables or computed keys.
  ```javascript
    const user = {
      name: "Alex",
      age: 30
    };

    console.log(user.name); // "Alex"
  ```

console.log(user.name); // "Alex"

- **Bracket notation (obj['prop']):** Accepts strings, variables, or expressions; handles any key, including symbols or numbers.
  - Pros: Dynamic, versatile (e.g., for loops).
  - Cons: Verbose, potential for runtime errors if key doesn't exist.
  ```javascript
    const user = {
      name: "Alex",
      age: 30,
      "user-id": "U123"
    };

    console.log(user["name"]); // "Alex"
    console.log(user["user-id"]); // "U123"
  ```

## Solution 43
*Reference: [Question 43](js-questions.md#question-43)*

### Q. ## What does Object.assign() do?

The `Object.assign()` method is a static method that copies the values of all enumerable own properties from one or more source objects to a target object. It returns the modified target object.

- Mutates the target (first arg).
- Overwrites existing keys with last source winning.
- Copies values by reference for objects/arrays (shallow).
- Ignores non-enumerable properties and prototypes.
- Basic syntax: `Object.assign(target, ...sources);`

```javascript
const defaults = { theme: 'light', size: 'medium' };
const userPrefs = { size: 'large' };
const settings = Object.assign({}, defaults, userPrefs); // { theme: 'light', size: 'large' } – immutable merge
```
**ommon use cases:**
- Creating shallow copies of objects
- Merging configuration objects
- Adding default properties
- Implementing object composition patterns
- Immutable updates in state management (though spread operator is now more common)

For deep copying, you would need to use alternatives like `JSON.parse(JSON.stringify(obj))` (with limitations).

## Solution 44
*Reference: [Question 44](js-questions.md#question-44)*

### Q. How does the spread operator work with objects?

The spread operator (...) for objects, introduced in ES2018, provides a concise syntax for copying properties from one object to another within object literals. It creates shallow copies by enumerating the object's own enumerable properties.

**Basic usage:**
```javascript
const person = { name: 'Alex', age: 30 };
const personCopy = { ...person };

console.log(personCopy); // { name: 'Alex', age: 30 }
```

## Solution 45
*Reference: [Question 45](js-questions.md#question-45)*

### Q. What is object destructuring?

Object destructuring is a JavaScript feature that allows you to extract values from objects and assign them to variables. It is a concise way to access and work with object properties.

```javascript
const person = { name: 'Alice', age: 30, address: { city: 'NY' } };
const { name, age, address: { city }, job = 'Engineer' } = person;
// name='Alice', age=30, city='NY', job='Engineer'

function greet({ name = 'Guest' }) {
  return `Hello, ${name}!`;
}
greet(person); // 'Hello, Alice!'
```

## Solution 46
*Reference: [Question 46](js-questions.md#question-46)*

### Q. What is a prototype in JavaScript?

A  prototype in JavaScript is a fundamental mechanism that enables inheritance and property sharing between objects. Every JavaScript object has a prototype (with the exception of objects created with Object.create(null)), which serves as a template or blueprint for that object.

JavaScript is often described as a prototype-based language, rather than a class-based language (though ES6 added class syntax as syntactic sugar over prototypes).

The prototype system works as follows:
```javascript
// Constructor function
function Person(name) {
  this.name = name;
}

// Adding a method to the prototype
Person.prototype.greet = function() {
  return `Hello, my name is ${this.name}`;
};

// Creating instances
const alice = new Person('Alice');
const bob = new Person('Bob');

console.log(alice.greet()); // "Hello, my name is Alice"
console.log(bob.greet());   // "Hello, my name is Bob"
```
Key points about prototypes:
1. **Property Lookup Chain**: When you try to access a property on an object, JavaScript first looks for the property on the object itself. If it doesn't find it, it looks up the prototype chain.
2. **Memory Efficiency**: Methods defined on the prototype are shared among all instances, saving memory as the method isn't duplicated for each object.
3. **Dynamic Nature**: Modifying a prototype affects all objects that inherit from it, even those created before the modification.
4. **Access to Constructor**: Every function in JavaScript automatically gets a `prototype` property when created, which is used when the function is used as a constructor.

## Solution 47
*Reference: [Question 47](js-questions.md#question-47)*

### Q. What is the difference between ``prototype`` and ``__proto__``?

prototype and `__proto__` both relate to inheritance but serve distinct roles—

**`prototype`**:
- It's a property of constructor functions (not regular objects)
- It's the object that will become the prototype of instances created with that constructor
- It defines what properties/methods will be inherited by instances
**`__proto__`** (also accessible via Object.getPrototypeOf()):
- It's a property of all objects (including functions)
- It references the prototype of the constructor that created the object
- It forms the link in the prototype chain for property lookup

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function() {
  return `${this.name} makes a sound`;
};

const dog = new Animal('Rex');

// Relationships
console.log(Animal.prototype === dog.__proto__); // true
console.log(Object.getPrototypeOf(dog) === Animal.prototype); // true

// Adding to prototype affects all instances
Animal.prototype.eat = function() {
  return `${this.name} is eating`;
};

console.log(dog.eat()); // "Rex is eating"
```

In modern JavaScript, we should use `Object.getPrototypeOf()` instead of `__proto__` as the latter is technically a non-standard feature (though widely supported and now standardized in ES6 for compatibility).

## Solution 48
*Reference: [Question 48](js-questions.md#question-48)*

### Q. How do you iterate over an object's properties?

Iterating objects requires handling own vs. inherited properties—options vary by need for keys, values, or control.

- ** `for...in` loop**: Iterates over all enumerable properties, including those in the prototype chain.

```javascript
const person = {
  name: 'Suman',
  age: 25,
  job: 'Developer'
};

for (const key in person) {
  // Check if property belongs to the object itself, not its prototype
  if (Object.prototype.hasOwnProperty.call(person, key)) {
    console.log(`${key}: ${person[key]}`);
  }
}
// Output:
// name: Suman
// age: 25
// job: Developer
```

- **`Object.keys()` with a loop**: Gets own enumerable property names and iterates over them.

```javascript
const person = {
  name: 'Suman',
  age: 30,
  job: 'Developer'
};

Object.keys(person).forEach(key => {
  console.log(`${key}: ${person[key]}`);
});
// Same output as above
```
- **`Object.entries()` with destructuring**: Gets key-value pairs as arrays and iterates over them.
```javascript
const person = {
  name: 'Suman',
  age: 30,
  job: 'Developer'
};

Object.entries(person).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
// Same output as above
```
- **`Object.getOwnPropertyNames()` with a loop**: Gets all own property names, including non-enumerable ones.
```javascript
const person = {
  name: 'Suman',
  age: 30,
  job: 'Developer'
};

Object.getOwnPropertyNames(person).forEach(key => {
  console.log(`${key}: ${person[key]}`);
});
// Same output as above (assuming no non-enumerable properties)
```
Each method has its use cases, but Object.keys() or Object.entries() are generally preferred in modern JavaScript due to their clarity and the fact that they only include the object's own properties.

## Solution 49
*Reference: [Question 49](js-questions.md#question-49)*

### Q. What are `Object.keys()`, `Object.values()`, and `Object.entries()`?

These three methods, introduced in ES6 and ES8, provide convenient ways to extract and work with object properties.

- **`Object.keys(obj)`** (ES6):
  - Returns an array of the object's own enumerable property names (keys)
  - Order is the same as for a `for...in` loop

  ```javascript
  const user = {
    id: 1,
    name: 'Alice',
    email: 'alice@example.com'
  };

  const keys = Object.keys(user);
  console.log(keys); // ['id', 'name', 'email']
  ```

- **`Object.values(obj)`** (ES8):
  - Returns an array of the object's own enumerable property values
  - Order corresponds to that of `Object.keys()`

  ```javascript
  const user = {
    id: 1,
    name: 'Alice',
    email: 'alice@example.com'
  };

  const values = Object.values(user);
  console.log(values); // [1, 'Alice', 'alice@example.com']
  ```

- **`Object.entries(obj)`** (ES8):
  - Returns an array of arrays, each containing a key-value pair
  - Each inner array is structured as [key, value]
  - Order corresponds to that of `Object.keys()`

  ```javascript
  const user = {
    id: 1,
    name: 'Alice',
    email: 'alice@example.com'
  };

  const entries = Object.entries(user);
  console.log(entries);
  // [
  //   ['id', 1],
  //   ['name', 'Alice'],
  //   ['email', 'alice@example.com']
  // ]

  // Common use case: converting to Map
  const userMap = new Map(Object.entries(user));
  console.log(userMap.get('name')); // 'Alice'
  ```
  These methods are incredibly useful for transforming objects and working with them in a functional programming style:

  ```javascript
  const prices = {
    banana: 1.25,
    apple: 0.75,
    orange: 1.00,
    pear: 1.50
  };

  // Filter for items cheaper than $1
  const affordableItems = Object.entries(prices)
    .filter(([_, price]) => price < 1)
    .map(([fruit]) => fruit);

  console.log(affordableItems); // ['apple']
  ```

## Solution 50
*Reference: [Question 50](js-questions.md#question-50)*

### Q. What is the difference between `Object.freeze()` and `Object.seal()`?

Both make objects immutable but to different degrees—vital for constants or preventing tampering in shared code.
- `Object.freeze(obj)`:
  - Prevents adding new properties
  - Prevents removing existing properties
  - Prevents modifying values of existing properties
  - Prevents modifying property attributes (configurable, writable, etc.)
  - Does not affect objects referenced by properties (shallow freeze)

  ```javascript
  const user = {
    name: 'Alice',
    preferences: {
      theme: 'dark'
    }
  };

  Object.freeze(user);

  // These operations will fail in strict mode or silently fail in non-strict mode
  user.name = 'Bob';           // Cannot modify existing property
  user.age = 30;               // Cannot add new property
  delete user.name;            // Cannot delete property

  // However, nested objects are not frozen
  user.preferences.theme = 'light'; // This works! (shallow freeze)
  console.log(user.preferences.theme); // 'light'

  console.log(Object.isFrozen(user)); // true
  ```

- `Object.seal(obj)`:
  - Prevents adding new properties
  - Prevents removing existing properties
  - Allows modifying values of existing properties
  - Prevents modifying property attributes
  - Does not affect objects referenced by properties

  ```javascript
  const user = {
    name: 'Alice',
    preferences: {
      theme: 'dark'
    }
  };

  Object.seal(user);

  user.name = 'Bob';           // This works! Can modify existing properties
  user.age = 30;               // Cannot add new property
  delete user.name;            // Cannot delete property

  user.preferences.theme = 'light'; // This works (nested object not sealed)

  console.log(Object.isSealed(user)); // true
  console.log(user.name); // 'Bob'
  ```

# Strings

  ## Solution 51
*Reference: [Question 51](js-questions.md#question-51)*

### Q. What are the different ways to concatenate strings?

String concatenation in JavaScript combines strings into one, but methods vary in efficiency, readability, and mutability implications—crucial for large-scale apps to prevent performance bottlenecks like quadratic time in loops.

- **Using the + operator**: The most traditional approach.
  ```javascript
  const firstName = "Suman";
  const lastName = "Sarkar";
  const fullName = firstName + " " + lastName; // "Suman Sarkar"
  ```
- **Using the += operator**: Useful for building strings incrementally.
  ```javascript
  let fullName = "";
  fullName += "Suman"; // "Suman"
  fullName += " " + "Sarkar"; // "Suman Sarkar"
  ```
- **Using the concat() method**: Can concatenate multiple strings at once.
  ```javascript
  const firstName = "Suman";
  const lastName = "Sarkar";
  const fullName = firstName.concat(" ", lastName); // "Suman Sarkar"
  ```
- **Using the template literal**: The most efficient way, especially for large-scale apps.
  ```javascript
  const firstName = "Suman";
  const lastName = "Sarkar";
  const fullName = `Hello, my name is ${firstName} ${lastName}`; // "Suman Sarkar"
  ```
- **Array Join()**: Collect in array, then join—optimal for loops to avoid intermediates
  ```javascript
  const firstName = "Suman";
  const lastName = "Sarkar";
  const fullName = [firstName, lastName].join(" "); // "Suman Sarkar"
  ```
- 1. **Using Array.prototype.reduce()**: For complex concatenation logic.
  ```javascript
  const fragments = ["Hello", "to", "the", "world"];
  const result = fragments.reduce((acc, val) => acc + " " + val); // "Hello to the world"
  ```

In modern JavaScript development, template literals are generally preferred for readability and flexibility when working with variables and expressions.

## Solution 52
*Reference: [Question 52](js-questions.md#question-52)*

### Q. What are template literals, and how are they useful?

Template literals, introduced in ES6, are string literals using backticks (`) allowing embedded expressions, multi-line strings, and tagged templates—revolutionizing string creation for readability and expressiveness.

- Basic Interpolation: `${expression}` evaluates inline.
- Multi-Line: No need for \n; preserves formatting.
- Tagged Templates: Function prefixes process literals (e.g., for sanitization).

```javascript
const name = 'Bob';
const age = 25;
const intro = `Hello, ${name}!
You are ${age} years old.
Status: ${age >= 18 ? 'Adult' : 'Minor'}`;
// Multi-line output

// Tagged
function upper(strings, ...values) {
  return strings.reduce((acc, str, i) => acc + str + (values[i] || '').toUpperCase(), '');
}
const tagged = upper`Hello, ${name}!`; // 'Hello, BOB!'
```

## Solution 53
*Reference: [Question 53](js-questions.md#question-53)*

### Q. Explain string methods like `indexOf()`, `includes()`, and `startsWith()`.

These methods are part of JavaScript's string manipulation toolset, allowing for efficient searching and pattern matching within strings.

- **`indexOf()`**: Returns the index of the first occurrence of a substring within a string, or -1 if not found.
  ```javascript
  const sentence = "JavaScript is amazing";
  console.log(sentence.indexOf("Script")); // 4
  console.log(sentence.indexOf("Java")); // 0
  console.log(sentence.indexOf("PHP")); // -1

  // Optional second parameter specifies the starting position for the search
  console.log(sentence.indexOf("a")); // 1 (first occurrence)
  console.log(sentence.indexOf("a", 2)); // 3 (first occurrence starting from index 2)
  ```

- **`includes()`**: Returns a boolean indicating whether a string contains a specified substring. Introduced in ES6.
  ```javascript
  const sentence = "JavaScript is amazing";
  console.log(sentence.includes("Script")); // true
  console.log(sentence.includes("PHP")); // false

  // Optional second parameter specifies the position to start searching from
  console.log(sentence.includes("a", 5)); // true (finds "a" after position 5)
  console.log(sentence.includes("Java", 1)); // false (starts searching after "J")
  ```

- **`startsWith()`**: Returns a boolean indicating whether a string starts with a specified substring. Introduced in ES6.
  ```javascript
  const sentence = "JavaScript is amazing";
  console.log(sentence.startsWith("Java")); // false
  console.log(sentence.startsWith("JavaScript")); // true
  ```

There's also a complementary endsWith() method that checks if a string ends with a specified substring:
```javascript
const filename = "document.pdf";
console.log(filename.endsWith(".pdf")); // true
console.log(filename.endsWith(".doc")); // false

// Optional parameter specifies length of string to consider
console.log(filename.endsWith("ment", 8)); // true (checks first 8 characters: "document")
```
These methods are often used for:
- Input validation (checking formats, patterns)
- Conditional logic based on string content
- Parsing text content
- Filtering collections of strings

The newer methods (includes(), startsWith(), endsWith()) generally provide more semantic clarity than the older indexOf() approach, making code more readable and intention-clear.

## Solution 54
*Reference: [Question 54](js-questions.md#question-54)*

### Q. How do split() and join() work on strings?

`split()` and `join()` are complementary methods that allow conversion between strings and arrays, enabling powerful text processing capabilities.

- **`split()`**: The `split()` method divides a string into an array of substrings based on a specified separator.
  ```javascript
  const sentence = "The quick brown fox jumps over the lazy dog";

  // Split by space
  const words = sentence.split(" ");
  console.log(words); 
  // ["The", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog"]

  // Split by character
  const letters = "hello".split("");
  console.log(letters); // ["h", "e", "l", "l", "o"]

  // Split with limit parameter (second parameter)
  const limitedWords = sentence.split(" ", 3);
  console.log(limitedWords); // ["The", "quick", "brown"]

  // Split on regex pattern
  const csvData = "John,Doe,42,New York";
  const fields = csvData.split(/,/);
  console.log(fields); // ["John", "Doe", "42", "New York"]

  // Special case: empty string separator splits into individual characters
  console.log("hello".split("")); // ["h", "e", "l", "l", "o"]

  // No separator returns the entire string as a single array element
  console.log(sentence.split()); // ["The quick brown fox jumps over the lazy dog"]
  ```

- **`join()`**: The `join()` method creates and returns a new string by concatenating all elements in an array, separated by a specified separator.
  ```javascript
  const words = ["The", "quick", "brown", "fox"];

  // Join with space separator
  const sentence = words.join(" ");
  console.log(sentence); // "The quick brown fox"

  // Join with different separators
  console.log(words.join("-")); // "The-quick-brown-fox"
  console.log(words.join("")); // "Thequickbrownfox"
  console.log(words.join(", ")); // "The, quick, brown, fox"

  // Default separator is comma if not specified
  console.log(words.join()); // "The,quick,brown,fox"

  // Works with non-string array elements
  const mixed = [1, "apple", true, null];
  console.log(mixed.join(" and ")); // "1 and apple and true and null"
  ```

## Solution 55
*Reference: [Question 55](js-questions.md#question-55)*

### Q. What does the trim() method do, and why is it useful?

The `trim()` method removes whitespace characters from both the beginning and end of a string, returning a new string without modifying the original. Whitespace includes spaces, tabs, newlines, and other characters that render as empty space.

```javascript
const text = "   Hello World!   ";
console.log(text.trim()); // "Hello World!"
console.log(messy.trimStart()); // 'Hello, world!   '
console.log(messy.trimEnd()); // '   Hello, world!'

const multiline = `
  This is a multiline string
  with extra whitespace.
`;
console.log(multiline.trim()); // "This is a multiline string\n  with extra whitespace."
```

# Control Flow

## Solution 56
*Reference: [Question 56](js-questions.md#question-56)*

### Q. How does the if-else statement work, and when would you use a switch instead?

The `if-else` statement is a fundamental control flow structure in JavaScript that executes a block of code based on whether a specified condition evaluates to true or false.

Syntax:
```javascript
if (condition) {
  // Code to execute if condition is true
} else {
  // Code to execute if condition is false
}
```
For example:
```javascript
const temperature = 75;

if (temperature > 90) {
  console.log("It's hot outside!");
} else if (temperature > 70) {
  console.log("It's warm outside.");
} else if (temperature > 50) {
  console.log("It's cool outside.");
} else {
  console.log("It's cold outside!");
}
// Output: "It's warm outside."
```

**When to use switch instead:**
You should use a switch statement when you're comparing a single value against multiple discrete, known values. The switch statement can be more readable and potentially more efficient when you have many possible conditions against the same variable.
```javascript
const day = new Date().getDay();

switch (day) {
  case 0:
    console.log("Sunday");
    break;
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  // ...and so on
  default:
    console.log("Unknown day");
}
```
Key benefits of switch over if-else:
- Cleaner syntax for multiple comparisons against a single value
- Potentially better performance for many conditions (though modern JavaScript engines optimize both well)
- Easier to read when dealing with many discrete cases
- The `default` case provides a clear fallback
Use if-else when:
- Your conditions involve different variables or complex expressions
- You have a small number of conditions
- You need to test ranges of values instead of discrete values
- Your conditions are not equality comparisons

## Solution 57
*Reference: [Question 57](js-questions.md#question-57)*

### Q. What are the differences between for, while, and do-while loops?

These loops control repetition, but differ in initialization, condition checking, and use cases—choosing the right one optimizes for clarity and prevents infinite loops or skipped iterations.

**for loop:** The for loop is ideal when you know the number of iterations in advance:
```javascript
// syntax
for (initialization; condition; iteration) {
  // Code to execute
}

// example
for (let i = 0; i < 5; i++) {
  console.log(i); // Outputs 0, 1, 2, 3, 4
}
```

**while loop:** The `while` loop is useful when you want to repeat a block of code until a certain condition is met:
```javascript
// syntax
while (condition) {
  // Code to execute
}

// example
let i = 0;
while (i < 5) {
  console.log(i); // Outputs 0, 1, 2, 3, 4
  i++;
}
```
**do-while loop:** The `do-while` loop is similar to the `while` loop, but ensures that the code block is executed at least once:

```javascript
// syntax
do {
  // Code to execute
} while (condition);

// example
let count = 0;
do {
  console.log(count); // Outputs 0, 1, 2, 3, 4
  count++;
} while (count < 5);
```
**Key differences:**
- **Condition checking:**
  - `for` and `while` check the condition before the first iteration
  - `do-while` checks the condition after the first iteration, ensuring at least one execution
- **Use cases:**
  - `for`: Best for known iteration counts and when initialization, condition, and iteration are closely related
  - `while`: Best for situations where the loop should continue until a condition changes
  - `do-while`: Best when you want to ensure the loop body executes at least once
- **Structure:**
  - `for` consolidates initialization, condition, and iteration in one line
  - `while` and `do-while` require manual initialization and iteration within the loop body


## Solution 58
*Reference: [Question 58](js-questions.md#question-58)*

### Q. Explain break and continue statements in loops.

`break` and `continue` alter loop flow—essential for optimization and control in iterative algorithms, like searching or filtering without full traversal.

**`break`**: Exits the nearest enclosing loop/switch immediately, skipping remaining iterations.
- Useful for early termination (e.g., found item).
```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Exit the loop when i is 5
  }
  console.log(i);
}
// Output: 0, 1, 2, 3, 4
```

**`continue`**: Skips the rest of the current iteration, jumping to the next (or condition check).
- Great for filtering invalid items without nested ifs.
```javascript
for (let i = 0; i < 10; i++) {
  if (i % 2 === 0) {
    continue; // Skip even numbers
  }
  console.log(i);
}
// Output: 1, 3, 5, 7, 9
```

## Solution 59
*Reference: [Question 59](js-questions.md#question-59)*

### Q. What are the differences between `for...in` and `for...of` loops?

The `for...in` loop iterates over the enumerable properties of an object, while the `for...of` loop iterates over the iterable values of an object.

**`for...in` loop:**
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30
};

for (const key in person) {
  console.log(`${key}: ${person[key]}`);
}
// Output:
// firstName: John
// lastName: Doe
// age: 30
```

**`for...of` loop:**
const colors = ['red', 'green', 'blue'];

for (const color of colors) {
  console.log(color);
}
// Output:
// red
// green
// blue
```

**Key differences:**
- **Use cases:**
  - `for-in`: Used for iterating over object properties (keys)
  - `for-of`: Used for iterating over iterable values (elements)
- **Behavior with arrays:**
  - `for-in` will iterate over array indices as strings, plus any enumerable properties added to Array.prototype
  - `for-of` will iterate over the actual values in the array

```javascript
const arr = ['a', 'b', 'c'];
arr.customProp = 'custom';

for (const key in arr) {
  console.log(key); // "0", "1", "2", "customProp"
}

for (const value of arr) {
  console.log(value); // "a", "b", "c" (customProp is ignored)
}
```
- **Iterability:**
  - `for-in` works with any object, including non-iterables
  - `for-of` only works with iterable objects (Arrays, Strings, Maps, Sets, etc.)
- **Order of iteration:**
  - `for-in` doesn't guarantee a specific order of iteration
  - `for-of` follows the iteration order defined by the iterable
- **Performance:**
  - `for-of` is generally faster for arrays than `for-in`

**Best practices:**
- Use `for-in` for iterating over object properties
- Use `for-of` for iterating over array elements, strings, and other iterables
- Avoid using `for-in` with arrays unless you specifically need to access properties beyond indices

## Solution 60
*Reference: [Question 60](js-questions.md#question-60)*

### Q. How does the ternary operator work, and provide an example.

The ternary operator (also called the conditional operator) is a concise way to write an if-else statement in a single line. It's the only JavaScript operator that takes three operands.

**Syntax:** `condition ? expression1 : expression2;`

The ternary operator evaluates the condition, and if it's true, it returns the value of expressionIfTrue; otherwise, it returns expressionIfFalse.

**Basic example:**
```javascript
const age = 18;
const canVote = age >= 18 ? 'You can vote' : 'You cannot vote';
console.log(canVote); // "You can vote"
```
more examples:
```javascript
// Using ternary in a function return
function getGreeting(hour) {
  return hour < 12 ? 'Good morning' : hour < 18 ? 'Good afternoon' : 'Good evening';
}

console.log(getGreeting(9));  // "Good morning"
console.log(getGreeting(14)); // "Good afternoon"
console.log(getGreeting(20)); // "Good evening"

// Using ternary with template literals
const temperature = 75;
console.log(`It's ${temperature > 80 ? 'hot' : 'pleasant'} outside.`);
// "It's pleasant outside."

// In a React component
const Button = ({ isLoggedIn }) => (
  <button>
    {isLoggedIn ? 'Logout' : 'Login'}
  </button>
);
```

# Closures

## Solution 61
*Reference: [Question 61](js-questions.md#question-61)*

### Q. What is a closure in JavaScript?

A closure is a fundamental JavaScript concept where a function retains access to its lexical scope even when executed outside that scope. In simpler terms, a closure is formed when a function "remembers" and can access variables from its parent scope, even after the parent function has finished executing.

Closures happen naturally in JavaScript due to two key language features:
- Functions can be nested within other functions
- Inner functions have access to variables declared in their outer scope

This creates a persistent lexical environment that stays connected to the function, allowing it to access variables that would otherwise be out of scope. The JavaScript engine maintains references to these outer variables, preventing them from being garbage collected as long as the inner function exists.

## Solution 62
*Reference: [Question 62](js-questions.md#question-62)*

### Q. Provide an example of a closure and explain how it works.

Here's a classic example: a counter factory that maintains private state.

```javascript
function createCounter() {
  let count = 0; // Outer scope variable
  return function increment() { // Inner function (closure)
    count++; // Accesses and modifies outer 'count'
    return count;
  };
}

const counter1 = createCounter();
console.log(counter1()); // 1
console.log(counter1()); // 2

const counter2 = createCounter(); // Independent closure
console.log(counter2()); // 1 (separate 'count')
```

- How It Works Step-by-Step:
  - `createCounter()` executes, declaring `count` in its scope.
  - It returns the `increment` function, which closes over `count`—creating a reference to the outer scope's variable environment.
  - After `createCounter()` finishes, its execution context pops off the stack, but `count` persists because `increment` references it.
  - Each call to `counter1()` resolves `count` via the closure's scope chain, incrementing the captured variable.
  - `counter2()` gets its own closure with a fresh `count`, demonstrating isolation.

This works because JavaScript uses a "variable environment" record per function, linked in a chain. Debug tip: In DevTools, inspect the [[Scopes]] property of a function to see closed-over vars. Real-world: This pattern powers Redux thunks or debounce functions, where state must survive across invocations without globals.


## Solution 63
*Reference: [Question 63](js-questions.md#question-63)*

### Q. What are common use cases for closeures?

Closures are incredibly versatile in JavaScript, appearing in many design patterns and techniques:

- **Data Privacy and Encapsulation**: Closures can be used to implement data privacy and encapsulation, where variables are hidden from the outside world and can only be accessed through functions.
  ```javascript
  function createBankAccount(initialBalance) {
    let balance = initialBalance;
      
    return {
      deposit: function(amount) {
        balance += amount;
        return balance;
      },
      withdraw: function(amount) {
        if (amount > balance) {
          throw new Error('Insufficient funds');
        }
        balance -= amount;
        return balance;
      },
      getBalance: function() {
        return balance;
      }
    };
  }
    
  const account = createBankAccount(100);
  account.deposit(50); // 150
  account.withdraw(30); // 120
  account.getBalance(); // 120
  // balance is protected and cannot be accessed directly
  ```
- **Function Factories** - creating specialized functions: 
  ```javascript
  function createMultiplier(factor) {
    return function(number) {
      return number * factor;
    };
  }
    
  const double = createMultiplier(2);
  const triple = createMultiplier(3);
    
  double(5); // 10
  triple(5); // 15
  ```

- **Memoization** - caching function results:
  ```javascript
  function memoize(fn) {
    const cache = {};
      
    return function(...args) {
      const key = JSON.stringify(args);
      if (!(key in cache)) {
        cache[key] = fn(...args);
      }
      return cache[key];
    };
  }
    
  const expensiveCalculation = memoize(function(n) {
    console.log("Computing...");
    return n * n;
  });
    
  expensiveCalculation(4); // Logs "Computing..." and returns 16
  expensiveCalculation(4); // Returns 16 without logging
  ```

- **Event Handlers and Callbacks**: Attaching event listeners and callbacks
  ```javascript
  function setupButton(buttonId, message) {
    const button = document.getElementById(buttonId);
    button.addEventListener('click', function() {
      alert(message); // Closure over message
    });
  }
    
  setupButton('submitBtn', 'Form submitted successfully!');
  ```

- **Currying and Partial Application**: Partially applying function arguments
  ```javascript
  function curry(fn) {
    return function curried(...args) {
      if (args.length >= fn.length) {
        return fn.apply(this, args);
      }
      return function(...moreArgs) {
        return curried.apply(this, args.concat(moreArgs));
      };
    };
  }
    
  const sum = curry((a, b, c) => a + b + c);
  sum(1)(2)(3); // 6
  sum(1, 2)(3); // 6
  ```

- **Iterators and Generators**:
  ```javascript
  function createIterator(array) {
    let index = 0;
      
    return {
      next: function() {
        return index < array.length ?
          { value: array[index++], done: false } :
          { done: true };
      }
    };
  }
    
  const iterator = createIterator([1, 2, 3]);
  iterator.next(); // { value: 1, done: false }
  iterator.next(); // { value: 2, done: false }
  iterator.next(); // { value: 3, done: false }
  iterator.next(); // { done: true }
  ```

## Solution 64
*Reference: [Question 64](js-questions.md#question-64)*

### Q. Explain the issue with closures in loops and how to fix it.

The classic issue with closures in loops occurs when creating functions inside a loop that reference loop variables. The problem is that closures capture variables by reference, not by value.

**The Problem:**
  ```javascript
  function createButtons() {
    for (var i = 0; i < 5; i++) {
      var button = document.createElement('button');
      button.textContent = 'Button ' + i;
      
      button.addEventListener('click', function() {
        console.log('Button ' + i + ' clicked');
      });
      
      document.body.appendChild(button);
    }
  }

  createButtons();
  // When clicked, all buttons will log "Button 5 clicked"
  ```
In this example, all button click handlers reference the same `i` variable. By the time any button is clicked, the loop has completed and `i` is 5, so all handlers log "Button 5 clicked".

**Solution:**
  - **Using an IIFE (Immediately Invoked Function Expression)** to create a new scope:
  ```javascript
  function createButtons() {
    for (var i = 0; i < 5; i++) {
      var button = document.createElement('button');
      button.textContent = 'Button ' + i;
        
      (function(index) {
        button.addEventListener('click', function() {
          console.log('Button ' + index + ' clicked');
        });
      })(i);
        
      document.body.appendChild(button);
    }
  }
  ```
  - **Using `let` instade of `var`**:
    ```javascript
    function createButtons() {
    for (let i = 0; i < 5; i++) {
      const button = document.createElement('button');
      button.textContent = 'Button ' + i;
        
      button.addEventListener('click', function() {
        console.log('Button ' + i + ' clicked');
      });
        
      document.body.appendChild(button);
    }
  }
  ```

The issue occurs because closures maintain references to variables, not copies of their values at creation time. Using let is the most elegant solution in modern JavaScript, as it creates a new lexical environment for each loop iteration.

## Solution 65
*Reference: [Question 65](js-questions.md#question-65)*

### Q. How can closures be used to implement the module pattern?

The module pattern is one of the most powerful applications of closures in JavaScript. It allows us to create private state and expose only selected functionality, simulating the private/public distinction found in other languages.

Here's how to implement the module pattern using closures
  ```javascript
  const calculator = (function() {
    // Private variables and functions
    let result = 0;
    
    function validateNumber(num) {
      if (typeof num !== 'number') {
        throw new Error('Only numbers are allowed');
      }
    }
    
    // Public API
    return {
      add: function(num) {
        validateNumber(num);
        result += num;
        return this;
      },
      
      subtract: function(num) {
        validateNumber(num);
        result -= num;
        return this;
      },
      
      multiply: function(num) {
        validateNumber(num);
        result *= num;
        return this;
      },
      
      divide: function(num) {
        validateNumber(num);
        if (num === 0) {
          throw new Error('Division by zero');
        }
        result /= num;
        return this;
      },
      
      getResult: function() {
        return result;
      },
      
      reset: function() {
        result = 0;
        return this;
      }
    };
  })();

  // Usage:
  calculator.add(5).multiply(2).subtract(3).divide(2).getResult(); // 3.5
  calculator.reset().add(10).getResult(); // 10
  ```
Key aspects of the module pattern:
1. **IIFE (Immediately Invoked Function Expression)**: The entire module is wrapped in an IIFE that executes immediately, creating a closure.
2. **Private members**: Variables and functions declared inside the IIFE but not returned are private, accessible only from inside the module.
3. **Public API**: The returned object contains methods that can access the private variables through closure, providing a controlled interface.
4. **State preservation**: The private variables maintain their values between function calls, creating persistent module state.

With modern JavaScript, we now have native modules with import and export statements, but the closure-based module pattern is still useful for creating encapsulated components with private state, especially in environments where ES modules aren't supported or when you want finer control over what's exposed.

# Asynchronous JavaScript

## Solution 66
*Reference: [Question 66](js-questions.md#question-66)*

### Q. What is the difference between synchronous and asynchronous code?

Synchronous and asynchronous code represent two fundamentally different approaches to program execution:
**Synchronous Code:**
- Executes line-by-line in sequence
- Each operation blocks execution until it completes
- Simple to understand and debug
- Can cause performance issues with long-running operations
  ```javascript
  console.log("First");
  const result = performLongCalculation(); // Blocks execution until complete
  console.log("Second"); // Only runs after calculation finishes
  console.log(result);
  ```

**Asynchronous Code:**
- Operations can execute in parallel without blocking
- Utilizes callbacks, promises, or async/await to handle future results
- Better for performance when dealing with I/O operations, network requests, timers
- More complex flow control and error handling
  ```javascript
  console.log("First");
  fetchData().then(result => {
    console.log(result); // Runs later when data is available
  });
  console.log("Second"); // Runs immediately without waiting for fetchData()
  ```

JavaScript is single-threaded but uses an event loop to handle asynchronous operations. This enables it to perform non-blocking operations despite running on a single thread. As observed in the Discord chat from Friday August 29, 2025, this is a key concept for modern web development and Node.js applications.

## Solution 67
*Reference: [Question 67](js-questions.md#question-67)*

### Q. What are callbacks, and how are they used?

Callbacks are functions passed as arguments to other functions, which are then invoked at a later time when a specific event occurs or an operation completes.
**Key characteristics of callbacks:**
- Functions passed as arguments to other functions
- Executed at a later time after certain operations complete
- Foundation of asynchronous programming in JavaScript
- Can be anonymous functions or named functions

```javascript
function fetchData(url, callback) {
  // Simulate async fetch
  setTimeout(() => {
    const data = { id: 1 }; // Mock response
    if (data) callback(null, data); // Node-style: error-first
    else callback(new Error('Failed'));
  }, 1000);
}

fetchData('/api', (err, data) => {
  if (err) console.error(err);
  else console.log(data);
});
```

## Solution 68
*Reference: [Question 68](js-questions.md#question-68)*

### Q. What is callback hell, and how can it be avoided?

Callback hell (also known as "pyramid of doom") refers to a situation where multiple nested callbacks create deeply indented, hard-to-read, and difficult-to-maintain code. It typically occurs when sequential asynchronous operations depend on the results of previous operations.

**Example of callback hell:**
```javascript
getUser(userId, function(user) {
  getUserPosts(user.id, function(posts) {
    getCommentsForFirstPost(posts[0].id, function(comments) {
      getAuthorOfFirstComment(comments[0].authorId, function(author) {
        getAuthorAddress(author.id, function(address) {
          // Deep nesting continues...
          console.log(address);
        }, function(error) {
          console.error("Error getting address:", error);
        });
      }, function(error) {
        console.error("Error getting author:", error);
      });
    }, function(error) {
      console.error("Error getting comments:", error);
    });
  }, function(error) {
    console.error("Error getting posts:", error);
  });
}, function(error) {
  console.error("Error getting user:", error);
});
```
**Strategies to avoid callback hell:**
- **Use named functions instead of anonymous functions:**
  ```javascript
  function handleUser(user) {
    getUserPosts(user.id, handlePosts, handleError);
  }

  function handlePosts(posts) {
    getCommentsForFirstPost(posts[0].id, handleComments, handleError);
  }

  function handleComments(comments) {
    // And so on...
  }

  function handleError(error) {
    console.error("An error occurred:", error);
  }

  getUser(userId, handleUser, handleError);
  ```

- **Use Promises to flatten the structure:**
  ```javascript
  getUserPromise(userId)
    .then(user => getUserPostsPromise(user.id))
    .then(posts => getCommentsForFirstPostPromise(posts[0].id))
    .then(comments => getAuthorOfFirstCommentPromise(comments[0].authorId))
    .then(author => getAuthorAddressPromise(author.id))
    .then(address => console.log(address))
    .catch(error => console.error("Error in promise chain:", error));
  ```
- **Use async/await for cleaner asynchronous code:**
  ```javascript
  async function getUserAddressFlow(userId) {
    try {
      const user = await getUserPromise(userId);
      const posts = await getUserPostsPromise(user.id);
      const comments = await getCommentsForFirstPostPromise(posts[0].id);
      const author = await getAuthorOfFirstCommentPromise(comments[0].authorId);
      const address = await getAuthorAddressPromise(author.id);
      console.log(address);
    } catch (error) {
      console.error("Error:", error);
    }
  }

  getUserAddressFlow(userId);
  ```

## Solution 69
*Reference: [Question 69](js-questions.md#question-69)*

### Q. What are Promises, and what states can they be in?

Promises are objects representing the eventual completion or failure of an asynchronous operation. They provide a way to handle asynchronous operations in a more structured and predictable way.

**A Promise can be in one of three states:**
1. **Pending**: Initial state, neither fulfilled nor rejected.
2. **Fulfilled**: The operation completed successfully, resulting in a value.
3. **Rejected**: The operation failed, resulting in an error reason.

Once a Promise is fulfilled or rejected, it's considered **settled** and cannot change to another state.
```javascript
// Creating a Promise
const promise = new Promise((resolve, reject) => {
  // Asynchronous operation
  const success = true;
  
  if (success) {
    resolve("Operation completed successfully"); // Changes state to fulfilled
  } else {
    reject(new Error("Operation failed")); // Changes state to rejected
  }
});

// Consuming a Promise
promise
  .then(result => {
    console.log("Success:", result); // Runs if fulfilled
  })
  .catch(error => {
    console.error("Error:", error); // Runs if rejected
  })
  .finally(() => {
    console.log("Promise settled"); // Runs in both cases
  });
```
**Common Promise methods:**
- `Promise.resolve(value)`: Creates an already fulfilled Promise
- `Promise.reject(reason)`: Creates an already rejected Promise
- `Promise.all(iterable)`: Returns a Promise that fulfills when all promises in the iterable fulfill
- `Promise.race(iterable)`: Returns a Promise that settles as soon as one of the promises settles
- `Promise.allSettled(iterable)`: Returns a Promise that resolves when all promises have settled
- `Promise.any(iterable)`: Returns a Promise that fulfills as soon as one of the promises fulfills

## Solution 70
*Reference: [Question 70](js-questions.md#question-70)*

### Q. Explain Promise chaining with an example.

Promise chaining connects multiple async ops via `.then()`, where each returns a new promise—allowing sequential execution with flat structure, automatic error bubbling to `.catch()`.
- Mechanics: `.then()` returns a new promise; resolve value passes to next.
- Error Handling: Unhandled rejections propagate.

```javascript
fetch('/user')
  .then(response => response.json()) // Parse
  .then(user => fetch(`/posts/${user.id}`)) // Next fetch
  .then(response => response.json())
  .then(posts => console.log(`Posts: ${posts.length}`))
  .catch(error => console.error('Chain failed:', error))
  .finally(() => console.log('Cleanup'));
```

## Solution 71
*Reference: [Question 71](js-questions.md#question-71)*

### Q. What is async/await, and how does it simplify asynchronous code?

Async/await is a modern JavaScript syntax introduced in ES2017 (ES8) that provides a more elegant way to work with Promises. It allows you to write asynchronous code that looks and behaves more like synchronous code, making it easier to read, write, and reason about.

```javascript
// Promise-based approach
function fetchUserData() {
  return fetch('https://api.example.com/users')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(data => {
      console.log(data);
      return data;
    });
}

// Async/await approach
async function fetchUserData() {
  const response = await fetch('https://api.example.com/users');
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  const data = await response.json();
  console.log(data);
  return data;
}
```
**How async/await simplifies asynchronous code:**
1. **Improved readability**: Code flows top-to-bottom like synchronous code, eliminating nested `.then()` chains.
2. **Cleaner error handling**: You can use traditional try/catch blocks instead of `.catch()` methods.
3. **Easier debugging**: Stack traces are more meaningful, and you can set breakpoints more naturally.
4. **Sequential execution clarity**: The sequential appearance of code matches its execution order.
5. **Variable scoping**: Variables declared in the async function are available throughout its scope, avoiding the need for extra closures.
6. **Avoiding callback hell**: It flattens the code structure, eliminating the pyramid of doom.

Under the hood, async/await is syntactic sugar over Promises. An async function always returns a Promise, and the await keyword can only be used inside an async function.


## Solution 72
*Reference: [Question 72](js-questions.md#question-72)*

### Q. How do you handle errors in async/await and Promises?

Error handling in asynchronous JavaScript is crucial for creating robust applications. Both Promises and async/await provide mechanisms for handling errors, though with different syntax.

- Promises:
  - `.catch(onRejected)`: Catches upstream errors.
  - Chain: Errors skip `.then()` until `.catch()`.
  - Global: `window.addEventListener('unhandledrejection', e => { ... });` (browsers); `process.on('unhandledRejection')` (Node).

- Async/Await:
  - Wrap in `try { await ... } catch (err) { ... }`.
  - Multiple awaits: One try-catch covers all.

```javascript
async function riskyOp() {
  try {
    const res = await fetch('/api');
    if (!res.ok) throw new Error('Bad response');
    return await res.json();
  } catch (err) {
    console.error('Handled:', err);
    throw err; // Rethrow if needed
  } finally {
    console.log('Cleanup');
  }
}
```

## Solution 73
*Reference: [Question 73](js-questions.md#question-73)*

### Q. What are setTimeout() and setInterval(), and how do they differ?

`setTimeout()` and `setInterval()` are Web API functions that allow you to execute code after a specified delay or at regular intervals, respectively. They are essential tools for handling time-based operations in JavaScript.

**setTimeout():** Executes a function once after a specified delay.
```javascript
// Basic usage
setTimeout(() => {
  console.log('This runs after 2 seconds');
}, 2000);

// With arguments
setTimeout((name) => {
  console.log(`Hello, ${name}!`);
}, 1000, 'John');

// Storing the timeout ID to cancel it if needed
const timeoutId = setTimeout(myFunction, 5000);
// Later, if needed:
clearTimeout(timeoutId); // Cancels the timeout if it hasn't executed yet
```

**setInterval():** Repeatedly executes a function at specified intervals until cleared.
```javascript
// Basic usage - runs every 3 seconds
const intervalId = setInterval(() => {
  console.log('This runs every 3 seconds');
}, 3000);

// With arguments
const counterId = setInterval((count) => {
  console.log(`Count: ${count}`);
  counter++;
  if (counter > 5) {
    clearInterval(counterId); // Stop after 5 iterations
  }
}, 1000, 1);

// To stop the interval
clearInterval(intervalId);
```

**Key differences between setTimeout() and setInterval():**
1. **Execution frequency**:
  - `setTimeout()`: Executes the callback function once after the specified delay.
  - `setInterval()`: Executes the callback function repeatedly at the specified interval.
2. **Timing behavior**:
  - `setTimeout()`: The delay is before the function executes.
  - `setInterval()`: The interval includes the function execution time.
3. **Use cases**:
  - `setTimeout()`: For delayed actions or debouncing.
  - `setInterval()`: For polling or animations.
4. **Cancellation**:
  - `setTimeout()`: Use `clearTimeout()` to cancel before execution.
  - `setInterval()`: Use `clearInterval()` to stop repeated executions



## Solution 74
*Reference: [Question 74](js-questions.md#question-74)*

### Q. Explain the JavaScript event loop.



The JavaScript event loop is a key concept that enables JavaScript's non-blocking, asynchronous behavior despite being single-threaded. It's the mechanism that allows JavaScript to handle operations like UI events, network requests, and timers efficiently.
**Core components of the JavaScript event loop architecture:**
1. **Call Stack**: Where JavaScript code execution happens. Functions are pushed onto and popped off this stack as they are called and completed.
2. **Web APIs**: Browser-provided interfaces (DOM, XMLHttpRequest, setTimeout, etc.) that handle operations outside the JavaScript engine.
3. **Callback Queue (Task Queue)**: Where callbacks from asynchronous operations wait to be executed.
4. **Microtask Queue**: A higher-priority queue for Promises and mutation observer callbacks.
5. **Event Loop**: The mechanism that constantly checks if the call stack is empty and moves tasks from the queues to the stack.

**How the event loop works:**
```javascript
console.log('Start'); // 1

setTimeout(() => {
  console.log('Timeout callback'); // 4
}, 0);

Promise.resolve().then(() => {
  console.log('Promise resolved'); // 3
});

console.log('End'); // 2
```

The execution sequence is:
1. 'Start' is logged immediately (synchronous code)
2. setTimeout callback is registered with Web APIs
3. Promise's then callback is registered as a microtask
4. 'End' is logged immediately (synchronous code)
5. Call stack is now empty, so the event loop checks queues
6. Microtask queue is processed first: 'Promise resolved' is logged
7. After all microtasks, the callback queue is checked: 'Timeout callback' is logged

**The event loop algorithm (simplified):**
1. Execute all synchronous code in the call stack.
2. When the call stack is empty, check if there are any microtasks:
  - If yes, execute all microtasks in order until the microtask queue is empty.
3. Render UI updates if needed.
14. If the call stack is still empty, take the first task from the callback queue and push it onto the call stack to execute.
15. Repeat from step 1.

This architecture allows JavaScript to handle I/O and time-based operations efficiently without blocking the main thread, which is crucial for maintaining responsive user interfaces.


## Solution 75
*Reference: [Question 75](js-questions.md#question-75)*

### Q. What is the difference between microtasks and macrotasks?

In JavaScript's event loop, tasks are categorized into microtasks and macrotasks (sometimes called tasks), which have different priorities and execution timing.

**Macrotasks (Tasks):**
- Executed one per event loop iteration
- Include: setTimeout, setInterval, setImmediate, requestAnimationFrame, I/O operations, UI rendering, script execution

**Microtasks:**
- Executed until the microtask queue is empty after each macrotask completes
- Higher priority than macrotasks
- Include: Promise callbacks (.then, .catch, .finally), queueMicrotask(),     MutationObserver callbacks, process.nextTick (Node.js)

**Execution order**:
```javascript
console.log('Script start'); // 1

setTimeout(() => {
  console.log('setTimeout'); // 5
}, 0);

Promise.resolve()
  .then(() => {
    console.log('Promise 1'); // 3
  })
  .then(() => {
    console.log('Promise 2'); // 4
  });

console.log('Script end'); // 2
```

The execution order is:
1. "Script start" (synchronous)
2. "Script end" (synchronous)
3. "Promise 1" (microtask)
4. "Promise 2" (microtask - note that new microtasks generated during microtask execution are added to the current microtask queue)
5. "setTimeout" (macrotask - executed in the next event loop iteration)

**Important characteristics:**
1. **Prioritization**: Microtasks have higher priority and are processed before the next macrotask.
2. **Execution timing**: All microtasks in the queue (including newly added ones during execution) are processed before the next rendering or macrotask.
3. **Starvation**: Excessive microtasks can starve macrotasks, potentially delaying UI updates.
4. **Use cases**:
  - Microtasks: For operations that should happen as soon as possible after the current script but before UI updates.
  - Macrotasks: For operations that should be deferred until after UI updates or should be explicitly scheduled for the future.

  ```javascript
  button.addEventListener('click', () => {
    console.log('Button clicked');
    
    // Macrotask - will run in a future iteration of the event loop
    setTimeout(() => {
      console.log('Timeout task');
    }, 0);
    
    // Microtask - will run before the next render
    Promise.resolve().then(() => {
      console.log('Promise microtask');
      
      // Adding another microtask during microtask execution
      Promise.resolve().then(() => {
        console.log('Nested promise microtask');
      });
    });
    
    console.log('Click handler end');
  });
  ```

Output when button is clicked:
1. "Button clicked"
2. "Click handler end"
3. "Promise microtask"
4. "Nested promise microtask"
5. *UI rendering may happen here*
6. "Timeout task"