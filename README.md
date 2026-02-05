# NXT Programming Language - Complete Documentation

> ⚠️ **IMPORTANT NOTICE**: NXT is currently in early development (v3.0.0) and contains many bugs and stability issues. This compiler is experimental and not recommended for production use. Use at your own risk!

## Known Issues & Limitations

🐛 **Current Known Bugs:**
- Type checking is unstable and may produce false errors
- Backend development may encounter compilation errors
- Complex nested structures sometimes fail to compile
- Error messages are not always accurate
- Some edge cases in variable scoping are not handled properly
- Class inheritance has limited support
- Async/await may not work in all contexts

**Recommendations:**
- Keep code simple and avoid deeply nested structures
- Test frequently and in small increments
- Disable type checking (`typeCheck: false`) for more stable compilation
- Report bugs on GitHub: https://github.com/Megamexlevi2

---

## Introduction

NXT is an experimental, statically-typed programming language designed for backend development, AI applications, games, and browser-based projects. It compiles to clean, optimized JavaScript and runs on both Node.js and modern browsers.

**Key Features:**
- Simplified type system with type aliases (str, num, bool, list, map)
- Flexible variable declarations (supports both syntaxes)
- Built-in null safety mechanisms
- Compiles to Node.js and Browser targets
- Full access to npm packages and Node.js APIs
- Tree shaking and code optimization
- Async/await support
- Pattern matching with else support
- Arrow functions with infinite nesting
- Class-based OOP

---

## Getting Started

### Installation

Install NXT globally via npm:

```bash
npm install -g @david0dev/nxt-lang
```

Or use directly with npx:

```bash
npx nxt help
```

### Your First Program

Create `hello.nxt`:

```nxt
log("Hello, World!")
```

Run it directly:

```bash
nxt run hello.nxt
```

Compile it:

```bash
nxt nax hello.nxt
node hello.js
```

---

## CLI Commands

### Run Command

Execute a NXT file directly (compiles and runs in one step):

```bash
nxt run <file.nxt>
```

Example:
```bash
nxt run app.nxt
```

### Compile Command (nax)

Compile a single NXT file to JavaScript:

```bash
nxt nax <file.nxt>
```

**Options:**
- `-b, --browser` - Compile for browser environment
- `-m, --minify` - Minify the output code
- `-s, --strict` - Enable strict type checking (NOT RECOMMENDED - BUGGY)
- `-o, --output <file>` - Specify output file path
- `--no-tree-shake` - Disable tree shaking
- `--credits` - Add compiler credits to output
- `--obfuscate` - Obfuscate runtime code

**Examples:**

```bash
nxt nax app.nxt
nxt nax -b app.nxt
nxt nax -m app.nxt
nxt nax -bm app.nxt
nxt nax -o output/app.js app.nxt
```

### Build Command

Build an entire project using a configuration file:

```bash
nxt build <config.json>
```

Example:
```bash
nxt build nxt.config.json
```

### Init Command

Create a `nxt.config.json` template file:

```bash
nxt init
```

This generates a configuration file with default settings.

### Watch Command

Watch a file and recompile on changes:

```bash
nxt watch <file.nxt>
```

You can also use the `-w` flag with compile:
```bash
nxt nax -w app.nxt
```

### REPL Command

Start an interactive REPL (Read-Eval-Print Loop):

```bash
nxt repl
```

**REPL Commands:**
- `exit` or `quit` - Exit the REPL
- `help` - Show help message
- `clear` - Clear the screen
- `version` - Show version information
- `reset` - Reset the context

### Version Command

Show version information:

```bash
nxt version
```

or

```bash
nxt -v
nxt --version
```

### Help Command

Show help message with all commands:

```bash
nxt help
```

or

```bash
nxt -h
nxt --help
```

---

## Language Syntax

### Output Functions

NXT supports multiple ways to print output:

```nxt
log("Hello")
print("Hello")
console.log("Hello")
```

All three work identically and compile to `console.log()`.

### Variables and Type Annotations

NXT supports TWO syntax styles for maximum flexibility:

**Style 1: Type-first (Classic)**
```nxt
name: str = "Alice"
age: num = 30
isActive: bool = true
items: list<str> = ["a", "b", "c"]
```

