# node-nam-dev
**********************Itroduction**************
Node js
    - its a java script run time build on cromes v8 engin 
    -Cross platform- run on different os
    - it is open sourece maintained by openjs
    -it help to run js outside of browser
    -it has event driver architecture 
    -it capable of async io also know as non blocking io


******************02 JS on server*******************
![Alt text]('../note-image/node js.jpg)
Q: What is a server?
        A server is essentially a remote computer. You can think of it as a computer
        whose CPU works remotely.
        Servers can be accessed over a network to provide resources and services to
        other computer programs.
        A server is a computer or system that provides data, services, resources, or
        programs to other computers, known as clients, over a network.
        Behind the scenes, when a computer needs to communicate with a server, it
        sends a request to the server using its IP address. Initially, JavaScript could only
        be executed within web browsers, limiting its use to client-side tasks. However,
        with the introduction of Node.js, JavaScript can now also be executed on servers,
        allowing developers to use the same language for both client-side and server-side
        programming

Q: What is v8
    -The V8 JavaScript engine is written in C.
   - V8 can be embedded into any C program, which is a crucial feature.
    The process works as follows: JavaScript code is executed by V8 (written in
    C, which then compiles it down to machine code that the computer can
    execute.


            NODEJS is a c++ application with v8 embedded into it
            ECMAScript is a standard for scripting languages, including JavaScript,
            JScript, and ActionScript. It is best known as the standard that defines
            JavaScript.
            ECMAScript standards are followed by JavaScript engines like V8,
            SpiderMonkey, Chakra, and others to ensure consistent behavior across
            different environments.
            so , v8 engines has to follow this ECMA standards. and node.js has v8
            engines, but node.js also has some superpowers, such as api calls on servers,
            which make it more powerful than v8 engines alone, which cannot do
            database connections, api calls, etc. because of ECMA standards. and this is
            known as the JS runtime.
            V8 is C code.


*********************Modules EP4*******************************
Module protect there variable and function from leaking 
to use those variable and function need to use `module.export = fun/var name`
and need to import where we want to use eg const fun/var name = require('path')

Q: How do you make two modules work together?
    -using a require function

Q: What is the required function?
    -In Node.js, the require() function is a built-in function that allows you to include or
    require other modules into your main modules.

Diff between        common js module        and        ES Module
                1) module export required        1)import export
                2)By default used by node js     2) by default used by fretwork like angular react
                3)Older way                      3) Newer way
                4)Synchronous                    4)async
                5)Not strict                     5)Strict


Synchronous vs. Asynchronous: CommonJS requires modules in a
synchronous manner, meaning the next line of code will execute only after the
module has been loaded. In contrast, ES modules load modules
asynchronously, allowing for more efficient and flexible code execution. 
Strict Mode: Another significant difference is that CommonJS code runs in
non-strict mode, while ES modules execute in strict mode. This means that ES
modules enforce stricter parsing and error handling, making them generally
safer and more reliable.



*********************Modules EP5*******************************
Module in depth
        Modules in Node.js work similarly to function scopes. When you require a file,
    Node.js wraps the code from that file inside a function. This means that all
    variables and functions in the module are contained within that functions
    scope and cannot be accessed from outside the module unless explicitly
    exported.
        To expose variables or functions to other modules, you use module.exports . This
    allows you to export specific elements from the module, making them
    accessible when required elsewhere in your application.
    All the code of a module is wrapped inside a function when you call require .
    This function is not a regular function; its a special type known as an IIFE
    (Immediately Invoked Function Expression). Heres how it works:



   #In Node.js, before passing the code to the V8 engine, it wraps the module code inside an IIFE. The purpose of IIFE is to:
        Immediately Invoke Code: The function runs as soon as it is defined.
        Keep Variables and Functions Private: By encapsulating the code within the
        IIFE, it prevents variables and functions from interfering with other parts of the
        code. This ensures that the code within the IIFE remains independent and
        private.
        Using IIFE solves multiple problems by providing scope isolation and immediate
        execution.
