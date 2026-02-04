# NXT Programming Language - Complete Documentation

## Introduction

NXT is a modern, statically-typed programming language designed for backend development, AI applications, games, and browser-based projects. It compiles to clean, optimized JavaScript and runs on both Node.js and modern browsers. NXT features a simplified syntax with type aliases, null safety, and seamless interoperability with the JavaScript ecosystem.

**Key Features:**
- Simplified type system with type aliases (str, num, bool, list, map)
- Optional variable assignment (auto const inference)
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
- `-s, --strict` - Enable strict type checking
- `-o, --output <file>` - Specify output file path
- `--no-tree-shake` - Disable tree shaking
- `--credits` - Add compiler credits to output
- `--obfuscate` - Obfuscate runtime code

**Examples:**

```bash
# Basic compilation (Node.js target)
nxt nax app.nxt

# Compile for browser
nxt nax -b app.nxt

# Compile with minification
nxt nax -m app.nxt

# Compile for browser with minification
nxt nax -bm app.nxt

# Compile with strict type checking
nxt nax -s app.nxt

# Compile with custom output path
nxt nax -o output/app.js app.nxt

# Compile for browser, minified, with strict checking
nxt nax -bms app.nxt
```

**Combined Flags:**
- `-bm` or `-mb` - Browser + minify
- `-bs` or `-sb` - Browser + strict
- `-ms` or `-sm` - Minify + strict
- `-bms`, `-bsm`, `-mbs`, `-msb`, `-sbm`, `-smb` - Browser + minify + strict

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

### Check Command

Type check a file without compiling:

```bash
nxt check <file.nxt>
```

Example:
```bash
nxt check app.nxt
```

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

## Language Fundamentals

### Variables and Type Annotations

NXT supports simplified variable declarations with optional type annotations:

```nxt
// Auto const inference - no keyword needed
x = 10

// Explicit variable types
var count: num = 0
count = 10

// Const declaration
const PI: num = 3.14159

// Init declaration (recommended for immutables)
init name: str = "Alex"
```

**Variable Keywords:**
- No keyword - Auto const inference (recommended for simple assignments)
- `var` - Mutable variable (can be reassigned)
- `let` - Mutable variable (can be reassigned)
- `const` - Immutable constant (cannot be reassigned)
- `init` - NXT-specific immutable declaration

**Type Aliases (Simplified Syntax):**

```nxt
// Simplified types
name: str = "Alice"
age: num = 25
isActive: bool = true
items: list<str> = ["apple", "banana"]
config: map = { key: "value" }
data: any = "can be anything"

// Full type names still supported
fullName: string = "Alice Smith"
count: number = 42
flag: boolean = true
array: Array<string> = ["a", "b", "c"]
object: Object = { id: 1 }
```

**Type Alias Mapping:**
- `str` → `string`
- `num` → `number`
- `bool` → `boolean`
- `list` → `Array`
- `map` → `Object`
- `any` → `any`

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

// Using full type names
stringArray: Array<string> = ["a", "b", "c"]
userData: Object = { id: 1, name: "Bob" }
```

### Nullable Types

```nxt
// Nullable types use ? suffix
user: User? = null
maybeValue: str? = getValue()

// Have operator for null checks
if value have {
  log(value)
}
```

### Type Inference

NXT can automatically infer types:

```nxt
// Auto const inference
count = 0
name = "Alice"
items = [1, 2, 3]
user = { id: 1, name: "Bob" }

// Explicit initialization
init age: num = 25
var score: num = 0
```

---

## Functions

### Function Declaration

```nxt
fn greet(name: str): str {
  return "Hello, " + name
}

fn add(a: num, b: num): num {
  return a + b
}

fn processUser(user: map): void {
  log(user.name)
}
```

### Arrow Functions

NXT supports arrow functions with infinite nested function support:

```nxt
// Single expression arrow function
double = (x: num) => x * 2

// Block body arrow function
sum = (a: num, b: num) => {
  return a + b
}

// Async arrow function
fetchData = async (url: str) => {
  response = await fetch(url)
  return await response.json()
}

// Nested arrow functions
createMultiplier = (factor: num) => (value: num) => value * factor
```

### Function Expressions

```nxt
multiply = fn(x: num, y: num): num {
  return x * y
}

