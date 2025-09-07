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


# File System

## Question 21
*Reference: [Question 21](node-questions.md#question-21)*

### Q. What is the fs module in Node.js, and how do you use it to read a file synchronously and asynchronously?

The `fs` module is a core built-in module in Node.js that provides an API for interacting with the file system. It enables you to work with files and directories, allowing operations such as reading, writing, updating, deleting, and watching files.

**Synchronous file reading (fs.readFileSync):**
Blocks the event loop until complete, ideal for startup scripts or CLI tools where performance isn't critical. It throws errors immediately, so wrap in try-catch. Returns a Buffer by default or string with encoding.

```javascript
const fs = require('fs');

try {
  // Synchronously reads the entire file content
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error('Error reading file:', err);
}
```
**Asynchronous file reading:**
Non-blocking; uses callbacks (fs.readFile) or promises (fs.promises.readFile). Callbacks take error-first pattern; promises enable async/await. Supports AbortSignal for cancellation in modern versions.

```javascript
const fs = require('fs');

// Using callback approach
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log(data);
});

// Using Promises (Node.js 10+ with fs.promises)
const fsPromises = require('fs').promises;

fsPromises.readFile('example.txt', 'utf8')
  .then(data => console.log(data))
  .catch(err => console.error('Error reading file:', err));

// Using async/await (modern approach)
async function readFileAsync() {
  try {
    const data = await fsPromises.readFile('example.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error('Error reading file:', err);
  }
}
readFileAsync();
```

## Question 22
*Reference: [Question 22](node-questions.md#question-22)*

### Q. Explain the difference between fs.readFile() and fs.readFileSync().

fs.readFile() and fs.readFileSync() both read files from the file system, but they differ in how they execute and impact program flow:

**fs.readFile()**:
- **Asynchronous**: Operates non-blocking
- **Callback-based**: Takes a callback function that executes when the operation completes
- **Program flow**: Continues execution without waiting for the file operation to complete
- **Use case**: Preferred in production environments where performance is critical
- **Error handling**: Through callback parameters
```javascript
fs.readFile('large-file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error:', err);
    return;
  }
  console.log('File read complete');
});
console.log('This runs before file is read!');
```
**fs.readFileSync()**:
- **Synchronous**: Operates blocking
- **Return value**: Returns the file content directly
- **Program flow**: Blocks execution until the file operation completes
- **Use case**: Simpler code for scripts, CLI tools, or program initialization
- **Error handling**: Through try/catch blocks
```javascript
try {
  const data = fs.readFileSync('config.txt', 'utf8');
  console.log('File read complete');
} catch (err) {
  console.error('Error:', err);
}
console.log('This runs after file is read');
```
The key difference is that readFileSync() blocks the event loop until the file is completely read, while readFile() allows the program to continue execution while the file is being read, improving application responsiveness, especially for large files or multiple concurrent operations.

## Question 23
*Reference: [Question 23](node-questions.md#question-23)*

### Q. How do you write to a file using the fs module?

Writing to files with fs supports sync, callback, and promise APIs—replacing files if they exist (use flags like 'a' for append). It's atomic where possible but not thread-safe for concurrent writes, so sequence ops in production.
- Synchronous (fs.writeFileSync): Blocks; throws on error.
- Asynchronous (fs.writeFile): Callback-based; non-blocking.
- Promises (fs.promises.writeFile): Awaitable; supports AbortSignal.

Data can be string, Buffer, or iterable; options include encoding, mode (permissions), flag ('w' default).

```javascript
const fs = require('node:fs');
const fsPromises = require('node:fs/promises');
const data = 'Hello, Node.js!';

// Synchronous
try {
  fs.writeFileSync('output.txt', data, 'utf8'); // Overwrites
  console.log('Sync write complete');
} catch (err) {
  console.error('Sync write error:', err);
}

// Asynchronous (Callback)
fs.writeFile('output.txt', data, 'utf8', (err) => {
  if (err) console.error('Async write error:', err);
  else console.log('Async write complete');
});

// Promises
async function writeAsync() {
  try {
    await fsPromises.writeFile('output.txt', data, 'utf8');
    console.log('Promise write complete');
  } catch (err) {
    console.error('Promise write error:', err);
  }
}
writeAsync();
```
**Additional options for file writing:**
```javascript
// Write with options
fs.writeFile('output.txt', 'Hello, World!', { 
  encoding: 'utf8',
  mode: 0o666,  // File permissions
  flag: 'w'     // 'w' for write (default), 'a' for append
}, (err) => {
  if (err) throw err;
  console.log('File written with options');
});

// Write binary data
const buffer = Buffer.from([0x48, 0x65, 0x6c, 0x6c, 0x6f]); // "Hello" in hex
fs.writeFile('binary.dat', buffer, (err) => {
  if (err) throw err;
  console.log('Binary file written');
});
```

## Question 24
*Reference: [Question 24](node-questions.md#question-24)*

### Q. What is fs.createReadStream() and when would you use it?

fs.createReadStream(path, [options]) creates a Readable stream for efficient, chunked file reading—emitting 'data' events as buffers/strings become available, ideal for handling large files without loading everything into memory. It's a core part of Node's streaming API, inheriting from stream.Readable.
- **How It Works**: Opens file, reads in chunks (highWaterMark option, default 64KB), supports start/end for ranges, encoding for strings, autoClose (default true) for fd cleanup.
- **Events**: 'open', 'data', 'end', 'error', 'close'.

```javascript
const fs = require('fs');

// Create a readable stream
const readStream = fs.createReadStream('large-file.txt', {
  encoding: 'utf8',
  highWaterMark: 64 * 1024 // 64KB chunks (default is 64KB)
});

// Handle stream events
readStream.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
  // Process chunk here
});

readStream.on('end', () => {
  console.log('Finished reading file');
});

readStream.on('error', (err) => {
  console.error('Stream error:', err);
});
```
**When to use fs.createReadStream():**
1. **Processing large files**: When dealing with files that are too large to fit comfortably in memory (logs, datasets, media files).
2. **Piping data**: When you need to pipe data between streams, such as from a file to an HTTP response.
```javascript
const http = require('http');
   
http.createServer((req, res) => {
  // Stream a video file directly to HTTP response
  const videoStream = fs.createReadStream('video.mp4');
  videoStream.pipe(res);
}).listen(3000);
```
3. **Real-time processing**: When you need to process data as it becomes available, without waiting for the entire file.
```javascript
const readline = require('readline');
   
const fileStream = fs.createReadStream('logs.txt');
const rl = readline.createInterface({
  input: fileStream,
  crlfDelay: Infinity
});
   
// Process the file line by line
rl.on('line', (line) => {
  if (line.includes('ERROR')) {
    console.log(`Found error: ${line}`);
  }
});
```
4. **Memory efficiency**: When performing operations like file uploads/downloads, parsing large CSV/JSON files, or processing logs
Streams are memory-efficient, improve application responsiveness, and are one of Node.js's greatest strengths for I/O operations.

## Question 25
*Reference: [Question 25](node-questions.md#question-25)*

### Q. How do you handle file paths in a cross-platform way in Node.js?

andling file paths across different operating systems (Windows, macOS, Linux) requires special attention due to differences in path separators and formats. Node.js provides the path module specifically for this purpose:
```javascript
const path = require('path');
const fs = require('fs');

// Join path segments in a cross-platform way
const filePath = path.join(__dirname, 'data', 'config.json');

// Read the file using the platform-appropriate path
fs.readFile(filePath, 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```
**Key path module functions for cross-platform compatibility:**
1. **path.join()**: Joins path segments using the platform-specific separator
```javascript
// Windows: C:\Users\username\project\data\config.json
// Unix: /home/username/project/data/config.json
const configPath = path.join(__dirname, 'data', 'config.json');
```
2. **path.resolve()**: Resolves a sequence of paths to an absolute path
```javascript
// Resolves to absolute path from current working directory
const absolutePath = path.resolve('data', 'config.json');
```
3. **path.normalize()**: Normalizes a path, resolving '..' and '.' segments
```javascript
const normalizedPath = path.normalize('/data/../config/./settings.json');
// Results in '/config/settings.json'
```
4. **path.parse()**: Returns an object with path components
```javascript
const pathInfo = path.parse('/home/user/file.txt');
// { root: '/', dir: '/home/user', base: 'file.txt', ext: '.txt', name: 'file' }
```
5. **path.sep** and **path.delimiter**: 1. Platform-specific path separator and PATH delimiter
```javascript
console.log(`Path separator: ${path.sep}`); // '\' on Windows, '/' on Unix
console.log(`Path delimiter: ${path.delimiter}`); // ';' on Windows, ':' on Unix
```
6. **__dirname** and **__filename**: Global variables for current directory and file
```javascript
console.log(`Current directory: ${__dirname}`);
console.log(`Current file: ${__filename}`);
```
Always use these path utilities instead of string concatenation to ensure your Node.js applications work consistently across all platforms.

## Question 26
*Reference: [Question 26](node-questions.md#question-26)*

### Q. Explain fs.watch() and its use cases.

fs.watch() is a method in the fs module that watches for changes on files or directories. It allows you to monitor file system events and execute callbacks when files are modified.
```javascript
const fs = require('fs');

// Watch a file for changes
const watcher = fs.watch('config.json', (eventType, filename) => {
  console.log(`Event type: ${eventType}`);
  if (filename) {
    console.log(`File changed: ${filename}`);
    // Reload configuration, restart services, etc.
  }
});

// Stop watching when needed
// watcher.close();

// Watch a directory for changes
fs.watch('./logs', { recursive: true }, (eventType, filename) => {
  console.log(`Event type: ${eventType}`);
  console.log(`File changed: ${filename}`);
});
```
**Key use cases for fs.watch():**
1. **Development tooling**: Creating file watchers for development servers that automatically reload when source files change
```javascript
// Simple development server that restarts on file changes
fs.watch('./src', { recursive: true }, (eventType, filename) => {
  if (filename.endsWith('.js')) {
    console.log(`${filename} changed, restarting server...`);
    // Logic to restart server
  }
});
```
2. **Configuration monitoring**: Automatically reloading application configuration when config files change
```javascript
fs.watch('config.json', (eventType) => {
  if (eventType === 'change') {
    console.log('Config changed, reloading...');
    try {
      const newConfig = JSON.parse(fs.readFileSync('config.json', 'utf8'));
      updateApplicationConfig(newConfig);
    } catch (err) {
      console.error('Error reloading config:', err);
    }
  }
});
```
3. **Log monitoring**: Watching log directories for new files or changes
```javascript
fs.watch('./logs', (eventType, filename) => {
  if (eventType === 'rename' && filename.endsWith('.log')) {
    console.log(`New log file detected: ${filename}`);
    // Process new log file
  }
});
```
4. **Automated testing**: Triggering test runs when source files change
```javascript
fs.watch('./src', { recursive: true }, debounce((eventType, filename) => {
  if (filename.endsWith('.js')) {
    console.log(`Running tests for ${filename}...`);
    runTests();
  }
}, 500));
```
**Important limitations and considerations:**
1. **Platform differences**: The behavior of `fs.watch()` varies across platforms.
2. **Event notification**: May receive multiple events for a single change.
3. **File renaming**: Some systems might report rename events differently.
4. **Recursive option**: Not supported on all platforms.
5. **Symlinks**: May not work as expected with symbolic links.
6. **Performance**: May have performance implications when watching large directory trees.

For more reliable file watching in production applications, third-party packages like chokidar are often preferred as they normalize behavior across platforms and provide additional features.


# Events and Event Loop

## Question 27
*Reference: [Question 27](node-questions.md#question-27)*

### Q. What is the EventEmitter class in Node.js?

The EventEmitter class is a built-in class in Node.js that provides a way to create and manage events. It allows you to create custom events and emit events to listeners.

Key characteristics of EventEmitter:
```javascript
const EventEmitter = require('events');

// Create an instance of EventEmitter
class MyEmitter extends EventEmitter {}
const myEmitter = new MyEmitter();

// Register an event listener
myEmitter.on('event', function(a, b) {
  console.log(a, b); // Prints: 1, 2
});

// Emit the event
myEmitter.emit('event', 1, 2);
```
EventEmitter provides several important methods:
- `on()` / `addListener()`: Register a listener for a named event.
- `once()`: Register a one-time listener that's removed after being called.
- `emit()`: Trigger an event with optional arguments.
- `removeListener()` / `off()`: Remove a specific listener.
- `removeAllListeners()`: Remove all listeners for an event.
- `setMaxListeners()`: Configure maximum listeners (default is 10).
- `listeners()`: Return array of listeners for an event.

EventEmitter is the backbone of Node.js's non-blocking I/O model, enabling asynchronous, event-driven programming throughout the Node.js ecosystem.

## Question 28
*Reference: [Question 28](node-questions.md#question-28)*

### Q. How do you create a custom event in Node.js?

Creating custom events in Node.js involves extending or using the EventEmitter class:
```javascript
const EventEmitter = require('events');

// Method 1: Create by extending EventEmitter (recommended)
class DatabaseConnection extends EventEmitter {
  connect() {
    // Simulate connection process
    setTimeout(() => {
      // Connection successful
      this.emit('connected', { 
        timestamp: new Date(),
        connectionId: Math.floor(Math.random() * 1000)
      });
    }, 1000);
  }
  
  query(sql) {
    // Simulate query execution
    setTimeout(() => {
      if (sql.includes('SELECT')) {
        this.emit('results', { rows: [{ id: 1, name: 'test' }] });
      } else {
        this.emit('error', new Error('Invalid query'));
      }
    }, 500);
  }
}

// Usage
const db = new DatabaseConnection();

db.on('connected', (data) => {
  console.log(`Database connected at ${data.timestamp} with ID: ${data.connectionId}`);
  db.query('SELECT * FROM users');
});

db.on('results', (data) => {
  console.log('Query results:', data.rows);
});

db.on('error', (err) => {
  console.error('Database error:', err.message);
});

db.connect();

// Method 2: Using EventEmitter instance directly
const myEmitter = new EventEmitter();

// Register event handlers
myEmitter.on('userLoggedIn', (user) => {
  console.log(`User logged in: ${user.name}`);
});

// Later in code, trigger the event
myEmitter.emit('userLoggedIn', { id: 123, name: 'John Doe' });
```
Best practices for custom events:
1. Use descriptive event names (e.g., 'data', 'end', 'error').
2. Document the event payload structure.
3. Always handle 'error' events to prevent crashes.
4. Avoid creating excessive listeners (monitor with `getMaxListeners()`).
5. Clean up listeners when they're no longer needed to prevent memory leaks.

## Question 29
*Reference: [Question 29](node-questions.md#question-29)*

### Q. Explain the phases of the Node.js event loop.

The Node.js event loop is a mechanism that allows Node.js to perform non-blocking I/O operations despite JavaScript being single-threaded. It works by offloading operations to the system kernel whenever possible and operates in several distinct phases:
1. **Timers phase**: Executes callbacks scheduled by `setTimeout()` and `setInterval()`
  - Processes timer thresholds that have elapsed.
  - Executes their callbacks in order of their creation time.
2. **Pending callbacks phase**: Executes I/O callbacks deferred to the next loop iteration
  - Handles callbacks for certain system operations (like TCP errors).
  - Processes any callbacks from previous loop iterations that were deferred.
3. **Idle, prepare phase**: Internal use only for Node.js
  - Used by the event loop itself for internal bookkeeping.
4. **Poll phase**: Retrieves new I/O events and executes I/O related callbacks
  - Waits for new I/O events if there are none pending.
  - Calculates how long to block for I/O considering timer thresholds.
  - Processes events in the poll queue.
5. **Check phase**: Executes callbacks registered via `setImmediate()`
  - Runs immediately after the poll phase completes.
  - Allows execution of callbacks after the poll phase has processed I/O callbacks.
6. **Close callbacks phase**: Executes close event callbacks
  - Handles 'close' events (e.g., `socket.on('close', ...)`).

Between each phase, the event loop checks if there are any pending process.nextTick() callbacks or microtasks (like Promise callbacks) and executes them.

This diagram represents the event loop phases:
```
   ┌───────────────────────────┐
┌─>│           timers          │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │
│  └─────────────┬─────────────┘      ┌───────────────┐
│  ┌─────────────┴─────────────┐      │   incoming:   │
│  │           poll            │<─────┤  connections, │
│  └─────────────┬─────────────┘      │   data, etc.  │
│  ┌─────────────┴─────────────┐      └───────────────┘
│  │           check           │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │
   └───────────────────────────┘
```

In summary, the event loop handles timers, pending callbacks, idle, prepare, poll, check, and close callbacks. It executes callbacks in a specific order to ensure they're processed in a timely manner.


## Question 30
*Reference: [Question 30](node-questions.md#question-30)*

### Q. What are the differences between setImmediate(), setTimeout(), and process.nextTick()?

These three functions all schedule callbacks to be executed, but they differ in when those callbacks are executed:

### process.nextTick()
```javascript
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
- Runs before any other phase of the event loop resumes.
- Executes after the current operation completes, regardless of the event loop phase.
- Has higher priority than any other asynchronous operation.
- Creates a "next tick queue" that's processed after the current operation finishes but before the event loop continues.
- Can cause "I/O starvation" if used incorrectly (recursive calls prevent the loop from proceeding).

### setImmediate()
```javascript
console.log('Start');
setImmediate(() => {
  console.log('setImmediate callback');
});
console.log('End');

// Output:
// Start
// End
// setImmediate callback
```
- Executes in the "check" phase of the event loop.
- Runs after the poll phase completes.
- Specifically designed to execute a callback after the current poll phase completes.
- Particularly useful within I/O cycles to execute callbacks after I/O events have been processed.

### setTimeout(fn, 0)
```javascript
console.log('Start');
setTimeout(() => {
  console.log('setTimeout callback');
}, 0);
console.log('End');

// Output:
// Start
// End
// setTimeout callback
```
- Executes in the "timers" phase of the event loop.
- Has a minimum threshold of 1ms (even with 0ms specified).
- Timing isn't guaranteed (affected by CPU load and other callbacks).
- Schedules execution after the specified timeout has elapsed.

### Execution Order
When used together, their execution order can be challenging to predict:
```javascript
setTimeout(() => console.log('setTimeout'), 0);
setImmediate(() => console.log('setImmediate'));
process.nextTick(() => console.log('nextTick'));

// Output:
// nextTick
// setTimeout or setImmediate (order can vary)
```
However, within an I/O cycle, setImmediate is always executed before any timers:
```javascript
const fs = require('fs');

fs.readFile(__filename, () => {
  setTimeout(() => console.log('setTimeout'), 0);
  setImmediate(() => console.log('setImmediate'));
});

// Output:
// setImmediate
// setTimeout
```

## Solution 31
*Reference: [Solution 31](node-questions.md#solution-31)*

### Q. How does Node.js handle blocking operations?

ode.js handles potentially blocking operations through several strategies to maintain its non-blocking, event-driven architecture:
### 1. Asynchronous APIs
Node.js provides asynchronous versions of most I/O operations:
```javascript
// Synchronous (blocking) version
const fs = require('fs');
try {
  const data = fs.readFileSync('/path/to/file', 'utf8');
  console.log(data);
} catch (err) {
  console.error(err);
}
console.log('This will only log after file is read');

// Asynchronous (non-blocking) version
fs.readFile('/path/to/file', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
console.log('This will log before file is read');

// Modern async/await with promises
const fsPromises = require('fs').promises;
async function readFile() {
  try {
    const data = await fsPromises.readFile('/path/to/file', 'utf8');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
readFile();
console.log('This will log before file is read');
```
### 2. Thread Pool (via libuv)
For operations that cannot be handled by the operating system's asynchronous interfaces, Node.js uses a thread pool managed by libuv:
- File system operations
- CPU-intensive crypto operations
- DNS lookups (in some cases)
- Some implementations of zlib operations
```javascript
const crypto = require('crypto');

// This is CPU-intensive and would block without the thread pool
function hashPassword(password) {
  const salt = crypto.randomBytes(16).toString('hex');
  
  // This will be executed in the thread pool
  return crypto.pbkdf2Sync(password, salt, 1000000, 64, 'sha512').toString('hex');
}

// Using it asynchronously with the thread pool
crypto.pbkdf2(password, salt, 1000000, 64, 'sha512', (err, derivedKey) => {
  if (err) throw err;
  console.log(derivedKey.toString('hex'));
});
```
### 3. Worker Threads (for CPU-bound tasks)
For truly CPU-intensive tasks, Node.js provides Worker Threads:
```javascript
const { Worker, isMainThread, parentPort, workerData } = require('worker_threads');

if (isMainThread) {
  // This is the main thread
  
  // Create a worker
  const worker = new Worker(__filename, {
    workerData: { numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] }
  });
  
  // Listen for messages from the worker
  worker.on('message', (result) => {
    console.log(`Sum: ${result}`);
  });
  
  worker.on('error', (err) => {
    console.error(err);
  });
  
  worker.on('exit', (code) => {
    if (code !== 0) console.error(`Worker stopped with exit code ${code}`);
  });
  
} else {
  // This is a worker thread
  
  // Calculate sum (CPU-intensive task)
  const data = workerData;
  const result = data.numbers.reduce((sum, num) => sum + num, 0);
  
  // Send the result back to the main thread
  parentPort.postMessage(result);
}
```
### 4. Child Processes
For very intensive operations, Node.js can spawn separate processes:
```javascript
const { exec, spawn } = require('child_process');

// Using exec
exec('find . -type f | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`exec error: ${error}`);
    return;
  }
  console.log(`Number of files: ${stdout}`);
});

// Using spawn for streaming data
const child = spawn('find', ['.', '-type', 'f']);

child.stdout.on('data', (data) => {
  console.log(`Found file: ${data}`);
});

child.stderr.on('data', (data) => {
  console.error(`stderr: ${data}`);
});

child.on('close', (code) => {
  console.log(`Child process exited with code ${code}`);
});
```
By leveraging these strategies, Node.js can maintain its event-driven, non-blocking model even when handling operations that would traditionally block the event loop.

## Solution 32
*Reference: [Solution 32](node-questions.md#solution-32)*

### What is libuv, and what does it provide to Node.js?

Libuv is a multi-platform C library that provides the event loop and asynchronous I/O capabilities that form the foundation of Node.js. It was originally developed specifically for Node.js but has since been adopted by other projects.
### Key features and capabilities libuv provides to Node.js:
1. **Cross-platform event loop** implementation
  - Abstracts platform-specific mechanisms like epoll (Linux), kqueue (macOS/BSD), event ports (Solaris), and IOCP (Windows)
  - Enables consistent event-driven programming across operating systems
2. **Thread pool** for offloading work
  - Allows CPU-intensive tasks to execute without blocking the main event loop
  - Handles file system operations, DNS resolution, and some cryptographic operations
3. **File system operations**
  - Provides asynchronous file I/O operations
  - Handles file watching and change notification
4. **Network I/O**
  - TCP/UDP socket handling
  - DNS resolution
  - Pipe support for inter-process communication
5. **Child process management**
  - Process spawning
  - Process stdio handling
  - Process termination
6. **Thread synchronization primitives**
  - Mutexes, semaphores, condition variables
  - Thread-local storage
7. **High-resolution time functionality**
  - Precise timers
  - Performance measurement capabilities
8. **Signal handling**
  - Management of system signals (SIGINT, SIGTERM, etc.)

### Architecture relationship between Node.js, V8, and libuv:
```
┌───────────────────────────┐
│           Node.js         │ JavaScript API
└─────────────┬─────────────┘
┌─────────────┴─────────────┐
│             V8            │ JavaScript Engine
└─────────────┬─────────────┘
┌─────────────┴─────────────┐
│            libuv          │ Asynchronous I/O
└───────────────────────────┘
```
Example of how Node.js APIs use libuv under the hood:
```javascript
// This simple Node.js code:
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Translates through layers:
// 1. Node.js fs module calls libuv's file operations
// 2. libuv schedules the I/O operation in its event loop
// 3. libuv delegates the actual file read to its thread pool
// 4. When complete, libuv triggers the callback in the next event loop iteration
// 5. V8 executes the JavaScript callback with the result
```
Libuv effectively handles the most challenging aspect of Node.js's architecture - managing asynchronous I/O operations efficiently across different operating systems. It allows Node.js to maintain its single-threaded programming model while still achieving high performance for I/O-bound applications.

# Node.js Streams

## Solution 33
*Reference: [Solution 33](node-questions.md#solution-33)*

### Q. What are streams in Node.js, and what types are there (Readable, Writable, Duplex, Transform)?

Streams in Node.js are abstract interfaces for working with streaming data. They allow you to process data piece by piece (chunks) instead of loading the entire dataset into memory, making them memory-efficient for handling large amounts of data or real-time information.

**he four main types of streams in Node.js are:**
1. **Readable Streams**: Sources that you can read data from (but not write to)
  - Examples: `fs.createReadStream()`, HTTP request objects, process.stdin.
  - Used for reading data from a source in chunks.
2. **Writable Streams**: Destinations that you can write data to (but not read from)
  - Examples: `fs.createWriteStream()`, HTTP response objects, process.stdout.
  - Used for writing data to a destination in chunks.
3. **Duplex Streams**: Both readable and writable (independent channels)
  - Examples: TCP sockets, Zlib streams.
  - Can both read from and write to a source.
4. **Transform Streams**: Special type of duplex streams where the output is computed based on the input
  - Examples: zlib.createGzip(), crypto streams.
  - Transforms data as it's being read or written (data out is transformation of data in).

All stream types are instances of EventEmitter, allowing them to emit and listen for events during data processing.

## Solution 34
*Reference: [Solution 34](node-questions.md#solution-34)*

### Q.  Provide an example of piping a readable stream to a writable stream.

Here's an example of piping a readable stream to a writable stream to create a file copy operation:

```javascript
const fs = require('fs');

// Create a readable stream for reading from a file
const readableStream = fs.createReadStream('source-file.txt', {
  encoding: 'utf8',
  highWaterMark: 64 * 1024 // 64KB chunks
});

// Create a writable stream for writing to another file
const writableStream = fs.createWriteStream('destination-file.txt');

// Pipe the readable stream to the writable stream
readableStream.pipe(writableStream);

// Handle events
writableStream.on('finish', () => {
  console.log('File copy operation completed successfully');
});

readableStream.on('error', (err) => {
  console.error('Error reading file:', err);
});

writableStream.on('error', (err) => {
  console.error('Error writing file:', err);
});
```
Another common example is streaming a file to an HTTP response:
```javascript
const fs = require('fs');
const http = require('http');

http.createServer((req, res) => {
  // Set appropriate headers for video content
  res.writeHead(200, {'Content-Type': 'video/mp4'});
  
  // Create a readable stream from a video file
  const videoStream = fs.createReadStream('video.mp4');
  
  // Pipe the video stream directly to the HTTP response
  videoStream.pipe(res);
  
  // Handle errors
  videoStream.on('error', (err) => {
    console.error('Error streaming video:', err);
    res.end('Error occurred while streaming');
  });
}).listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```

## Question 35
*Reference: [Question 35](node-questions.md#question-35)*

### Q. How do you handle errors in streams?

roper error handling is crucial in stream operations to prevent application crashes. Since streams are EventEmitters, they emit 'error' events when something goes wrong.

**Best practices for handling stream errors:**
1. **Always listen for the 'error' event on all streams:**
```javascript
const fs = require('fs');
const readStream = fs.createReadStream('non-existent-file.txt');

readStream.on('error', (err) => {
  console.error('Error occurred:', err.message);
  // Perform cleanup or recovery operations
});
```
2. **Error handling with pipe():**
When using pipe(), errors from the source stream don't automatically propagate to destination streams. You need to handle errors on each stream separately:
```javascript
const fs = require('fs');
const readStream = fs.createReadStream('source.txt');
const writeStream = fs.createWriteStream('destination.txt');

// Handle errors on both streams
readStream.on('error', (err) => {
  console.error('Read error:', err.message);
  // Clean up the write stream if needed
  writeStream.end();
});

writeStream.on('error', (err) => {
  console.error('Write error:', err.message);
  // Stop the read stream to prevent more data flow
  readStream.destroy();
});

// Pipe data
readStream.pipe(writeStream);
```
3. **Using pipeline() (Node.js v10.0.0+) for automatic error propagation:**
```javascript
const { pipeline } = require('stream');
const fs = require('fs');

const readStream = fs.createReadStream('source.txt');
const writeStream = fs.createWriteStream('destination.txt');

pipeline(
  readStream,
  writeStream,
  (err) => {
    if (err) {
      console.error('Pipeline failed:', err.message);
    } else {
      console.log('Pipeline succeeded');
    }
  }
);
```
4. **Promisified version with stream/promises (Node.js v15.0.0+):**
```javascript
const { pipeline } = require('stream/promises');
const fs = require('fs');

async function copyFile() {
  try {
    await pipeline(
      fs.createReadStream('source.txt'),
      fs.createWriteStream('destination.txt')
    );
    console.log('Pipeline succeeded');
  } catch (err) {
    console.error('Pipeline failed:', err.message);
  }
}

copyFile();
```

## Solution 36
*Reference: [Solution 36](node-questions.md#solution-36)*

### Q. What is backpressure in streams, and how is it managed?

Backpressure is a mechanism in Node.js streams that handles situations where data is coming in faster than it can be processed or written. It's essential for preventing memory overflow and ensuring efficient data processing.

**How backpressure works:**
1. When a writable stream's internal buffer fills up (reaches highWaterMark), the `write()` method returns `false`.
2. This signals to the source (readable stream) that it should temporarily pause sending data.
3. When the writable stream's buffer drains (emits a 'drain' event), the readable stream can resume sending data.

**Managing backpressure:**
1. **Using pipe()** - The simplest way to handle backpressure automatically:
```javascript
readableStream.pipe(writableStream);
```
The `pipe()` method handles backpressure internally by pausing the readable stream when necessary and resuming it when the writable stream emits a 'drain' event.

2. **Manual backpressure management** - When not using pipe():
```javascript
const fs = require('fs');

const readStream = fs.createReadStream('largefile.txt');
const writeStream = fs.createWriteStream('destination.txt');

readStream.on('data', (chunk) => {
  // Try to write the chunk
  const canContinue = writeStream.write(chunk);
  
  // If write returns false, pause the readable stream
  if (!canContinue) {
    readStream.pause();
    
    // Resume the readable stream once the writable stream drains
    writeStream.once('drain', () => {
      readStream.resume();
    });
  }
});

readStream.on('end', () => {
  writeStream.end();
});

// Error handling
readStream.on('error', (err) => {
  console.error('Read error:', err);
  writeStream.end();
});

writeStream.on('error', (err) => {
  console.error('Write error:', err);
  readStream.destroy();
});
```
3 **Using pipeline() (Node.js v10.0.0+)** - Handles backpressure and errors automatically:
```javascript
const { pipeline } = require('stream');

pipeline(
  fs.createReadStream('largefile.txt'),
  fs.createWriteStream('destination.txt'),
  (err) => {
    if (err) {
      console.error('Pipeline failed:', err);
    } else {
      console.log('Pipeline succeeded');
    }
  }
);
```

## Question 37
*Reference: [Question 37](node-questions.md#question-37)*

### Q. Explain the difference between flowing mode and paused mode in readable streams.

eadable streams in Node.js can operate in two modes: flowing and paused (non-flowing). These modes determine how data is consumed from the stream.

**Paused Mode:**
- Default mode for all Readable streams.
- Data must be explicitly requested using the `read()` method.
- You control when and how much data is read.
- Works with the 'readable' event to signal that data is available to be read.
- More control but requires more manual code.

```javascript
const fs = require('fs');
const readStream = fs.createReadStream('file.txt');

// Using paused mode
readStream.on('readable', () => {
  let chunk;
  // read() returns null when no more data is available
  while (null !== (chunk = readStream.read())) {
    console.log(`Read ${chunk.length} bytes of data`);
    console.log(chunk.toString());
  }
});

readStream.on('end', () => {
  console.log('No more data to read');
});

readStream.on('error', (err) => {
  console.error('Error:', err);
});
```
**Flowing Mode:**
- Stream automatically pushes data to the consumer as soon as it's available.
- Triggered by attaching a 'data' event handler, using `pipe()`, or calling `resume()`.
- Easier to use but offers less control over data consumption.
- Data can be lost if not handled immediately.
```javascript
const fs = require('fs');
const readStream = fs.createReadStream('file.txt');

// Switch to flowing mode by adding a 'data' event handler
readStream.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
  console.log(chunk.toString());
});

readStream.on('end', () => {
  console.log('No more data to read');
});

readStream.on('error', (err) => {
  console.error('Error:', err);
});
```
**Switching between modes:**
- From paused to flowing: Add a 'data' event listener, call stream.resume(), or pipe to another stream.
- From flowing to paused: Call stream.pause(), remove all 'data' event listeners, or unpipe() from all destinations.
```javascript
const readStream = fs.createReadStream('file.txt');

// Start in flowing mode
readStream.on('data', processChunk);

// Later, switch to paused mode
setTimeout(() => {
  readStream.pause();
  console.log('Stream paused');
  
  // Process some data in paused mode
  process.nextTick(() => {
    console.log('Processing in paused mode');
    let chunk = readStream.read();
    if (chunk) processChunk(chunk);
    
    // Switch back to flowing mode
    readStream.resume();
    console.log('Stream resumed to flowing mode');
  });
}, 1000);

function processChunk(chunk) {
  console.log(`Processed ${chunk.length} bytes`);
}
```

# HTTP and Servers

## Solution 38
*Reference: [Solution 38](node-questions.md#solution-38)*

### Q. How do you create a basic HTTP server in Node.js using the http module?

You can create a basic HTTP server in Node.js using the built-in http module, which provides the functionality to create and manage HTTP servers.

```javascript
// Basic HTTP Server
const http = require('http');

// Create server instance
const server = http.createServer((req, res) => {
  // Set response headers
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  
  // Send response body
  res.end('Hello, World!');
});

// Define port
const PORT = 3000;

// Start listening
server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}/`);
});
```
This simple server listens for incoming requests on port 3000 and responds with "Hello, World!" to every request. The createServer() method takes a callback function that receives two parameters:
- `req` (request): Contains information about the incoming request
- `res` (response): Used to formulate and send a response back to the client

## Solution 39
*Reference: [Solution 39](node-questions.md#solution-39)*

### Q. What is the `request` and `response` object in an HTTP server?

The request (`req`) and response (`res`) objects are core components of Node.js HTTP servers, providing interfaces for handling HTTP interactions.

**Request Object (`req`)**
The request object contains information about the incoming HTTP request:
```javascript
const http = require('http');

http.createServer((req, res) => {
  console.log('Method:', req.method);          // GET, POST, PUT, DELETE, etc.
  console.log('URL:', req.url);                // Path requested (/api/users, etc.)
  console.log('Headers:', req.headers);        // Request headers object
  console.log('HTTP Version:', req.httpVersion); // HTTP version used
  
  // Reading request body (for POST, PUT requests)
  let body = '';
  req.on('data', (chunk) => {
    body += chunk.toString();
  });
  
  req.on('end', () => {
    console.log('Body:', body);
    res.end('Request received');
  });
}).listen(3000);
```
**Response Object (`res`)**
The response object is used to send data back to the client:
```javascript
const http = require('http');

http.createServer((req, res) => {
  // Set status code
  res.statusCode = 200; // OK
  
  // Set response headers
  res.setHeader('Content-Type', 'application/json');
  res.setHeader('X-Custom-Header', 'CustomValue');
  
  // Alternatively, use writeHead to set status and headers at once
  // res.writeHead(200, {
  //   'Content-Type': 'application/json',
  //   'X-Custom-Header': 'CustomValue'
  // });
  
  // Write response body (can be called multiple times)
  res.write('{"message": ');
  
  // End response with optional final data
  res.end('"Hello, World!"}');
}).listen(3000);
```
Key response methods:
- `res.statusCode`: Sets the HTTP status code
- `res.setHeader(name, value)`: Sets a response header
- `res.writeHead(statusCode, headers)`: Writes the status code and headers
- `res.write(data)`: Writes a chunk of the response body
- `res.end([data])`: Signals that all response headers and body have been sent

## Question 40
*Reference: [Question 40](node-questions.md#question-40)*

### Q. Explain how to handle different HTTP methods (GET, POST, etc.) in a Node.js server.

You can handle different HTTP methods in a Node.js server by checking the req.method property and implementing method-specific logic:
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  const url = req.url;
  
  // Set default response headers
  res.setHeader('Content-Type', 'application/json');
  
  // Handle different HTTP methods
  switch(req.method) {
    case 'GET':
      if (url === '/api/users') {
        // Handle GET request to /api/users
        res.statusCode = 200;
        res.end(JSON.stringify({ users: ['John', 'Jane', 'Bob'] }));
      } else if (url.match(/\/api\/users\/\d+/)) {
        // Handle GET request to /api/users/:id
        const id = url.split('/').pop();
        res.statusCode = 200;
        res.end(JSON.stringify({ id, name: `User ${id}` }));
      } else {
        // Handle 404 for unknown GET routes
        res.statusCode = 404;
        res.end(JSON.stringify({ error: 'Not Found' }));
      }
      break;
      
    case 'POST':
      if (url === '/api/users') {
        // Handle POST request to /api/users
        let body = '';
        
        req.on('data', (chunk) => {
          body += chunk.toString();
        });
        
        req.on('end', () => {
          try {
            const userData = JSON.parse(body);
            // Process user data (e.g., save to database)
            res.statusCode = 201;
            res.end(JSON.stringify({ 
              message: 'User created successfully',
              user: userData 
            }));
          } catch (error) {
            res.statusCode = 400;
            res.end(JSON.stringify({ error: 'Invalid JSON' }));
          }
        });
      } else {
        // Handle 404 for unknown POST routes
        res.statusCode = 404;
        res.end(JSON.stringify({ error: 'Not Found' }));
      }
      break;
      
    case 'PUT':
      if (url.match(/\/api\/users\/\d+/)) {
        // Handle PUT request to /api/users/:id
        const id = url.split('/').pop();
        let body = '';
        
        req.on('data', (chunk) => {
          body += chunk.toString();
        });
        
        req.on('end', () => {
          try {
            const userData = JSON.parse(body);
            // Update user (e.g., in database)
            res.statusCode = 200;
            res.end(JSON.stringify({ 
              message: `User ${id} updated`,
              user: userData 
            }));
          } catch (error) {
            res.statusCode = 400;
            res.end(JSON.stringify({ error: 'Invalid JSON' }));
          }
        });
      } else {
        res.statusCode = 404;
        res.end(JSON.stringify({ error: 'Not Found' }));
      }
      break;
      
    case 'DELETE':
      if (url.match(/\/api\/users\/\d+/)) {
        // Handle DELETE request to /api/users/:id
        const id = url.split('/').pop();
        // Delete user (e.g., from database)
        res.statusCode = 200;
        res.end(JSON.stringify({ message: `User ${id} deleted` }));
      } else {
        res.statusCode = 404;
        res.end(JSON.stringify({ error: 'Not Found' }));
      }
      break;
      
    default:
      // Handle unsupported methods
      res.statusCode = 405;
      res.setHeader('Allow', 'GET, POST, PUT, DELETE');
      res.end(JSON.stringify({ error: 'Method Not Allowed' }));
  }
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```

## Solution 41
*Reference: [Solution 41](node-questions.md#solution-41)*

### Q. What is middleware in the context of Node.js servers?

Middleware in Node.js server context refers to functions that have access to the request object, the response object, and the next middleware function in the application's request-response cycle. Middleware functions can -
1. Execute any code.
2. Modify the request and response objects.
3. End the request-response cycle.
4. Call the next middleware in the stack.

While Express.js made middleware popular, you can implement middleware pattern in vanilla Node.js as well.
```javascript
const http = require('http');

// Middleware functions
const loggerMiddleware = (req, res, next) => {
  console.log(`${new Date().toISOString()} - ${req.method} ${req.url}`);
  next(); // Call the next middleware
};

const authMiddleware = (req, res, next) => {
  const authHeader = req.headers.authorization;
  
  if (!authHeader || authHeader !== 'Bearer valid-token') {
    res.statusCode = 401;
    res.end(JSON.stringify({ error: 'Unauthorized' }));
    return; // Stop the middleware chain
  }
  
  // Add user info to request
  req.user = { id: 1, name: 'Authenticated User' };
  next();
};

// Create middleware stack
const createStack = (...middlewares) => {
  return (req, res) => {
    function executeMiddleware(i) {
      if (i < middlewares.length) {
        middlewares[i](req, res, () => executeMiddleware(i + 1));
      }
    }
    executeMiddleware(0);
  };
};

// Main request handler (final middleware)
const requestHandler = (req, res) => {
  res.setHeader('Content-Type', 'application/json');
  
  if (req.url === '/api/private') {
    res.statusCode = 200;
    res.end(JSON.stringify({ 
      message: 'Private data', 
      user: req.user 
    }));
  } else {
    res.statusCode = 200;
    res.end(JSON.stringify({ message: 'Public endpoint' }));
  }
};

// Conditional middleware stacks
const server = http.createServer((req, res) => {
  if (req.url.startsWith('/api/private')) {
    // Protected routes use all middleware
    createStack(loggerMiddleware, authMiddleware, requestHandler)(req, res);
  } else {
    // Public routes only use logger middleware
    createStack(loggerMiddleware, requestHandler)(req, res);
  }
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```
Common uses of middleware include:
- Logging requests
- Authentication/authorization
- CORS handling (as seen in your long-term memories from around August 31, 2025)
- Body parsing
- Error handling
- Response compression


## Question 42
*Reference: [Question 42](node-questions.md#question-42)*

### Q. How do you parse query parameters and body data in HTTP requests?

Query parameters appear in the URL after a question mark (?) and can be parsed using the built-in url module
```javascript
const http = require('http');
const url = require('url');

const server = http.createServer((req, res) => {
  // Parse the URL and query parameters
  const parsedUrl = url.parse(req.url, true);
  const pathname = parsedUrl.pathname;
  const queryParams = parsedUrl.query;
  
  res.setHeader('Content-Type', 'application/json');
  
  if (pathname === '/api/search') {
    // Access query parameters
    const term = queryParams.term || '';
    const limit = parseInt(queryParams.limit) || 10;
    const page = parseInt(queryParams.page) || 1;
    
    res.statusCode = 200;
    res.end(JSON.stringify({
      search: {
        term,
        limit,
        page
      },
      results: [`Results for "${term}" (page ${page}, limit ${limit})`]
    }));
  } else {
    res.statusCode = 404;
    res.end(JSON.stringify({ error: 'Not Found' }));
  }
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```
For a URL like `/api/search?term=nodejs&limit=5&page=2`, this will parse `term`, `limit`, and `page`.

**Parsing Body Data**

Parsing body data from POST/PUT requests requires reading the data in chunks -
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.method === 'POST' || req.method === 'PUT') {
    let body = '';
    
    // Handle data chunks
    req.on('data', (chunk) => {
      body += chunk.toString();
      
      // Limit body size to prevent attacks
      if (body.length > 1e6) {
        body = '';
        res.statusCode = 413; // Payload Too Large
        res.end(JSON.stringify({ error: 'Request body too large' }));
        req.connection.destroy();
      }
    });
    
    // Process completed body
    req.on('end', () => {
      res.setHeader('Content-Type', 'application/json');
      
      try {
        // For JSON data
        if (req.headers['content-type'] === 'application/json') {
          const jsonData = JSON.parse(body);
          res.statusCode = 200;
          res.end(JSON.stringify({ 
            message: 'JSON data received',
            data: jsonData
          }));
        } 
        // For form data
        else if (req.headers['content-type'] === 'application/x-www-form-urlencoded') {
          const formData = new URLSearchParams(body);
          const formObject = {};
          
          for (const [key, value] of formData.entries()) {
            formObject[key] = value;
          }
          
          res.statusCode = 200;
          res.end(JSON.stringify({ 
            message: 'Form data received',
            data: formObject
          }));
        }
        else {
          res.statusCode = 200;
          res.end(JSON.stringify({ 
            message: 'Raw data received',
            data: body
          }));
        }
      } catch (error) {
        res.statusCode = 400;
        res.end(JSON.stringify({ 
          error: 'Invalid data format',
          details: error.message
        }));
      }
    });
  } else {
    res.statusCode = 405;
    res.setHeader('Allow', 'POST, PUT');
    res.end(JSON.stringify({ error: 'Method Not Allowed' }));
  }
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```
This server can handle:
- JSON data with `Content-Type: application/json`
- Form data with `Content-Type: application/x-www-form-urlencoded`
- Raw text/binary data with other content types
For more complex applications, it's common to use libraries like body-parser (or built-in middleware in Express.js) to handle parsing of different content types more elegantly.


# Express.js

## Solution 43
*Reference: [Solution 43](node-questions.md#solution-43)*

### Q. What is Express.js, and why is it commonly used with Node.js?

Express.js is a minimal, unopinionated web application framework for Node.js designed to make building web applications and APIs simpler and more organized. It provides a robust set of features for web and mobile applications without obscuring Node.js's core functionality.

**Key features of Express.js:**
- **Middleware architecture**: Allows for processing requests through a series of functions.
- **Routing system**: Simplifies directing HTTP requests to appropriate handlers.
- **Template engine integration**: Supports various view engines like Pug, EJS, and Handlebars.
- **Error handling**: Provides built-in error handling mechanisms.
- **HTTP utility methods**: Simplifies sending various HTTP responses.

**Why Express.js is commonly used with Node.js:**
1. **Simplicity**: Express provides a thin layer of fundamental web application features without obscuring Node's features.
2. **Middleware ecosystem**: The middleware pattern allows for easy integration of additional functionalities (authentication, logging, CORS, etc.).
3. **Performance**: Being lightweight, Express adds minimal overhead to Node.js applications.
4. **Flexibility**: Unlike opinionated frameworks, Express allows developers to structure applications as they see fit.
5. **Community support**: Express has a large community, extensive documentation, and numerous plugins.
6. **Industry adoption**: Many major companies use Express in production, making it a battle-tested solution.

Express.js strikes a perfect balance between providing essential structure and allowing developer freedom, making it the most popular web framework for Node.js applications.

## Solution 44
*Reference: [Solution 44](node-questions.md#solution-44)*

### Q. How do you set up a basic Express server?

Setting up a basic Express server involves a few straightforward steps:

**Step 1: Initialize your project and install Express**
```bash
mkdir my-express-app
cd my-express-app
npm init -y
npm install express
```
**Step 2: Create a server file (e.g., app.js or server.js)**
```javascript
// Import the express module
const express = require('express');

// Create an Express application
const app = express();

// Define a port
const PORT = process.env.PORT || 3000;

// Create a simple route
app.get('/', (req, res) => {
  res.send('Hello World! Welcome to my Express server.');
});

// Start the server
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```
**Step 3: Run your server**
```bash
node app.js
```
**More complete example with additional common setup:**
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Middleware for parsing JSON and URL-encoded data
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Middleware for logging requests
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url} at ${new Date().toISOString()}`);
  next();
});

// Basic routes
app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.get('/api/users', (req, res) => {
  res.json([
    { id: 1, name: 'John Doe' },
    { id: 2, name: 'Jane Smith' }
  ]);
});

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});

// Start the server
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

## Solution 45
*Reference: [Solution 45](node-questions.md#solution-45)*

### Q. Explain routing in Express with examples.

Routing in Express refers to determining how an application responds to client requests to specific endpoints, which consist of a URI (path) and a specific HTTP request method (GET, POST, PUT, DELETE, etc.). Routing is one of Express's core features that makes building web applications and APIs straightforward.
**Basic Route Structure:**
```javascript
app.METHOD(PATH, HANDLER);
```
- `app` is an instance of Express
- `METHOD` is an HTTP request method (lowercase)
- `PATH` is the route path on the server
- `HANDLER` is the function executed when the route is matched

**Basic Routing Examples:**
```javascript
const express = require('express');
const app = express();

// Basic GET route
app.get('/', (req, res) => {
  res.send('Home Page');
});

// Route for about page
app.get('/about', (req, res) => {
  res.send('About Us Page');
});

// POST route for form submission
app.post('/submit-form', (req, res) => {
  res.send('Form submitted successfully!');
});

// PUT route for updating a resource
app.put('/users/:id', (req, res) => {
  res.send(`User ${req.params.id} updated`);
});

// DELETE route for removing a resource
app.delete('/users/:id', (req, res) => {
  res.send(`User ${req.params.id} deleted`);
});

// Handle 404 - Route not found
app.use((req, res) => {
  res.status(404).send('Page not found');
});
```

**Route Handlers:**
Route handlers can be a single function, a series of functions, or an array of functions:
```javascript
// Single handler
app.get('/example1', (req, res) => {
  res.send('Example with single handler');
});

// Multiple handlers as middleware
app.get('/example2', 
  (req, res, next) => {
    console.log('First handler');
    req.user = { id: 1, name: 'John' };
    next();
  },
  (req, res) => {
    res.send(`Example with user: ${req.user.name}`);
  }
);

// Array of handlers
const validateUser = (req, res, next) => {
  // Validation logic
  if (req.query.userId) {
    next();
  } else {
    res.status(400).send('User ID required');
  }
};

const getUser = (req, res, next) => {
  // Get user data
  req.userData = { id: req.query.userId, name: 'Sample User' };
  next();
};

app.get('/user', [validateUser, getUser], (req, res) => {
  res.json(req.userData);
});
```
**Route Groups using Express Router:**
For larger applications, you can organize routes using Express Router:
```javascript
// users.js
const express = require('express');
const router = express.Router();

// All routes here are prefixed with /users
router.get('/', (req, res) => {
  res.send('Get all users');
});

router.get('/:id', (req, res) => {
  res.send(`Get user with ID ${req.params.id}`);
});

router.post('/', (req, res) => {
  res.send('Create new user');
});

module.exports = router;

// app.js
const usersRouter = require('./users');
app.use('/users', usersRouter);
```
Routing is the foundation of creating RESTful APIs and web applications in Express, allowing you to organize your application's endpoints in a clean, modular fashion.

## Solution 46
*Reference: [Solution 46](node-questions.md#solution-46)*

### Q. What are route parameters and query parameters in Express?

Route parameters and query parameters are two important ways to pass data to an Express.js server, each serving different purposes in API and web application design.
### Route Parameters
Route parameters are named URL segments used to capture values at specific positions in the URL. They are defined by prefixing a colon to the parameter name in the route path.

**Key characteristics:**
- Part of the route path definition.
- Essential for RESTful resource identification.
- Accessed via `req.params` object.
- Typically used for identifying specific resources.

**Examples:**
```javascript
const express = require('express');
const app = express();

// Route with a single parameter
app.get('/users/:userId', (req, res) => {
  res.send(`Fetching user with ID: ${req.params.userId}`);
});

// Route with multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.send(`Fetching post ${postId} by user ${userId}`);
});

// Optional parameters using ?
app.get('/products/:category/:id?', (req, res) => {
  const { category, id } = req.params;
  if (id) {
    res.send(`Fetching product ${id} in category ${category}`);
  } else {
    res.send(`Fetching all products in category ${category}`);
  }
});

// Parameter with specific pattern (regex)
app.get('/files/:filename(\\d+)', (req, res) => {
  // Only matches if filename consists of digits
  res.send(`Fetching file: ${req.params.filename}`);
});
```
**Query Parameters**
Query parameters are key-value pairs appended to the URL after a question mark, used for filtering, sorting, pagination, and other optional parameters.

**Key characteristics:**
- Appended to the URL after `?` with format `?key1=value1&key2=value2`.
- Optional and don't affect route matching.
- Accessed via `req.query` object.
- Typically used for filtering, sorting, or optional configurations.

**Examples:**
```javascript
// Route handling query parameters for filtering and pagination
app.get('/products', (req, res) => {
  const { category, minPrice, maxPrice, sort, page, limit } = req.query;
  
  let response = 'Fetching products';
  
  // Building response based on query parameters
  if (category) {
    response += ` in category: ${category}`;
  }
  
  if (minPrice || maxPrice) {
    response += ` with price range: ${minPrice || '0'} to ${maxPrice || 'unlimited'}`;
  }
  
  if (sort) {
    response += ` sorted by: ${sort}`;
  }
  
  if (page && limit) {
    response += ` (page ${page}, ${limit} items per page)`;
  }
  
  res.send(response);
});

// Search functionality using query parameters
app.get('/search', (req, res) => {
  const { q, type } = req.query;
  res.send(`Searching for "${q}" in category: ${type || 'all'}`);
});
```
**Key Differences**

1. **Position in URL**:
  - Route parameters: Part of the URL path (`/users/123`)
  - Query parameters: After the `?` in the URL (`/users?id=123`)
2. **Requirement**:
  - Route parameters: Usually required (unless made optional with `?`)
  - Query parameters: Always optional
3. **Use case**:
  - Route parameters: Identifying specific resources (RESTful approach)
  - Query parameters: Filtering, sorting, pagination, and optional configuration
4. **Route matching**:
  - Route parameters: Affect which route handler is matched
  - Query parameters: Don't affect route matching


## Solution 47
*Reference: [Solution 47](node-questions.md#solution-47)*

### Q. How do you handle static files in Express?

Handling static files (like CSS, JavaScript, images) in Express is accomplished using the built-in express.static middleware. This middleware allows you to serve static files directly from specified directories without having to create individual routes for each file.

**Basic Static File Serving**
```javascript
const express = require('express');
const path = require('path');
const app = express();

// Serve static files from the 'public' directory
app.use(express.static('public'));

// Now files in the 'public' directory are accessible at the root URL
// Example: If you have public/styles/main.css, it's accessible at http://localhost:3000/styles/main.css
```
**Advanced Static File Configuration**
**1. Multiple Static Directories:**
```javascript
// Serve static files from multiple directories
app.use(express.static('public'));
app.use(express.static('assets'));
app.use(express.static('uploads'));

// Express looks for files in directories in the order they are defined
// If a file isn't found in 'public', it looks in 'assets', then 'uploads'
```
**2. Virtual Path Prefix:**
```javascript
// Add a virtual path prefix to static files
app.use('/static', express.static('public'));

// Now a file at public/css/style.css is accessible at http://localhost:3000/static/css/style.css
```
**3. Absolute Paths (Recommended for Production):**
```javascript
// Use absolute paths to avoid confusion
app.use(express.static(path.join(__dirname, 'public')));

// With virtual path
app.use('/assets', express.static(path.join(__dirname, 'public/assets')));
```
**4. Static File Options:**
```javascript
app.use(express.static('public', {
  dotfiles: 'ignore',     // Ignore dotfiles (default)
  etag: true,             // Enable etag generation (default)
  extensions: ['html'],   // Try these extensions if no extension in URL
  index: 'index.html',    // Default file to serve for directories
  lastModified: true,     // Set Last-Modified header (default)
  maxAge: '1d',           // Cache control max age: 1 day (in milliseconds)
  setHeaders: (res, path, stat) => {
    // Custom header setting function
    res.set('x-timestamp', Date.now());
  }
}));
```

**Complete Example with HTML Template**
```javascript
const express = require('express');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

// Serve static files from 'public' directory
app.use(express.static(path.join(__dirname, 'public')));

// Set up a virtual path for assets
app.use('/assets', express.static(path.join(__dirname, 'assets')));

// Set up a special path for user uploads with longer cache time
app.use('/uploads', express.static(path.join(__dirname, 'uploads'), {
  maxAge: '1d'
}));

// Serve index.html for the root route
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'views', 'index.html'));
});

// Error handler for static files
app.use((err, req, res, next) => {
  console.error(err);
  res.status(500).send('Error loading static resources');
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Best Practices for Static Files**
1. **Security considerations:**
  - Never serve directories containing sensitive information
  - Use helmet.js to set appropriate security headers
  - Consider rate limiting for public assets
2. **Performance optimization:**
  - Set appropriate cache headers using the maxAge option
  - Consider using a CDN for production applications
  - Compress static files using middleware like compression
3. **Organization:**
  - Keep static files in separate directories based on type (css, js, images)
  - Use virtual paths that make the resource type clear
4. **Fallbacks:**
  - For SPAs, configure your server to serve index.html for routes not found
```javascript
// For a Single Page Application, serve index.html for all non-file routes
app.use(express.static('public'));

// Handle any routes not matched by static files or API routes
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});
```

## Solution 48
*Reference: [Solution 48](node-questions.md#solution-48)*

### Q. What is the purpose of app.use() in Express?

`app.use()` is a method in Express.js that mounts middleware functions at a specified path. It's one of the most important methods in Express as it enables the core middleware functionality that makes Express so powerful and flexible.

**Key purposes of app.use():**
1. **Mounting middleware**: It adds middleware functions to the Express application's request-response cycle.
```javascript
// Example: Adding a simple logging middleware
app.use((req, res, next) => {
  console.log(`${new Date().toISOString()} - ${req.method} ${req.url}`);
  next();
});
```
2. **Path-specific middleware**: When provided with a path parameter, the middleware only executes for requests matching that path.
```javascript
// This middleware only runs for requests to the /api path or its subpaths
app.use('/api', (req, res, next) => {
  console.log('API request received');
  next();
});
```
3. **Mounting routers**: It can be used to mount entire router instances at specific paths.
```javascript
const userRouter = express.Router();
userRouter.get('/', userController.getAllUsers);
userRouter.post('/', userController.createUser);

// Mount the router at /users
app.use('/users', userRouter);
```
4. **Serving static files**: It's used with the built-in `express.static` middleware to serve static assets.
```javascript
// Serve static files from the 'public' directory
app.use(express.static('public'));
```
5. **Adding built-in or third-party middleware**: It integrates middleware like body parsers, cookie parsers, etc.
```javascript
// Parse JSON request bodies
app.use(express.json());
// Parse URL-encoded form data
app.use(express.urlencoded({ extended: true }));
```
The power of app.use() lies in its flexibility and the way it enables the middleware architecture that makes Express so extensible.


## Solution 49
*Reference: [Solution 49](node-questions.md#solution-49)*

### Q. How do you implement error handling middleware in Express?

Error handling middleware in Express is a special type of middleware function that takes four parameters instead of three: (err, req, res, next). Express recognizes this pattern by the presence of four arguments and treats it as error-handling middleware.
**Implementing error handling middleware:**
```javascript
// Basic error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```
**A more comprehensive error handling implementation:**
```javascript
// Define custom error types
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
    this.statusCode = 400;
  }
}

class NotFoundError extends Error {
  constructor(message) {
    super(message);
    this.name = 'NotFoundError';
    this.statusCode = 404;
  }
}

// Normal route that might throw an error
app.get('/users/:id', (req, res, next) => {
  const id = req.params.id;
  
  // Validation check
  if (!id.match(/^\d+$/)) {
    return next(new ValidationError('User ID must be numeric'));
  }
  
  // Resource not found
  if (id === '999') {
    return next(new NotFoundError('User not found'));
  }
  
  // Unexpected error
  if (id === '500') {
    throw new Error('Internal server error example');
  }
  
  res.send(`User ${id} details`);
});

// Handle 404 errors for routes not found
app.use((req, res, next) => {
  next(new NotFoundError('Resource not found'));
});

// Comprehensive error handler
app.use((err, req, res, next) => {
  // Log the error for debugging
  console.error(`${new Date().toISOString()} - Error:`, {
    name: err.name,
    message: err.message,
    stack: process.env.NODE_ENV === 'development' ? err.stack : undefined
  });
  
  // Set appropriate status code
  const statusCode = err.statusCode || 500;
  
  // Prepare error response
  const errorResponse = {
    error: {
      name: err.name,
      message: err.message,
      // Only include stack trace in development
      ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
    },
    // Add request ID for tracking if available
    requestId: req.id
  };
  
  // Send error response
  res.status(statusCode).json(errorResponse);
});
```
**Key best practices for error handling in Express:**
1. **Error handling middleware should be defined last**, after all other middleware and routes.
2. **Use try/catch in async route handlers** or use a wrapper like `express-async-errors`.
3. **Differentiate between operational errors and programming errors** - handle operational errors gracefully, but let programming errors crash the process.
4. **Use custom error classes** to standardize error handling across your application.
5. **Always log errors** for debugging purposes.

## Solution 50
*Reference: [Solution 50](node-questions.md#solution-50)*

### Q. Explain how to use template engines like EJS or Pug with Express.

Template engines allow you to generate HTML dynamically by embedding server-side code directly into your templates. Express.js makes it easy to integrate with various template engines like EJS, Pug (formerly Jade), Handlebars, and more.

**Setting up a template engine with Express:**
1. **Install the template engine:**
```bash
# For EJS
npm install ejs

# For Pug
npm install pug
```
2. **Configure the template engine in your Express app:**
```javascript
const express = require('express');
const app = express();
const path = require('path');

// Set the view engine (EJS or Pug)
app.set('view engine', 'ejs'); // or 'pug'

// Set the directory where your template files are located
app.set('views', path.join(__dirname, 'views'));
```
3. **Create template files:**
For EJS (views/index.ejs):
```html
<!DOCTYPE html>
<html>
<head>
  <title><%= title %></title>
</head>
<body>
  <h1><%= heading %></h1>
  <ul>
    <% users.forEach(function(user) { %>
      <li><%= user.name %> - <%= user.email %></li>
    <% }); %>
  </ul>
</body>
</html>
```
For Pug (views/index.pug):
```pug
doctype html
html
  head
    title= title
  body
    h1= heading
    ul
      each user in users
        li #{user.name} - #{user.email}
```
4. **Render templates in your routes:**
```javascript
app.get('/', (req, res) => {
  // Render the template with data
  res.render('index', {
    title: 'User List',
    heading: 'Our Users',
    users: [
      { name: 'John Doe', email: 'john@example.com' },
      { name: 'Jane Smith', email: 'jane@example.com' }
    ]
  });
});
```
**Template engine features:**
5. **Layouts and partials** - Most template engines support layout templates and partial views for code reuse.
For EJS partials:
```html
<!-- views/partials/header.ejs -->
<!DOCTYPE html>
<html>
<head>
  <title><%= title %></title>
</head>
<body>
  <header>
    <nav><!-- Navigation items --></nav>
  </header>

<!-- In your main template -->
<%- include('partials/header') %>
<main>
  <!-- Page content -->
</main>
<%- include('partials/footer') %>
```
For Pug layouts:
```pug
// views/layout.pug
doctype html
html
  head
    title= title
    block styles
  body
    include partials/header
    block content
    include partials/footer

// views/home.pug
extends layout

block styles
  link(rel='stylesheet', href='/css/home.css')

block content
  h1 Welcome to our site
  p This is the home page
```

6. **Conditional rendering and loops:**
```javascript
// EJS conditionals
<% if (user.isAdmin) { %>
  <div class="admin-panel"><!-- Admin content --></div>
<% } else { %>
  <div class="user-panel"><!-- User content --></div>
<% } %>

// Pug conditionals
if user.isAdmin
  .admin-panel
    //- Admin content
else
  .user-panel
    //- User content
```
**Performance considerations:**
Template engines add some processing overhead, so for high-performance applications, consider:
2. Template caching (enabled by default in production)
3. Precompiling templates during build
4. For API-only applications, consider not using template engines at all


# Asynchronous Programming

## Solution 51
*Reference: [Solution 51](node-questions.md#solution-51)*

### Q. How do callbacks work in Node.js, and what is callback hell?

***Callbacks in Node.js***
In Node.js, callbacks are functions passed as arguments to other functions that will be executed later when an operation completes. Node.js uses an event-driven, non-blocking I/O model, and callbacks are fundamental to this architecture.
```javascript
// Example of a Node.js callback
const fs = require('fs');

fs.readFile('/path/to/file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log('File content:', data);
});

console.log('This runs before file content is displayed');
```
Node.js callbacks typically follow the "error-first callback" pattern, where:
- The first parameter is reserved for an error object
- If the operation was successful, the first parameter will be null or undefined
- Subsequent parameters contain the operation's result(s)

**Callback Hell**
Callback hell (also known as "pyramid of doom") refers to the situation where callbacks are nested within callbacks, creating deeply indented code that becomes difficult to read, maintain, and debug.
```javascript
// Callback hell example
fs.readFile('config.json', 'utf8', (err, configData) => {
  if (err) return console.error('Error reading config:', err);
  
  const config = JSON.parse(configData);
  fs.readFile(config.userDataFile, 'utf8', (err, userData) => {
    if (err) return console.error('Error reading user data:', err);
    
    const user = JSON.parse(userData);
    fs.readFile(user.profilePicture, (err, imageData) => {
      if (err) return console.error('Error reading profile picture:', err);
      
      processImageData(imageData, (err, processedImage) => {
        if (err) return console.error('Error processing image:', err);
        
        saveProcessedImage(processedImage, (err, savedImage) => {
          if (err) return console.error('Error saving image:', err);
          
          console.log('Everything completed successfully!');
        });
      });
    });
  });
});
```
This example demonstrates how callback-based code quickly becomes unwieldy as complexity increases. Each level of nesting makes the code harder to understand and introduces potential for errors in error handling logic.

### Solutions to Callback Hell
1. **Modularize code**: Break nested callbacks into named functions
2. **Use Promises**: Convert callback-based APIs to Promise-based
3. **Use async/await**: Further simplify Promise-based code
4. **Use control flow libraries**: Like the async module

## Solution 52
*Reference: [Solution 52](node-questions.md#solution-52)*

### Q. What are Promises in Node.js, and how do they help with async code?

Promises are objects representing the eventual completion or failure of an asynchronous operation. They provide a cleaner alternative to callbacks for handling asynchronous operations.

**Promise States**
A Promise can be in one of three states:
- **Pending**: Initial state, neither fulfilled nor rejected
- **Fulfilled**: The operation completed successfully
- **Rejected**: The operation failed
```javascript
// Creating a Promise
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  const success = true;
  if (success) {
    resolve('Operation succeeded');  // fulfilled state
  } else {
    reject(new Error('Operation failed'));  // rejected state
  }
});

// Consuming a Promise
myPromise
  .then(result => {
    console.log(result);  // 'Operation succeeded'
  })
  .catch(error => {
    console.error(error);
  });
```
**How Promises Help with Async Code**
1. **Chainable operations**: Promises can be chained using `.then()`, making sequential async operations cleaner
2. **Centralized error handling**: Using `.catch()` for all errors in a chain
3. **Avoiding deeply nested code**: Flattening the "pyramid of doom"
4. **Composition**: Combining promises with methods like `Promise.all()` and `Promise.race()`
Example of Promise chaining vs callback hell:
```javascript
// Using Promises to avoid callback hell
fs.promises.readFile('config.json', 'utf8')
  .then(configData => {
    const config = JSON.parse(configData);
    return fs.promises.readFile(config.userDataFile, 'utf8');
  })
  .then(userData => {
    const user = JSON.parse(userData);
    return fs.promises.readFile(user.profilePicture);
  })
  .then(imageData => {
    return processImageData(imageData);
  })
  .then(processedImage => {
    return saveProcessedImage(processedImage);
  })
  .then(() => {
    console.log('Everything completed successfully!');
  })
  .catch(err => {
    console.error('An error occurred:', err);
  });
```
**Promise Composition**
```javascript
// Promise.all - wait for all promises to resolve
const promise1 = fetchUserProfile();
const promise2 = fetchUserPosts();
const promise3 = fetchUserFriends();

Promise.all([promise1, promise2, promise3])
  .then(([profile, posts, friends]) => {
    // All data is available here
    console.log(profile, posts, friends);
  })
  .catch(error => {
    // If any promise rejects, this will execute
    console.error(error);
  });

// Promise.race - get result of first resolved promise
const cachePromise = checkCache('user-123');
const dbPromise = queryDatabase('user-123');

Promise.race([cachePromise, dbPromise])
  .then(userData => {
    // First result (either from cache or DB)
    displayUserData(userData);
  });
```

## Solution 53
*Reference: [Solution 53](node-questions.md#solution-53)*

### Q. Explain async/await in Node.js with an example.

sync/await is a syntactic feature introduced in Node.js 7.6+ (based on ES2017) that makes asynchronous code look and behave more like synchronous code. It's built on top of Promises and makes async code even more readable and maintainable.

**Key Concepts**
- **async function**: A function declared with the `async` keyword, which returns a Promise implicitly.
- **await operator**: Used inside async functions to wait for a Promise to settle before continuing execution.

```javascript
// Basic async/await example
async function getUserData() {
  try {
    // await pauses execution until the promise resolves
    const response = await fetch('https://api.example.com/users/1');
    
    // This line only executes after the fetch completes
    const userData = await response.json();
    
    return userData;  // Automatically wrapped in a Promise
  } catch (error) {
    console.error('Error fetching user data:', error);
    throw error;  // Re-throwing maintains the Promise rejection chain
  }
}

// Using the async function
getUserData()
  .then(data => console.log(data))
  .catch(err => console.error(err));

// Or with another async function
async function displayUserInfo() {
  try {
    const userData = await getUserData();
    console.log(`User: ${userData.name}`);
  } catch (error) {
    console.error('Failed to display user info:', error);
  }
}
```

## Solution 54
*Reference: [Solution 54](node-questions.md#solution-54)*

### Q. How do you promisify a callback-based function?

Promisification is the process of converting callback-based functions to return Promises. This allows you to use modern async/await syntax with older callback-based APIs.

**Manual Promisification**
```javascript
// Original callback-based function
function readFileCallback(path, options, callback) {
  fs.readFile(path, options, callback);
}

// Manual promisification
function readFilePromise(path, options) {
  return new Promise((resolve, reject) => {
    fs.readFile(path, options, (err, data) => {
      if (err) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
}

// Usage
readFilePromise('config.json', 'utf8')
  .then(data => console.log(data))
  .catch(err => console.error(err));
```
**Using util.promisify (Node.js built-in)**
Node.js provides a built-in utility for promisification:
```javascript
const util = require('util');
const fs = require('fs');

// Convert the callback-based function to return a promise
const readFile = util.promisify(fs.readFile);

// Now use it with async/await
async function readConfig() {
  try {
    const data = await readFile('config.json', 'utf8');
    return JSON.parse(data);
  } catch (error) {
    console.error('Error reading config:', error);
    throw error;
  }
}
```
**Creating a Generic Promisify Function**
If you need to support older Node.js versions without `util.promisify`.
```javascript
function promisify(fn) {
  return function(...args) {
    return new Promise((resolve, reject) => {
      fn(...args, (err, result) => {
        if (err) {
          reject(err);
        } else {
          resolve(result);
        }
      });
    });
  };
}

// Usage
const readFile = promisify(fs.readFile);
```
**Promisifying Methods with Context**
When promisifying methods that need to preserve this context
```javascript
function promisifyMethod(obj, methodName) {
  const originalMethod = obj[methodName];
  
  obj[methodName + 'Async'] = function(...args) {
    return new Promise((resolve, reject) => {
      originalMethod.call(this, ...args, (err, result) => {
        if (err) {
          reject(err);
        } else {
          resolve(result);
        }
      });
    });
  };
}

// Example with a database client
promisifyMethod(dbClient, 'query');
// Now you can use dbClient.queryAsync()
```

## Solution 55
*Reference: [Solution 55](node-questions.md#solution-55)*

### Q. What is the async module, and when might you use it?

The async module is a utility library that provides powerful functions for working with asynchronous JavaScript. While modern JavaScript features (Promises, async/await) have reduced the need for this module, it still offers valuable tools for managing complex asynchronous workflows.

**Key Features of the async Module**
1. **Flow control**: Managing the execution of asynchronous operations
2. **Collections**: Processing collections of items in parallel or series
3. **Utilities**: Helper functions for common async patterns

**Installation**
```bash
npm install async
```
**Common Use Cases and Examples**
**Series Execution (waterfall)**
Execute functions in sequence, passing results to the next function:
```javascript
const async = require('async');

async.waterfall([
  function(callback) {
    fetchUserData(userId, callback);
  },
  function(userData, callback) {
    fetchUserPosts(userData.postIds, callback);
  },
  function(posts, callback) {
    processPostData(posts, callback);
  }
], function(err, result) {
  if (err) {
    console.error('Error in waterfall:', err);
    return;
  }
  console.log('Final result:', result);
});
```
**Parallel Execution**
Execute functions in parallel and collect all results:
```javascript
async.parallel({
  profile: function(callback) {
    fetchUserProfile(userId, callback);
  },
  posts: function(callback) {
    fetchUserPosts(userId, callback);
  },
  friends: function(callback) {
    fetchUserFriends(userId, callback);
  }
}, function(err, results) {
  if (err) {
    console.error('Error in parallel execution:', err);
    return;
  }
  // results contains {profile: ..., posts: ..., friends: ...}
  displayDashboard(results);
});
```
**Processing Collections**
Process array items with controlled concurrency:
```javascript
// Process up to 5 items at once
async.mapLimit(largeArrayOfUrls, 5, function(url, callback) {
  fetchData(url, callback);
}, function(err, results) {
  if (err) {
    console.error('Error in mapLimit:', err);
    return;
  }
  console.log('All URLs processed:', results);
});
```
**Retry with Backoff**
Retry an operation with exponential backoff:
```javascript
async.retry({
  times: 5,
  interval: function(retryCount) {
    return 1000 * Math.pow(2, retryCount); // Exponential backoff
  }
}, function(callback) {
  // Operation that might fail
  unstableApiCall(data, callback);
}, function(err, result) {
  if (err) {
    console.error('Operation failed after multiple retries:', err);
    return;
  }
  console.log('Operation succeeded:', result);
});
```
**When to Use the async Module**
1. **Complex control flows**: Managing intricate sequences of async operations
2. **Throttling and concurrency control**: When you need to limit parallel operations
3. **Legacy codebases**: Working with callback-based code that hasn't been promisified
4. **Specialized patterns**: For retry logic, queuing, and other patterns not easily handled with Promises alone

**Modern Alternatives
For new projects, consid**er these alternatives:
- Native Promises with `Promise.all`, `Promise.race`, etc.
- Async/await with try/catch blocks
- Libraries like Bluebird for advanced Promise patterns