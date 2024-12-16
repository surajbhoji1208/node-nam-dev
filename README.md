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
asynchronously, allowing for more efficient and flexible code execution. This
distinction is a powerful feature and an important point to remember for
interviews.
Strict Mode: Another significant difference is that CommonJS code runs in
non-strict mode, while ES modules execute in strict mode. This means that ES
modules enforce stricter parsing and error handling, making them generally
safer and more reliable.