square = fn(n: num): num => n * n
```

### Default Parameters

```nxt
fn createUser(name: str, role: str = "user"): map {
  return { name: name, role: role }
}

user1 = createUser("Alice")
user2 = createUser("Bob", "admin")
```

### Rest Parameters

```nxt
fn sum(...numbers: list<num>): num {
  total: num = 0
  for num of numbers {
    total = total + num
  }
  return total
}

log(sum(1, 2, 3, 4, 5))
```

### Async Functions

```nxt
async fn fetchData(url: str): Promise<map> {
  response = await fetch(url)
  data = await response.json()
  return data
}

async fn loadUser(id: num): Promise<map> {
  try {
    user = await getUser(id)
    posts = await getPosts(id)
    return { user: user, posts: posts }
  } catch err {
    log("Error:", err.message)
    return null
  }
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
} else if score >= 70 {
  log("Grade: C")
} else {
  log("Grade: F")
}
```

### Ternary Operator

```nxt
status: str = age >= 18 ? "adult" : "minor"
max: num = a > b ? a : b
```

### Have Operator (Null Safety)

The `have` operator provides null safety:

```nxt
value: any? = getValue()

// Have expression in if statement
if value have {
  processValue(value)
}

// Have in logical expressions
isValid: bool = value have and value > 0

// IfHave statement (legacy support)
user: map? = getUser()

ifhave user {
  log("User exists")
}
```

### While Loops

```nxt
count: num = 0

while count < 5 {
  log(count)
  count = count + 1
}
```

### For-In Loops

Iterate over object properties:

```nxt
person: map = { 
  name: "Alice", 
  age: 30, 
  city: "NYC" 
}

for key in person {
  log(`${key}: ${person[key]}`)
}
```

### For-Of Loops

Iterate over array elements:

```nxt
numbers: list<num> = [10, 20, 30, 40]

for num of numbers {
  log(num * 2)
}
```

### Traditional For Loops

```nxt
for var i: num = 0; i < 10; i = i + 1 {
  log(i)
}
```

### Match Statements (Pattern Matching)

```nxt
status: str = "success"

match status {
  "success" -> log("Operation succeeded")
  "error" -> log("Operation failed")
  "pending" -> log("Still processing")
  else -> log("Unknown status")
}

day: num = 3

match day {
  1 -> log("Monday")
  2 -> log("Tuesday")
  3 -> log("Wednesday")
  4 -> log("Thursday")
  5 -> log("Friday")
  6, 7 -> log("Weekend")
  else -> log("Invalid day")
}
```

### Break and Continue

```nxt
for var i: num = 0; i < 10; i = i + 1 {
  if i == 5 {
    break
  }
  if i % 2 == 0 {
    continue
  }
  log(i)
}
```

---

## Operators

### Arithmetic Operators

```nxt
a: num = 10
b: num = 3

sum = a + b
diff = a - b
prod = a * b
quot = a / b
mod = a % b
pow = a ** b
```

### Comparison Operators

```nxt
x: num = 5
y: num = 10

equal = x == y
notEqual = x != y
greater = x > y
less = x < y
greaterOrEqual = x >= y
lessOrEqual = x <= y
```

### Logical Operators

```nxt
isActive: bool = true
hasPermission: bool = false

// Using keyword operators
canAccess = isActive and hasPermission
shouldAlert = not isActive or hasPermission

// Using symbol operators (also supported)
result1 = isActive && hasPermission
result2 = isActive || hasPermission
result3 = !isActive
```

### Null Coalescing

```nxt
value: str? = null
result: str = value ?? "default"

user: map? = getUser()
name: str = user?.name ?? "Guest"
```

### Spread Operator

```nxt
arr1: list<num> = [1, 2, 3]
arr2: list<num> = [...arr1, 4, 5, 6]

obj1: map = { a: 1, b: 2 }
obj2: map = { ...obj1, c: 3 }
```

### Assignment Operators

```nxt
count: num = 0

count += 5
count -= 2
count *= 3
count /= 2
count %= 4
```

### Update Operators

```nxt
i: num = 0

i++
++i
i--
--i
```

---

## Classes

### Class Declaration

```nxt
class Person {
  init(name: str, age: num) {
    this.name = name
    this.age = age
  }
  
  fn greet(): str {
    return `Hello, I'm ${this.name}`
  }
  
