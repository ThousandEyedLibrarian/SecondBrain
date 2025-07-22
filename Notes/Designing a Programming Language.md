Much of this contains material taken from Robert Nystrom's *Crafting Interpreters*, a great book to read cover to cover if this interests you.

## A Language in Stages - Input Stream to Program

### 1. Scanning

AKA lexing or lexical analysis.

Welcome to the language designer's "front end", so to speak.

A [[Scanner (Lexer)]] takes a linear stream of characters and chunks them together. 

Each of these tokens (e.g. `(` or `123` or `hello`) is scanned and whitespace or commenting in the character stream is ignored (generally), then they are fed to the [[Parser]].

### 2. Parsing

A parser takes the sequence of tokens fed from the scanner and builds an [[Abstract Syntax Tree (AST)]] that mimics the structure of the language grammar ([[Formal Languages and Grammar]]). It also lets us know when we as the user are making some sort of syntax error, which happens all too often.

### 3. [[Static Analysis]]

The language now needs to undergo analysis based on its structuring/design.

First, it performs something called binding or resolution, where each identifier (AST node really) is matched to a name, [[Scope]] comes into play here as we name match based on the scope we are in at the time of course.

[[Static Typing]] in your language? This is where we type check and report any type errors like `int i = "hello"`.

If your language is dynamically typed, we will do this at program runtime.

#### 3a. Analysis Storage

It deserved a small subsection.

We need to store the analysis you have so painstakingly performed, this can be done a few ways.

1. Storing as *attributes* in the [[Abstract Syntax Tree (AST)]] itself, extra fields in the nodes that remain uninitialised during parsing.
2. In a lookup table allocated probably on the [[Heap]] (?), with the keys being identifiers (names and declarations of variables). This is called a [[Symbol Table]], the value associated with the key determines what that key refers to.
3. Transform the AST into a new data structure that expresses the code semantics directly.

### 4. Intermediate Representations (IRs)

A critical junction, time for a semantic note.

> *The frontend of a [[Compiler]] is principally concerned with the source language a program is written in.*
> 
> *The backend of a Compiler is concerned with the final [[CPU]] architecture where the program will run.*
> 
> *This point, the intermediate point, is where the code isn't tied tightly to either, and must be stored in some sort of IR which acts as an interface between these two languages.
> 
> See: "control flow graph", "continuation-passing style", "static single assignment" and "three-address code" for well-established IR styles.*

Why is this the case? 

***Because it lets you support multiple source languages and target platforms with way less effort.*** 

Otherwise you are stuck implementing compilers individually for every possible combo of the languages and architectures you want to support, sure it's fine if you just want one combo, but it becomes unwieldy quickly.

This way, we write one shared IR that takes one shared front end for each source language and produces that IR, then you only need one back end for each target architecture, you mix and match to get every combo.

See [[GCC]] for an example of this at scale, it supports compilation to Motorola 68k architecture for God's sake.

### 5. Optimisation

We now understand what the user intends to do with their program, so we can effectively swap stuff out to achieve the same end in more optimised ways if they are bad programmers or just abstracted away from the optimal.

This is a whole thing in and of itself, so standalone research should be done into this and it won't be covered here.

Example, constant folding.

### 6. Code Generation

We now, *finally*, generate the runnable code, i.e. the machine code runnable by the [[CPU]].

This is the language designer's defined "back end", so to speak.

