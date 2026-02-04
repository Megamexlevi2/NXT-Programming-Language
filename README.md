NXT Programming Language

A modern, statically-typed programming language designed for backend development, AI applications, games, and browser-based projects. NXT compiles to clean, optimized JavaScript and runs on both Node.js and modern browsers.

Features

· Statically Typed - Type checking with simplified type aliases (str, num, bool, list, map)
· Null Safety - Built-in null safety mechanisms with the have operator
· Modern Syntax - Arrow functions, pattern matching, async/await support
· Cross-Platform - Compiles to both Node.js and Browser targets
· Optimized Output - Tree shaking and code optimization
· JavaScript Interop - Full access to npm packages and Node.js APIs
· Object-Oriented - Class-based OOP with inheritance
· Runtime Options - Configurable compilation with minification and obfuscation

Installation

Install globally via npm:

```bash
npm install -g @david0dev/nxt-lang
```

Quick Start

Create a file hello.nxt:

```nxt
print("Hello, World!")
```

Run it directly:

```bash
nxt run hello.nxt
```

Or compile it to JavaScript:

```bash
nxt nax hello.nxt
node hello.js
```

Project Configuration

Create a nxt.config.json file:

```bash
nxt init
```

This generates a configuration file with default settings. Modify it according to your project needs.

Command Reference

Development Commands

· nxt run <file.nxt> - Execute a NXT file directly
· nxt nax <file.nxt> - Compile a NXT file to JavaScript
· nxt build <config.json> - Build an entire project
· nxt check <file.nxt> - Type check without compiling
· nxt watch <file.nxt> - Watch file and recompile on changes
· nxt repl - Start interactive REPL

Compilation Options

The compiler supports various flags:

```bash
# Browser target with minification
nxt nax -bm app.nxt

# Strict type checking
nxt nax -s app.nxt

# Custom output path
nxt nax -o dist/app.js app.nxt

# With obfuscation
nxt nax --obfuscate app.nxt

# Disable tree shaking
nxt nax --no-tree-shake app.nxt
```

Information Commands

· nxt help - Show help message
· nxt version - Show version information

Documentation

Complete language documentation is available in the API.md file, covering:

· Language syntax and type system
· Control flow structures
· Functions and classes
· Error handling
· Imports and exports
· Best practices and patterns
· Migration guide

For 3D game development, see GAME3D.md.

License

NXT is licensed under the Apache License 2.0.

Naming and Identity Protection:

· The project must always be referred to as "NXT Programming Language"
· Releasing the project under a different name is not permitted
· Forks may add identifiers (e.g., NXT-Extended, NXT-Fork) but cannot remove or replace the NXT name
· NXT is an identity-protected programming language

Note: The term "NXT" may be used by other companies or brands in different contexts. This project refers specifically to the NXT Programming Language, which is independent of any company using the name "NXT".

Support

· GitHub: github.com/Megamexlevi2
· NPM Package: @david0dev/nxt-lang

Contributing

Forks are allowed under the terms of the Apache License 2.0. The project identity must be preserved as specified in the license terms.