**Style 2: Variable-first (JavaScript-like)**
```nxt
var name: str = "Alice"
var age: num = 30
var isActive: bool = true
var items: list<str> = ["a", "b", "c"]
```

**Both syntaxes work!** Choose the one you prefer.

**Variable Keywords:**
- `var` - Mutable variable (can be reassigned)
- `let` - Mutable variable (can be reassigned)
- `const` - Immutable constant (cannot be reassigned)
- `init` - NXT-specific immutable declaration

**Type Aliases (Simplified Syntax):**

```nxt
name: str = "Alice"
age: num = 25
isActive: bool = true
items: list<str> = ["apple", "banana"]
config: map = { key: "value" }
data: any = "can be anything"
```

**Type Alias Mapping:**
- `str` → `string`
- `num` → `number`
- `bool` → `boolean`
- `list` → `Array`
- `map` → `Object`
- `any` → `any`
- `void` → `void`

### Primitive Types

```nxt
integer: num = 42
decimal: num = 3.14
text: str = "Hello"
template: str = `Value: ${integer}`
flag: bool = true
empty = null
undef = undefined
```

### Complex Types

```nxt
numbers: list<num> = [1, 2, 3, 4, 5]
mixed: list<any> = [1, "text", true, null]

person: map = {
  name: "Alice",
  age: 30,
  email: "alice@example.com"
}
```

---

## Functions

### Function Declaration

Both syntaxes supported:

**Style 1: Return type after parameters**
```nxt
fn greet(name: str): str {
  return "Hello, " + name
}

fn add(a: num, b: num): num {
  return a + b
}
```

**Style 2: More verbose**
```nxt
fn processUser(user: map): void {
  log(user.name)
}
```

### Arrow Functions

```nxt
double = (x: num) => x * 2

sum = (a: num, b: num) => {
  return a + b
}

fetchData = async (url: str) => {
  response = await fetch(url)
  return await response.json()
}
```

### Async Functions

```nxt
async fn fetchData(url: str): Promise<map> {
  response = await fetch(url)
  data = await response.json()
  return data
}
```

---

## Control Flow

### If Statements

```nxt
score: num = 85

if score >= 90 {
  log("Grade: A")
} else if score >= 80 {
  log("Grade: B")
} else {
  log("Grade: C")
}
```

### Ternary Operator

```nxt
status: str = age >= 18 ? "adult" : "minor"
max: num = a > b ? a : b
```

### Have Operator (Null Safety)

```nxt
value: any? = getValue()

if value have {
  processValue(value)
}

user: map? = getUser()

ifhave user {
  log("User exists")
}
```

### While Loops

```nxt
count: num = 0

while count < 5 {
  log("Count: " + count)
  count = count + 1
}
```

### For Loops

```nxt
for i in 5 {
  log("Iteration: " + i)
}

items: list<str> = ["a", "b", "c"]

for item of items {
  log(item)
}

for i = 0; i < 10; i = i + 1 {
  log(i)
}
```

### Match Statements

```nxt
status: str = "success"

match status {
  "pending" -> log("Processing...")
  "success" -> log("Complete!")
  "error" -> log("Failed")
  else -> log("Unknown status")
}
```

---

## Complete Example

Here's a working example showing both syntax styles:

```nxt
fn getUser(id: num): str {
  user = database.getUser(id)
  if user have {
    return user.name ?? "Guest"
  }
  return "Guest"
}

name: str = "David"
var count: num = 0

fn greet(user: str): str {
  return "Hello, " + user
}

fn main(): void {
  log(greet(name))
  print("Starting counter...")
  
  while count < 5 {
    console.log("Counter: " + count)
    count = count + 1
  }
  
  log("Done!")
}

main()
```

---

## Error Handling

### Try-Catch

```nxt
try {
  data = parseJSON(input)
  log(data.value)
} catch err {
  log("Error:", err.message)
}
```

### Async Error Handling

```nxt
async fn safeRequest(url: str): Promise<map?> {
  try {
    response = await fetch(url)
    return await response.json()
  } catch err {
    log("Request failed:", err.message)
    return null
  }
}
```

---

## Classes

```nxt
class User {
  init(name: str, email: str) {
    this.name = name
    this.email = email
  }
  
  fn greet(): str {
    return "Hello, " + this.name
  }
}

user = new User("Alice", "alice@example.com")
log(user.greet())
```

