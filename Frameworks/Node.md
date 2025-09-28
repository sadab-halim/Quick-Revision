# Node.js

---

<details>
  <summary>01: Introduction to Node.js</summary>

### What is Node.js and Why Use It?

Node.js is a JavaScript runtime built on Chrome's V8 engine that allows developers to run JavaScript on the server side. It is not a framework or a programming language; it is an environment that executes JavaScript code outside of a web browser.

It is primarily used for building fast, scalable, and data-intensive network applications, such as:

* APIs (RESTful, GraphQL)
* Real-time applications (chat apps, online gaming)
* Microservices
* Streaming services
* Command-line tools


### Event-Driven, Non-Blocking I/O Model (IMP)

This is the core architectural principle of Node.js that enables its high performance and concurrency, even while being single-threaded.

* **Event-Driven**: Node.js operates on an event loop. Actions like a user making an HTTP request or a database query finishing trigger events. You write code (callbacks, Promises) that listens for and reacts to these events.
* **Non-Blocking I/O**: Instead of waiting for a long-running I/O operation (like reading a file or a network request) to complete, Node.js initiates the operation and then immediately moves on to execute the next line of code. When the I/O operation finishes, an event is emitted, and the corresponding callback function is placed in a queue to be executed by the event loop.

**Real-life Analogy (Restaurant Waiter):**
A traditional (blocking) waiter would take one customer's order, wait for the kitchen to cook it, serve it, and *only then* move to the next table. A Node.js (non-blocking) waiter takes an order, gives it to the kitchen, and immediately proceeds to the next table to take their order. When the kitchen finishes a dish, it rings a bell (emits an event), and the waiter serves the food to the correct table (executes the callback). This allows one waiter to handle many tables concurrently and efficiently.

**Common Pitfall**: Writing synchronous, CPU-intensive code (like complex calculations in a loop) will block the single main thread, making the entire application unresponsive.

### Single-Threaded Architecture Explained

Node.js runs your JavaScript code in a single main thread. This simplifies programming as you don't have to deal with the complexities of multithreading (like deadlocks or race conditions).

However, Node.js is not *purely* single-threaded. It uses the **Libuv** library to handle I/O operations asynchronously. Libuv manages a thread pool (typically 4 threads, but configurable) to offload heavy I/O tasks (like file system access or DNS lookups) from the main thread, preventing them from blocking it. Once a task is complete in the thread pool, its callback is pushed to the event loop's queue to be run on the main thread.

### V8 JavaScript Engine Basics

V8 is Google's open-source, high-performance JavaScript and WebAssembly engine, written in C++. It is the same engine that powers Google Chrome.

* **Function**: V8 takes your JavaScript code, compiles it into native machine code, and executes it.
* **Performance**: It uses advanced techniques like Just-In-Time (JIT) compilation, garbage collection, and various optimization strategies to make JavaScript execution incredibly fast, which is a key reason for Node.js's performance.


### Node.js vs. Browser JavaScript

While both environments run JavaScript using the V8 engine, their capabilities and execution contexts are very different.


| Feature | Node.js | Browser JavaScript |
| :-- | :-- | :-- |
| **Global Object** | `global`, `process` | `window`, `document` |
| **Purpose** | Server-side logic, backend services, file system access, networking. | Client-side logic, DOM manipulation, user interactions, browser events. |
| **APIs** | Provides APIs for `fs`, `http`, `os`, `path`, `child_process`, etc. | Provides Web APIs like `fetch`, `localStorage`, `console`, `setTimeout`. |
| **Module System** | Primarily CommonJS (`require`). ES Modules (`import`) supported. | ES Modules (`import/export`) is the standard. No built-in module system historically. |
| **Execution Environment** | Runs directly on the machine's OS. | Runs within a sandboxed browser environment with security restrictions. |



</details>

---

<details>
  <summary>02: Setting Up the Environment</summary>

### **Section 2: Setting Up the Environment**

### Installing Node.js (LTS vs Current)

When you visit the official Node.js download page, you'll see two main versions available: LTS and Current.[^3_1]

* **LTS (Long-Term Support):** This version is recommended for most users, especially for production environments. It prioritizes stability, security, and long-term maintenance. LTS versions receive critical bug fixes and security patches for an extended period (typically 30 months), ensuring a reliable foundation for your applications.[^3_2][^3_3]
* **Current:** This version includes the latest features and updates. It's great for experimenting with new functionalities but can be less stable and may introduce breaking changes. It's generally used for development purposes where you need access to cutting-edge features.[^3_4][^3_3]

**Best Practice**: Always use the **LTS** version for your projects unless you have a specific need for a feature only available in the Current version.[^3_3]

### Using Node Version Manager (nvm) (IMP)

Managing different Node.js versions for various projects can be challenging. `nvm` is a command-line tool that solves this by allowing you to easily install, manage, and switch between multiple Node.js versions on the same machine.[^3_5][^3_6]

**Why it's a Best Practice**:

* **Project Isolation**: Different projects might require different Node.js versions. `nvm` prevents version conflicts.
* **Easy Upgrades/Downgrades**: Switch between versions with a single command without needing to uninstall and reinstall Node.js globally.[^3_5]

**Common `nvm` Commands**:


| Command | Description |
| :-- | :-- |
| `nvm install <version>` | Install a specific version of Node.js (e.g., `nvm install 20.11.1`) [^3_5]. |
| `nvm install --lts` | Install the latest LTS version [^3_7]. |
| `nvm use <version>` | Switch to a specific version for your current terminal session (e.g., `nvm use 20.11.1`) [^3_8][^3_9]. |
| `nvm alias default <version>` | Set a default Node.js version for all new terminal sessions. |
| `nvm ls` | List all installed versions. |
| `nvm ls-remote` | List all available versions for installation [^3_5]. |

### REPL Basics

REPL stands for **Read-Eval-Print-Loop**. It's an interactive shell that you get by simply typing `node` in your terminal. It's excellent for quickly testing small JavaScript code snippets without creating a file.[^3_10][^3_11]

* **Read**: Reads the user's input.
* **Eval**: Evaluates the input code.
* **Print**: Prints the result of the evaluation.
* **Loop**: Waits for the next input.

**Handy REPL Features**:

* **Multi-line expressions**: The REPL automatically detects when you're writing a multi-line block, like a function or loop.[^3_10]
* **`_` (underscore) variable**: The `_` variable always holds the result of the last executed expression, which is useful for chaining operations.[^3_10]

```javascript
// Example in REPL
> const a = 5;
undefined
> a + 10;
15
> _ * 2 // Uses the last result (15)
30
```


### Understanding CommonJS \& ES Modules (IMP)

Node.js has two module systems for organizing and sharing code. Understanding them is critical.

* **CommonJS (CJS)**: The original, traditional module system in Node.js. It's synchronous and widely used in older codebases and many existing npm packages.[^3_12]
* **ES Modules (ESM)**: The standardized module system for JavaScript, introduced in ECMAScript 2015 (ES6). It's asynchronous and is the modern standard for both browser and server-side JavaScript.[^3_13]

**To use ES Modules in Node.js, you can either:**

1. Name your files with an `.mjs` extension.
2. Add `"type": "module"` to your `package.json` file.

**Comparison Table:**


| Feature | CommonJS (require) | ES Modules (import) |
| :-- | :-- | :-- |
| **Syntax** | `const myModule = require('./myModule');` | `import myModule from './myModule.js';` |
| **Loading** | **Synchronous** [^3_14][^3_12]. The event loop is blocked until the module is loaded. | **Asynchronous** [^3_14][^3_12]. Modules are parsed and loaded in parallel, which is more performant. |
| **Exporting** | `module.exports = { ... };` or `exports.fn = ...;` | `export default ...;` or `export const fn = ...;` |
| **Where it runs** | Native to Node.js. Requires bundlers for browsers. | Native to modern browsers and supported in Node.js. |
| **Tree Shaking** | Difficult, as exports are dynamic objects. | Easy for bundlers to perform (removes unused code). |
| **Best For** | Server-side development, especially in existing Node.js projects [^3_14]. | New projects, universal (isomorphic) code, and front-end development [^3_14][^3_13]. |

**Node.js Version Note**: While CommonJS remains the default in many cases, ES Module support has become stable and robust in recent Node.js LTS versions. For new projects, it's often recommended to start with ES Modules.[^3_15]


</details>

---

<details>
  <summary>03: Core Concepts</summary>

### **Section 3: Core Concepts**

### Event Loop in Node.js (IMP)

The event loop is the heart of Node.js. It's what allows Node.js to perform non-blocking I/O operations, making it highly concurrent despite running on a single thread.[^4_1][^4_2]

**Real-life Analogy (A Busy Chef):**
Imagine a chef in a kitchen.

* **Synchronous (Blocking):** The chef starts cooking a soup that takes 30 minutes. He stands there and watches it, doing nothing else until it's done. The entire kitchen's productivity halts.
* **Asynchronous (Event Loop):** The chef starts the soup, sets a 30-minute timer (registers an event), and immediately starts chopping vegetables for the next dish. When the timer rings (the event occurs), the chef takes the soup off the stove (executes the callback) and serves it. He handled multiple tasks "concurrently."

The event loop continuously checks for and processes events from a queue. It operates in a cycle of distinct phases.[^4_3][^4_1]

**Execution Order (IMP):**

1. **Synchronous Code:** All synchronous code in your script runs first.
2. **Microtasks:** After the synchronous code finishes, all queued *microtasks* are executed. This includes `process.nextTick()` callbacks and resolved `Promise` callbacks (`.then()`, `.catch()`, `.finally()`). `process.nextTick` has higher priority and runs before Promises.
3. **Macrotasks (Event Loop Phases):** Only after the microtask queue is empty does the event loop proceed to the main task queues (macrotasks), such as `setTimeout`, `setImmediate`, and I/O events.[^4_1]
```javascript
console.log('Start'); // 1. Sync

setTimeout(() => {
  console.log('Timeout'); // 4. Macrotask (Timer)
}, 0);

Promise.resolve().then(() => {
  console.log('Promise'); // 3. Microtask
});

console.log('End'); // 2. Sync

// Output: Start, End, Promise, Timeout
```


### Callbacks and Async Programming

A callback is a function passed as an argument to another function, which is then executed after an asynchronous operation has completed. This was the original pattern for handling async code in Node.js.[^4_4][^4_5]

**Error-First Convention (IMP):**
By convention, the first argument of a callback function is reserved for an error object. If the operation is successful, this argument is `null` or `undefined`.[^4_2]

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', 'utf8', (err, data) => {
  // Check for the error first
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  // If no error, process the data
  console.log('File content:', data);
});
```

**Common Pitfall**: "Callback Hell" or the "Pyramid of Doom" occurs when you nest multiple asynchronous callbacks, leading to code that is hard to read and maintain. Promises and `async/await` were introduced to solve this.

### Understanding the Libuv Library

Libuv is a multi-platform C library that is a critical part of Node.js. It provides the event loop and handles asynchronous I/O operations. While JavaScript is single-threaded, Libuv uses a pool of threads to run long-running tasks without blocking the main event loop.[^4_6][^4_7][^4_8]

**What Libuv Handles**:

* Asynchronous file and file system operations (`fs` module).[^4_7][^4_8]
* Asynchronous network operations (TCP/UDP sockets, DNS lookups).[^4_7]
* The event loop itself.[^4_7]
* The thread pool for heavy tasks.


### The Role of the Thread Pool

The thread pool is a set of threads managed by Libuv, used to offload operations that would otherwise block the event loop. By default, it has **4 threads**, but this can be configured using the `UV_THREADPOOL_SIZE` environment variable.[^4_9][^4_10][^4_6]

**Tasks that use the thread pool**:

* File I/O (most `fs` operations).
* CPU-intensive work like `crypto.pbkdf2()` (password hashing) and compression.[^4_9]
* Some DNS lookups (`dns.lookup()`).

**Important Distinction**: Not all async operations use the thread pool. Network I/O (like HTTP requests) is generally handled directly by the operating system's non-blocking mechanisms and does not use the thread pool.[^4_10]

### EventEmitter API

The `EventEmitter` is a core class from the `events` module that allows objects to emit named events and subscribe to them with listener functions. It's the foundation of Node.js's event-driven architecture. Many core Node.js objects, like HTTP servers and streams, inherit from `EventEmitter`.[^4_11][^4_12]

**Real-World Example (A Radio Station):**

* An `EventEmitter` is like a radio station (`eventEmitter`).
* `eventEmitter.emit('news', data)` is the station broadcasting a "news" segment with some data.
* `eventEmitter.on('news', (data) => { ... })` is a person tuning their radio to that station to listen for "news" broadcasts.

```javascript
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();

// Register a listener for the 'greet' event
myEmitter.on('greet', (name) => {
  console.log(`Hello, ${name}!`);
});

// Emit the 'greet' event
myEmitter.emit('greet', 'Node.js Developer'); // Output: Hello, Node.js Developer!
```

**Best Practice**: For custom classes that need to manage their own events, it's best to have them extend the `EventEmitter` class.

</details>

---

<details>
  <summary>04: Node.js Modules</summary>

### **Section 4: Node.js Modules**

### CommonJS `require()` vs. ES `import`

This is a foundational concept tied to the two module systems in Node.js.


| Feature | CommonJS (`require`) | ES Modules (`import`) |
| :-- | :-- | :-- |
| **Loading** | **Synchronous**: `require()` reads and executes the module file immediately, blocking the main thread. | **Asynchronous**: `import` statements are hoisted and loaded in the background before the script's execution. |
| **Syntax** | `const fs = require('fs');` | `import fs from 'fs';` or `import { readFile } from 'fs/promises';` |
| **`this` context** | `this` refers to `module.exports`. | `this` is `undefined` at the top level of an ES module. |
| **Dynamic Use** | Can be called anywhere in the code, like inside a function or `if` block. | `import` statements must be at the top level. For dynamic loading, use the `import()` function. |

**Best Practice**: Modern Node.js (v14+) has excellent support for ES Modules. For new projects, prefer ESM for its better performance characteristics and standardization with browser JavaScript. For existing projects or dependencies that only support CommonJS, you must use `require`.

### Built-in Core Modules

Node.js comes with a rich set of built-in modules that provide essential functionality without needing any external installation. You just need to import them.

Here are some of the most frequently used core modules:

* **`fs` (File System) (IMP)**: For all file-related operations: reading, writing, watching, and managing directories.[^5_3][^5_6]
* **`path`**: Provides utilities for working with file and directory paths in a cross-platform way (e.g., `path.join()`, `path.resolve()`).
* **`os`**: Provides operating system-related utility methods and properties (e.g., `os.cpus()`, `os.freemem()`).
* **`http` / `https`**: Core modules for creating HTTP/S servers and clients.
* **`events`**: The module that provides the `EventEmitter` class, crucial for building event-driven applications.
* **`crypto`**: Provides cryptographic functionality, including hashing, encryption, and decryption (e.g., for passwords or secure data).

```javascript
// Example using 'path' and 'fs'
const fs = require('fs');
const path = require('path');

