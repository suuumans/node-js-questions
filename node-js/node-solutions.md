# Node.js Basics

## Question 1
*Reference: [Question 1](node-questions.md#question-1)*

### Q. What is Node.js, and how does it differ from traditional server-side languages like PHP or Java?

Node.js is an open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside a web browser. It allows developers to use JavaScript for server-side scripting to produce dynamic web content.

**Key characteristics of Node.js:**
- Built on Chrome's V8 JavaScript engine
- Event-driven, non-blocking I/O model
- Lightweight and efficient for data-intensive real-time applications
- Uses a single-threaded event loop for handling concurrent operations

**Differences from traditional server-side languages:**
| Feature | Node.js | PHP | Java |
| :--- | :--- | :--- | :--- |
| **Language** | JavaScript | PHP | Java |
| **Execution Model** | Event-driven, non-blocking I/O | Request-response, primarily blocking | Thread-based, can be blocking or non-blocking |
| **Concurrency Model** | Single-threaded event loop | Process/thread per request | Multi-threaded |
| **Performance** | Excellent for I/O-bound tasks | Good for CPU-bound tasks | Excellent for CPU-bound tasks |
| **Memory Usage** | Low memory footprint initially | Moderate | High memory footprint |
| **Development Speed** | Rapid development | Rapid development | More structured, typically slower development |
| **Ecosystem** | npm (largest package ecosystem) | Composer | Maven/Gradle |
| **Use Cases** | Real-time applications, APIs, streaming | Traditional web applications, CMS | Enterprise applications, complex systems |

Node.js excels at handling many simultaneous connections with high throughput, making it ideal for applications like chat applications, streaming services, and real-time analytics platforms.


## Question 2
*Reference: [Question 2](node-questions.md#question-2)*

### Q. What is the V8 engine, and what role does it play in Node.js?

V8 is Google's open-source, high-performance JavaScript and WebAssembly engine written in C++. It was originally designed for Google Chrome but now serves as the foundation for Node.js.

**Key features of the V8 engine:**
- Compiles JavaScript directly to native machine code before execution (JIT - Just-In-Time compilation).
- Implements optimized garbage collection.
- Implements ECMAScript standards.
- Features efficient memory management.
- Provides excellent performance by optimizing frequently executed code.

**Role in Node.js:**
- V8 is the core component that executes JavaScript code in Node.js.
- It provides the JavaScript runtime environment.
- Node.js adds APIs for file system access, networking, HTTP, and other server-side functionalities on top of V8.
- V8 handles memory allocation for JavaScript objects and garbage collection.
- Node.js uses V8's C++ APIs to integrate JavaScript with underlying operating system features.

V8's performance is a key factor in Node.js's efficiency. The engine is continuously updated with performance improvements that directly benefit Node.js applications.


## Question 3
*Reference: [Question 3](node-questions.md#question-3)*

### Q. Explain the single-threaded nature of Node.js and how it handles concurrency.

Node.js operates on a single-threaded event loop model, but this doesn't mean it can only perform one operation at a time. It's designed to handle concurrency efficiently without the complexity and overhead of managing multiple threads.

**Single-threaded architecture:**
- The main application thread runs a single event loop.
- JavaScript code execution is single-threaded.
- Synchronous operations execute sequentially.

**Concurrency handling in Node.js:**
1. **Event Loop**: The core mechanism that allows Node.js to perform non-blocking I/O operations despite being single-threaded.
2. **Libuv**: A multi-platform C library that provides the event loop implementation and abstracts asynchronous I/O operations.
3. **Callback Pattern**: Functions that will be executed after an asynchronous operation completes.
4. **Asynchronous APIs**: Most Node.js core APIs are designed to be asynchronous and non-blocking.

**How it works:**
```
   ┌───────────────────────────┐
┌─>│           Timers          │ setTimeout(), setInterval()
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     Pending Callbacks     │ Deferred callbacks from operations
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       Idle, Prepare       │ Internal use
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           Poll            │ Process I/O callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           Check           │ setImmediate() callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      Close Callbacks      │ Socket close callbacks
   └───────────────────────────┘
```
1. When an asynchronous operation (like file I/O, network request) is initiated, Node.js registers a callback.
2. The operation is handed off to system kernel/libuv worker threads.
3. The event loop continues to run, handling other operations.
4. When the asynchronous operation completes, its callback is queued to be executed.
5. The event loop executes the callback when appropriate.

**Example demonstrating Node.js concurrency:**
```javascript
console.log('Starting');

// Asynchronous file operation
fs.readFile('largefile.txt', (err, data) => {
  if (err) throw err;
  console.log('File read complete');
});

// Asynchronous HTTP request
http.get('http://example.com', (res) => {
  console.log('HTTP request complete');
});

console.log('Continuing execution');
```
Output order:
```
Starting
Continuing execution
HTTP request complete   // These may appear in either order
File read complete      // depending on which finishes first
```
This model makes Node.js highly scalable for I/O-bound applications, though it's not ideal for CPU-intensive tasks that would block the single thread.


## Question 4
*Reference: [Question 4](node-questions.md#question-4)*

### Q. What is the difference between Node.js and JavaScript?

While Node.js and browser JavaScript both use the same language (ECMAScript), they operate in different environments with different capabilities and constraints.
**Key differences:**
| Feature | Node.js | Browser JavaScript |
| :--- | :--- | :--- |
| **Global Object** | global | window or globalThis |
| **Document Object Model (DOM)** | Not available | Available (core browser API) |
| **File System Access** | Direct access via fs module | Limited access (only via user interaction) |
| **Module System** | CommonJS (require/module.exports) and ES Modules | ES Modules (import/export) |
| **Package Management** | npm/yarn with package.json | Traditionally none; now using bundlers like Webpack |
| **Threading Model** | Single-threaded with worker threads available | Main thread with Web Workers |
| **Network Requests** | HTTP/HTTPS modules, TCP/UDP sockets | Fetch API, XMLHttpRequest |
| **Security Model** | Full system access (based on user permissions) | Sandbox model with Same-Origin Policy |
| **Execution Environment** | Server/desktop | Browser |
| **Buffer/Typed Arrays** | Built-in Buffer class | ArrayBuffer, TypedArray |
| **APIs Available** | OS, File System, Network, Crypto, etc. | DOM, Web APIs, WebRTC, WebGL, etc. |

**Example of code that works in Node.js but not in browsers:**
```javascript
// Node.js specific - works on server
const fs = require('fs');
const os = require('os');

// Read a file from disk
fs.readFile('/path/to/file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Get system information
console.log(`Platform: ${os.platform()}`);
console.log(`Memory: ${os.totalmem() / 1024 / 1024 / 1024} GB`);
```
**Example of code that works in browsers but not in Node.js:**
```javascript
// Browser specific - works in browser
// Access the DOM
document.getElementById('myButton').addEventListener('click', () => {
  alert('Button clicked!');
});

// Use browser-specific APIs
navigator.geolocation.getCurrentPosition((position) => {
  console.log(`Latitude: ${position.coords.latitude}`);
  console.log(`Longitude: ${position.coords.longitude}`);
});
```
Understanding these differences is crucial when writing isomorphic/universal JavaScript applications that run in both environments.


## Question 5
*Reference: [Question 5](node-questions.md#question-5)*

### Q. How do you check the version of Node.js installed on your system?

To check the Node.js version, use the command-line flag `-v` or `--version` in your terminal—this outputs the installed version string, useful for compatibility checks or debugging.

- CLI Command: `node -v` or `node --version` (e.g., outputs "v20.5.1").
- Programmatically: In code, `process.version` or `process.versions.node`.
- With npm/nvm: `npm -v` for npm; `nvm ls` for managed versions.

Example in Script:
```javascript

console.log(process.version); // 'v20.5.1'
```

It's important to check Node.js versions when deploying applications or when specific Node.js features are required. The semantic versioning of Node.js follows the format major.minor.patch, where:
- Major versions may contain breaking changes
- Minor versions add functionality in a backward-compatible manner
- Patch versions include backward-compatible bug fixes
Each Node.js version has its own support lifecycle, with LTS (Long Term Support) versions receiving longer maintenance and security updates.


## Question 6
*Reference: [Question 6](node-questions.md#question-6)*

### Q. What is the REPL in Node.js, and how is it useful?

REPL stands for Read-Eval-Print Loop, which is an interactive programming environment provided by Node.js. When you run the node command without any arguments in your terminal, you enter the Node.js REPL.

The REPL works as follows:
- **Read**: It reads user input (code or expressions)
- **Eval**: It evaluates the input
- **Print**: It prints the result
- **Loop**: It loops back and waits for new input

```javascript
// Example of using Node.js REPL
$ node
> const greeting = "Hello, World!"
undefined
> greeting
'Hello, World!'
> 5 + 10
15
> const sum = (a, b) => a + b
undefined
> sum(3, 4)
7
```

**Why the REPL is useful:**
1. **Quick Testing**: Perfect for testing small code snippets without creating files
2. **Learning Tool**: Great for learning JavaScript and Node.js features
3. **Debugging**: Helps inspect variables and test functions during development
4. **API Exploration**: Allows exploring Node.js APIs and third-party modules interactively
5. **Rapid Prototyping**: Enables rapid prototyping of ideas before implementing them in actual code.

The REPL also offers special commands prefixed with a dot (.):
- `.help`: Shows available commands
- `.break`: Exits from multiline expression
- `.clear`: Alias for `.break`
- `.editor`: Enters editor mode for multiline editing
- `.exit` or `.quit`: Exits the REPL
- `.save`: Saves the current REPL session to a file
- `.load`: Loads a file into the current REPL session


## Question 7
*Reference: [Question 7](node-questions.md#question-7)*

### Q. Explain the concept of non-blocking I/O in Node.js.

Non-blocking I/O is a core architectural feature of Node.js that allows it to handle many concurrent operations without using multiple threads. This approach is fundamental to Node.js's performance and scalability.

**How it works:**

In traditional blocking I/O models, when code makes a request to read a file or fetch data from a database, the execution thread waits (blocks) until that operation completes before continuing. This can lead to inefficient resource utilization and poor performance under load.

Node.js, however, uses a non-blocking I/O model where:
1. I/O operations (file, network, database) don't block the main thread.
2. The program continues executing other code while waiting for I/O operations to complete.
3. When an I/O operation finishes, a callback function is executed.

    ```javascript
    // Blocking I/O (for illustration only, Node.js rarely uses this approach)
    const fs = require('fs');
    const data = fs.readFileSync('/path/to/file.txt'); // Execution stops here until file is read
    console.log(data);
    console.log('This runs after file is read');

    // Non-blocking I/O (Node.js approach)
    fs.readFile('/path/to/file.txt', (err, data) => {
    if (err) throw err;
    console.log(data); // This runs when file is ready
    });
    console.log('This runs immediately, before file is read');
    ```
**Benefits of non-blocking I/O:**
1. **Scalability**: Can handle thousands of concurrent connections with minimal resources
2. **Throughput**: Processes more requests per second by not waiting for I/O
3. **Efficiency**: Makes better use of CPU resources
4. **Responsiveness**: Application remains responsive even during heavy I/O


## Question 8
*Reference: [Question 8](node-questions.md#question-8)*

### Q. What are the core modules in Node.js? Name a few.

Core modules are built-in modules that come with Node.js installation and provide essential functionality. They can be used without any additional installation, simply by requiring them.

**Key core modules in Node.js:**
1. **fs** (File System): Provides file operations such as reading, writing, and deleting files.
```javascript
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```
2. **http/https**: Enables creating HTTP/HTTPS servers and making HTTP/HTTPS requests.
```javascript
const http = require('http');
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});
server.listen(3000);
```
3. **path**: Utilities for working with file and directory paths.
```javascript
const path = require('path');
const fullPath = path.join(__dirname, 'files', 'example.txt');
console.log(fullPath);
```
4. **os**: Provides operating system-related utility methods.
```javascript
const os = require('os');
console.log(`Platform: ${os.platform()}`);
console.log(`Total Memory: ${os.totalmem()} bytes`);
```
5. **events**: Implements the Observer pattern with event emitters.
```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();
myEmitter.on('event', () => console.log('Event occurred!'));
myEmitter.emit('event');
```
6. **util**: Utility functions for developers.
```javascript
const util = require('util');
const debugLog = util.debuglog('app');
debugLog('Debug message');
```
7. **crypto**: Provides cryptographic functionality.
```javascript
const crypto = require('crypto');
const hash = crypto.createHash('sha256').update('password').digest('hex');
```
8. **url**: Utilities for URL resolution and parsing.
```javascript
const url = require('url');
const myURL = new URL('https://example.com/path?query=value');
console.log(myURL.hostname); // example.com
```
9. **stream**: Interface for working with streaming data.
```javascript
const fs = require('fs');
const readStream = fs.createReadStream('large-file.txt');
readStream.pipe(process.stdout);
```
10. **buffer**: Handling binary data.
```javascript
const buffer = Buffer.from('Hello World');
console.log(buffer.toString());
```
11. **child_process**: Spawning new processes.
```javascript
const childProcess = require('child_process');
const ls = childProcess.spawn('ls', ['-lh', '/usr']);
ls.stdout.on('data', (data) => console.log(data.toString()));
```

These core modules form the foundation of Node.js and are essential for most Node.js applications.


## Question 9
*Reference: [Question 9](node-questions.md#question-9)*

### Q. How does Node.js handle errors in synchronous vs asynchronous code?

Error handling in Node.js varies by sync/async to prevent uncaught exceptions crashing the process—using try-catch for sync, callbacks/promises for async.

### Synchronous Error Handling
In synchronous code, errors can be caught using traditional try-catch blocks:
```javascript
try {
  const result = performLongCalculation(); // Synchronous operation
  console.log(result);
} catch (error) {
  console.error('An error occurred:', error.message);
  // Handle the error appropriately
}
```
Key points about synchronous error handling:

- Errors propagate up the call stack immediately.
- try-catch blocks work as expected.
- The program flow is predictable.
- If not caught, the error will crash the application.

### Asynchronous Error Handling
For asynchronous operations, error handling depends on the pattern used:

#### 1. Callback Pattern (Error-first callbacks)
The Node.js convention is to use error-first callbacks, where the first parameter is reserved for an error object:
```javascript
fs.readFile('file.txt', (err, data) => {
  if (err) {
    console.error('Error reading file:', err.message);
    return;
  }
  
  // Process data if no error occurred
  console.log(data.toString());
});
```
#### 2. Promise Pattern
romises use .catch() or the second argument of .then() for error handling:
```javascript
fetchData()
  .then(data => {
    console.log('Data received:', data);
  })
  .catch(error => {
    console.error('Error fetching data:', error.message);
    // Handle error appropriately
  });
```
#### 3. Async/Await Pattern
Async/await combines the readability of synchronous code with the power of promises, and uses try-catch for error handling:
```javascript
async function getData() {
  try {
    const data = await fetchData();
    console.log('Data received:', data);
  } catch (error) {
    console.error('Error fetching data:', error.message);
    // Handle error appropriately
  }
}
```
### Important differences:
1. **Error propagation**: In synchronous code, errors propagate up the call stack automatically. In asynchronous code, errors must be explicitly passed through callbacks, promises, or caught in try-catch with async/await.
2. **Uncaught errors**: Uncaught errors in asynchronous operations can be hard to trace and might not crash the application immediately, leading to "silent failures."
3. **Global error handling**:
  - For synchronous errors: `process.on('uncaughtException', callback)`
  - For promise rejections: `process.on('unhandledRejection', callback)`

```javascript
// Global handlers for uncaught errors
process.on('uncaughtException', (error) => {
  console.error('Uncaught Exception:', error);
  // Perform cleanup, log the error, then exit
  process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Promise Rejection:', reason);
  // Log the error but don't necessarily exit
});
```

## Solution 10
*Reference: [Question 10](node-questions.md#question-10)*

### Q. What is the purpose of the process object in Node.js?

The process object is a global object in Node.js that provides information about, and control over, the current Node.js process. It's one of the most important objects in Node.js, offering a bridge between your application and its running environment.

**Key functionalities of the process object:**
1. **Environment Information**:
```javascript
console.log(process.env); // Environment variables
console.log(process.version); // Node.js version
console.log(process.platform); // Operating system platform
console.log(process.arch); // Architecture (x64, arm, etc.)
```
2. **Command Line Arguments**:
```javascript
// For a command like: node app.js arg1 arg2
console.log(process.argv);
// Outputs: ['node', '/path/to/app.js', 'arg1', 'arg2']
```
3. **Process Control**:
```javascript
process.exit(0); // Exit process with success code
process.exit(1); // Exit process with error code
   
// Graceful shutdown
process.on('SIGTERM', () => {
  console.log('Received SIGTERM, shutting down gracefully');
  server.close(() => {
    console.log('Process terminated');
  });
});
```
4. **Standard I/O Streams**:
```javascript
process.stdout.write('Hello world\n'); // Output
process.stderr.write('Error occurred\n'); // Error output
   
// Reading from stdin
process.stdin.on('data', (data) => {
  console.log(`You typed: ${data.toString().trim()}`);
});
```
5. **Current Directory**:
```javascript
console.log(process.cwd()); // Current working directory
process.chdir('/new/directory'); // Change directory
```
6. **Memory Usage**:
```javascript
console.log(process.memoryUsage());
// Outputs memory usage statistics including:
// { rss, heapTotal, heapUsed, external, arrayBuffers }
```
7. **Event Handling**:
```javascript
// Handle uncaught exceptions
process.on('uncaughtException', (err) => {
  console.error('Uncaught exception:', err);
  // Perform cleanup
  process.exit(1);
});
   
// Handle unhandled promise rejections
process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled rejection at:', promise, 'reason:', reason);
});
```
1. **Next Tick Queue**:
```javascript
// process.nextTick() executes callback after current operation
// but before the next event loop tick
console.log('Start');
process.nextTick(() => {
  console.log('nextTick callback');
});
console.log('End');
   
// Output:
// Start
// End
// nextTick callback
```
The process object is essential for:
- Building robust applications with proper error handling
- Creating cross-environment applications that work in different settings
- Implementing graceful shutdowns
- Monitoring application performance
- Handling command-line interfaces
- Managing application lifecycle


# Modules and NPM

## Question 11
*Reference: [Question 11](node-questions.md#question-11)*

### Q. What are modules in Node.js, and how do you create one?

Modules in Node.js are reusable blocks of code that encapsulate related functionality, making applications more maintainable and organized. They help prevent global namespace pollution and promote code reusability.

**How to create a module in Node.js:**
```javascript
// math.js - A simple module
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

// Export specific functions
module.exports = {
  add: add,
  subtract: subtract
};

// Alternative shorthand syntax
// module.exports = { add, subtract };
```
**Using the module:**
```javascript
// app.js - Using the module
const math = require('./math');

console.log(math.add(5, 3));      // 8
console.log(math.subtract(10, 4)); // 6
```
You can also export a single function or object:
```javascript
// logger.js - Single export module
function log(message) {
  console.log(`[${new Date().toISOString()}] ${message}`);
}

module.exports = log;
```
**Using the single export module:**
```javascript
// app.js
const logger = require('./logger');

logger('Application started'); // [2025-09-04T20:21:06.992Z] Application started
```

## Question 12
*Reference: [Question 12](node-questions.md#question-12)*

### Q. What is the difference between `require()` and `import` in Node.js?

The require() and import statements serve the same purpose of loading modules but belong to different module systems with important differences:

**require() (CommonJS):**
```javascript
// Importing with require (CommonJS)
const fs = require('fs');
const { readFile } = require('fs');
const myModule = require('./my-module');
```
**import (ES Modules):**
```javascript
// Importing with import (ES Modules)
import fs from 'fs';
import { readFile } from 'fs';
import myModule from './my-module.js';
```
**Key differences:**
1. **Syntax**: `require()` is a function call, while `import` is a declarative statement.
2. **Loading behavior**:
  - `require()` is synchronous and loads modules at runtime
  - `import` is asynchronous and processes imports during parsing (before execution).
3. **File extension requirements**:
  - `require()` doesn't need file extensions for JS files.
  - `import` typically requires file extensions (`.js`, `.mjs`).
4. **Dynamic loading**:
  - `require()` can be called anywhere in code (conditionally).
  - Traditional `import` must be at the top level (ES2020 added dynamic `import()`).
5. **Support in Node.js**:
  - `require()` is natively supported in all Node.js versions.
  - `import` requires either `.mjs` extension, `"type": "module"` in package.json, or newer Node.js versions.


## Question 13
*Reference: [Question 13](node-questions.md#question-13)*

### Q. What is CommonJS vs ES Modules in Node.js?

**CommonJS** and **ES Modules** are two different module systems in Node.js with different syntax, loading behavior, and features.
**CommonJS:**
```javascript
// Exporting in CommonJS
const PI = 3.14159;
function calculateArea(radius) {
  return PI * radius * radius;
}

module.exports = { PI, calculateArea };

// Importing in CommonJS
const { PI, calculateArea } = require('./circle');
console.log(calculateArea(5)); // 78.53975
```
**ES Modules:**
```javascript
// Exporting in ES Modules
export const PI = 3.14159;
export function calculateArea(radius) {
  return PI * radius * radius;
}

// Or default export
export default function calculateCircumference(radius) {
  return 2 * PI * radius;
}

// Importing in ES Modules
import { PI, calculateArea } from './circle.js';
import calculateCircumference from './circle.js';
console.log(calculateArea(5)); // 78.53975
```
**Key differences:**
1. **Syntax**:
  - CommonJS: `module.exports`, `exports`, and `require()`
  - ES Modules: `export`, `export default`, and `import`.
2. **Loading mechanism**:
  - CommonJS loads modules synchronously and evaluates them on demand.
  - ES Modules loads asynchronously and bindings are live references to exports.
3. **Static vs. Dynamic**:
  - CommonJS allows dynamic module loading (conditional requires).
  - ES Modules imports are static and analyzed at parse time (though dynamic import() is available in ES2020).
4. **Node.js Support**:
  - CommonJS is the original Node.js module system.
  - ES Modules support was added later (stable since Node.js 12+).
  - Use `.mjs` extension or `"type": "module"` in package.json for ES Modules.


## Question 14
*Reference: [Question 14](node-questions.md#question-14)*

### Q. how does module caching work in Node.js?

Node.js caches modules after they're loaded for the first time, which optimizes performance and ensures module state is maintained across an application.

**Key aspects of module caching:**
- **Singleton pattern**: When you `require()` a module multiple times, you get the same instance:
  ```javascript
  // counter.js
  let count = 0;

  function increment() {
    return ++count;
  }

  module.exports = { increment };

  // app.js
  const counter1 = require('./counter');
  const counter2 = require('./counter');

  console.log(counter1.increment()); // 1
  console.log(counter2.increment()); // 2 (shared state, not 1)
  console.log(counter1.increment()); // 3 (shared state)
  ```
- **Cache location**: Modules are cached in the `require.cache` object, keyed by their resolved filename.
- **Clearing the cache**:
```javascript
// Delete a specific module from cache
delete require.cache[require.resolve('./my-module')];

// Clear entire cache (rarely needed)
Object.keys(require.cache).forEach(key => {
  delete require.cache[key];
});
```
- **Module initialization**: The code in a module runs only once, when it's first required.
- **Circular dependencies**: Node.js handles circular dependencies by returning partially loaded modules.


## Question 15
*Reference: [Question 15](node-questions.md#question-15)*

### Q. What is NPM, and how do you initialize a new project with it?

NPM (Node Package Manager) is the default package manager for Node.js. It's a command-line tool and online registry that allows developers to discover, install, and manage JavaScript packages and dependencies.

**Key features of NPM:**
- Package installation and management.
- Dependency resolution.
- Script running.
- Package versioning.
- Publishing packages.

**Initializing a new Node.js project with NPM:**
1. **Create a new directory for your project:**
```bash
mkdir my-new-project
cd my-new-project
```
2. **Initialize a new npm project:**
```bash
npm init
```
This interactive command prompts you for information about your project (name, version, description, entry point, test command, git repository, keywords, author, license).

3. **For quick initialization with defaults:**
```bash
npm init -y
```
This creates a package.json with default values without prompting.

4. **The resulting package.json file:**
```json
{
  "name": "my-new-project",
  "version": "1.0.0",
  "description": "My awesome Node.js project",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
5. **Installing dependencies:**
```bash
npm install express       # Install and add to dependencies
npm install jest --save-dev  # Install and add to devDependencies
```
6. **Running scripts:**
Add custom scripts to package.json:
```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js",
  "test": "jest"
}
```
Then run them with:
```bash
npm run start
npm run dev
npm test  # shorthand for npm run test
```

NPM is essential to modern Node.js development, allowing developers to leverage the vast ecosystem of open-source packages and tools available in the JavaScript community.


## Question 16
*Reference: [Question 16](node-questions.md#question-16)*

### Q. ## Explain package.json and its key fields.

The `package.json` file is a central manifest for Node.js projects that defines project metadata, dependencies, scripts, and configuration. It serves as the control center for your Node.js project.

Key fields in package.json include:
```json
{
  "name": "my-project",           // Required: Project name
  "version": "1.0.0",             // Required: Project version (following SemVer)
  "description": "A sample Node.js project",  // Project description
  "main": "index.js",             // Entry point of the package
  "type": "module",               // Module type: "commonjs" (default) or "module" (ESM)
  
  "scripts": {                    // NPM scripts that can be run with npm run <script>
    "start": "node index.js",
    "test": "jest",
    "build": "webpack"
  },
  
  "dependencies": {               // Production dependencies
    "express": "^4.18.2"
  },
  
  "devDependencies": {            // Development-only dependencies
    "jest": "^29.5.0"
  },
  
  "peerDependencies": {           // Dependencies required by consumers of your package
    "react": "^18.0.0"
  },
  
  "engines": {                    // Node.js version requirements
    "node": ">=14.0.0"
  },
  
  "private": true,                // Prevents accidental publishing to NPM registry
  
  "author": "Your Name <email@example.com>",  // Author information
  "license": "MIT",               // License type
  
  "repository": {                 // Source code repository
    "type": "git",
    "url": "https://github.com/username/repository.git"
  },
  
  "keywords": ["node", "example", "package"],  // Keywords for NPM search
  
  "browserslist": [               // Browser compatibility targets
    ">0.2%",
    "not dead"
  ]
}
```

Some additional important but less common fields include:
- `bin`: Defines executable scripts that should be installed.
- `files`: Specifies files to include when publishing to NPM.
- `homepage`: Project homepage URL.
- `bugs`: Issue tracker URL.
- `config`: Configuration values for use in package scripts.

## Question 17
*Reference: [Question 17](node-questions.md#question-17)*

### Q. What is the difference between dependencies and devDependencies in package.json?

dependencies and devDependencies serve different purposes in your Node.js project.

**dependencies**:
- Packages required for your application to run in production.
- Installed by default with `npm install` or when your package is installed as a dependency.
- Examples: frameworks (Express, React), utility libraries, database drivers.

**devDependencies**:
- Packages needed only for local development and testing.
- Not installed in production environments when using `npm install --production`.
- Not installed when your package is installed as a dependency by other projects.
- Examples: testing frameworks, build tools, linters, bundlers.

```json
{
  "dependencies": {
    "express": "^4.18.2",        // Required in production
    "mongoose": "^7.0.3",        // Required in production
    "dotenv": "^16.0.3"          // Required in production
  },
  "devDependencies": {
    "jest": "^29.5.0",           // Only for testing
    "eslint": "^8.38.0",         // Only for code linting
    "nodemon": "^2.0.22",        // Only for development server
    "webpack": "^5.80.0"         // Only for bundling
  }
}
```
Best practices:
- Use `npm install package --save` or `npm install package` to add to `dependencies`
- Use `npm install package --save-dev` to add to `devDependencies`
- Keep production dependencies minimal to reduce deployment size and security surface
- In CI/CD pipelines, use `npm ci --production` to install only production dependencies


## Question 18
*Reference: [Question 18](node-questions.md#question-18)*

### Q. How do you handle version control conflicts in NPM?

Version conflicts in NPM can occur when different dependencies require incompatible versions of the same package. Here are the strategies to handle them.

1. **Understanding npm's dependency resolution**:
  - NPM uses a nested dependency structure where each package can have its own dependencies.
  - From NPM v3 onward, it attempts to flatten dependencies when possible to deduplicate.

2. **Using package-lock.json**:
  - `package-lock.json` locks down exact versions of all dependencies and their dependencies.
  - Ensures consistent installations across environments.
  - Always commit this file to version control.

3. **Resolving conflicts manually**:
```bash
# View dependency tree to identify conflicts
npm ls package-name
   
# Force a specific version
npm install package-name@specific-version
   
# Check for outdated packages
npm outdated
```
4. **Using npm-check and npm-check-updates**:
```bash
# Install tools
npm install -g npm-check npm-check-updates
   
# Check for updates and conflicts
npm-check
   
# Update all dependencies to latest versions
ncu -u
```
4. **Using resolutions field** (with Yarn or pnpm):
```json
{
  "resolutions": {
    "package-name": "1.2.3"
  }
}
```
5. **Using overrides field** (npm v8.3+):
```json
{
  "overrides": {
    "package-name": "1.2.3"
  }
}
```
6. **Consider alternative package managers**:
  1. **Consider alternative package managers**:
  - Yarn: Better conflict resolution with its "selective version resolution"
  - pnpm: Uses a symlinked approach that handles conflicts differently
7. **Auditing and fixing security vulnerabilities**:
```bash
# Check for vulnerabilities
npm audit
   
# Fix vulnerabilities
npm audit fix
```

## Question 19
*Reference: [Question 19](node-questions.md#question-19)*

### Q. What are semantic versioning (SemVer) rules in NPM?

Semantic Versioning (SemVer) is a versioning scheme used by NPM packages that follows the format MAJOR.MINOR.PATCH (e.g., 2.11.7).
**SemVer Rules**:
1. **Version format**: `MAJOR.MINOR.PATCH[-PRERELEASE][+BUILD]`
  - **MAJOR**: Incremented for incompatible API changes
  - **MINOR**: Incremented for backward-compatible new functionality
  - **PATCH**: Incremented for backward-compatible bug fixes
  - **PRERELEASE**: Optional tag for pre-release versions (e.g., `alpha`, `beta`)
  - **BUILD**: Optional build metadata (e.g., `build.1234`)
2. **Version increments**:
  - `1.0.0` → `2.0.0`: Breaking changes (MAJOR)
  - `1.0.0` → `1.1.0`: New features, no breaking changes (MINOR)
  - `1.0.0` → `1.0.1`: Bug fixes, no new features or breaking changes (PATCH)
3. **Pre-release versions**:
  - `1.0.0-alpha` < `1.0.0-alpha.1` < `1.0.0-beta` < `1.0.0-rc.1` < `1.0.0`

**NPM's version specifiers**:
| Symbol | Meaning | Example | Description |
| :--- | :--- | :--- | :--- |
| `^` | Compatible with | `^2.11.7` | Allows `2.x.x` but not `3.0.0` |
| `~` | Approximately | `~2.11.7` | Allows `2.11.x` but not `2.12.0` |
| `>` | Greater than | `>2.0.0` | Any version greater than `2.0.0` |
| `>=` | Greater than or equal | `>=2.0.0` | Any version `2.0.0` or greater |
| `<` | Less than | `<3.0.0` | Any version less than `3.0.0` |
| `<=` | Less than or equal | `<=3.0.0` | Any version `3.0.0` or less |
| `=` | Equal | `=2.11.7` | Exactly version `2.11.7` |
| no symbol | Equal | `2.11.7` | Exactly version `2.11.7` |
| `1.x` | X-Range | `1.x` | Any version where major is `1` |
| `*` | Any | `*` | Any version |
| `latest` | Latest | `latest` | The latest published version |

**Version range examples**:
- `^1.2.3` allows `1.2.3` to `1.999.999` but not `2.0.0`
- `~1.2.3` allows `1.2.3` to `1.2.999` but not `1.3.0`
- `>=1.2.3 <2.0.0` allows versions between `1.2.3` and `2.0.0` (excluding `2.0.0`)
- `1.2.x` allows any patch version in the `1.2` minor version

## Question 20
*Reference: [Question 20](node-questions.md#question-20)*

### Q. How can you publish a package to NPM?

Publishing a package to NPM involves several steps to prepare, test, and publish your code:
1. **Create an NPM account**:
```bash
# Create account on npmjs.com or via CLI
npm adduser
```
2. **Login to NPM**:
```bash
npm login
```
3. **Prepare your package**:
  - Create a complete `package.json` with:
    - Unique name (`name` field)
    - Version (`version` field)
    - Entry point (`main` field)
    - Description and keywords
    - Author and license information
  - Structure your package properly:
    - Implement main entry file
    - Add README.md with documentation
    - Add LICENSE file
  - Control included files using either:
    - `files` field in `package.json`
    - `.npmignore` file (similar to `.gitignore`)
    ```json
    {
      "name": "my-awesome-package",
      "version": "1.0.0",
      "description": "A useful utility library",
      "main": "index.js",
      "files": [
        "dist",
        "lib",
        "index.js"
      ]
    }
    ```

4. **Test your package locally**:
```bash
# Install your package globally in development mode
npm link
   
# Create a test project and link to your package
mkdir test-project
cd test-project
npm link my-awesome-package
   
# Or use npm pack to create a tarball and install it
npm pack  # Creates my-awesome-package-1.0.0.tgz
npm install ../my-awesome-package-1.0.0.tgz
```
5. **Run integrity checks**:
```bash
# Verify package contents
npm pack
tar -tf my-awesome-package-1.0.0.tgz
   
# Run tests
npm test
```
6. **Publish to NPM registry**:
```bash
# For first-time publish
npm publish
   
# For scoped packages (@username/package-name)
npm publish --access=public
```
7. **Versioning and updates**:
```bash
# Update version according to SemVer
npm version patch  # Increments 1.0.0 to 1.0.1
npm version minor  # Increments 1.0.0 to 1.1.0
npm version major  # Increments 1.0.0 to 2.0.0
   
# Publish the update
npm publish
```
8. **Managing 1. **ackage visibility and distribution**:
```bash
# Publish to a custom registry
npm publish --registry=https://registry.example.com
   
# Create an organization-scoped package
npm init --scope=@myorg
   
# Unpublish (only within first 72 hours)
npm unpublish my-awesome-package@1.0.0
```
Advanced publishing considerations:
- Set up two-factor authentication for account security
- Use CI/CD pipelines for automated testing and publishing
- Consider using semantic-release for automated versioning based on commit messages
- For TypeScript packages, include type definitions and set `types` field in package.json