  fn getAge(): num {
    return this.age
  }
}

person = new Person("Alice", 30)
log(person.greet())
```

### Class Inheritance

```nxt
class Animal {
  init(name: str) {
    this.name = name
  }
  
  fn speak(): str {
    return "Some sound"
  }
}

class Dog extends Animal {
  init(name: str, breed: str) {
    super(name)
    this.breed = breed
  }
  
  fn speak(): str {
    return "Woof!"
  }
}

dog = new Dog("Rex", "Labrador")
log(dog.speak())
```

### Static Methods

```nxt
class MathHelper {
  static fn add(a: num, b: num): num {
    return a + b
  }
  
  static fn multiply(a: num, b: num): num {
    return a * b
  }
}

result = MathHelper.add(5, 3)
```

---

## Imports and Exports

### Import Statements

```nxt
// Import from Node.js modules
import fs from "fs"
import path from "path"

// Import specific exports
import { readFile, writeFile } from "fs"

// Import with alias
import express as app from "express"

// Import everything
import * as utils from "./utils"
```

### Export Statements

```nxt
// Export functions
export fn calculateSum(a: num, b: num): num {
  return a + b
}

// Export classes
export class User {
  init(name: str) {
    this.name = name
  }
}

// Export variables
export const API_KEY = "secret"
```

---

## Error Handling

### Try-Catch

```nxt
try {
  result = riskyOperation()
  log(result)
} catch err {
  log("Error:", err.message)
}

try {
  data = await fetchData()
} catch err {
  log("Failed to fetch:", err)
} finally {
  log("Cleanup")
}
```

### Throwing Errors

```nxt
fn divide(a: num, b: num): num {
  if b == 0 {
    throw "Cannot divide by zero"
  }
  return a / b
}
```

### Error Statement

```nxt
fn validateUser(user: map) {
  if not user.name {
    error 400
  }
}
```

---

## Project Configuration

### Configuration File (nxt.config.json)

Create a configuration file using:

```bash
nxt init
```

Default configuration structure:

```json
{
  "input": "./src",
  "output": "./dist",
  "target": "node",
  "minify": false,
  "sourceMap": false,
  "strict": false,
  "typeCheck": true,
  "treeShake": true,
  "credits": false,
  "obfuscateRuntime": false
}
```

**Configuration Options:**

- `input` - Source directory (default: "./src")
- `output` - Output directory (default: "./dist")
- `target` - Compilation target: "node" or "browser" (default: "node")
- `minify` - Minify output code (default: false)
- `sourceMap` - Generate source maps (default: false)
- `strict` - Enable strict type checking (default: false)
- `typeCheck` - Enable type checking (default: true)
- `treeShake` - Enable tree shaking optimization (default: true)
- `credits` - Add compiler credits to output (default: false)
- `obfuscateRuntime` - Obfuscate runtime code (default: false)

### Building a Project

```bash
# Create config file
nxt init

# Build entire project
nxt build nxt.config.json
```

The build command will:
1. Read the configuration file
2. Find all `.nxt` files in the input directory
3. Compile them to JavaScript
4. Output compiled files to the output directory
5. Display compilation summary

---

## New Syntax Features (v3.0)

### 1. Simplified Type Aliases

```nxt
// Old syntax
name: String = "Alice"
age: Number = 30
items: Array<String> = ["a", "b"]

// New simplified syntax
name: str = "Alice"
age: num = 30
items: list<str> = ["a", "b"]
```

### 2. Optional Assignment (Auto Const)

```nxt
// No keyword needed - auto const inference
x = 10
name = "Alice"
items = [1, 2, 3]

// These are equivalent to:
const x = 10
const name = "Alice"
const items = [1, 2, 3]
```

### 3. Have Operator

```nxt
// Check if value exists (not null/undefined)
if value have {
  log(value)
}

// Use in expressions
isValid = value have and value > 0
```

### 4. Match with Else

```nxt
// Use 'else' instead of '_' for default case
match status {
  "success" -> log("OK")
  "error" -> log("Failed")
  else -> log("Unknown")
}
```

### 5. Arrow Functions

```nxt
// Infinite nested function support
makeAdder = (x: num) => (y: num) => x + y
add5 = makeAdder(5)
result = add5(3)  // 8