// BAD: Prone to errors on different OSes
const wrongPath = __dirname + '/files/my-file.txt';

// GOOD: 'path.join' creates a correct path for any OS
const correctPath = path.join(__dirname, 'files', 'my-file.txt');

fs.readFile(correctPath, 'utf8', (err, data) => {
  // ...
});
```


### Creating Custom Modules

Creating your own modules is how you structure and organize your application code.

**CommonJS (`module.exports`)**
You export functionality by assigning it to the `module.exports` object.

```javascript
// 📁 /utils/math.js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

module.exports = {
  add,
  subtract
};

// 📁 main.js
const math = require('./utils/math');
console.log(math.add(5, 3)); // Output: 8
```

**ES Modules (`export`)**
You can use named exports or a single default export.

```javascript
// 📁 /utils/math.mjs (using named exports)
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// 📁 main.mjs
import { add } from './utils/math.mjs';
console.log(add(5, 3)); // Output: 8
```


### Module Caching Behavior (IMP)

When you `require()` a module for the first time, Node.js executes the code, creates the `exports` object, and **caches it**. Subsequent calls to `require()` for the same module will return the **cached object** directly without re-executing the module's code.

**Why this is important**:

* **Performance**: It avoids redundant file reads and execution, making module loading very fast after the initial load.
* **Shared State**: The cached module instance is a singleton. This means any stateful object exported by a module (like a database connection or a configuration object) will be shared across all parts of your application that import it.

**Real-World Example (Database Connection)**:
You can create a `db.js` module that establishes a database connection and exports the connection object. Other modules can then `require('./db.js')` to get the exact same connection instance, preventing multiple connections from being created.

```javascript
// 📁 /config/database.js
console.log('Connecting to database...');
const dbConnection = { host: 'localhost', user: 'root' }; // Simulate connection object

module.exports = dbConnection;

// 📁 service-one.js
const db = require('./config/database');
console.log('Service One uses the DB.');

// 📁 service-two.js
const db2 = require('./config/database');
console.log('Service Two uses the DB.');

// Output:
// Connecting to database...
// Service One uses the DB.
// Service Two uses the DB.

// "Connecting to database..." is logged only ONCE because the module is cached.
```

**Common Pitfall**: Be careful with modifying a cached module's exported object from different parts of your application, as it can lead to unexpected side effects.


</details>

---

<details>
  <summary>05: File System & Path Operations</summary>

### **Section 5: File System & Path Operations**
### Reading/Writing Files (Sync \& Async) (IMP)

The `fs` module is the primary tool for interacting with the file system. It offers both synchronous and asynchronous methods for most operations.[^6_4][^6_7]

* **Asynchronous (Non-blocking)**: These methods take a callback function (or return a Promise) and do not block the event loop. This is the recommended approach for server applications.
* **Synchronous (Blocking)**: These methods have `Sync` in their names (e.g., `readFileSync`). They block the event loop until the operation is complete. They are useful for simple scripts or CLI tools but should be **avoided in servers**.

| Operation | Asynchronous Example (`async/await` with promises) | Synchronous Example |
| :-- | :-- | :-- |
| **Reading** | `const data = await fs.promises.readFile('file.txt', 'utf8');` | `const data = fs.readFileSync('file.txt', 'utf8');` |
| **Writing** | `await fs.promises.writeFile('new-file.txt', 'Hello World!');` | `fs.writeFileSync('new-file.txt', 'Hello World!');` |
| **Appending** | `await fs.promises.appendFile('log.txt', 'New entry\n');` | `fs.appendFileSync('log.txt', 'New entry\n');` |

**Best Practice**: Always use the asynchronous, promise-based versions of the `fs` methods (from `require('fs/promises')`) in modern Node.js applications to keep the event loop from being blocked.[^6_1]

### Working with Directories

The `fs` module also provides functions for managing directories.

* **Create a directory**: `fs.promises.mkdir('new-directory')`
* **Read directory contents**: `fs.promises.readdir('directory-path')` returns an array of file and folder names.
* **Remove a directory**: `fs.promises.rmdir('empty-directory')`. To remove a directory with contents, use the option `{ recursive: true }`.
* **Check existence**: `fs.promises.access('path/to/check')` will throw an error if the path does not exist.


### Streams and Buffers (IMP)

When working with large files, loading the entire file into memory at once is inefficient and can crash your application. **Streams** are the solution.

* **Real-life Analogy (Streaming a Movie):** You don't download an entire 2-hour movie before you start watching. You download and watch it in small chunks. This is exactly how streams work. They process data in chunks instead of all at once.
* **Buffers**: A `Buffer` is a region of fixed-size physical memory that Node.js uses to represent binary data, such as the chunks of a file being read in a stream.

**Streams are efficient because:**

* **Memory**: They use a small, fixed amount of memory regardless of the file size.
* **Time**: You can start processing data as soon as the first chunk arrives, rather than waiting for the entire file.

**Example: Copying a large file with streams:**

```javascript
import { createReadStream, createWriteStream } from 'fs';
import { pipeline } from 'stream/promises';

const source = createReadStream('large-video.mp4');
const destination = createWriteStream('video-copy.mp4');

try {
  // pipeline() handles data flow, backpressure, and error handling automatically.
  await pipeline(source, destination);
  console.log('File copied successfully!');
} catch (err) {
  console.error('Pipeline failed:', err);
}
```

**Best Practice**: Always use `pipeline` for connecting streams. It is more robust than `source.pipe(destination)` because it properly handles cleanup and error propagation.

### Watching Files (`fs.watch`)

You can monitor a file or directory for changes using `fs.watch`. This is useful for tasks like automatic server restarts during development (like nodemon does) or live-reloading configuration files.

`fs.watch` is more efficient and reliable than `fs.watchFile`, which polls the file system at intervals.

```javascript
import { watch } from 'fs';

try {
  const watcher = watch('config.json');
  console.log('Watching for changes in config.json...');

  for await (const event of watcher) {
    if (event.eventType === 'change') {
      console.log(`File ${event.filename} changed. Reloading configuration...`);
      // Add logic here to re-read and apply the config file.
    }
  }
} catch (err) {
  console.error('Failed to watch file:', err);
}
```


</details>

---

<details>
  <summary>06: Networking & HTTP</summary>

### **Section 6: Networking \& HTTP**
### Creating HTTP Servers with `http` Module (IMP)

The built-in `http` module is the foundation for building web servers in Node.js. You can create a server, have it listen for requests on a specific port, and process each request through a callback function.[^7_1][^7_2]

While frameworks like Express or Fastify are typically used for building complex applications, understanding the underlying `http` module is crucial.

**Real-World Example: A basic web server**
This server listens on port 3000 and responds with "Hello, World!" to every request.[^7_1]

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  // Set the response header
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  
  // Send the response body and end the connection
  res.end('Hello, World!\n');
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}/`);
});
```


### Handling Requests \& Responses

In the `createServer` callback, you get two critical objects: `req` (request) and `res` (response).[^7_3]

* **`req` (IncomingMessage):** This object contains information about the incoming client request.
  * `req.url`: The request URL path (e.g., `/users?id=123`).
  * `req.method`: The HTTP method (e.g., 'GET', 'POST').[^7_3]
  * `req.headers`: An object containing the request headers.
  * It is a Readable Stream, which means you can listen for `data` events to receive the request body (e.g., from a POST request).
* **`res` (ServerResponse):** This object is used to build and send the response back to the client.
  * `res.writeHead(statusCode, headers)`: Sends the response status code and headers.[^7_1]
  * `res.write(chunk)`: Writes a chunk of the response body.
  * `res.end([data])`: Signals that the response is complete. Can optionally include the final piece of data to send.[^7_1]
  * It is a Writable Stream.

**Example: Simple Routing**

```javascript
// Inside http.createServer callback
if (req.url === '/') {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Welcome to the homepage!');
} else if (req.url === '/api/data' && req.method === 'GET') {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ message: 'This is some JSON data' }));
} else {
  res.writeHead(404, { 'Content-Type': 'text/plain' });
  res.end('404 Not Found');
}
```


### HTTPS Setup with TLS/SSL

To create a secure server that uses HTTPS, you need the `https` module. It works just like the `http` module but requires an additional options object containing a **TLS/SSL certificate** and a **private key**.[^7_4][^7_5]

For development, you can generate a self-signed certificate using tools like OpenSSL. For production, you must obtain a certificate from a trusted Certificate Authority (CA) like Let's Encrypt.[^7_4]

```javascript
const https = require('https');
const fs = require('fs');

const options = {
  key: fs.readFileSync('path/to/private-key.pem'),
  cert: fs.readFileSync('path/to/certificate.pem')
};

const server = https.createServer(options, (req, res) => {
  res.writeHead(200);
  res.end('Hello from a secure server!');
});

server.listen(443); // Default HTTPS port
```


### HTTP/2 in Node.js

HTTP/2 is a major revision of the HTTP protocol, offering significant performance improvements over HTTP/1.1. The `http2` core module allows you to leverage these features.[^7_6][^7_7]

**Key Benefits of HTTP/2**:

* **Multiplexing**: Allows multiple requests and responses to be sent over a single TCP connection, eliminating head-of-line blocking.[^7_6]
* **Server Push**: Lets the server proactively send resources to the client that it knows the client will need, reducing latency.[^7_8]
* **Header Compression**: Reduces the overhead of HTTP headers.

```javascript
const http2 = require('http2');
const fs = require('fs');

const options = {
  key: fs.readFileSync('private-key.pem'),
  cert: fs.readFileSync('certificate.pem')
};

const server = http2.createSecureServer(options);
server.on('stream', (stream, headers) => {
  stream.respond({
    'content-type': 'text/plain; charset=utf-8',
    ':status': 200
  });
  stream.end('Hello HTTP/2!');
});

server.listen(8443);
```


### TCP \& UDP Servers with `net` and `dgram`

For lower-level networking beyond HTTP, Node.js provides the `net` and `dgram` modules.

* **`net` (TCP)**: Provides an asynchronous network wrapper for creating **TCP servers and clients**. TCP is a connection-oriented protocol that guarantees message delivery and order, making it suitable for applications like chat services, remote logins (SSH), and database connections.[^7_9]
* **`dgram` (UDP)**: Provides an implementation of **UDP datagram sockets**. UDP is a connectionless protocol that is faster but does not guarantee delivery or order. It's ideal for applications where speed is more critical than reliability, such as live video/audio streaming, online gaming, and DNS.[^7_10][^7_11]

**Example: A simple TCP echo server**

```javascript
const net = require('net');

const server = net.createServer((socket) => {
  console.log('Client connected.');
  socket.write('Welcome to the TCP echo server!\n');

  // When data is received, echo it back
  socket.on('data', (data) => {
    console.log(`Received: ${data.toString().trim()}`);
    socket.write(`Echo: ${data}`);
  });

  socket.on('end', () => {
    console.log('Client disconnected.');
  });
});

server.listen(5000, () => {
  console.log('TCP server listening on port 5000');
});
```

</details>

---

<details>
  <summary>07: Asynchronous Patterns</summary>

### **Section 7: Asynchronous Patterns**
### Callbacks

Callbacks are functions passed as arguments to be executed once an asynchronous operation completes. This was the original pattern for async programming in Node.js.

* **Pattern**: The `(err, data)` error-first convention is standard.
* **Problem**: Deeply nested callbacks lead to "Callback Hell" or the "Pyramid of Doom," which is hard to read, debug, and maintain.

**Example of Callback Hell:**

```javascript
fs.readFile('file1.txt', 'utf8', (err, data1) => {
  if (err) throw err;
  fs.readFile('file2.txt', 'utf8', (err, data2) => {
    if (err) throw err;
    console.log(data1, data2);
    // And so on...
  });
});
```


### Promises

A `Promise` is an object representing the eventual completion (or failure) of an asynchronous operation. It can be in one of three states:

1. **Pending**: The initial state; not yet fulfilled or rejected.
2. **Fulfilled**: The operation completed successfully.
3. **Rejected**: The operation failed.

Promises allow you to chain asynchronous operations using `.then()` for successes and `.catch()` for errors, avoiding nested callbacks and making the code more linear and readable.

**Example of Promises:**

```javascript
const fs = require('fs/promises');

fs.readFile('file1.txt', 'utf8')
  .then(data1 => {
    console.log('File 1 read:', data1);
    return fs.readFile('file2.txt', 'utf8'); // Return the next promise
  })
  .then(data2 => {
    console.log('File 2 read:', data2);
  })
  .catch(err => {
    // A single .catch() can handle errors from any preceding .then() in the chain.
    console.error('An error occurred:', err);
  });
