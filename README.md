# Scope and Closure Questions

## What is scope? 

The term scope can be used a few different ways, but one good way to think about it, courtesy of Kyle Simpson, is as **a set of rules (scoping rules) for storing variables in a location and then finding them again later**. JavaScript's rules are simple: 

1. When executing code, look for the name of a particular variable or function in the body of the function that is currently being executed.
2. If it can't be found there, look next in the body of the function in which the currently executing function is nested. Continue this process of traveling 'up' the scope 'chain' until you either find the name of the variable or function or you reach the global context. The process ends as soon as the variable or function name is found, even if further up the scope chain there are other variables or functions that have the same name (see 'shadowing').
3. If the name can't be found in any scope on the scope chain or in the global context, either create a new global variable with the value undefined or throw a reference error.

You can also talk about the scope of a name binding. A 'name binding' is an association of a name to an entity, such as a variable. **A binding's scope is the portion of a program where the binding is valid: where the name can be used to refer to the entity**.

The term "scope" is also sometimes used to refer to the set of all entities that are visible within a portion of the program or at a given point in a program. It's probably better to refer to this as the execution context (broadly speaking) or lexical environment (more narrowly speaking), but the terms scope and execution environment or lexcial environment are sometimes used interchangeably. 

## What is lexical scope?

Lexical scoping is one way to determine when or where a name is in scope and whether that name can be used during code execution. Specifically, **in lexical scoping, name of variables and functions are in scope and ready to be used only if they appear in body of the function that's currently executing as that function appears in the source code**, or in the body of the function in which the currently executing function is nested or in some other part of the nested hierarchy of functions (the 'scope chain') of which the currently executing functions is a part, or if they were declared in the global context. If your code attempts to use a variable or function name that was not declared within any scope in the scope chain of the currently executing code, the JavaScript engine will throw an error.

## What are static and dynamic scope?

First, the terms static scope and lexical scope are synonymous.  Second, JavaScript uses static/lexical scoping and does not use dynamic scoping.

In static/lexical scoping, names refer to the local environment that they appear in in your code, independent of the runtime call stack. Resolving the name of a variable or function only requires looking at your unchanging, 'static' source code, hence 'static scoping.'

If function f invokes non-nested function g, then under lexical scoping, function g does not have access to f's local variables, while under dynamic scoping, function g does have access to f's local variables, because g is invoked during the invocation of f.

## What are block scope and function scope and what is their relationship to one another?

## What's the difference between scope and execution context?

**Scope is a property of a name/identifier and is fixed. Context is a property of a program and varies by position in the program.** Context can refer to either lexical context - a position in a program's code - or execution context - a point during runtime. 

The execution context is the environment in which code is executed. That environment consists of all of the variables, functions, and objects that are at play during the execution of a piece of code. The execution context is built before any code executes and the order in which it is built is important. A lot of things happen while building an execution context, but let's focus on variable declaration and assignment and function declarations.

When encountering a variable declaration-and-assignment like "let a = 2" the JavaScript engine **declares** a variable (if not previously declared in the current scope). This happens before execution begins. Later, during execution, when the engine encounters the variable again, it looks up the variable in scope and, if it's found, **assigns** a value to it.

Functions are handled differently. When encountering a function declaration, the engine declares the function with its definition. This happens before code begins to execute.

Together, these two phenomena are referred to as "**hoisting**."

Execution contexts are private and are destroyed as soon as a function finishes executing. When you call a function, you create a new, private execution context. When the function finishes executing, that context is destroyed. When you call the function a second time, you create a new different execution context during the second execution. Then this second context is destroyed. And so on.

## What is closure?

A closure is created when you define a function — not when you execute it. Then, every time you execute that function, its already-defined closure gives it access to all the function scopes available around it.

A closures encompasses everything the defined function can access. This means the defined function’s scope, and all the nested scopes between the global scope and the defined function scope plus the global scope itself.

### What does closure make possible?

Object oriented programming in JavaScript, recursion, the creation of privileged methods, partial application, and currying all examples of things that wouldn't be possible in JavaScript without closure. 

We're all taking advantage of closure all of the time, whether we're aware of it or not. 

### What are partial application and currying?

**Application** is the process of applying a function to its arguments in order to produce a return value.

**Partial Application** is the process of applying a function to some of its arguments. The partially applied function gets returned for later use. In other words, a function that takes a function with multiple parameters and returns a function with fewer parameters. Partial application fixes or binds (partially applies the function to) one or more arguments inside the returned function, and the returned function takes the remaining parameters as arguments in order to complete the function application.

## What's the difference between scope and closure?

A function's scope includes everything in the body of that function as it is defined in your code. The same function's closure gives it access to the its own scope and but also to all of the scopes within which it is nested, traveling all the way "up" the "scope chain" until you reach global scope.

## What's the relationship of the scope chain to closure?

## What is an execution context?

The execution context is the environment in which code is executed. That environment consists of all of the variables, functions, and objects that are at play during the execution of a piece of code. The execution context is built before any code executes and the order in which it is built is important.

When encountering a variable declaration-and-assignment like "let a = 2" the JavaScript engine declares a variable (if not previously declared in the current scope). This happens before execution begins. Later, during execution, when the engine encounters the variable again, it looks up the variable in scope and, if it's found, assigns a value to it.

Functions are handled differently. When encountering a function declaration, the engine declares the function with its definition. This happens before code begins to execute.

Together, these two phenomena are referred to as "hoisting."

Execution contexts are private and are destroyed as soon as a function finishes executing. When you call a function, you create a new, private execution context. When the function finishes executing, that context is destroyed. When you call the function a second time, you create a new different execution context during the second execution. Then this second context is destroyed. And so on.

At any point in time, there can only be one execution context running. Browsers maintain this execution context using a *call stack*. A call stack is a Last In First Out (LIFO) data structure, meaning the most recent thing that you pushed onto the stack is the first thing that gets popped off it. 

## What are the creation and activation stages? 
