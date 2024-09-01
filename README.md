# Node_js

Node js is a javascript run time environment to run the javascript outside the browser by using v8 engine to create backend. It is open source with some additional features that helps to create server or backend of an application. 

## What is a runtime?
## res.params vs res.query?
## Body-parser and its functionality and features?
## Explain the default security mechanism in node js?


# What you should know.

1. Javascript
2. Node.js(foundational part)
3. Node installed
4. VS code (free for any language)



## Strucutre of Node js.

```scss
global
│
├── Global Functions
│   ├── setTimeout(callback, delay[, ...args])
│   ├── clearTimeout(timeoutObject)
│   ├── setInterval(callback, delay[, ...args])
│   ├── clearInterval(intervalObject)
│   ├── setImmediate(callback[, ...args])
│   ├── clearImmediate(immediateObject)
│   ├── queueMicrotask(callback)
│   ├── require(id)
│   ├── module.exports
│   ├── exports
│   └── process.nextTick(callback[, ...args])
│
├── Global Variables
│   ├── __dirname
│   ├── __filename
│   └── globalThis (reference to the global object itself)
│
├── Global Objects
│   ├── process
│   │   ├── argv (Command-line arguments)
│   │   ├── env (Environment variables)
│   │   ├── cwd() (Current working directory)
│   │   ├── exit([code]) (Exit the process)
│   │   ├── nextTick(callback[, ...args]) (Defer the execution of a function)
│   │   ├── stdout (Standard output stream)
│   │   ├── stderr (Standard error stream)
│   │   └── stdin (Standard input stream)
│   │
│   ├── console
│   │   ├── log([data, ...args])
│   │   ├── error([data, ...args])
│   │   ├── warn([data, ...args])
│   │   ├── info([data, ...args])
│   │   ├── debug([data, ...args])
│   │   └── dir(obj[, options])
│   │
│   ├── Buffer
│   │   ├── from(string[, encoding])
│   │   ├── alloc(size[, fill[, encoding]])
│   │   ├── allocUnsafe(size)
│   │   └── byteLength(string[, encoding])
│   │
│   ├── globalThis
│   │   ├── Reflect
│   │   ├── Symbol
│   │   ├── Object
│   │   └── Function
│   │
│   └── module
│       ├── exports (Alias for module.exports)
│       ├── id (The identifier for the module)
│       ├── filename (The fully resolved filename of the module)
│       ├── loaded (Whether the module is loaded)
│       ├── parent (The module that required this one)
│       └── children (The list of children modules)
│
├── Global Symbols
│   ├── Symbol.iterator
│   ├── Symbol.asyncIterator
│   └── Symbol.hasInstance
│
└── Additional Globals
    ├── setTimeout (Redundant; same as global.setTimeout)
    ├── clearTimeout (Redundant; same as global.clearTimeout)
    ├── setInterval (Redundant; same as global.setInterval)
    ├── clearInterval (Redundant; same as global.clearInterval)
    ├── setImmediate (Redundant; same as global.setImmediate)
    ├── clearImmediate (Redundant; same as global.clearImmediate)
    ├── queueMicrotask (Redundant; same as global.queueMicrotask)
    ├── URL (Used for parsing URLs)
    ├── URLSearchParams (Used for working with URL query strings)
    └── TextDecoder, TextEncoder (Used for encoding and decoding text)

```



| **Category**           | **Functions/Methods/Properties**                                                                                         |
|------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Global Functions**   | `setTimeout(callback, delay[, ...args])`                                                                                  |
|                        | `clearTimeout(timeoutObject)`                                                                                            |
|                        | `setInterval(callback, delay[, ...args])`                                                                                 |
|                        | `clearInterval(intervalObject)`                                                                                           |
|                        | `setImmediate(callback[, ...args])`                                                                                       |
|                        | `clearImmediate(immediateObject)`                                                                                         |
|                        | `queueMicrotask(callback)`                                                                                                |
|                        | `require(id)`                                                                                                             |
|                        | `module.exports`                                                                                                          |
|                        | `exports`                                                                                                                 |
|                        | `process.nextTick(callback[, ...args])`                                                                                   |
| **Global Variables**   | `__dirname`                                                                                                               |
|                        | `__filename`                                                                                                              |
|                        | `globalThis` (reference to the global object itself)                                                                      |
| **Global Objects**     | `process`                                                                                                                 |
|                        | ├── `argv` (Command-line arguments)                                                                                       |
|                        | ├── `env` (Environment variables)                                                                                         |
|                        | ├── `cwd()` (Current working directory)                                                                                   |
|                        | ├── `exit([code])` (Exit the process)                                                                                     |
|                        | ├── `nextTick(callback[, ...args])` (Defer the execution of a function)                                                   |
|                        | ├── `stdout` (Standard output stream)                                                                                     |
|                        | ├── `stderr` (Standard error stream)                                                                                      |
|                        | └── `stdin` (Standard input stream)                                                                                       |
|                        |                                                                                                                           |
|                        | `console`                                                                                                                 |
|                        | ├── `log([data, ...args])`                                                                                                |
|                        | ├── `error([data, ...args])`                                                                                              |
|                        | ├── `warn([data, ...args])`                                                                                               |
|                        | ├── `info([data, ...args])`                                                                                               |
|                        | ├── `debug([data, ...args])`                                                                                              |
|                        | └── `dir(obj[, options])`                                                                                                 |
|                        |                                                                                                                           |
|                        | `Buffer`                                                                                                                  |
|                        | ├── `from(string[, encoding])`                                                                                            |
|                        | ├── `alloc(size[, fill[, encoding]])`                                                                                     |
|                        | ├── `allocUnsafe(size)`                                                                                                   |
|                        | └── `byteLength(string[, encoding])`                                                                                      |
|                        |                                                                                                                           |
|                        | `globalThis`                                                                                                              |
|                        | ├── `Reflect`                                                                                                             |
|                        | ├── `Symbol`                                                                                                              |
|                        | ├── `Object`                                                                                                              |
|                        | └── `Function`                                                                                                            |
|                        |                                                                                                                           |
|                        | `module`                                                                                                                  |
|                        | ├── `exports` (Alias for `module.exports`)                                                                                |
|                        | ├── `id` (The identifier for the module)                                                                                  |
|                        | ├── `filename` (The fully resolved filename of the module)                                                                |
|                        | ├── `loaded` (Whether the module is loaded)                                                                               |
|                        | ├── `parent` (The module that required this one)                                                                          |
|                        | └── `children` (The list of children modules)                                                                             |
| **Global Symbols**     | `Symbol.iterator`                                                                                                         |
|                        | `Symbol.asyncIterator`                                                                                                    |
|                        | `Symbol.hasInstance`                                                                                                      |
| **Additional Globals** | `setTimeout` (Redundant; same as `global.setTimeout`)                                                                     |
|                        | `clearTimeout` (Redundant; same as `global.clearTimeout`)                                                                 |
|                        | `setInterval` (Redundant; same as `global.setInterval`)                                                                   |
|                        | `clearInterval` (Redundant; same as `global.clearInterval`)                                                               |
|                        | `setImmediate` (Redundant; same as `global.setImmediate`)                                                                 |
|                        | `clearImmediate` (Redundant; same as `global.clearImmediate`)                                                             |
|                        | `queueMicrotask` (Redundant; same as `global.queueMicrotask`)                                                             |
|                        | `URL` (Used for parsing URLs)                                                                                             |
|                        | `URLSearchParams` (Used for working with URL query strings)                                                               |
|                        | `TextDecoder`, `TextEncoder` (Used for encoding and decoding text)                                                        |