```


### `async/await` (IMP)

`async/await` is syntactic sugar built on top of Promises. It lets you write asynchronous code that looks and behaves like synchronous code, making it exceptionally clean and easy to follow [^8_6].

* `async`: A keyword placed before a function declaration to indicate that it returns a Promise.
* `await`: A keyword that can only be used inside an `async` function. It pauses the function execution until the awaited Promise is settled (fulfilled or rejected).

**Comparison Table: The Evolution of Async Code**


| Pattern | Example | Pros \& Cons |
| :-- | :-- | :-- |
| **Callbacks** | `readFile('file.txt', (err, data) => {})` | **Pros:** Simple for single operations. **Cons:** Leads to Callback Hell, difficult error handling. |
| **Promises** | `readFile('file.txt').then(data => {}).catch(err => {})` | **Pros:** Better chainability, centralized error handling. **Cons:** Can still be verbose. |
| **`async/await`** | `try { const data = await readFile('file.txt'); } catch (err) {}` | **Pros:** Cleanest syntax, reads like synchronous code, standard error handling with `try...catch`. **Cons:** Requires an `async` function context. |

**Best Practice**: Use `async/await` for all new asynchronous code. It is the modern standard and offers the best readability and maintainability.

### Error Handling in Async Code (IMP)

Proper error handling is critical, especially in async code.

* **Callbacks**: Use the `if (err)` check at the beginning of every callback.
* **Promises**: Use a `.catch()` block at the end of a promise chain to handle any rejection that occurs in the chain.
* **`async/await`**: Use a standard `try...catch` block, which is the most intuitive and robust method.[^8_5]

```javascript
// The modern, recommended way with async/await
async function readTwoFiles() {
  try {
    const data1 = await fs.promises.readFile('file1.txt', 'utf8');
    const data2 = await fs.promises.readFile('file2.txt', 'utf8');
    console.log(data1, data2);
  } catch (err) {
    console.error('Failed to read files:', err);
    // You can handle the error here (e.g., send a 500 response in an API)
  }
}
```


### Parallel vs. Sequential Execution

`async/await` makes it easy to control whether operations run one after another or at the same time.

* **Sequential Execution**: Awaiting promises one by one. The second operation only starts after the first one is complete.

```javascript
// Sequential: `request2` waits for `request1` to finish
const result1 = await makeApiRequest('endpoint1');
const result2 = await makeApiRequest('endpoint2');
```

* **Parallel Execution**: To run operations concurrently, use `Promise.all()`. It takes an array of promises and returns a single promise that resolves when all of the input promises have resolved. This is much more efficient if the operations don't depend on each other.

```javascript
// Parallel: Both requests start at the same time
const [result1, result2] = await Promise.all([
  makeApiRequest('endpoint1'),
  makeApiRequest('endpoint2')
]);
```

**Common Pitfall**: Using `await` sequentially for independent operations is a common performance bottleneck. Always use `Promise.all()` when tasks can be run in parallel.

### Using `util.promisify`

For older, callback-based libraries or Node.js APIs that don't have a promise-based version, you don't need to wrap them in promises manually. The built-in `util` module provides a `promisify` function to convert them automatically.

```javascript
const util = require('util');
const fs = require('fs');

// Convert the callback-based fs.readFile into a function that returns a promise
const readFilePromise = util.promisify(fs.readFile);

async function main() {
  try {
    const data = await readFilePromise('my-file.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
main();
```

</details>

---

<details>
  <summary>08: Streams & Buffer</summary>

### **Section 8: Streams \& Buffer**

### Readable \& Writable Streams

Streams are one of the most powerful concepts in Node.js, allowing you to handle large amounts of data efficiently. They process data in chunks rather than loading it all into memory at once.

* **Readable Stream**: A source of data. Examples include `fs.createReadStream()` (reading a file), `http.IncomingMessage` (the `req` object in a server, representing an incoming request body), or `process.stdin`.
* **Writable Stream**: A destination for data. Examples include `fs.createWriteStream()` (writing to a file), `http.ServerResponse` (the `res` object, for sending a response to a client), or `process.stdout`.

**Real-life Analogy (Water Pipe System):**

* A **Readable Stream** is like a large water tank (the source).
* A **Writable Stream** is like an empty bucket (the destination).
* Piping (`.pipe()`) is connecting a hose from the tank to the bucket to let the water flow.

```javascript
const { createReadStream, createWriteStream } = require('fs');

const readableStream = createReadStream('large-input-file.txt');
const writableStream = createWriteStream('output-file.txt');

// The .pipe() method automatically handles the flow of data from readable to writable.
readableStream.pipe(writableStream);

writableStream.on('finish', () => {
  console.log('Finished writing data to file.');
});
```

**Common Pitfall**: Not handling errors on streams. Both readable and writable streams can emit `error` events that must be handled to prevent application crashes. The `pipeline` function is the best practice for this.

### Duplex \& Transform Streams

* **Duplex Stream**: A stream that is both Readable and Writable. It acts as both a source and a destination. A TCP socket (`net.Socket`) is a perfect example. You can write to it and read from it independently.
* **Transform Stream (IMP)**: A special type of Duplex stream where the output is a transformation of its input. It reads data, modifies it, and then passes the modified data along. This is incredibly useful for on-the-fly data processing.
  * **Examples**: Zipping/unzipping files (`zlib` module), encrypting/decrypting data (`crypto` module), or parsing CSV data.

**Example: Compressing a file with a Transform Stream**

```javascript
const { createReadStream, createWriteStream } = require('fs');
const { createGzip } = require('zlib'); // zlib.createGzip() is a Transform stream
const { pipeline } = require('stream/promises');

const source = createReadStream('huge-log-file.log');
const gzip = createGzip(); // The transform stream
const destination = createWriteStream('huge-log-file.log.gz');

await pipeline(source, gzip, destination);

console.log('File compressed successfully!');
```

In this example, data flows from the source file, through the `gzip` transform stream which compresses it, and then to the destination file.

### Backpressure and Flow Control (IMP)

What happens if the Readable stream produces data much faster than the Writable stream can consume it? For example, reading a fast SSD and writing to a slow network connection.

* **The Problem**: The fast reader would overwhelm the slow writer, causing data to buffer in memory, which can lead to high memory usage and application crashes.
* **The Solution**: **Backpressure**. This is a mechanism where the slow Writable stream can signal back to the fast Readable stream to "pause" sending data. When the writer is ready for more, it signals the reader to "resume."

**Best Practice**: The `.pipe()` method and the `pipeline()` function handle backpressure automatically for you. This is a major reason why you should always use them instead of manually listening for `'data'` events and calling `write()`, which does not handle backpressure by default.

### Buffer Manipulation and Encoding

A `Buffer` is a raw binary data store. It's a Node.js-specific object that represents a fixed-size chunk of memory outside the V8 JavaScript engine heap.

* **Why Buffers?** JavaScript traditionally had no good way to handle raw binary data. Buffers were created to allow Node.js to work with binary streams, like reading from files or TCP sockets.

**Common Buffer Operations:**

* **Creating a Buffer**:
  * `Buffer.from('hello', 'utf8')`: Create a buffer from a string with a specific encoding.
  * `Buffer.alloc(10)`: Allocate a new, zero-filled buffer of 10 bytes.
* **Encoding**: Buffers can be converted to and from strings using different character encodings. The default is `'utf8'`. Others include `'hex'`, `'base64'`, `'latin1'`, etc.

```javascript
const buf = Buffer.from('Hello World');

console.log(buf); // <Buffer 48 65 6c 6c 6f 20 57 6f 72 6c 64>
console.log(buf.toString('utf8'));   // 'Hello World'
console.log(buf.toString('hex'));    // '48656c6c6f20576f726c64'
console.log(buf.toString('base64')); // 'SGVsbG8gV29ybGQ='

// Modify buffer content
buf[^9_0] = 74; // Change 'H' (72) to 'J' (74)
console.log(buf.toString()); // 'Jello World'
```

</details>

---

<details>
  <summary>09: Process & OS Interaction</summary>

### **Section 9: Process & OS Interaction**

### Environment Variables (`process.env`) (IMP)

The global `process` object provides information about, and control over, the current Node.js process. `process.env` is a property on this object that contains all the user environment variables.[^10_1][^10_2][^10_3]

This is the standard way to handle application configuration, allowing you to separate configuration from code.[^10_4]

**Why it's a Best Practice**:

* **Security**: Keeps sensitive information like API keys and database credentials out of your version-controlled code.
* **Flexibility**: Allows you to configure the same application differently for various environments (development, testing, production) without changing the code.

**How to Use It**:
You can set environment variables in your shell before running the script.

```bash
# Set an environment variable in the terminal
PORT=5000 NODE_ENV=production node server.js
```

In your Node.js code, you access them via `process.env`:

```javascript
// Provide a default value in case the variable is not set
const PORT = process.env.PORT || 3000;
const app = require('./app');

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

if (process.env.NODE_ENV === 'production') {
  console.log('Running in production mode.');
}
```


### Process Events (`exit`, `uncaughtException`)

The `process` object is an `EventEmitter` and can emit several key events.

* `'exit'`: Emitted when the Node.js process is about to exit. You can perform **synchronous** cleanup tasks here (e.g., closing a log file). You cannot prevent the exit and no asynchronous operations will be completed.[^10_5]
* `'uncaughtException'` (IMP): Emitted when a JavaScript error is thrown but not caught anywhere.[^10_5]

**Best Practice for `uncaughtException`**:
The official recommendation is to **avoid resuming your application** after an uncaught exception, as the application is now in an unknown and potentially unstable state. The correct use is to perform synchronous cleanup (like logging the error) and then let the process exit gracefully. A process manager like PM2 should then restart it.[^10_5]

```javascript
process.on('uncaughtException', (err, origin) => {
  console.error(`Caught exception: ${err}\n` + `Exception origin: ${origin}`);
  // Perform synchronous cleanup here
  process.exit(1); // Exit with a failure code
});
```


### Spawning Child Processes (`child_process`)

The `child_process` module allows you to run external commands or scripts as separate processes. This is useful for leveraging other system tools or running CPU-intensive tasks without blocking the main event loop.[^10_6][^10_7]

* `spawn()`: Launches a command in a new process. It's best for long-running processes or when the command produces a large amount of data, as it streams the I/O.[^10_7][^10_6]
* `exec()`: Spawns a shell and runs a command within that shell. It buffers the output and passes it to a callback function when the process is complete. Good for quick, simple commands.
* `fork()`: A special version of `spawn()` for creating a new Node.js process. It establishes an IPC (Inter-Process Communication) channel, allowing the parent and child to send messages to each other using `.send()` and `.on('message', ...)`.[^10_6][^10_7]


### Clustering for Multi-Core Scaling (IMP)

By default, a Node.js application runs on a single CPU core. The `cluster` module is the key to taking advantage of multi-core systems.[^10_8][^10_9]

It allows you to create a "cluster" of Node.js processes. A single **master process** can fork multiple **worker processes**. The master process can then distribute incoming connections (e.g., to an HTTP server) across the worker processes in a round-robin fashion.[^10_10]

**Real-life Analogy (Supermarket Checkouts):**
Instead of having one cashier (a single Node.js process) handle a huge line of customers, you open up multiple checkout lanes (worker processes). A manager (the master process) directs incoming customers to the next available cashier. This drastically improves throughput.

```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  console.log(`Master ${process.pid} is running`);

  // Fork workers for each CPU core
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  // Listen for dying workers and fork a new one
  cluster.on('exit', (worker, code, signal) => {
    console.log(`worker ${worker.process.pid} died`);
    cluster.fork(); // Replace the dead worker
  });
} else {
  // Workers can share any TCP connection
  // In this case, it is an HTTP server
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end('Hello from a worker process!\n');
  }).listen(8000);

  console.log(`Worker ${process.pid} started`);
}
```


### OS Info and Signals Handling

* **`os` module**: Provides methods for getting information about the operating system, like `os.cpus()`, `os.totalmem()`, `os.userInfo()`.
* **Process Signals**: You can listen for POSIX signals like `SIGINT` (sent when you press `Ctrl+C`) or `SIGTERM` (a generic termination signal). This allows for graceful shutdown logic.

```javascript
process.on('SIGINT', () => {
  console.log('Received SIGINT. Shutting down gracefully...');
  // Perform cleanup and then exit
  server.close(() => {
    process.exit(0);
  });
});
```

</details>

---

<details>
  <summary>10: Package Management</summary>

### **Section 10: Package Management**
### npm Basics (install, update, uninstall)

**npm (Node Package Manager)** is the default package manager for Node.js. It's a command-line tool and an online registry of open-source packages.[^11_1][^11_2]

**Common Commands:**


| Command | Description |
| :-- | :-- |
| `npm init -y` | Initializes a new Node.js project by creating a `package.json` file with default values. |
| `npm install <package-name>` | Installs a package as a production dependency (e.g., `express`) [^11_3]. |
| `npm install <package-name> --save-dev` | Installs a package as a development dependency (e.g., `nodemon`, `jest`). |
| `npm uninstall <package-name>` | Removes a package from your project and updates `package.json` [^11_3]. |
| `npm update <package-name>` | Updates a specific package to the latest version allowed by `package.json`. |
| `npm ls` | Lists all installed packages in the project. |
| `npm run <script-name>` | Executes a script defined in the `scripts` section of `package.json` [^11_3]. |

### `package.json` \& `package-lock.json` (IMP)

These two files are central to managing dependencies in a Node.js project.

* **`package.json`**: This file is the manifest for your project. It contains metadata like the project name, version, and license. Most importantly, it lists the **dependencies** (`dependencies` and `devDependencies`) your project needs, along with a semantic versioning range for each.
* **`package-lock.json`**: This file is a "snapshot" of your entire dependency tree. It records the **exact versions** of every package that was installed, including all sub-dependencies. Its purpose is to guarantee that every installation results in the exact same file structure in `node_modules`, ensuring consistent and reproducible builds across different machines (e.g., your machine vs. a CI/CD server).[^11_4][^11_5]

**Best Practice**: Always commit `package-lock.json` to your version control system (like Git). This ensures that every developer on the team gets the exact same dependencies when they run `npm install`.

### Semantic Versioning (Semver) (IMP)

SemVer is a versioning standard used by npm to manage dependency updates safely. A version number is formatted as **`MAJOR.MINOR.PATCH`** (e.g., `16.8.1`).[^11_6][^11_7]

* **`MAJOR`**: Incremented for incompatible API changes (breaking changes).
* **`MINOR`**: Incremented for adding new functionality in a backward-compatible manner.
* **`PATCH`**: Incremented for backward-compatible bug fixes.

**Special Characters in `package.json`:**

* **`^` (Caret)**: Allows updates to the latest minor and patch versions. For `^1.2.3`, it will match any version from `1.2.3` up to (but not including) `2.0.0`. This is the default for `npm install`.
* **`~` (Tilde)**: Allows only patch-level updates. For `~1.2.3`, it will match any version from `1.2.3` up to (but not including) `1.3.0`.


### `yarn` \& `pnpm` Alternatives

While npm is the default, other package managers offer improvements in performance, disk space efficiency, and feature sets.


| Feature | npm | yarn | pnpm |
| :-- | :-- | :-- | :-- |
| **Performance** | Good, but can be slower than alternatives. | Generally faster than npm, with robust caching. | Often the fastest due to its efficient storage model [^11_8]. |
| **Disk Space** | Duplicates packages across projects. | Better than npm due to caching. | **Highly efficient**. Packages are stored in a global content-addressable store and linked to projects, saving significant disk space [^11_8]. |
| **`node_modules`** | Creates a large, hoisted `node_modules` folder. | Can use Plug'n'Play (PnP) which avoids `node_modules` altogether, or a hoisted structure similar to npm. | Uses a non-flat, symlinked `node_modules` structure that is more strict and prevents packages from accessing unlisted dependencies [^11_9]. |
| **Lock File** | `package-lock.json` | `yarn.lock` | `pnpm-lock.yaml` |

**Best Practice**: `pnpm` is gaining significant popularity for its performance and disk-space efficiency, especially in monorepos. `yarn` (v2+) is powerful but can have a steeper learning curve due to its PnP architecture.[^11_10]

### Creating and Publishing npm Packages

Sharing your own code on the npm registry is a straightforward process.[^11_11]

1. **Prepare Your Package**:
  * Create your code. The main entry point is usually `index.js`.
  * Ensure your `package.json` is complete with a unique `name`, `version`, `description`, `main` entry point, and `license`.[^11_11]
  * Create a `README.md` to explain what your package does.
  * Create a `.npmignore` file to exclude any files you don't want in the final package (e.g., tests, source files if you're transpiling).
2. **Login to npm**:
  * Run `npm login` in your terminal and enter your npm account credentials.
3. **Publish the Package**:
  * Navigate to your package's root directory.
  * Run `npm publish`. If your package name is taken, you can publish it under your username by making it a "scoped" package (e.g., `@username/package-name`) and running `npm publish --access public`.[^11_12][^11_13]
4. **Update a Package**:
  * Make your changes.
  * Increment the version in `package.json` according to SemVer (e.g., `npm version patch`, `npm version minor`).
  * Run `npm publish` again.

</details>

---

<details>
  <summary>11: Debugging & Profiling</summary>

### **Section 11: Debugging \& Profiling**

### Using Node.js Debugger (`node inspect`)

Node.js has a built-in command-line debugger. You can start it by adding the `inspect` keyword when running your script.[^12_1][^12_2]

```bash
node inspect my-script.js
```

This starts an interactive debugging session in your terminal. It's useful for quick debugging without leaving the command line, but its interface is less user-friendly than graphical debuggers. You can also place the `debugger;` statement in your code to create a breakpoint.[^12_3]

### Chrome DevTools with Node.js (IMP)

This is the most powerful and common way to debug Node.js applications. By starting your Node.js process with the `--inspect` or `--inspect-brk` flag, you can connect to it using the same Chrome DevTools you use for front-end JavaScript.[^12_4][^12_5]

* `--inspect`: Runs the code and makes it available for a debugger to attach.
* `--inspect-brk`: Runs the code but breaks on the very first line, waiting for you to attach a debugger and start execution manually.[^12_4]

**Steps to Debug with Chrome DevTools:**

1. Run your app with the inspect flag:

```bash
node --inspect-brk server.js
```

2. Open Google Chrome and navigate to `chrome://inspect`.[^12_2]
3. Click on "**Open dedicated DevTools for Node**" or find your target process listed and click "**inspect**".[^12_2]

