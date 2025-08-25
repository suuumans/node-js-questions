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