Q2: How do you get access to module.exports ? Where does this
    module come from?
        In Node.js, when your code is wrapped inside a function, this function has a parameter named module . 
        This parameter is an object provided by Node.js that includes module.exports .

        `When you use module.exports , you're modifying the exports object of the current
        module. Node.js relies on this object to determine what will be exported from the
        module when it's required in another file.
        The module object is automatically provided by Node.js and is passed as a
        parameter to the function that wraps your code. This mechanism allows you to
        define which parts of your module are accessible externally.`

How require() Works Behind the Scenes
     Resolving the Module
        Node.js first determines the path of the module. It checks whether the
        path is a local file ( ./local ), a JSON file ( .json ), or a module from the
        node_modules directory, among other possibilities.
     Loading the Module
        Once the path is resolved, Node.js loads the file content based on its type.
        The loading process varies depending on whether the file is JavaScript,
     Wrapping Inside an IIFE
        The module code is wrapped in an Immediately Invoked Function
        Expression IIFE. This wrapping helps encapsulate the module's scope,
        keeping variables and functions private to the module.
     Code Evaluation and Module Exports
        After wrapping, Node.js evaluates the modules code. During this
        evaluation, module.exports is set to export the module's functionality or
        data. This step essentially makes the module's exports available to other
        files.
     Caching(very imp)
        Importance: Caching is crucial for performance. Node.js caches the result
        of the require() call so that the module is only loaded and executed once.

**************************libuv and async i/o EP6*****************************************
Q: What type of threading does JavaScript use?
   - JavaScript is a synchronous, single-threaded language, meaning there is only
    one thread in which the JavaScript engine (such as the V8 engine) runs. In
    JavaScript, code is executed line by line within this single thread.
   - In other languages like C++ or Java, code can be executed across multiple
    threads. For example, a portion of the code might be executed in one thread,
    while another part runs simultaneously in a different thread. However,
    JavaScript handles this process more straightforwardly—executing code one
    line after the other in sequence.
   - So, if you're executing line 2 in JavaScript, it will only run after line 1 has
    finished executing. This is the essence of synchronous execution: each task is
    performed one after the other, without overlap.


                `JavaScript itself is synchronous, but with the power of Node.js, it can
            handle asynchronous operations, allowing JavaScript to perform multiple tasks
            concurrently.`
Q: what are the portions inside the JS engine and How synchronous code is executed By JS Engine ?
A:
    The JavaScript engine operates with a single call stack, and all the code you
    write is executed within this call stack. The engine runs on a single thread,
    meaning it can only perform one operation at a time.
    8In addition to the call stack, the JavaScript engine also includes a memory
    heap. This memory heap stores all the variables, numbers, and functions that
    your code uses.
    One key feature of the JavaScript V8 engine is its garbage collector. The
    garbage collector automatically identifies and removes variables that are no
    longer in use, freeing up memory. Unlike languages like C++, where
    developers need to manually allocate and deallocate memory, JavaScript
    handles this process automatically. This means you don't have to worry about
    memory management—it's all taken care of by the engine.


    #LIBUV
        The JS engine cannot directly access OS files, so it calls on Libuv. Libuv, being
    very cool and full of superpowers, communicates with the OS, performs all the
    necessary tasks, and then returns the response to the JS engine. He offloads the
    work and does wonders behind the scene.

    ****************************Async Sync SeTimeout Crypto EP7********************************************
    What is crypto ?
      - The crypto module is one of the core modules provided by Node.js, similar to
        other core modules like https , fs (file system), and zlib (used for
        compressing files).
      -  These core modules are built into Node.js, so when you write require('crypto') ,
        you're importing a module that is already present in Node.js.
        You can also import it using require('node:crypto') to explicitly indicate that it’s a
        core module, but this is optional.

    ****************************V8 Engine  EP8********************************************
    HOW V8 ENGIN WORKS
            When JavaScript code is executed, it goes through several stages in the V8
        engine. The first stage is
        parsing, which includes lexical analysis and tokenization. Heres how it works:
        A) Parsing Stage: Lexical Analysis and Tokenization
            1. Lexical Analysis
                Purpose The main goal of lexical analysis is to break down the raw JavaScript
                code into manageable pieces called tokens.
            2. What is Tokenization?
                Definition Tokenization is the process of converting code into a series of
                tokens. Each token represents a fundamental element of the language, such
                as keywords, operators, identifiers, and literals.
                Why Tokenization? Tokenization helps the V8 engine to read and understand
                the code more effectively by breaking it down into smaller, more manageable
                pieces. This step is crucial for further analysis and compilation.

            2nd Stage: Syntax Analysis and Abstract Syntax Tree (AST)
                lexical analysis and tokenization stages, the next step in the parsing process is
                    syntax analysis. In this stage, the tokens are converted into an Abstract Syntax
                    Tree AST. This process is crucial for transforming the flat list of tokens into a
                    structured representation of the code.

        B) Interpreter and Compilation
            Interpreted Languages:
                Definition These languages are executed line by line. The interpreter reads
                and executes the code directly, which can lead to slower execution times
                compared to compiled languages.
                Pros Faster to start executing code, easier to debug.
                Cons Slower execution compared to compiled languages because of the lineby-line interpretation.
                Episode-08 | Deep dive into v8 JS Engine 9
                Example Python
            Compiled Languages:
                Definition These languages are first translated into machine code (binary
                code) through a process called compilation. The machine code is then
                executed by the computers hardware, leading to faster execution times.
                Example C, C.
                Pros Faster execution because the code is pre-compiled into machine code.
                Cons Longer initial compilation time, more complex debugging process.