This opens a DevTools window connected to your Node.js process, giving you access to:

* **Breakpoints**: Pause execution at specific lines.
* **Variable Inspection**: See the values of variables in the current scope.
* **Call Stack**: Trace the path of function calls that led to the current point.
* **Console**: A REPL connected to your Node.js process.
* **Profiling Tools**: For CPU and memory analysis.


### Profiling with `--inspect` and Flamegraphs

**Profiling** is the process of analyzing your application's performance to identify bottlenecks.

* **CPU Profiling**: Identifies which functions are consuming the most CPU time. This is crucial for optimizing slow, CPU-bound operations. You can start a CPU profile from the "Profiler" tab in Chrome DevTools.[^12_6]
* **Flame Graph**: A visualization of profiled stack traces that helps you quickly spot the code paths that are most frequently executed. Wider bars in the graph represent functions that were on the CPU for a longer time, making them primary candidates for optimization.[^12_7][^12_8]

**Tools for Flamegraphs**:

* `0x`: A popular command-line tool that can generate an interactive flame graph for a Node.js process with a single command.[^12_9]

```bash
# Install 0x globally
npm install -g 0x

# Profile your app and automatically open the flamegraph
0x my-app.js
```


### Memory Leak Detection with Heapdump (IMP)

A **memory leak** occurs when your application allocates memory but fails to release it when it's no longer needed, causing memory usage to grow over time and eventually crash the process.

**Heap Snapshots** are the primary tool for diagnosing memory leaks. A heap snapshot is a "photo" of all the objects in your app's memory at a specific moment.[^12_10]

**How to detect a leak**:

1. Take a heap snapshot when your application starts.
2. Perform the actions that you suspect are causing the leak (e.g., make many API requests).
3. Take a second heap snapshot.
4. Compare the two snapshots. In Chrome DevTools, you can use the "Comparison" view.
5. Look for a large number of objects that have been created but not garbage collected. The tool will show you what objects are retaining references to them, helping you trace the source of the leak.[^12_10]

### CPU Profiling

CPU profiling helps identify functions that consume significant processing time, enabling you to optimize them and improve application performance.[^12_8]

**How to perform CPU profiling**:

1. In the Chrome DevTools connected to your Node.js process, go to the **Profiler** tab.
2. Click the **Start** button to begin recording a CPU profile.
3. Interact with your application to trigger the functionality you want to analyze.
4. Click **Stop**.
5. DevTools will display a detailed report, often as a flame graph or a tree view, showing the functions that took the most time to execute.[^12_8]

By analyzing the profile, you can pinpoint inefficient algorithms or "hot paths" that need refactoring.

</details>

---

<details>
  <summary>12: Error Handling</summary>

### **Section 12: Error Handling**
### Try/Catch in Sync \& Async Code (IMP)

The `try...catch` block is the standard way to handle synchronous errors in JavaScript. With the introduction of `async/await`, it also became the primary method for handling errors in asynchronous code, making error handling consistent across both paradigms.[^13_1][^13_2]

* **Synchronous Code**:

```javascript
try {
  const result = JSON.parse('{ "malformed": json }');
} catch (error) {
  console.error('Sync Error:', error.message); // Catches the parsing error
}
```

* **Asynchronous Code (with `async/await`)**:

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://invalid-url');
    const data = await response.json();
    return data;
  } catch (error) {
    // Catches errors from the fetch call or the .json() parsing
    console.error('Async Error:', error.message);
  }
}
```


### Error-First Callback Convention

Before promises and `async/await`, Node.js established the **error-first callback** convention as the standard for asynchronous operations.[^13_3]

* **Rule**: The first argument to any callback function is reserved for an error object.[^13_4][^13_3]
* **Logic**: If an error occurred, the first argument will be an `Error` object, and the subsequent arguments will be undefined. If the operation was successful, the first argument will be `null`, and the following arguments will contain the result data.[^13_3]

```javascript
const fs = require('fs');

fs.readFile('a-file-that-does-not-exist.txt', (err, data) => {
  // ALWAYS check for the error first
  if (err) {
    console.error('An error occurred:', err);
    return;
  }
  // Only proceed if err is null
  console.log('File data:', data);
});
```


### Custom Error Classes

For better error handling in large applications, it's a best practice to create your own custom error classes that extend the built-in `Error` class. This allows you to add more context, like HTTP status codes or error types, and handle different errors in different ways.[^13_5]

**Benefits**:

* Adds semantic meaning to errors (e.g., `NotFoundError` vs. `ValidationError`).
* Allows you to attach custom properties like `statusCode`.
* Enables checking error types with `instanceof`.

**Example:**

```javascript
// Define a custom error for resource not found
class NotFoundError extends Error {
  constructor(message) {
    super(message);
    this.name = 'NotFoundError';
    this.statusCode = 404;
  }
}

// Use it in your application
function findUser(id) {
  if (id !== 1) {
    throw new NotFoundError(`User with id ${id} not found.`);
  }
  return { id: 1, name: 'John Doe' };
}

try {
  const user = findUser(2);
} catch (error) {
  if (error instanceof NotFoundError) {
    // Send a 404 response
    console.error(`Status ${error.statusCode}: ${error.message}`);
  } else {
    // Handle other types of errors
    console.error('An unexpected error occurred:', error);
  }
}
```


### Centralized Error Handling in Apps (IMP)

In frameworks like Express, instead of putting `try...catch` blocks in every single route handler, you can use a **centralized error-handling middleware**. This middleware is defined with four arguments: `(err, req, res, next)` and is placed at the very end of your middleware stack.[^13_6][^13_7]

Any error passed to `next()` (e.g., `next(error)`) from any preceding route or middleware will be caught and processed by this single function.[^13_7]

**Example in Express:**

```javascript
const express = require('express');
const app = express();

app.get('/user/:id', (req, res, next) => {
  try {
    if (parseInt(req.params.id) > 100) {
      throw new Error('User ID too high!'); // This will be caught below
    }
    res.send('User data');
  } catch (error) {
    next(error); // Pass the error to the centralized handler
  }
});

// Centralized error-handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  
  // Use custom error status code or default to 500
  const statusCode = err.statusCode || 500;
  
  res.status(statusCode).json({
    status: 'error',
    message: err.message || 'Something went wrong!',
  });
});

app.listen(3000);
```


### Handling Unhandled Promise Rejections

If a Promise is rejected but doesn't have a `.catch()` handler or isn't awaited inside a `try...catch` block, it becomes an **unhandled rejection**. In older Node.js versions, these were silently ignored. In modern versions, they will crash the process.[^13_8][^13_9]

It is a critical best practice to listen for these globally to prevent your application from crashing unexpectedly.[^13_9]

```javascript
process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection at:', promise, 'reason:', reason);
  // Log the error and then exit gracefully
  // so a process manager can restart the application in a clean state.
  process.exit(1);
});
```


</details>

---

<details>
  <summary>13: Node.js with Databases</summary>

### **Section 13: Node.js with Databases**
### Connecting to Relational Databases (PostgreSQL, MySQL)

To connect to relational databases (SQL), you use a specific driver package from npm. These drivers provide the interface to send SQL queries to the database and get results back.[^14_1]

* **PostgreSQL**: The most common driver is `pg`.[^14_2]
* **MySQL**: The most common driver is `mysql2`, which is a more performant, promise-compatible version of the original `mysql` driver.

**Example: Connecting to PostgreSQL with `pg`**

```javascript
const { Client } = require('pg');

const client = new Client({
  host: 'localhost',
  user: 'db_user',
  password: 'db_password',
  database: 'my_database',
  port: 5432,
});

async function connectAndQuery() {
  try {
    await client.connect();
    console.log('Connected successfully to PostgreSQL!');
    
    const res = await client.query('SELECT NOW()');
    console.log('Current time from DB:', res.rows[^14_0].now);
    
    await client.end();
  } catch (err) {
    console.error('Connection error', err.stack);
  }
}

connectAndQuery();
```


### Connecting to NoSQL (MongoDB, Redis)

Connecting to NoSQL databases also requires specific drivers.

* **MongoDB**: The standard driver is `mongodb`, but it's most often used through an ODM like **Mongoose**, which provides a schema-based modeling environment.
* **Redis**: The most popular clients are `redis` and `ioredis`. Redis is an in-memory data store often used as a high-speed cache, a message broker, or a session store.[^14_3]

**Example: Connecting to MongoDB with Mongoose**

```javascript
const mongoose = require('mongoose');

const mongoURI = 'mongodb://localhost:27017/myAppDB';

mongoose.connect(mongoURI)
  .then(() => console.log('MongoDB connected successfully.'))
  .catch(err => console.error('MongoDB connection error:', err));
```


### Connection Pooling \& Performance Tips (IMP)

Opening and closing a database connection for every single query is extremely inefficient due to the overhead of the network handshake. **Connection pooling** is the solution.[^14_4]

* **What it is**: A "pool" of pre-established, reusable database connections is created when your application starts. When you need to run a query, you "borrow" a connection from the pool. When you're done, you "release" it back to the pool instead of closing it.[^14_4]
* **Why it's essential**: It dramatically improves application performance by reducing the latency associated with creating new connections.[^14_5]

**Best Practice**: Most modern database drivers (`pg`, `mysql2`, `mongoose`) have built-in connection pooling that is enabled by default or with simple configuration. Always use it in production applications.[^14_6][^14_4]

**Example: Connection Pool with `mysql2`**

```javascript
const mysql = require('mysql2/promise');

const pool = mysql.createPool({
  host: 'localhost',
  user: 'user',
  database: 'test_db',
  waitForConnections: true,
  connectionLimit: 10, // Max number of connections in pool
  queueLimit: 0
});