---

## Import/Export

```nxt
import { helper } from "./utils"
import defaultExport from "./main"

export fn myFunction(): void {
  log("Exported function")
}

export { helper, myFunction }
```

---

## Configuration File

Create `nxt.config.json`:

```json
{
  "input": "./src",
  "output": "./dist",
  "target": "node",
  "minify": false,
  "sourceMap": false,
  "strict": false,
  "typeCheck": false,
  "treeShake": true,
  "credits": false,
  "obfuscateRuntime": false
}
```

**Recommended settings:**
- `typeCheck: false` - Type checking is buggy, keep it disabled
- `strict: false` - Strict mode causes errors
- `treeShake: true` - Tree shaking works well

---

## Troubleshooting

### Common Issues

**Compilation errors with backend code:**
- Try simplifying your code structure
- Avoid deeply nested functions
- Keep functions short and focused

**Type checking errors:**
- Set `typeCheck: false` in config
- Remove type annotations if causing issues
- Use `any` type for problematic variables

**Variables not working:**
- Both syntaxes work: `name: str = "value"` OR `var name: str = "value"`
- Make sure you're using one consistently

**Functions failing:**
- Check that all parameters have types
- Use explicit return types
- Avoid complex async patterns

### Getting Help

- **GitHub**: https://github.com/Megamexlevi2
- **NPM Package**: `@david0dev/nxt-lang`
- **Issues**: Report bugs on GitHub with code examples

---

## Best Practices

### Do's ✓
- Keep code simple and straightforward
- Use `log()`, `print()`, or `console.log()` - all work
- Test frequently during development
- Use `var` for mutable variables
- Disable type checking if you encounter issues
- Use arrow functions for callbacks

### Don'ts ✗
- Don't use strict type checking in production
- Avoid complex nested structures
- Don't mix too many async operations
- Avoid very large files (split into modules)
- Don't rely on advanced type features yet

---

## Example Programs

### Simple Hello World

```nxt
fn main(): void {
  log("Hello, NXT!")
}

main()
```

### Counter Program

```nxt
var count: num = 0

while count < 10 {
  print("Count: " + count)
  count = count + 1
}
```

### User Greeting

```nxt
fn greet(name: str): str {
  return "Welcome, " + name + "!"
}

var userName: str = "Alice"
log(greet(userName))
```

---

## Version History

### v3.0.0 (Current - ALPHA/EXPERIMENTAL)
- ⚠️ Early experimental release with known bugs
- Simplified type system (str, num, bool, list, map)
- Support for both variable declaration syntaxes
- Multiple print functions (log, print, console.log)
- Have operator for null safety
- Match with else support
- Arrow functions support
- Improved compiler (still buggy)
- Type checking disabled by default (unstable)

---

## License

NXT is licensed under the Apache License 2.0.

**Naming and Identity Protection:**
- The project must always be referred to as "NXT Programming Language"
- Releasing the project under a different name is not permitted
- Forks may add identifiers (e.g., NXT-Extended, NXT-Fork) but cannot remove or replace the NXT name
- NXT is an identity-protected programming language

Note: The term "NXT" may be used by other companies or brands in different contexts. This project refers specifically to the NXT Programming Language, which is independent of any company using the name "NXT".

---

## Support

- **GitHub**: [github.com/Megamexlevi2](https://github.com/Megamexlevi2)
- **NPM Package**: `@david0dev/nxt-lang`
- **Author**: David Dev

---

## Contributing

Forks are allowed under the terms of the Apache License 2.0. The project identity must be preserved as specified in the license terms.

**Help wanted:**
- Bug reports with reproducible examples
- Simple bug fixes
- Documentation improvements
- Example programs

---

## Conclusion

NXT v3.0 is an **experimental language** with many bugs and limitations. It brings simplified syntax and powerful features but is **not production-ready**. Use it for learning, experimentation, and simple projects only.

**Quick Start Recap:**

1. Install: `npm install -g @david0dev/nxt-lang`
2. Create file: `hello.nxt`
3. Run: `nxt run hello.nxt`
4. Or compile: `nxt nax hello.nxt` then `node hello.js`

⚠️ **Remember**: This is early alpha software. Expect bugs, crashes, and breaking changes!

Start experimenting with NXT today, but don't use it for anything critical!