SUMMERY:
        1. Code is move to parsing phase 
        2.After that it converted it into tokens with syntax analysis
        3. Then it transform into ATS(Abstract syntax tree)
        4. This tree then pass to interpreter called ignition interpreter
        5. This interpreter convert the code into byte code and then code get executed
        6. While this possess interpreter analyze some code that reuse again and again than code is forwarded to compiler called turbofan compiler
        7. Then compiler optimism this code into machine code and again that code will get executed
        
    ****************************EVENT LOOP LIBUV  EP9********************************************
EVENT LOOP:
    - It allow js to perform non blocking io operation even if js is a single threaded language
CALLBACK QUEUE:
    - The callback queue is were callback are store after async operation are competed
THREAD POOL:
    - It is used to handle more time consuming task that cannot be handel with event loop without blocking it 

   # The event loop in LIBUV operates in four major phases:
     1)Timers Phase:  In this phase, all callbacks that were set using setTimeout or
                    setInterval are executed. These timers are checked, and if their time has
                    expired, their corresponding callbacks are added to the callback queue for
                    execution.
    2) Poll Phase:  After timers, the event loop enters the Poll phase, which is crucial
                    because it handles I/O callbacks.
    3) Check Phase: Next is the Check phase, where callbacks scheduled by the
                    setImmediate function are executed.
    4) Close Callbacks Phase: Finally, in the Close Callbacks phase, any callbacks
                              associated with closing operations, such as socket closures, are handled


Before the event loop moves to each of its main phases Timers, I/O Callbacks,Poll, Check, and Close Callbacks), it first processes any pending microtasks.
Microtasks include tasks scheduled using
process.nextTick() and Promise callbacks. This ensures that these tasks are handled promptly before moving on to the next phase

    1- Start event loop
    2- Process process.nextTick() callback
            Execute all the process.nextTick() callbacks
    3- Process promise callback
            Execute all promises callback(microtask)
    4- Move to timer phase
            Execute timer callback
    5. Move to i/o callback phase
            Execute    i/o callbacks
    6. Move to poll phase
            Execute all i/o events
    7. Move to check phase
            Execute setImmediate callback
    8. Move to close callback phase
            Execute close callback
    9. Repeat event loop cycle

    #When the event loop is empty and there are no more tasks to execute, it enters the poll phase and essentially waits for incoming events