// To run a query, you get a connection from the pool
const [rows, fields] = await pool.query('SELECT * FROM users');
```


### ORM/ODM Usage (Sequelize, Prisma, Mongoose) (IMP)

**ORM (Object-Relational Mapping)** and **ODM (Object-Document Mapping)** libraries provide a higher level of abstraction for interacting with your database. They let you work with JavaScript objects and methods instead of writing raw SQL or database-specific query syntax.[^14_7]


| Library | Type | Supported Databases | Key Feature |
| :-- | :-- | :-- | :-- |
| **Sequelize** | ORM | PostgreSQL, MySQL, MariaDB, SQLite, MSSQL [^14_8][^14_9]. | Mature and feature-rich. Uses the Active Record pattern. Great for traditional relational databases [^14_10]. |
| **Prisma** | ORM | PostgreSQL, MySQL, SQLite, SQL Server, MongoDB. | A "next-generation" ORM. Uses a declarative schema file (`schema.prisma`) to generate a type-safe client, providing excellent autocompletion and developer experience [^14_11]. |
| **Mongoose** | ODM | MongoDB [^14_8]. | The de-facto standard for MongoDB in Node.js. Provides schema validation, middleware, and query building on top of the native driver [^14_8]. |

**Why use an ORM/ODM?**

* **Productivity**: Faster development since you write less boilerplate code.
* **Safety**: Helps prevent SQL injection vulnerabilities by design.
* **Abstraction**: Makes it easier to switch between databases (with some limitations).
* **Readability**: Code becomes more declarative and easier to understand (`User.create(...)` vs. `INSERT INTO ...`).

**Common Pitfall**: Over-reliance on ORMs for complex queries can sometimes lead to inefficient database queries. It's important to understand the SQL/queries being generated by the ORM and to use raw queries when necessary for performance optimization.


</details>

---

<details>
  <summary>14: Node.js & APIs</summary>

### **Section 14: Node.js \& APIs**
### Building REST APIs with Express/Fastify/Koa

While you can build APIs with the native `http` module, frameworks provide routing, middleware, and other utilities that make development much faster and more organized.

* **Express**: The most popular and longest-standing Node.js web framework. It's minimalist, flexible, and has a massive ecosystem of middleware. Its design is heavily based on the middleware pattern.[^15_1]
* **Koa**: Developed by the original creators of Express, Koa aims to be a smaller, more expressive, and more robust foundation for web applications. It uses `async/await` to eliminate callback hell and improve error handling.
* **Fastify**: A modern, high-performance framework that focuses on speed and low overhead. It achieves its performance through intelligent optimizations like schema-based JSON serialization and efficient routing.[^15_2][^15_3]

**Comparison Table:**


| Feature | Express | Koa | Fastify |
| :-- | :-- | :-- | :-- |
| **Popularity** | Very High | Medium | Growing Rapidly |
| **Performance** | Good | Good | Excellent |
| **Philosophy** | Unopinionated, middleware-centric | Modern, `async/await` based, minimal core | Performance-focused, schema-driven [^15_1] |
| **Middleware** | Uses standard `(req, res, next)` middleware [^15_4]. | Uses `async` functions as middleware, with a `ctx` (context) object. | Uses a hook and plugin architecture. |

### Middleware Patterns (IMP)

Middleware functions are the heart of frameworks like Express. They are functions that have access to the request object (`req`), the response object (`res`), and the `next` function in the application’s request-response cycle.[^15_4]

**Real-life Analogy (Factory Assembly Line):**
An HTTP request is like a raw product entering an assembly line. Each middleware is a station on the line that performs a specific task: one station checks for authentication, another parses the request body, and another adds logs. Each station does its job and then passes the product to the `next` station.

**Common Middleware Tasks:**

* Parsing request bodies (e.g., `express.json()`).
* Logging requests.
* Authenticating and authorizing users.
* Compressing responses.
* Handling errors.

```javascript
// Example of a simple logger middleware in Express
const express = require('express');
const app = express();

const loggerMiddleware = (req, res, next) => {
  console.log(`${req.method} ${req.url} - ${new Date().toISOString()}`);
  next(); // Pass control to the next middleware in the chain
};

app.use(loggerMiddleware); // Apply the middleware to all routes

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(3000);
```


### Route Handling \& Modularization

As an application grows, putting all your routes in a single file becomes unmanageable. The best practice is to modularize your routes by feature. Express's `Router` is perfect for this.[^15_5]

1. Create separate files for each feature's routes (e.g., `userRoutes.js`, `productRoutes.js`).
2. Use `express.Router()` in each file to define the routes for that feature.[^15_5]
3. Export the router from each file.
4. In your main server file, import and `app.use()` the routers with a specific path prefix.

**Example:**

`routes/userRoutes.js`:

```javascript
const express = require('express');
const router = express.Router();

router.get('/:id', (req, res) => { /* Get user by ID */ });
router.post('/', (req, res) => { /* Create a new user */ });

module.exports = router;
```

`server.js`:

```javascript
const express = require('express');
const app = express();
const userRoutes = require('./routes/userRoutes');

// Mount the user routes on the '/api/users' path
app.use('/api/users', userRoutes);

app.listen(3000);
```


### API Versioning Strategies (IMP)

When you need to introduce breaking changes to your API, you must create a new version to avoid breaking existing client applications. There are several common strategies for this:[^15_6]


| Strategy | Example | Pros \& Cons |
| :-- | :-- | :-- |
| **URI Path (Most Common)** | `/api/v1/products` | **Pros:** Simple, explicit, easy to see in logs [^15_7]. **Cons:** Violates the principle that a URI should represent a single resource. |
| **Query Parameter** | `/api/products?version=1` | **Pros:** Easy to implement [^15_8]. **Cons:** Can clutter URLs, harder to manage routing. |
| **Custom Header** | `Accepts-version: 1.0` | **Pros:** Keeps URLs clean [^15_8]. **Cons:** Not visible to the user, requires custom client configuration. |
| **Accept Header (Media Type)** | `Accept: application/vnd.myapi.v2+json` | **Pros:** Considered the most "RESTful" approach. **Cons:** More complex, can be confusing for consumers [^15_8]. |

**Best Practice**: **URI Path versioning** (`/v1`, `/v2`) is the most widely used and understood method. It is clear, explicit, and easy for both API providers and consumers to work with.[^15_7]

### Integrating with External APIs

Node.js applications often need to communicate with other third-party APIs (e.g., payment gateways, weather services).

**Best Practices for Integration:**

1. **Use a Robust HTTP Client**: Libraries like **Axios** or **node-fetch** are highly recommended over the native `http` module. They provide a simpler, promise-based interface and handle common tasks like setting headers and parsing JSON responses automatically.[^15_9]
2. **Isolate API Logic**: Create a dedicated "service" or "client" module for each external API you interact with. This keeps your main business logic clean and makes the API client code reusable and testable.
3. **Handle Errors Gracefully**: External API calls can fail due to network issues, rate limits, or server errors. Always wrap your API calls in `try...catch` blocks and have a strategy for retries or graceful failure.
4. **Secure API Keys**: Never hardcode API keys or secrets in your code. Store them securely in environment variables (`process.env`).[^15_10]


</details>

---

<details>
  <summary>15: Authentication & Authorization</summary>

### **Section 15: Authentication \& Authorization**
### JWT-based Authentication (IMP)

**JSON Web Token (JWT)** is a compact, URL-safe standard for creating access tokens that assert a number of claims. It is a **stateless** authentication mechanism, meaning the server does not need to store session information about the user.[^16_1]

**How it works**:

1. **Login**: A user logs in with their credentials.
2. **Token Generation**: If the credentials are valid, the server generates a JWT containing a payload (e.g., `userId`, `roles`) and signs it with a secret key.
3. **Token Storage**: The server sends this JWT back to the client, which stores it (e.g., in `localStorage` or an `HttpOnly` cookie).
4. **Authenticated Requests**: For subsequent requests to protected routes, the client sends the JWT in the `Authorization` header, typically as a Bearer token (`Authorization: Bearer <token>`).
5. **Token Verification**: The server receives the token, verifies its signature using the secret key, and if valid, processes the request.[^16_2]

**JWT Structure:** A JWT consists of three parts separated by dots (`.`): `header.payload.signature`.[^16_2]

**Best Practice**: Store your JWT secret key securely in an environment variable and never expose it. Use a strong, long, and un-guessable secret.

### Session-based Authentication

This is a **stateful** authentication mechanism where the server maintains a session for each logged-in user.[^16_3]

**How it works**:

1. **Login**: A user logs in with their credentials.
2. **Session Creation**: The server creates a session and stores session data (like `userId`) on the server-side (in memory, a database, or a Redis cache).[^16_4]
3. **Session ID**: The server sends a unique Session ID back to the client, which stores it in a cookie.[^16_5]
4. **Authenticated Requests**: The browser automatically sends this cookie with every subsequent request to the same domain.
5. **Session Validation**: The server uses the Session ID from the cookie to look up the session data and identify the user.[^16_4]

**Comparison Table: JWT vs. Sessions**


| Feature | JWT (Stateless) | Session-based (Stateful) |
| :-- | :-- | :-- |
| **Server State** | No state stored on the server. Self-contained token. | Server must store session data for every active user [^16_4]. |
| **Scalability** | **Highly scalable**. Any server with the secret key can validate the token. Ideal for microservices. | Can be harder to scale. Requires shared session storage (e.g., Redis) if using multiple servers. |
| **Storage** | Client stores the token. | Server stores the session; client stores only a session ID cookie. |
| **Revocation** | Harder to revoke a single token before it expires. Requires a blacklist. | Easy to revoke. Just delete the session from the server-side store. |
| **Use Case** | APIs, mobile apps, single-page applications (SPAs). | Traditional monolithic web applications. |

### OAuth 2.0 / OpenID Connect

* **OAuth 2.0**: An **authorization framework** that allows a third-party application to obtain limited access to a user's account on another service, without giving it the user's password. For example, allowing a "photo printing" app to access your photos on Google Photos.[^16_6]
* **OpenID Connect (OIDC)**: A thin identity layer built on top of OAuth 2.0. It provides **authentication** by allowing clients to verify the identity of the user based on the authentication performed by an Authorization Server. It adds a standardized `id_token` (a JWT) to the OAuth 2.0 flow.[^16_6]

**Best Practice**: Use well-established libraries like **Passport.js** (`passport-google-oauth20`, `passport-github2`, etc.) to implement these flows in Node.js, as they handle the complexities of the protocol for you.[^16_6]

### Role-Based Access Control (RBAC)

**Authorization** is different from authentication. Authentication confirms who you are; authorization determines what you are allowed to do. RBAC is a common pattern for managing permissions.[^16_7]

**How it works**:

1. **Define Roles**: Define roles for your application (e.g., `admin`, `editor`, `viewer`).[^16_8]
2. **Assign Roles to Users**: When a user is created or updated, assign them one or more roles. This information is often stored in the database and can be included in the JWT payload.
3. **Protect Routes with Middleware**: Create a middleware that checks the user's role before allowing access to a specific route or resource.[^16_9]

**Example: RBAC Middleware in Express**

```javascript
// Middleware to check if user has the 'admin' role
const requireAdmin = (req, res, next) => {
  // Assuming user object with a 'roles' array is attached to the request
  // by a previous authentication middleware (e.g., from a decoded JWT)
  if (req.user && req.user.roles.includes('admin')) {
    next(); // User is an admin, proceed
  } else {
    res.status(403).json({ message: 'Forbidden: Admins only' });
  }
};

// Protect a route with the RBAC middleware
app.delete('/api/users/:id', requireAdmin, (req, res) => {
  // This code will only run if the user is an admin
  res.send('User deleted successfully');
});
```


### CSRF Protection in Node.js Apps

**Cross-Site Request Forgery (CSRF)** is an attack that tricks a user into submitting a malicious request. It leverages the fact that browsers automatically include cookies (like session cookies) on requests to a domain.

This is primarily a concern for **session-based authentication**. It is generally not an issue for stateless APIs that use Bearer tokens in the `Authorization` header, as these tokens are not sent automatically by the browser.

**How to Protect (Synchronizer Token Pattern)**:

1. On a GET request for a form, the server generates a unique, random CSRF token.
2. The server sends this token to the client and embeds it in a hidden input field in the form.[^16_10]
3. When the user submits the form via POST, the CSRF token is sent back in the request body.
4. The server middleware checks if the received token matches the one associated with the user's session. If they match, the request is valid. If not, it's rejected.[^16_11]

**Best Practice**: Use a library like `csurf` to implement CSRF protection in Express applications.[^16_10]


</details>

---

<details>
  <summary>16: Security Best Practices</summary>


### **Section 16: Security Best Practices**

### Preventing XSS, CSRF, SQL Injection (IMP)

These are three of the most common web application vulnerabilities.

* **XSS (Cross-Site Scripting)**: Occurs when an attacker injects malicious scripts into content that is then delivered to a user's browser.[^17_1]
  * **Prevention**:

1. **Validate Input**: Never trust user input. Reject any input that doesn't match the expected format.[^17_2]
2. **Encode Output**: Before rendering any user-generated content in HTML, encode it to turn special characters like `<` and `>` into their HTML entity equivalents (`&lt;` and `&gt;`). Most template engines (like EJS, Pug) do this by default.[^17_3]
3. **Use Content Security Policy (CSP)**: Set the `Content-Security-Policy` HTTP header to tell the browser which sources of scripts are safe to execute.[^17_4]
* **CSRF (Cross-Site Request Forgery)**: An attack that forces an authenticated user to execute unwanted actions on a web application.
  * **Prevention**: Use the **Synchronizer Token Pattern**. Libraries like `csurf` for Express can implement this for you by generating and validating a unique token for each session and form submission.[^17_5]
* **SQL Injection**: Occurs when an attacker manipulates user input to interfere with the SQL queries an application makes to its database.[^17_6]
  * **Prevention**:

1. **Never use string concatenation** to build queries with user input.
2. **Use Parameterized Queries (Prepared Statements)**: This is the most effective defense. It ensures that user input is always treated as data, not as executable SQL code.[^17_7][^17_6]
3. **Use an ORM/ODM**: Libraries like Sequelize, Prisma, or Mongoose handle query parameterization automatically, which significantly reduces the risk of SQL injection.[^17_7]


### Avoiding `eval` and Insecure Deserialization

* **`eval()`**: The `eval()` function executes a string as JavaScript code. It is extremely dangerous and should almost never be used, as it can execute malicious code passed in through user input. There is almost always a safer alternative.
* **Insecure Deserialization**: This occurs when an application deserializes user-controlled data without proper validation, potentially leading to remote code execution. Be cautious with functions like `JSON.parse()` if the input source is not fully trusted, and avoid libraries that deserialize complex object graphs from untrusted sources.


### Secure Headers with `helmet` (IMP)

HTTP headers can be used to significantly improve your application's security. The **`helmet`** package for Express is a collection of middleware functions that set various security-related HTTP headers to sensible defaults.[^17_8]

**It helps prevent**:

* Clickjacking (using `X-Frame-Options`).
* XSS by enabling the browser's built-in filter (`X-XSS-Protection`).[^17_4]
* Protocol-downgrading attacks (`Strict-Transport-Security`).
* Content type sniffing (`X-Content-Type-Options`).

**Usage is extremely simple**:

```javascript
const express = require('express');
const helmet = require('helmet');