// Async arrow functions
fetchUser = async (id: num) => {
  data = await api.get(`/users/${id}`)
  return data
}
```

### 6. Type Annotations

```nxt
// Type annotations with simplified types
user: map = { id: 1 }
score: num = 100
active: bool = true
items: list<str> = ["a", "b", "c"]
```

---

## Best Practices

### 1. Use Simplified Types

```nxt
// Recommended
fn calculateTotal(items: list<map>): num {
  total: num = 0
  for item of items {
    total += item.price
  }
  return total
}
```

### 2. Use Auto Const for Simple Values

```nxt
// Recommended for simple assignments
MAX_USERS = 100
API_KEY = "your-api-key"
CONFIG = { timeout: 5000, retries: 3 }

// Use explicit keywords for clarity when needed
var counter = 0
const PI = 3.14159
```

### 3. Leverage Have Operator

```nxt
fn getUser(id: num): User? {
  return database.findUser(id)
}

user = getUser(1)

if user have {
  log(user.name)
} else {
  log("User not found")
}
```

### 4. Use Match with Else

```nxt
match status {
  "pending" -> processPending()
  "approved" -> processApproved()
  "rejected" -> processRejected()
  else -> handleUnknown()
}
```

### 5. Use Arrow Functions for Callbacks

```nxt
// Clean and concise
items.map(x => x * 2)
items.filter(x => x > 0)
items.forEach(x => log(x))

// With block bodies
items.map(item => {
  processed = transform(item)
  return processed
})
```

### 6. Handle Errors Properly

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

## Advanced Patterns

### Factory Pattern

```nxt
class UserFactory {
  static fn create(type: str): User {
    match type {
      "admin" -> return new AdminUser()
      "editor" -> return new EditorUser()
      else -> return new RegularUser()
    }
  }
}

user = UserFactory.create("admin")
```

### Repository Pattern

```nxt
class UserRepository {
  async fn findById(id: num): Promise<User?> {
    result = await db.query("SELECT * FROM users WHERE id = ?", [id])
    if result.length > 0 {
      return new User(result[0])
    }
    return null
  }
  
  async fn save(user: User): Promise<void> {
    await db.query("INSERT INTO users VALUES (?, ?)", [user.id, user.name])
  }
}
```

### Observer Pattern

```nxt
class EventEmitter {
  init() {
    this.listeners = {}
  }
  
  fn on(event: str, callback: Function) {
    if not this.listeners[event] {
      this.listeners[event] = []
    }
    this.listeners[event].push(callback)
  }
  
  fn emit(event: str, data: any) {
    if this.listeners[event] have {
      for listener of this.listeners[event] {
        listener(data)
      }
    }
  }
}
```

### Functional Composition

```nxt
// Using arrow functions for composition
compose = (f, g) => (x) => f(g(x))

double = (x: num) => x * 2
square = (x: num) => x * x

doubleThenSquare = compose(square, double)
result = doubleThenSquare(3)  // (3 * 2)^2 = 36
```

---

## Migration Guide

### From JavaScript to NXT

```javascript
// JavaScript
function getUser(id) {
  const user = database.getUser(id);
  if (user && user.name) {
    return user.name;
  }
  return "Guest";
}
```

```nxt
// NXT
fn getUser(id: num): str {
  user = database.getUser(id)
  if user have {
    return user.name ?? "Guest"
  }
  return "Guest"
}
```

### From Old NXT to New NXT

```nxt
// Old NXT syntax
var name: String = "Alice"
var age: Number = 30
var items: Array<String> = ["a", "b", "c"]

init PI: Number = 3.14159

fn add(a: Number, b: Number): Number {
  return a + b
}

match status {
  "success" -> log("OK")
  _ -> log("Unknown")
}
```

```nxt
// New NXT syntax (v3.0+)
name: str = "Alice"
age: num = 30
items: list<str> = ["a", "b", "c"]

PI = 3.14159

fn add(a: num, b: num): num {
  return a + b
}

// Or using arrow function
add = (a: num, b: num) => a + b

match status {
  "success" -> log("OK")
  else -> log("Unknown")
}
```

---

## Compiler Features

### Tree Shaking

The compiler automatically removes unused code:

```nxt
// Only used functions are included in output
fn helper1() { log("Used") }
fn helper2() { log("Unused") }

