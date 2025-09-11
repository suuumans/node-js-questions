# Node.js Questions

# Node.js Basics

## Question 1
What is Node.js, and how does it differ from traditional server-side languages like PHP or Java?

## Question 2
What is the V8 engine, and what role does it play in Node.js?

## Question 3
Explain the single-threaded nature of Node.js and how it handles concurrency.

## Question 4
What is the difference between Node.js and browser JavaScript?

## Question 5
How do you check the version of Node.js installed on your system?

## Question 6
What is the REPL in Node.js, and how is it useful?

## Question 7
Explain the concept of non-blocking I/O in Node.js.

## Question 8
What are the core modules in Node.js? Name a few.

## Question 9
How does Node.js handle errors in synchronous vs asynchronous code?

## Question 10
What is the purpose of the process object in Node.js?

# Modules and NPM

## Question 11
What are modules in Node.js, and how do you create one?

## Question 12
Explain the difference between require() and import in Node.js.

## Question 13
What is CommonJS vs ES Modules in Node.js?

## Question 14
How does the module caching work in Node.js?

## Question 15
What is NPM, and how do you initialize a new project with it?

## Question 16
Explain package.json and its key fields.

## Question 17
What is the difference between dependencies and devDependencies in package.json?

## Question 18
How do you handle version conflicts in NPM?

## Question 19
What are semantic versioning (SemVer) rules in NPM?

## Question 20
20. How can you publish a package to NPM?

# File System

## Question 21
What is the fs module in Node.js, and how do you use it to read a file synchronously and asynchronously?

## Question 22
Explain the difference between fs.readFile() and fs.readFileSync().

## Question 23
How do you write to a file using the fs module?

## Question 24
What is fs.createReadStream() and when would you use it?

## Question 25
How do you handle file paths in a cross-platform way in Node.js?

## Question 26
Explain fs.watch() and its use cases.

# Events and Event Loop

## Question 27
What is the EventEmitter class in Node.js?

## Question 28
How do you create a custom event in Node.js?

## Question 29
Explain the phases of the Node.js event loop.

## Question 30
What are the differences between setImmediate(), setTimeout(), and process.nextTick()?

## Question 31
How does Node.js handle blocking operations?

## Question 32
What is libuv, and what does it provide to Node.js?

# Streams

## Question 33
What are streams in Node.js, and what types are there (Readable, Writable, Duplex, Transform)?

## Question 34
Provide an example of piping a readable stream to a writable stream.

## Question 35
How do you handle errors in streams?

## Question 36
What is backpressure in streams, and how is it managed?

## Question 37
Explain the difference between flowing mode and paused mode in readable streams.

# HTTP and Servers

## Question 38
How do you create a basic HTTP server in Node.js using the http module?

## Question 39
What is the request and response object in an HTTP server?

## Question 40
Explain how to handle different HTTP methods (GET, POST, etc.) in a Node.js server.

## Question 41
What is middleware in the context of Node.js servers?

## Question 42
How do you parse query parameters and body data in HTTP requests?

# Express.js

## Question 43
What is Express.js, and why is it commonly used with Node.js?

## Question 44
How do you set up a basic Express server?

## Question 45
Explain routing in Express with examples.

## Question 46
What are route parameters and query parameters in Express?

## Question 47
How do you handle static files in Express?

## Question 48
What is the purpose of app.use() in Express?

## Question 49
How do you implement error handling middleware in Express?

## Question 50
Explain how to use template engines like EJS or Pug with Express.

# Asynchronous Programming

## Question 51
How do callbacks work in Node.js, and what is callback hell?

## Question 52
What are Promises in Node.js, and how do they help with async code?

## Question 53
Explain async/await in Node.js with an example.

## Question 54
How do you promisify a callback-based function?

## Question 55
What is the async module, and when might you use it?

# Databases

## Question 56
How do you connect to a MongoDB database using Mongoose in Node.js?

## Question 57
What is the difference between MongoDB and SQL databases in a Node.js context?

## Question 58
Explain how to perform CRUD operations with MongoDB in Node.js.

## Question 59
How do you use the mysql or pg module to connect to a SQL database?

## Question 60
What are ORMs like Sequelize, and how do they simplify database interactions?

# Authentication and Security

## Question 61
How do you implement JWT authentication in a Node.js application?

## Question 62
What is bcrypt, and how is it used for password hashing?

## Question 63
Explain CORS and how to handle it in a Node.js server.

## Question 64
What are common security vulnerabilities in Node.js apps (e.g., XSS, CSRF) and how to mitigate them?

## Question 65
How do you use environment variables for secure configuration in Node.js?

## Question 66
What is helmet middleware, and what does it do?


# Error Handling and Debugging

## Question 67
67. How do you handle uncaught exceptions in Node.js?

## Question 68
68. What is the domain module, and is it still recommended?

## Question 69
69. Explain how to use try-catch with async/await.

## Question 70
70. What tools can you use for debugging Node.js applications (e.g., Node Inspector, VS Code debugger)?

## Question 71
71. How do you log errors effectively in a production Node.js app?


# Testing

## Question 72
72. What is Mocha, and how do you set up tests with it?

## Question 73
73. Explain the difference between unit tests and integration tests in Node.js.

## Question 74
74. How do you use Chai for assertions in tests?

## Question 75
75. What is Supertest for testing Express APIs?

## Question 76
76. How do you mock dependencies in Node.js tests using Sinon?


# Performance and Scaling

## Question 77
What is clustering in Node.js, and how does it improve performance?

## Question 78
Explain the pm2 process manager and its benefits.

## Question 79
How do you profile a Node.js application for performance issues?

## Question 80
What is load balancing in a Node.js context?

## Question 81
How can you optimize Node.js for handling high traffic?



# RESTful APIs and Advanced Topics

## Question 82
What makes an API RESTful, and how do you build one in Node.js?

## Question 83
Explain GraphQL vs REST in Node.js applications.

## Question 84
How do you implement WebSockets using Socket.io in Node.js?

## Question 85
What is serverless architecture, and how does Node.js fit in (e.g., AWS Lambda)?

## Question 86
How do you handle file uploads in Node.js using multer?

## Question 87
What are microservices, and how can Node.js be used to build them?


# Core Node.js Internals & OS Interaction

## Question 88
What are Buffers in Node.js? Why are they necessary when dealing with binary data, and how do they differ from plain JavaScript strings?

## Question 89
Explain the different types of child processes (spawn, exec, execFile, fork). When would you use each?

## Question 90
How does the fork() method specifically enable inter-process communication (IPC) between Node.js processes?

## Question 91
What is the purpose of the C++ bindings in the Node.js architecture?


# Advanced Networking & Data Handling

## Question 92
What is the difference between WebSockets, Server-Sent Events (SSE), and Long Polling? When would you choose one over the others?

## Question 93
What is gRPC? How does it compare to REST, and what are its potential benefits in a microservices architecture?

## Question 94
How would you create a basic TCP server in Node.js using the net module?

## Question 95
What is the difference between the http and http2 core modules? What are the main advantages of HTTP/2?