const app = express();

// Use helmet() to apply all of its default security headers
app.use(helmet());

// Your routes...
```


### Rate Limiting \& Brute Force Protection

**Rate limiting** restricts how many times a user can perform an action in a given time frame. It is essential for :[^17_9]

* Preventing brute-force login attempts.
* Protecting your APIs from denial-of-service (DoS) attacks.
* Reducing costs by controlling resource-intensive API calls.

**Implementation**:

* Use a library like `express-rate-limit` to easily add rate limiting to your Express application. It can be configured to limit requests based on IP address or other identifiers.[^17_10]

```javascript
const rateLimit = require('express-rate-limit');

const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 5, // Limit each IP to 5 login requests per window
  message: 'Too many login attempts, please try again after 15 minutes.',
});

// Apply the rate limiter only to the login route
app.post('/login', loginLimiter, (req, res) => {
  // ... login logic
});
```


### Using `npm audit` and Dependency Scanning

Your application is only as secure as its weakest dependency. A vulnerability in one of your packages is a vulnerability in your application.

* **`npm audit`**: A built-in npm command that scans your project's dependencies for known security vulnerabilities. It provides a report detailing the vulnerabilities, their severity, and the path to the affected package.[^17_11]
* **`npm audit fix`**: This command will attempt to automatically update vulnerable dependencies to a safe version without causing breaking changes in your project.[^17_3]

**Best Practice**:

1. Run `npm audit` regularly as part of your development workflow and in your CI/CD pipeline.[^17_12]
2. Use automated security scanning tools like **Snyk** or **GitHub Dependabot**, which continuously monitor your dependencies and automatically create pull requests to fix vulnerabilities.


</details>

---

<details>
  <summary>17: Testing in Node.js</summary>

### **Section 17: Testing in Node.js**
### Unit Testing with Jest/Mocha

**Unit testing** involves testing the smallest individual parts of your application (functions, classes) in isolation.[^18_1]

* **Jest**: An "all-in-one" testing framework that is extremely popular in the JavaScript ecosystem. It comes with a test runner, assertion library (`expect`), and mocking capabilities built-in. It's known for its "zero-config" setup and powerful features like snapshot testing.[^18_2]
* **Mocha**: A highly flexible and mature testing framework. Unlike Jest, Mocha is just a test runner. You need to bring your own libraries for assertions (e.g., **Chai**) and for creating test doubles (e.g., **Sinon**). This flexibility makes it a favorite for backend development.[^18_3][^18_4][^18_2]

**Comparison Table: Jest vs. Mocha**


| Feature | Jest | Mocha |
| :-- | :-- | :-- |
| **Philosophy** | All-in-one, zero-configuration [^18_2]. | Flexible, bring your own libraries [^18_5]. |
| **Setup** | Very easy, works out of the box. | Requires more setup (e.g., installing Chai, Sinon). |
| **Assertions** | Built-in (`expect`). | Requires an external library like Chai. |
| **Mocking** | Built-in (`jest.mock`, `jest.fn`). | Requires an external library like Sinon.js. |
| **Use Case** | Excellent for React and front-end; also very capable for Node.js. | Traditionally very strong for backend Node.js testing [^18_2]. |

### Integration Testing

**Integration testing** verifies that different modules or services in your application work together correctly. For a Node.js API, this often means testing that an API endpoint correctly interacts with the database.[^18_6]

**Example Scenario**:

* A test that sends an HTTP request to a `POST /users` endpoint.
* The test then connects to a test database to verify that a new user record was actually created.
* Finally, it cleans up by deleting the record it created.

**Best Practice**: Integration tests should run against a real, but separate, test database—not your production or development database.[^18_7]

### E2E Testing with Supertest or Playwright

**End-to-End (E2E) testing** simulates a real user workflow from start to finish to validate the entire application stack.[^18_8]

* **Supertest**: An excellent library for testing Node.js HTTP servers. It allows you to make programmatic requests to your API endpoints without needing to run the server on a live port. It's perfect for testing API workflows (e.g., register -> login -> fetch data).[^18_7]

```javascript
const request = require('supertest');
const app = require('../app'); // Your Express app

describe('GET /users', () => {
  it('should respond with a list of users', async () => {
    const response = await request(app)
      .get('/users')
      .set('Accept', 'application/json');
    
    expect(response.status).toBe(200);
    expect(response.body).toBeInstanceOf(Array);
  });
});
```

* **Playwright**: A modern E2E testing framework for web applications. It automates a real browser (Chromium, Firefox, WebKit) to perform actions just like a user would (clicking buttons, filling forms, navigating pages). It is used for testing the full front-end and back-end interaction.[^18_9][^18_8]


### Test Doubles: Mocks, Stubs, Spies (IMP)

Test doubles are objects that stand in for real dependencies in your tests. They are essential for isolating the unit of code you are testing.[^18_10]

* **Stub**: Provides a pre-programmed, canned answer to a function call. It's used when your test needs a dependency to return a specific value.[^18_10]
  * **Use Case**: Stubbing a database call to return a specific user object without actually hitting the database.
* **Spy**: A wrapper around a real function that records how it was used (e.g., how many times it was called, and with what arguments) without changing the original function's behavior.[^18_10]
  * **Use Case**: Verifying that a `logger.log()` function was called exactly once when an error occurs.
* **Mock**: An object with pre-programmed expectations about how it will be used. A mock will cause the test to fail if it's not used in the way you expected.[^18_10]
  * **Use Case**: Mocking an email service and setting an expectation that its `sendEmail` method must be called with a specific user's email address.

**Libraries**: **Sinon.js** is the most popular library for creating all three types of test doubles when using Mocha. Jest has these capabilities built-in.

### Code Coverage

**Code coverage** is a metric that measures what percentage of your codebase is executed by your automated tests. It helps you identify parts of your application that are not being tested.[^18_11]

**Key Coverage Metrics** :[^18_11]

* **Statement Coverage**: Percentage of statements executed.
* **Branch Coverage**: Percentage of `if/else` and other control structure branches taken.
* **Function Coverage**: Percentage of functions called.

**How to Generate It**:

* **Jest**: Run Jest with the `--coverage` flag.
* **Mocha**: Use a tool like `nyc` (the successor to Istanbul) to instrument your code and generate a coverage report.[^18_11]

A high percentage doesn't guarantee your tests are good, but a low percentage is a clear sign that your application is under-tested.


</details>

---

<details>
  <summary>18: Performance Optimization</summary>

### **Section 18: Performance Optimization**
### Caching Strategies (in-memory, Redis) (IMP)

Caching involves storing frequently accessed data temporarily to reduce the need for expensive operations like database queries or external API calls.[^19_1]

* **In-Memory Caching**: The simplest strategy, where data is stored directly in the application's memory (e.g., in a global object or a `Map`).
  * **Pros**: Extremely fast access, no external dependencies.
  * **Cons**:
    * Cache is lost if the application restarts.
    * Not suitable for clustered environments, as each instance would have its own separate cache.[^19_2]
  * **Libraries**: `node-cache` is a popular choice for simple in-memory caching with features like TTL (time-to-live).[^19_2]
* **Distributed Caching (Redis)**: Uses an external, centralized cache like **Redis** that all application instances can share. Redis is an in-memory key-value store renowned for its speed, making it an excellent choice for a distributed cache.[^19_3][^19_2]
  * **Pros**:
    * Cache is shared across all application instances (clusters).[^19_1]
    * Cache persists even if one application instance restarts.
    * Provides advanced data structures and features.
  * **Cons**: Adds an external dependency and a network hop.

**Common Caching Pattern: Cache-Aside**

1. Application requests data.
2. It first checks the **cache** (e.g., Redis) for the data.
3. **Cache Hit**: If the data is found in the cache, it's returned immediately.
4. **Cache Miss**: If the data is not in the cache, the application queries the **database**, stores the result in the cache for future requests, and then returns the data.

### Clustering \& Load Balancing

* **Clustering**: The native `cluster` module allows a Node.js application to fork multiple worker processes, enabling it to utilize all available CPU cores on a machine. The master process distributes incoming requests among the workers (typically in a round-robin fashion), drastically improving the throughput of a single server.[^19_4][^19_5]
* **Load Balancing**: While clustering scales an application on a *single machine* (vertical scaling), a load balancer distributes incoming traffic across *multiple machines* (horizontal scaling). Tools like **NGINX** or cloud-native load balancers (e.g., AWS ELB) sit in front of your application servers and route requests to them, providing high availability and scalability.


### Worker Threads for CPU-bound tasks (IMP)

The Node.js event loop is excellent for I/O-bound tasks but struggles with CPU-bound tasks (e.g., complex calculations, image processing, encryption), as they block the single main thread and make the application unresponsive.[^19_6][^19_7]

**Worker Threads** are the solution. They allow you to run CPU-intensive JavaScript code in a separate thread without blocking the main event loop.[^19_8]

**Real-life Analogy (A CEO and an Analyst):**
A CEO (the main thread) shouldn't get bogged down doing a 10-hour financial analysis (a CPU-bound task). Instead, they delegate it to a financial analyst (a worker thread). While the analyst crunches the numbers, the CEO remains free to take calls and make decisions (handle I/O). When the analysis is done, the analyst hands a report back to the CEO.

```javascript
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  // This is the main thread. Offload the heavy task to a worker.
  const worker = new Worker(__filename);
  worker.on('message', (result) => {
    console.log(`Heavy task finished with result: ${result}`);
  });
  console.log('Main thread is still responsive and can do other things.');
} else {
  // This is the worker thread. Perform the CPU-intensive task.
  let result = 0;
  for (let i = 0; i < 1e9; i++) {
    result += i;
  }
  parentPort.postMessage(result); // Send the result back to the main thread
}
```


### Efficient Async Patterns

Using the right asynchronous pattern is key to performance.

* **Parallel Execution**: For independent asynchronous tasks, always run them in parallel with `Promise.all()`. Running them sequentially with `await` is a common performance bottleneck.

```javascript
// SLOW: Sequential
const user = await db.getUser(1);
const products = await db.getProducts();

// FAST: Parallel
const [user, products] = await Promise.all([
  db.getUser(1),
  db.getProducts()
]);
```

* **`Promise.allSettled`**: Use this if you need all operations to complete, even if some fail.
* **`Promise.any`**: Use this if you only need the result from the first operation that successfully completes.


### Avoiding Blocking the Event Loop

This is the single most important rule for Node.js performance. Any synchronous code that takes a long time to execute will block the entire application.[^19_9]

**What to Avoid in Production Servers:**

* **Synchronous I/O**: `fs.readFileSync()`, `fs.writeFileSync()`, etc.[^19_6]
* **Complex Calculations**: Long-running loops, complex regex, synchronous encryption/compression.
* **`JSON.parse()` and `JSON.stringify()` with large objects**: These are synchronous and can be surprisingly slow with large payloads.

**What to Do Instead:**

* Use asynchronous APIs for all I/O operations.[^19_6]
* Offload CPU-intensive tasks to **Worker Threads**.[^19_6]
* Break up long-running calculations into smaller chunks using timers (`setImmediate` or `setTimeout`) to yield to the event loop.


</details>

---

<details>
  <summary>19: Advanced Node.js Features</summary>

### **Section 19: Advanced Node.js Features**
### Worker Threads API

As covered in performance, **Worker Threads** are the standard way to handle CPU-intensive tasks in Node.js without blocking the main event loop. They allow for true parallel execution of JavaScript by running code in separate threads.[^20_1][^20_2]

**Key Concepts**:

* **Isolation**: Each worker has its own isolated V8 instance and event loop. They do not share memory by default, which prevents race conditions.[^20_3]
* **Communication**: The main thread and worker threads communicate by passing messages through a message channel (`postMessage`, `parentPort.on('message',...)`).[^20_4]
* **Memory Sharing**: For high-performance scenarios, memory can be shared explicitly using `SharedArrayBuffer` instances, but this requires careful management of concurrent access using tools like `Atomics`.[^20_5]

**Use Cases**:

* Image or video processing.
* Heavy cryptographic calculations.
* Large-scale data processing or analysis.
* Complex scientific or mathematical computations.


### Native Add-ons with Node-API (N-API)

For ultimate performance, you can write parts of your application in C or C++ and use them in Node.js as a **native add-on**. This allows you to leverage existing C/C++ libraries or write highly optimized code for performance-critical tasks.

* **Node-API (N-API)**: This is the modern, stable API for building native add-ons. It provides an **Application Binary Interface (ABI)** that is independent of the underlying JavaScript engine (V8).[^20_6]
* **ABI Stability**: The major advantage of N-API is that an add-on compiled for one version of Node.js will continue to work with later versions of Node.js without needing to be recompiled. This solves a major maintenance problem that existed with the older NAN (Native Abstractions for Node.js) approach.[^20_7]

**When to use Native Add-ons**:

* When you need to squeeze out every last drop of performance for a CPU-bound task and Worker Threads are not sufficient.
* When you need to integrate with an existing system library written in C or C++.


### Using WebAssembly in Node.js

**WebAssembly (Wasm)** is a binary instruction format for a stack-based virtual machine. It's designed as a portable compilation target for high-level languages like C, C++, and Rust, enabling you to run code on the web and on servers at near-native speed.[^20_8]

**Node.js has built-in support for WebAssembly**. You can load a `.wasm` module, instantiate it, and call its exported functions directly from your JavaScript code.[^20_9][^20_10]

**Wasm vs. Native Add-ons**:

* **Portability \& Security**: Wasm is more portable and secure. It runs in a sandboxed environment with a well-defined interface, whereas native add-ons have full access to the host system.
* **Performance**: Both offer significant performance gains over plain JavaScript. Native add-ons may have a slight edge as they have direct system access, but Wasm is very close.
* **Ease of Use**: Integrating Wasm is often simpler and safer than building and distributing native add-ons.

```javascript
// Example: Loading and running a .wasm file
const fs = require('fs');