helper1()  // Only this function is in final output
```

Disable tree shaking:
```bash
nxt nax --no-tree-shake app.nxt
```

### Runtime Optimization

The compiler generates optimized runtime code with:
- Minimal runtime overhead
- Optional runtime obfuscation
- Browser and Node.js compatibility
- Efficient feature detection

Enable runtime obfuscation:
```bash
nxt nax --obfuscate app.nxt
```

### Type Checking

```bash
# Check types without compiling
nxt check app.nxt

# Enable strict type checking during compilation
nxt nax -s app.nxt
```

---

## Performance Tips

### 1. Enable Tree Shaking

Tree shaking is enabled by default. It removes unused code from the final output.

```json
{
  "treeShake": true
}
```

### 2. Use Minification

```bash
nxt nax -m app.nxt
```

### 3. Optimize Loops

```nxt
// Efficient array processing
processedItems = items
  .filter(x => x.active)
  .map(x => x.value)
```

### 4. Use Arrow Functions

```nxt
// Arrow functions are optimized
callback = (x) => x * 2

// Better than function expressions
callback = fn(x) { return x * 2 }
```

---

## Troubleshooting

### Common Errors

**Type mismatch:**
```nxt
// Error
count: num = "123"

// Fix
count: num = 123
```

**Cannot reassign constant:**
```nxt
// Error
x = 10
x = 20  // Error: x is auto const

// Fix
var x = 10
x = 20
```

**Null reference:**
```nxt
// Error
user = getUser()
log(user.name)  // May be null

// Fix
user = getUser()
if user have {
  log(user.name)
}
```

**File not found:**
```bash
# Error: [NXT Error] File not found: app.nxt

# Fix: Ensure the file exists and path is correct
nxt run ./path/to/app.nxt
```

**No config file:**
```bash
# Error: [NAX Error] No config file specified

# Fix: Create config file first
nxt init
nxt build nxt.config.json
```

---

## Complete Command Reference

### Basic Commands

```bash
# Run a NXT file
nxt run app.nxt

# Compile to JavaScript
nxt nax app.nxt

# Show help
nxt help

# Show version
nxt version
```

### Compilation Options

```bash
# Compile for browser
nxt nax -b app.nxt

# Compile with minification
nxt nax -m app.nxt

# Compile with strict type checking
nxt nax -s app.nxt

# Combine options
nxt nax -bm app.nxt        # Browser + minify
nxt nax -bs app.nxt        # Browser + strict
nxt nax -bms app.nxt       # Browser + minify + strict

# Custom output path
nxt nax -o dist/app.js app.nxt

# Disable tree shaking
nxt nax --no-tree-shake app.nxt

# Add compiler credits
nxt nax --credits app.nxt

# Obfuscate runtime
nxt nax --obfuscate app.nxt
```

### Project Commands

```bash
# Initialize project
nxt init

# Build project
nxt build nxt.config.json

# Type check without compiling
nxt check app.nxt

# Watch mode
nxt watch app.nxt
nxt nax -w app.nxt
```

### Development Commands

```bash
# Start REPL
nxt repl

# Check types
nxt check app.nxt

# Watch and recompile
nxt watch app.nxt
```

---

## Version History

### v3.0.0 (Current)
- Simplified type system (str, num, bool, list, map)
- Auto const inference
- Have operator for null safety
- Match with else support
- Arrow functions with infinite nesting
- Improved compiler performance
- Enhanced tree shaking
- Better error messages
- REPL improvements

### v2.x
- Initial type system
- Class support
- Async/await
- Pattern matching

---

## License

NXT is licensed under the Apache License 2.0.

---

## Support

- **GitHub**: [github.com/Megamexlevi2](https://github.com/Megamexlevi2)
- **NPM Package**: `@david0dev/nxt-lang`
- **Documentation**: This guide
- **Issues**: Report bugs on GitHub
- **Author**: David Dev

---

## Conclusion

NXT v3.0 brings simplified syntax and powerful features that make development faster and more intuitive. With type aliases, auto const inference, the have operator, and arrow functions, NXT provides a modern development experience while maintaining full JavaScript compatibility.

**Quick Start Recap:**

1. Install: `npm install -g @david0dev/nxt-lang`
2. Create file: `hello.nxt`
3. Run: `nxt run hello.nxt`
4. Compile: `nxt nax hello.nxt`
5. Execute: `node hello.js`

Start building with NXT today!