const wasmBuffer = fs.readFileSync('./add.wasm');

// Instantiate the Wasm module
WebAssembly.instantiate(wasmBuffer).then(wasmModule => {
  const { add } = wasmModule.instance.exports;
  const sum = add(5, 10);
  console.log(sum); // 15
});
```


### Node.js Internals Deep Dive (V8, Libuv, C++)

Understanding the core components of Node.js can help you write better, more performant code.

* **V8 Engine**: Google's high-performance JavaScript engine written in C++. It compiles your JavaScript to native machine code.
* **Libuv**: A C library that provides the event loop and handles all asynchronous I/O operations (files, network, etc.) by interfacing with the underlying operating system. It manages the thread pool for heavy I/O and CPU-bound tasks.[^20_11][^20_12]
* **C++ Bindings \& Node.js Core API**: A layer of C++ code that acts as a "bridge" between your JavaScript code and the lower-level C/C++ libraries (like V8 and Libuv). When you call `fs.readFile()`, you are calling a JavaScript function in the Node.js core that, through these bindings, eventually calls a function in Libuv.[^20_11]


### Writing CLI Tools in Node.js

Node.js is an excellent platform for building cross-platform Command-Line Interface (CLI) tools.

**Key Steps \& Packages**:

1. **Parsing Arguments**: Use a library like **`commander`** or **`yargs`** to parse command-line arguments, create commands and sub-commands, and generate help text.[^20_13]
2. **Entry Point**: Create an entry file (e.g., `bin/index.js`) and make it executable. Add a `bin` field to your `package.json` to map your CLI command name to this file.[^20_14]

```json
"bin": {
  "my-cli-tool": "./bin/index.js"
}
```

3. **Shebang**: Add `#!/usr/bin/env node` to the top of your entry file. This tells the system to execute the file using the Node.js runtime.
4. **Styling Output**: Use a library like **`chalk`** to add color and styling to your terminal output, making it more user-friendly.[^20_13]
5. **User Interaction**: Use a library like **`inquirer`** to create interactive prompts (questions, lists, confirmations) for the user.


</details>

---

<details>
  <summary>20: Logging & Monitoring</summary>

### **Section 20: Logging \& Monitoring**
### Console vs. Structured Logging

* **Console Logging (`console.log`)**: Simple, string-based logging. It's great for quick debugging during development but is unsuitable for production.[^21_1]
  * **Problem**: Unstructured logs are difficult for machines to parse, making them hard to search, filter, and analyze in a production environment.[^21_1]
* **Structured Logging (IMP)**: A practice where logs are written in a consistent, machine-readable format, typically JSON. Each log entry contains key-value pairs of metadata (e.g., `timestamp`, `level`, `message`, `userId`, `requestId`).[^21_2][^21_3]
  * **Benefit**: Structured logs can be easily ingested, indexed, and queried by log management systems (like Splunk, Datadog, or the ELK stack), enabling powerful analysis, visualization, and alerting.[^21_2][^21_1]

```javascript
// Unstructured Log
console.log('User 42 failed to log in.');

// Structured Log
logger.warn({
  userId: 42,
  event: 'LOGIN_FAILURE',
  reason: 'Invalid password'
}, 'User failed to log in.');
```


### Winston, Pino, Bunyan Logging Frameworks

These are the most popular logging libraries for Node.js, all of which strongly support structured logging.[^21_4]


| Feature | Winston | Pino | Bunyan |
| :-- | :-- | :-- | :-- |
| **Philosophy** | Highly flexible and extensible with a large ecosystem of "transports." | Extremely fast and lightweight, focused on high-performance JSON logging . | Simple, JSON-based logging. One of the first to popularize structured logging in Node.js . |
| **Performance** | Good, but can be slower due to its flexible architecture . | **Excellent**. Often cited as the fastest logging library for Node.js . | Very good, but generally not as fast as Pino. |
| **Transports** | Core feature. Can log to console, files, databases, and external services simultaneously . | Core library logs only to standard output. Transports are handled by piping the output to separate processes. | Core library logs to a stream. Transports are managed by piping output. |
| **Best For** | Applications needing complex logging configurations and multiple output destinations . | High-performance applications where logging overhead must be minimal . | Applications where simple, reliable JSON logging is the primary requirement. |

![Comparison of Winston, Pino, and Bunyan logging frameworks in Node.js across key criteria.](https://ppl-ai-code-interpreter-files.s3.amazonaws.com/web/direct-files/0693c2bf4216e8b1012de0032ac5a8fe/d8592423-d8ee-47db-a652-ede0674add67/2c5673b4.png)

Comparison of Winston, Pino, and Bunyan logging frameworks in Node.js across key criteria.

### Request Tracking \& Correlation IDs

In a microservices architecture, a single user request might travel through multiple services. To trace its entire journey, we use a **Correlation ID** (also known as a Trace ID).[^21_5]

* **How it works**:

1. When a request first enters your system, a unique ID is generated (e.g., a UUID).
2. This ID is attached to the request, often as an HTTP header (e.g., `X-Request-ID`).[^21_5]
3. Every service that handles this request includes this correlation ID in all of its log entries related to that request.[^21_5]
4. When making calls to other services, it passes the ID along in the headers.
* **Benefit**: You can filter your centralized logs by this one ID to see the complete, end-to-end lifecycle of a single request across all services, making debugging distributed systems much easier.[^21_6]


### Monitoring with PM2, Forever, or Nodemon

These tools are process managers that help run and monitor your Node.js application.

* **Nodemon**: A **development-only** tool that automatically restarts your application whenever it detects file changes in your project. It is not meant for production.[^21_7]
* **Forever**: A simple CLI tool for ensuring a script runs continuously (i.e., forever). It will automatically restart the script if it crashes.
* **PM2 (IMP)**: A production-ready process manager for Node.js. It's feature-rich and is the de-facto standard for running Node.js applications in production.[^21_8]
  * **Key Features**:
    * **Auto-Restart**: Restarts the app on crash or server reboot.[^21_8]
    * **Clustering**: Built-in load balancer that runs your app on all available CPU cores (`-i max`).[^21_8]
    * **Log Management**: Gathers logs from all clustered processes into one place.
    * **Monitoring**: Provides a command-line dashboard to monitor CPU and memory usage (`pm2 monit`).
    * **Zero-Downtime Reloads**: Allows you to reload your application with new code without dropping any connections.[^21_8]


### Metrics with Prometheus \& Grafana

While logs record discrete events, **metrics** are numerical measurements taken over time (e.g., CPU usage, memory consumption, request latency).

* **Prometheus**: An open-source monitoring and alerting toolkit. It works by "scraping" a metrics endpoint on your application at regular intervals to collect time-series data.[^21_9][^21_10]
* **Grafana**: An open-source visualization tool. It connects to data sources like Prometheus to create powerful, interactive dashboards for visualizing your metrics and creating alerts.[^21_11][^21_9]

**The Workflow**:

1. **Instrument Your App**: Use a library like `prom-client` to create an HTTP endpoint (e.g., `/metrics`) in your Node.js app that exposes metrics in the Prometheus format.
2. **Configure Prometheus**: Set up a Prometheus server to periodically scrape the `/metrics` endpoint of your application instances.
3. **Visualize in Grafana**: Connect Grafana to your Prometheus server as a data source and build dashboards to monitor your application's health and performance in real-time.


</details>

---

<details>
  <summary>21: Deployment & Scaling</summary>

### **Section 22: Real-Time Applications**

### WebSockets with `ws` or Socket.IO (IMP)

- **WebSocket** is a protocol for full-duplex, low-latency communication between client and server—ideal for chat apps, games, notifications, and collaborative tools.
- `ws` is a lightweight Node.js WebSocket library for basic use-cases.
- **Socket.IO** builds on WebSockets, adding fallback transports (for old browsers), automatic reconnection, event-based messaging, rooms/groups, and easy binary/message serialization.[^23_1][^23_2]

**WebSocket Example:**
Server

```javascript
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (msg) => ws.send(`Server received: ${msg}`));
});
```

Client

```javascript
const ws = new WebSocket('ws://localhost:8080');
ws.on('open', () => ws.send('Hello Server!'));
ws.on('message', (data) => console.log('Received:', data));
```

**Socket.IO Example:**

```javascript
const server = require('http').createServer();
const io = require('socket.io')(server);

io.on('connection', (socket) => {
  socket.emit('newMessage', { text: 'Welcome!' });
  socket.on('createMessage', (msg) => io.emit('newMessage', msg));
});
server.listen(3000);
```

**Comparison Table: ws vs Socket.IO**


| Feature | ws | Socket.IO |
| :-- | :-- | :-- |
| Pure WebSockets | Yes | No (uses various transports) |
| Fallbacks | No | Yes |
| Event API | Basic | Advanced |
| Rooms/Groups | Manual | Built-in |
| Reconnection | Manual | Built-in |
| Use Cases | Simple | Complex |


***

### Server-Sent Events (SSE)

- SSE allows server → browser (one-way) data streaming over HTTP.
- Each client makes a simple HTTP request, the server holds connection open and pushes updates as plain text.
- Used for notifications, live feeds, system events.[^23_3][^23_4][^23_5]

**Server Example:**

```javascript
// Express route for SSE
app.get('/events', (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  setInterval(() => res.write(`data: ${Date.now()}\n\n`), 1000);
});
```

**Client Example:**

```javascript
const es = new EventSource('/events');
es.onmessage = ({ data }) => console.log('Received:', data);
```


***

### Real-Time Data Sync Patterns

- **Client-Server Sync:** All devices connect to a central server, which pushes updates to all connected clients when the data changes (e.g., Firebase real-time DB, Socket.IO, custom WebSocket server).[^23_6][^23_7]
- **Peer-to-Peer (P2P) Sync:** Devices communicate directly (e.g., with WebRTC). Used for low-latency mesh networks, decentralized collaboration. Requires careful handling of concurrency and conflict resolution.[^23_7]

**Best Practices:**

- Always handle network failures and reconnections gracefully.
- Implement concurrency control for shared data (e.g., transactions, timestamps).

***

</details>

---

<details>
  <summary>23: Message Queues & Event-Driven Architecture</summary>

### **Section 23: Message Queues \& Event-Driven Architecture**
### RabbitMQ, Kafka Integration with Node.js (IMP)

**Why Message Queues?**
Used to decouple and scale microservices, smooth traffic spikes, and guarantee delivery of critical events in distributed systems.

**RabbitMQ**

- Follows AMQP protocol (has exchanges, queues, producers, consumers, bindings).
- Popular for job queues, order/event pipelines, async tasks (emails, notifications).
- Use the `amqplib` or `rabbitmq-nodejs-client` npm package.[^24_1]

```javascript
// Producer with amqplib
const amqp = require('amqplib');
(async () => {
  const conn = await amqp.connect('amqp://localhost');
  const channel = await conn.createChannel();
  await channel.assertQueue('order_queue');
  channel.sendToQueue('order_queue', Buffer.from(JSON.stringify({orderId: 1})));
})();
```

- **Benefits:** Built-in retries, dead lettering, prioritization, rate limiting.[^24_2]

**Kafka** (IMP for streaming)

- Distributed event log. Handles massive throughput, partitioned topics for scale.
- Use the `kafkajs` package.[^24_3][^24_4]

```javascript
const { Kafka } = require('kafkajs');
const kafka = new Kafka({ clientId: 'app', brokers: ['localhost:9092'] });
const producer = kafka.producer();
await producer.connect();
await producer.send({ topic: 'logs', messages: [{ value: 'event data' }] });
// Consume with a consumer group for scale/out-of-order processing.
```

- **Benefits:** Durability, partitions for concurrent processing, stream data pipelines.
- **Comparison:** Kafka excels at event streams and analytics; RabbitMQ is simpler for task queues and workflows.[^24_5][^24_2]

***

### Using Redis Pub/Sub

- Redis Pub/Sub is very simple: producers (publishers) send messages to a channel, subscribers (consumers) listen for them.[^24_6][^24_7][^24_8]
- Not persistent (if the consumer is offline, the message is lost); best for real-time signals, non-critical events, and chat.

**Example:**

```javascript
const redis = require('redis');
const pub = redis.createClient();
const sub = redis.createClient();
sub.subscribe("chat");
sub.on("message", (chan, msg) => console.log(`${chan}: ${msg}`));
pub.publish("chat", "Hello Redis!");
```


***

### Event Sourcing Patterns

- **What:** Instead of storing the current state, you store all state-changing events; rebuild state by re-playing events.[^24_9][^24_10]
- **Benefits:** Complete audit log, easily undo/redo actions, time-travel queries, powerful for CQRS (Command Query Responsibility Segregation).[^24_11][^24_12]
- **Node.js Example:**

```javascript
const events = [
  { type: "open", id: "a1", balance: 150 },
  { type: "transfer", fromId: "a1", toId: "a2", amount: 50 }
];
const accounts = events.reduce((acc, evt) => {
  // apply logic based on event type
  // ...
  return acc;
}, {});
```

- **Real-life Analogy:** Like an accounting ledger—never overwrite, just append; current balance is computed by summing up all transactions.

</details>

---

<details>
  <summary>24: GraphQL with Node.js</summary>

### **Section 24: GraphQL with Node.js**

### Setting Up Apollo Server

- **Apollo Server** is a popular tool for building GraphQL APIs in Node.js.
- **Basic steps:**

1. Initialize your project and install dependencies:

```bash
npm init -y
npm install @apollo/server graphql
```

2. Define your schema using the GraphQL schema language (`typeDefs`).
3. Implement resolvers—plain JS functions for each field.
4. Start the server:

```javascript
import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';

const server = new ApolloServer({ typeDefs, resolvers });
const { url } = await startStandaloneServer(server, { listen: { port: 4000 } });
console.log(`🚀 Server ready at: ${url}`);
```


***

### Schema \& Resolvers (IMP)

- **Schema:** Defines the types, queries, and mutations clients can use.
- **Resolvers:** Functions providing logic for fetching/modifying data for each field.

```javascript
// Example typeDefs and resolvers
const typeDefs = `type Query { hello: String }`;
const resolvers = {
  Query: {
    hello: () => "Hello world!",
  },
};
```

- Resolvers can return sync or async results, make DB/API calls, batch data via [DataLoader].[^25_1][^25_2]

***

### Query Batching \& Caching

- **Batching:** Combine multiple queries into a single request/build fragments for efficiency (DataLoader is common for grouping DB requests).[^25_3][^25_4]
- **Caching:** Store results from expensive queries (in-memory, Redis, persisted queries) to boost performance and scalability.[^25_4]
- Apollo Server and Apollo Client have built-in support for caching and query persistence. Fine-tune caching behavior to fit your data (e.g., cache per-user queries, invalidate cache on mutation).[^25_5]

***

### Real-Time GraphQL with Subscriptions (IMP)

- **GraphQL Subscriptions** enable server → client, real-time updates on specific events (e.g., new messages, data changes).[^25_6][^25_7][^25_8]
- Implemented via **WebSockets** in Apollo Server.
- Clients send a subscription query specifying the event to listen for; server pushes updates when those events happen.

**Example:**

```javascript
const { PubSub } = require('graphql-subscriptions');
const pubsub = new PubSub();

const typeDefs = `
  type Message { text: String! }
  type Subscription { newMessage: Message }
`;

const resolvers = {
  Subscription: {
    newMessage: {
      subscribe: () => pubsub.asyncIterator(['MESSAGE_CREATED']),
    },
  },
};
```

**Best Practices:**

- Secure written queries/mutations to prevent abuse.
- Use fragments for maintainable, re-usable queries.[^25_9]
- Apply field-level resolvers and business logic only once per request to avoid duplicate computations.

***


</details>

---

<details>
  <summary>25: Node.js in Microservices</summary>

### **Section 25: Node.js in Microservices**
### Service Communication Patterns (HTTP, gRPC, Messaging) (IMP)

- **HTTP/REST:** Most popular for synchronous communication (request/response). Easy, widely supported, but can be slow for "chatty" services.[^26_1]
- **gRPC:** High-performance, strongly-typed protocol over HTTP/2. Uses Protocol Buffers for efficient serialization; supports streaming and bi-directional communication. Use libraries like `@grpc/grpc-js` in Node.js.[^26_2][^26_3][^26_4][^26_5][^26_6]
- **Messaging (RabbitMQ, Kafka, Redis):** For async, decoupled flows (events, job queues). Allows reliable communication and scalability with eventual consistency.[^26_1]

| Pattern | Use Case | Libraries |
| :-- | :-- | :-- |
| REST/HTTP | User-facing endpoints, easy integration | Express, Axios |
| gRPC | Service-to-service, streaming, efficiency | @grpc/grpc-js |
| Messaging | Jobs, events, pub/sub | amqplib, kafkajs, ioredis |


***

### Service Discovery

Microservices should NOT use hardcoded URLs. **Service discovery** ensures services can find each other dynamically, usually via a registry (Consul, etcd, DNS SRV).[^26_7][^26_8][^26_9]

- **Client-side discovery:** Service registry maintains service instances; clients fetch and balance.[^26_7]
- **Server-side discovery:** Router or load balancer directs requests; often used with API gateway.[^26_7]

**Example: Using Consul with Node.js**

```javascript
import consul from 'consul';
const consulClient = consul();
consulClient.agent.service.register({ name: 'order-service', port: 3004 });
consulClient.health.service({ service: 'order-service', passing: true }, (err, result) => {
  // Get healthy instance details dynamically
});
```


***

### API Gateway Integration

An **API gateway** is the front door for microservices. Key features :[^26_10][^26_11][^26_12]

- Centralizes authentication, rate-limiting, and routing.
- Can aggregate responses from multiple microservices.
- Popular tools: Kong, AWS API Gateway, custom Node.js (with `http-proxy-middleware`, Express).

**Benefits:** Simplifies clients, enhances security, scales easily, enables monitoring.

***

### Distributed Tracing (Jaeger, OpenTelemetry) (IMP)

Modern microservice apps need **observability**—tracking requests as they flow across dozens of services.

- **OpenTelemetry:** Standard instrumentation API for Node.js; traces requests, collects metrics, propagates context.[^26_13][^26_14][^26_15][^26_16]
- **Jaeger:** Popular backend for storing and visualizing trace data; helps debug latency, bottlenecks, failures.

**How to use:**

- Instrument your code with OpenTelemetry:

```bash
npm install @opentelemetry/sdk-node @opentelemetry/api
```

- Export traces to Jaeger, Zipkin, or built-in dashboards.[^26_15][^26_13]


</details>

---

<details>
  <summary>26: Advanced Build & Tooling</summary>

### **Section 26: Advanced Build \& Tooling**
### Babel \& SWC with Node.js (IMP)

- **Babel:** Long-time standard for JavaScript transpilation (ES2015+ to ES5), TypeScript, React JSX, feature polyfills. Highly extensible, slower for large codebases.
- **SWC:** Fast Rust-based alternative. Up to 20-70x faster than Babel for transpilation/minification. Ideal for monorepos and large-scale apps.[^27_1][^27_2][^27_3][^27_4]
- **Config Example for SWC:**

```json
{
  "jsc": { "parser": { "syntax": "ecmascript", "jsx": true } },
  "module": { "type": "commonjs" }
}
```

**Use Cases:**

- Next.js and Vite use SWC for blazing fast builds.
- Migration from Babel to SWC is usually drop-in for most use cases.[^27_4]

***

### ES Module Transpilation

- Node.js natively supports ES Modules using `.mjs` extension or `"type": "module"` in `package.json` (since v12+, better in v14+).[^27_5][^27_6]
- Transpilation (via Babel, SWC, Webpack) is still useful for:
  - Using latest JS features on older Node.js versions/browsers.[^27_7]
  - Converting TypeScript and JSX to JS.

***

### Code Linting \& Formatting (ESLint, Prettier) (IMP)

- **ESLint:** Checks code for errors, bugs, style violations, and enforces code standards.[^27_8]
- **Prettier:** Automatic code formatter—ensures consistent style, eliminates debates about tabs vs spaces.[^27_9][^27_10][^27_11]
- **Combined Workflow:** Run both together for max code quality.

```json
// package.json scripts section
{
  "scripts": {
    "format:write": "prettier --write .",
    "lint:fix": "eslint --fix ."
  }
}
```

- **Best Practice:** Use VSCode extensions for real-time lint/format on save.

***

### Monorepo Setup with Nx or Turborepo (IMP)

- **Monorepo:** Repo structure where multiple services/packages (backend, frontend, shared libs) live in one codebase.[^27_12][^27_13][^27_14]
- **Nx:** Powerful monorepo framework with advanced caching, dependency graphs, workspace management. Used for fullstack React/Node apps, microservices.[^27_15][^27_13]
- **Turborepo:** High-speed task runner and build pipeline for JS/TS monorepos. Great caching, easy parallel builds, integrates with Vercel CI/CD.[^27_14][^27_12]
- **Setup Flow:**

1. Init: `npx lerna init` or `npx nx init` or `npm install turbo -D`
2. Define tasks/pipelines in `nx.json` or `turbo.json`.
3. Cacheable operations: `build`, `test`, `lint`.[^27_15]
4. Use workspaces and dependency graphs for fast builds.[^27_12]

***

</details>

---

<details>
  <summary>27: Maintenance & Upgrades</summary>

### **Section 27: Maintenance \& Upgrades**
### LTS vs Current Releases in Production (IMP)

- **LTS (Long Term Support):** For stability, security, and backwards compatibility. No new features or breaking changes after initial release. Ideal for production environments; receives critical patches and maintenance for years.[^28_1][^28_2][^28_3][^28_4][^28_5][^28_6]
- **Current:** New features and improvements, but can contain breaking changes. Suited for experimentation and testing upcoming features. Not recommended for most production deployments.[^28_4]

**Release Cycle:**

- Even-numbered major versions (e.g., v18, v20, v22) → transition to LTS.
- Node.js maintains around 3 supported versions at any time: Current, Active LTS, Maintenance LTS.[^28_4]

***

### Handling Node.js Version Migrations (IMP)

- **Why Upgrade?**
  - Security patches, performance improvements, support for new JS features, avoid EOL risks.[^28_7]
- **Best Practices:**

1. **Upgrade to LTS only:** Always move to an even-numbered LTS version for production use.[^28_8]
2. **Use nvm for local dev:** Easily test and switch between versions.
3. **Back up your code and data before upgrading.**
4. **Read the official migration/changelog** for breaking changes before upgrading.[^28_9][^28_8]
5. **Upgrade incrementally:** Move one major version at a time if coming from far behind.
6. **Run your full test suite and check all deployment/CI scripts after upgrading Node.**[^28_7][^28_9]
7. **Update scripts/configs** (like Dockerfiles, CI/CD, Netlify, Heroku, etc.) to reflect the new version.[^28_8]
8. If you need a different `npm` version, set an explicit `NPM_VERSION` in your workflow.[^28_8]

***

### Dependency Upgrade Strategies (IMP)

- **Why it's hard:** Dependency trees get complex; breaking changes in one library can cause “dependency hell.” Some packages may be abandoned or not yet compatible with new Node.js versions.[^28_10][^28_11]
- **Upgrade approach:**

1. **Audit your dependencies regularly (`npm audit`).**
2. Use `npm outdated` to check which packages have updates.
3. Upgrade dependencies one by one, testing each time (not all at once). Start with crucial or outdated ones.[^28_12][^28_9]
4. Use comprehensive automated tests to catch regressions.
5. For monorepos, upgrade shared libs first before services that depend on them.
6. Record issues and fixes for future upgrades.[^28_9][^28_12]
- **Automate:** Integrate tools like Dependabot or Renovate for scheduled dependency updates.
- **Fallback:** If a dependency is abandoned, look for a maintained fork, patch it yourself, or refactor to replace it.


</details>

<details>
  <summary>28: Real-World Project Architecture</summary>

### **Section 28: Real-World Project Architecture**
### Layered Architecture in Node.js Apps (IMP)

- **Three Core Layers:**
  - **Router/Controller Layer:** Handles HTTP routing and request parsing.
  - **Service Layer:** Business logic (validation, processing, workflows).
  - **Data Access Layer (DAL)/Repository:** All DB access, queries, ORM code.[^29_1][^29_2][^29_3][^29_4]
- **Benefits:** Separation of concerns, testability, maintainability. Adopt high cohesion and low coupling.[^29_3]
- **Example Structure:**

```
├── routes/
├── services/
├── repositories/
└── models/
```


***

### Clean Architecture \& Hexagonal Patterns

- **Clean Architecture:** Separates domain (business logic) from frameworks, databases, and UI. Independent core, easy swapping of infrastructure.
- **Hexagonal Architecture (Ports \& Adapters):**
  - *Core Logic* lives in the center (“hexagon”).
  - *Adapters* (for DB, HTTP, messaging) interact via interfaces called *Ports*.
  - Easily change tech stack, isolated testability, loose coupling.[^29_5][^29_6][^29_7][^29_8][^29_9]
- **Benefit:** Prevents codebase rot and dependency spaghetti.

***

### Monolith vs Microservices vs Serverless (IMP)

- **Monolith:** Everything in one repo/process. Simple, low initial cost, direct communication. Painful to scale, slow to iterate/manage big teams.[^29_10][^29_11][^29_12][^29_13]
- **Microservices:** Split app into independent processes/services. Each service owns data, API, scaling. Brings flexibility, scale, but complexity (DevOps, monitoring, coordination).[^29_11][^29_10]
- **Serverless:** Code as functions, not always running. Cloud runs, bills per use (e.g., AWS Lambda). Superb for periodic/spiky workloads. Cold starts, latency, and debugging are challenges.[^29_10][^29_11]

| Pattern | Pros | Cons | When to Use |
| :-- | :-- | :-- | :-- |
| Monolith | Simple, Fast Dev | Hard to scale/iterate | Small teams, MVPs |
| Microservices | Scalability, Team | Complex Infra, Overhead | Large teams, mixed workloads |
| Serverless | Cost, Autoscale | Startup lag, less control | Sporadic or bursty workloads |

**Migration:** Start monolithic. Move features/services out piece-by-piece as you grow.[^29_10]

***

### Multi-Tenant App Design in Node.js

- **Multi-tenancy:** Serve multiple organizations/users from one app, data/app isolation for each “tenant”.[^29_14][^29_15][^29_16]
- **Models:**
  - *Shared DB, Shared Schema:* Fastest, but harder to secure.
  - *Shared DB, Schema-per-tenant:* Balanced approach.
  - *DB-per-tenant:* Best isolation, highest infra cost.[^29_15][^29_16]
- **Security:** Isolate tenant data, strong RBAC/auth, secrets per tenant.
- **Customization:** Branding, features per client via feature flags/config.[^29_14]

**Best Practice:** Choose based on your target users (SMB vs Enterprise) and growth expectations.


</details>