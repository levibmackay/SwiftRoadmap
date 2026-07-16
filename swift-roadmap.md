# Swift Roadmap: Zero to Interview-Ready

A project-based path from "knows Python and C#" to "reads production Swift and passes an Apple iOS interview." Every module ends with something that runs. Nothing here is optional filler — if a section feels slow, you're moving too fast through the previous one.

**How to use this document:** Check off boxes as you finish them. Don't check a box until the mini project runs and you can answer the reflection questions without looking at your code. If you get stuck on an exercise, that's the point — struggle for at least 20 minutes and try to break the problem down before looking anything up.

---

## Table of Contents

- [Getting Started](#getting-started)
- [Module 1: Swift Fundamentals](#module-1-swift-fundamentals)
- [Module 2: Optionals & Safety](#module-2-optionals--safety)
- [Module 3: Collections & Functional Patterns](#module-3-collections--functional-patterns)
- [Milestone 1: Foundations Check](#milestone-1-foundations-check)
- [Module 4: Structs, Classes & Value vs Reference Semantics](#module-4-structs-classes--value-vs-reference-semantics)
- [Module 5: Enums, Protocols & Extensions](#module-5-enums-protocols--extensions)
- [Module 6: Error Handling & Generics](#module-6-error-handling--generics)
- [Milestone 2: Type System Check](#milestone-2-type-system-check)
- [Module 7: ARC, Memory & Concurrency Basics](#module-7-arc-memory--concurrency-basics)
- [Module 8: Async/Await & Networking](#module-8-asyncawait--networking)
- [Milestone 3: Memory & Concurrency Check](#milestone-3-memory--concurrency-check)
- [Module 9: SwiftUI Fundamentals](#module-9-swiftui-fundamentals)
- [Module 10: Property Wrappers & State Management](#module-10-property-wrappers--state-management)
- [Milestone 4: SwiftUI State Check](#milestone-4-swiftui-state-check)
- [Module 11: Persistence](#module-11-persistence)
- [Module 12: Networking + MVVM in SwiftUI](#module-12-networking--mvvm-in-swiftui)
- [Milestone 5: Architecture Check](#milestone-5-architecture-check)
- [Module 13: Combine Basics](#module-13-combine-basics)
- [Module 14: Testing & Performance](#module-14-testing--performance)
- [Milestone 6: Full Mock Interview](#milestone-6-full-mock-interview)
- [Module 15: Advanced Generics & Streaming (AI Client)](#module-15-advanced-generics--streaming-ai-client)
- [Capstone: App Store-Quality SwiftUI App](#capstone-app-store-quality-swiftui-app)
- [Appendix: Apple Interview Question Bank](#appendix-apple-interview-question-bank)

---

## Getting Started

- [ ] Xcode installed (Mac App Store or developer.apple.com), latest stable version
- [ ] Create one throwaway "Playground" project (`File > New > Playground`) — this is your REPL for Modules 1–8
- [ ] Skim the Xcode interface: Navigator (left), Editor (center), Inspector (right), Debug area (bottom)
- [ ] Know the difference between a **Playground**, a **Swift Package**, and an **App target** — you'll use all three across this roadmap

**Python/C# comparison to anchor on:** Xcode Playgrounds ≈ a Jupyter notebook or `dotnet-script` REPL — fast iteration, no build step, great for Modules 1–8. Once you hit SwiftUI (Module 9), you'll switch to full App projects because Playgrounds can't render interactive UI reliably.

**Tooling you'll use later:** `swift` CLI (comes with Xcode), Swift Package Manager (≈ pip/NuGet), `xcodebuild` (≈ `dotnet build`), Instruments (profiler, no direct Python equivalent — closest is `py-spy` + a memory profiler combined).

---

## Module 1: Swift Fundamentals

### 1. Goal

Read and write basic Swift: declare typed values, write functions, control flow, and string work — without reaching for docs every line.

### 2. Concepts

- variables (`var`) and constants (`let`)
- type inference and explicit typing
- basic types: `Int`, `Double`, `String`, `Bool`
- operators and string interpolation
- `if`/`else`, `for`, `while`
- functions: parameters, return types, argument labels

### 3. Short Explanation

**`let` vs `var`.** Swift makes immutability a first-class citizen the way C# does with `readonly` and Python doesn't do at all by default. `let` is the default you reach for; `var` is the exception you have to justify. This isn't style preference — the compiler enforces it, and Apple's interviewers notice when candidates default to `var` out of Python habit.

**Type inference.** Like `var` in C# or nothing in Python — Swift infers `let age = 25` as `Int` without you writing it. Unlike Python, the type is fixed forever after inference; unlike C#'s `var`, Swift's inference works in more places (including generic contexts). You *can* write `let age: Int = 25`, and you will, whenever inference would be ambiguous or you want documentation-by-type.

**Argument labels.** This is the biggest syntax shock coming from Python/C#. Swift functions can have an external label (what the caller writes) that's different from the internal parameter name (what the function body uses):

```swift
func greet(to name: String) -> String { "Hello, \(name)" }
greet(to: "Ada")  // caller writes "to:", body uses "name"
```

There's no equivalent in Python or C#. It exists because Swift reads like natural language at call sites — `greet(to: "Ada")` reads better than `greet("Ada")` when there are multiple arguments (`move(from:to:)`).

**String interpolation.** `\(expression)` inside a string literal — functionally identical to C#'s `$"{expression}"` or Python's f-string `{expression}`.

### 4. Syntax Cheatsheet

```swift
let name = "Ada"              // constant, type inferred as String
var score: Int = 0            // variable, explicit type
score += 10

let message = "Score: \(score)"           // interpolation
let isPassing = score >= 50               // Bool

if isPassing {
    print("Passing")
} else if score > 0 {
    print("Trying")
} else {
    print("No score")
}

for i in 1...5 { print(i) }               // closed range, includes 5
for i in 1..<5 { print(i) }               // half-open range, excludes 5

var i = 0
while i < 3 { i += 1 }

func add(_ a: Int, _ b: Int) -> Int {     // "_" means no external label
    return a + b
}
add(2, 3)

func greet(to name: String, from sender: String = "Team") -> String {
    "Hello \(name), from \(sender)"        // implicit return, single expression
}
greet(to: "Ada")                           // default parameter used
```

### 5. Exercises

1. Declare a constant `pi` and a variable `radius`; compute and print circle area.
2. Write a function `isEven(_ n: Int) -> Bool`.
3. Write a function `fizzbuzz(upTo n: Int)` that prints FizzBuzz 1...n.
4. Write a function `celsiusToFahrenheit(_ c: Double) -> Double`.
5. Write a function with two labeled parameters that computes a rectangle's perimeter: `perimeter(width:height:)`.
6. Write a function with a default parameter: `power(_ base: Int, to exponent: Int = 2) -> Int`.
7. Predict-then-run: what does `let x = 5 / 2` evaluate to, and why might that surprise a Python developer? Verify.
8. Write a loop that sums all multiples of 3 or 5 below 1000 (Project Euler #1).
9. Write a function `reverse(_ s: String) -> String` without using a built-in reverse method.
10. **Harder:** write a function that returns a tuple `(min: Int, max: Int)` from an array of `Int` — no library shortcuts.

### 6. Mini Project: Tip Calculator (CLI)

Build a command-line program (in a Playground or a `swift run`-able package) that:
- Takes a bill amount, tip percentage, and number of people as inputs (hardcode or read via `readLine()`)
- Prints the tip amount, total, and per-person split
- Handles a 0-person edge case without crashing

### 7. Reflection Questions

- Why does Swift force you to specify a type for empty collection literals but not for `let x = 5`?
- What's the actual difference between `1...5` and `1..<5`, and when would each matter in a loop over an array's indices?
- Why might a language designer make argument labels the default (rather than Python/C#'s positional-only-plus-optional-keyword style)?

### 8. Common Mistakes

- **Using `var` everywhere out of Python habit.** Swift's optimizer and Apple reviewers both expect `let` by default. If you never reassign it, it should be `let`.
- **Forgetting argument labels exist.** Coming from Python, writing `greet("Ada")` when the function is declared `greet(to:)` won't compile. Swift is not "labels optional" — it's "labels are part of the function's identity."
- **Assuming integer division behaves like Python 3.** `5 / 2` in Swift on two `Int`s is `2`, not `2.5` — same trap as C#, opposite of Python 3's `/`.
- **Confusing `1...5` (closed) and `1..<5` (half-open)** and getting off-by-one errors, especially when indexing arrays.

### 9. Challenge

Write a single CLI program that reads a list of numbers (space-separated on one line via `readLine()`), parses them, and prints: sum, average, min, max, and how many are above the average — all using functions you wrote yourself, no `Array` convenience methods beyond basic iteration.

---

## Module 2: Optionals & Safety

### 1. Goal

Understand *why* Swift has optionals, and handle "value or no value" without force-unwrapping your way into crashes.

### 2. Concepts

- `Optional<T>` / `T?`
- `if let`, `guard let`
- nil-coalescing (`??`)
- optional chaining (`?.`)
- force unwrapping (`!`) and why it's dangerous
- implicitly unwrapped optionals (`T!`)

### 3. Short Explanation

**The core idea.** Python's `None` and C#'s nullable reference types (or plain `null`) both let *any* reference silently be absent, and the compiler mostly can't help you. Swift instead makes "might be absent" part of the type itself: `String` can *never* be nil; `String?` might be. This is checked at compile time, not discovered at runtime. This single design decision is why Swift apps crash from nil far less often than Objective-C apps did — and it's a favorite interview topic because it explains *why* Swift exists.

**Optional is literally an enum.** Under the hood:

```swift
enum Optional<Wrapped> {
    case none
    case some(Wrapped)
}
```

That's it — no magic. `nil` is just `.none`. This matters for interviews: when asked "what is an optional," the strong answer is "a two-case enum," not "a nullable thing."

**`if let` vs `guard let`.** Both unwrap. `if let` scopes the unwrapped value to an `if` block — use it when the rest of the function doesn't need the value. `guard let` requires an early exit (`return`/`throw`/`continue`) in its `else` and unwraps into the *surrounding* scope — use it to avoid pyramid-of-doom nesting, C#'s equivalent of early-return null checks but compiler-enforced.

**`!` is a promise, not a cast.** Force-unwrapping (`value!`) tells the compiler "trust me, this has a value" — if you're wrong, the app crashes immediately (a trap, not a catchable exception like C#'s `NullReferenceException`). Interviewers ask about this constantly because production crash logs are full of force-unwraps that were wrong.

### 4. Syntax Cheatsheet

```swift
var middleName: String? = nil
middleName = "Grace"

if let name = middleName {
    print("Have a middle name: \(name)")
}

func processUser(name: String?) {
    guard let name = name else {
        print("No name provided")
        return
    }
    print("Processing \(name)")   // `name` is a non-optional String here
}

let displayName = middleName ?? "N/A"        // nil-coalescing

struct Address { var city: String? }
struct Person { var address: Address? }
let person = Person(address: Address(city: "Rexburg"))
let city = person.address?.city ?? "Unknown" // optional chaining

let forced: String! = "implicitly unwrapped" // avoid unless you have a strong reason
print(forced.count)                          // used like a non-optional, still crashes if nil
```

### 5. Exercises

1. Write `func safeDivide(_ a: Int, _ b: Int) -> Int?` returning `nil` on division by zero.
2. Rewrite exercise 1 using `guard let` inside a caller function that prints the result or an error message.
3. Given `let ages: [String: Int] = ["Ada": 30]`, safely print `"Grace"`'s age or `"unknown"` using `??`.
4. Write a function that takes `String?` and returns its uppercase version or `"EMPTY"` — using optional chaining, not `if let`.
5. Predict-then-run: what happens when you force-unwrap a `nil` optional? Run it and read the actual crash message.
6. Write a struct with three levels of nested optionals and chain through all three safely in one line.
7. Refactor a function with three nested `if let`s into a single `guard let ... , let ... , let ...` (comma-chained guard).
8. Write a function that returns an optional tuple `(Int, Int)?` and safely destructure it at the call site.
9. **Harder:** write a generic function `func firstNonNil<T>(_ values: T?...) -> T?` that returns the first non-nil value from a variadic list.
10. **Harder:** explain (in a comment) why `T!` exists at all, then find one real justified use case (hint: think about `@IBOutlet` in UIKit) and write an example.

### 6. Mini Project: BMI Calculator (CLI)

Build a CLI that:
- Reads height and weight as optional `String` input (from `readLine()`, which returns `String?`)
- Safely converts to `Double?` and validates (height > 0, weight > 0)
- Uses `guard let` to bail out with a clear error message on invalid input, without crashing
- Prints BMI and a category (underweight/normal/overweight) only on the success path

### 7. Reflection Questions

- Why is `Optional` implemented as an enum instead of a special compiler primitive?
- What's the practical difference between a `NullReferenceException` in C# and force-unwrapping `nil` in Swift, in terms of *when* you find out something is wrong?
- When is `guard let` strictly better than `if let`, and when are they equivalent?

### 8. Common Mistakes

- **Force-unwrapping "because it compiles."** `!` always compiles — that's the trap. It converts a compile-time safety net into a runtime crash risk. Treat every `!` in your code as a claim you must be able to justify.
- **Chained `if let` nesting ("pyramid of doom")** instead of a single `guard` or comma-separated `if let a, let b, let c`.
- **Using `T!` as a shortcut to "avoid dealing with optionals."** It's not a workaround, it's a deferred crash.
- **Forgetting `??` short-circuits.** `a ?? expensiveCall()` only calls `expensiveCall()` if `a` is nil — same laziness as C#'s `??`, different from eagerly evaluating both sides.

### 9. Challenge

Write a function `parseConfig(_ lines: [String]) -> [String: String]` that parses `"key=value"` lines, skipping malformed ones (no `=`, empty key, or empty value) using optionals and `guard`/`continue` — with **zero** force unwraps anywhere in the function.

---

## Module 3: Collections & Functional Patterns

### 1. Goal

Work fluently with `Array`, `Dictionary`, `Set`, and Swift's functional collection methods — and know when to reach for each.

### 2. Concepts

- `Array`, `Dictionary`, `Set`, tuples
- closures (syntax, trailing closure syntax, capturing)
- `map`, `filter`, `reduce`, `sorted`, `compactMap`, `flatMap`
- `switch` with pattern matching
- `for-in` over collections, `enumerated()`

### 3. Short Explanation

**Collections are value types.** This is a preview of Module 4 but you need it now: `Array` and `Dictionary` in Swift are **structs**, not classes. Assigning an array to a new variable copies it (conceptually — Swift optimizes with copy-on-write so it's not literally memory-copied until mutation). This is opposite to Python (lists are reference types) and C# (arrays/List<T> are reference types). It's one of the most-asked "gotcha" interview questions.

**Closures ≈ lambdas, but more powerful.** A Swift closure is like a Python lambda or a C# `Func<>`/`Action<>` delegate — except closures can capture variables *by reference* and Swift has compact trailing-closure syntax that makes functional chains read cleanly:

```swift
numbers.filter { $0 > 5 }.map { $0 * 2 }
```

`$0` is shorthand for "first (only) parameter" — similar spirit to C#'s implicit lambda parameters in very short expressions, more terse than Python's `lambda x: x > 5`.

**`map`/`filter`/`reduce`/`compactMap`.** Direct equivalents of Python's `map()`/`filter()`/`functools.reduce()` or C#'s LINQ `.Select()`/`.Where()`/`.Aggregate()`. `compactMap` is the one with no direct one-word equivalent: it maps *and* drops `nil` results in one pass — like `.Select().Where(x => x != null)` in C#, or `[y for x in xs if (y := f(x)) is not None]` in Python.

**`switch` is exhaustive and pattern-matches.** Unlike Python's `match` (3.10+, structurally similar) and much more powerful than C#'s classic `switch`, Swift's `switch` must handle every case (or have `default`), and can match ranges, tuples, and enum associated values in one statement.

### 4. Syntax Cheatsheet

```swift
var fruits = ["apple", "banana", "cherry"]
fruits.append("date")

let scores: [String: Int] = ["Ada": 90, "Grace": 95]
for (name, score) in scores { print(name, score) }

var uniqueTags: Set<String> = ["swift", "ios"]
uniqueTags.insert("swift")   // no-op, already present

let doubled = [1, 2, 3].map { $0 * 2 }                  // [2, 4, 6]
let evens = [1, 2, 3, 4].filter { $0 % 2 == 0 }          // [2, 4]
let total = [1, 2, 3].reduce(0) { $0 + $1 }              // 6, or reduce(0, +)
let strings = ["1", "two", "3"].compactMap { Int($0) }   // [1, 3], "two" dropped

let sortedNames = ["Grace", "Ada", "Bob"].sorted()                 // ascending
let byLength = ["Grace", "Ada", "Bob"].sorted { $0.count < $1.count }

for (index, fruit) in fruits.enumerated() {
    print("\(index): \(fruit)")
}

let httpStatus = 404
switch httpStatus {
case 200...299: print("Success")
case 404: print("Not found")
case 400..<500: print("Client error")
default: print("Other")
}

let point = (x: 1, y: 0)
switch point {
case (0, 0): print("origin")
case (_, 0): print("on x-axis")
case (0, _): print("on y-axis")
default: print("elsewhere")
}
```

### 5. Exercises

1. Given `[1, 2, 3, 4, 5]`, use `map`/`filter`/`reduce` chained together to sum the squares of even numbers.
2. Write a function that takes `[String]` and returns a `[String: Int]` of word → character count using a dictionary literal built with a loop, then again with `reduce(into:)`.
3. Deduplicate an array while preserving order (don't just convert to `Set`, since that loses order — write the logic).
4. Use `compactMap` to parse an array of strings into an array of `Int`, dropping invalid entries.
5. Write a `switch` over an `Int` grade (0–100) that prints a letter grade using range pattern matching.
6. Given a `[(name: String, age: Int)]` array of tuples, sort by age descending using a trailing closure.
7. Predict-then-run: does mutating a copy of an array after `let copy = original` affect `original`? Verify and explain why in one sentence.
8. Write a closure stored in a variable that captures an outer `var count` and increments it each call (a manual counter/generator).
9. **Harder:** implement your own generic `myMap<T, U>(_ array: [T], _ transform: (T) -> U) -> [U]` without using the built-in `map`.
10. **Harder:** given a `[String: [Int]]` of student → scores, compute the student with the highest average using only functional methods (no manual loops).

### 6. Mini Project: To-Do CLI App

Build an in-memory to-do list CLI (looped `readLine()` menu):
- Add a task (string), list tasks (numbered), mark complete, delete a task, filter to show only incomplete
- Store tasks as an array of a small struct `Task { let title: String; var isDone: Bool }`
- Use `filter`/`map`/`enumerated()` for listing and filtering — no manual index-juggling loops where a functional method fits better

### 7. Reflection Questions

- Why does it matter for performance and correctness that `Array` is a value type, if you're passing a 10,000-element array into a function?
- What's the difference between `map` and `compactMap`, precisely — not "one filters nils," but *why* that's a single-pass operation instead of `map` then `filter`?
- When would you prefer a `for-in` loop over `map`/`filter`/`reduce`, given that the functional style is often considered more "Swifty"?

### 8. Common Mistakes

- **Assuming array/dictionary mutation is shared like Python/C#.** `var b = a; b.append(x)` does **not** change `a` in Swift. This trips up almost everyone coming from reference-type-collection languages.
- **Chaining `.map().filter()` when `.compactMap()` does both.** Not wrong, just wasteful and non-idiomatic — flagged in code review and in interviews.
- **Forgetting `switch` must be exhaustive.** Missing a `default` (or missing an enum case) is a compile error, not a runtime surprise like Python's `match` without a wildcard.
- **Using `Set` when order matters**, then being confused when iteration order isn't insertion order.

### 9. Challenge

Given a CSV-like `[String]` of `"name,department,salary"` lines, write a pipeline (using `map`/`filter`/`reduce`/`compactMap`, minimal manual loops) that produces a `[String: Double]` of department → average salary, gracefully skipping malformed lines.

---

## Milestone 1: Foundations Check

Treat this like a real technical screen — 45 minutes, no AI, no docs beyond the official Swift language reference if you're truly stuck on syntax.

1. **(Coding)** Write a function that returns whether a string is a palindrome, ignoring case and spaces.
2. **(Coding)** Given an array of integers, return the two indices whose values sum to a target (classic "Two Sum") — first using a nested loop, then again using a `Dictionary` for O(n).
3. **(Conceptual)** Explain, out loud or in writing, why `Array` being a value type changes how you'd write a function that "sorts in place" versus one that "returns a sorted copy."
4. **(Conceptual)** What does the compiler actually do when you write `guard let x = optional else { return }`? Describe it precisely.
5. **(Debug)** You're given a snippet with a force-unwrap that crashes intermittently in production. Without running it, identify *why* it's intermittent and how you'd make it safe.

Don't move to Module 4 until you can do #2's dictionary version cold, in under 5 minutes, without looking anything up.

---

## Module 4: Structs, Classes & Value vs Reference Semantics

### 1. Goal

Choose correctly between `struct` and `class`, and explain *why* — this is arguably the single most-asked Swift interview topic.

### 2. Concepts

- `struct` vs `class`
- value semantics vs reference semantics
- `mutating` methods
- identity (`===`) vs equality (`==`)
- initializers, memberwise init
- copy-on-write (conceptual)

### 3. Short Explanation

**This is the concept, more than any other, that separates "knows Swift syntax" from "understands Swift."** In Python, everything you define with `class` is a reference type — there's no lightweight value-type alternative for user types. In C#, you *do* have `struct` vs `class`, so this concept isn't entirely foreign, but C# programmers default to `class` almost always, and Swift flips that default: **prefer `struct` unless you have a specific reason to need a class.**

**Value semantics** means: when you assign or pass a `struct` instance, you get an independent copy. Mutating the copy never affects the original. **Reference semantics** (classes) means: assignment/passing shares the same underlying instance — mutate it anywhere, and every reference sees the change, exactly like Python objects or C# classes.

**Why prefer structs?** No shared mutable state means no "who else is holding a reference to this and could change it under me" bugs — a huge source of production issues in reference-heavy codebases. `Array`, `Dictionary`, `String`, and nearly all of Swift's standard library are structs for this reason. Apple's own guidance (and every serious Swift interview) expects you to justify reaching for `class`.

**When you *do* need a class:** you want shared, mutable identity (e.g., a view controller that multiple parts of your app hold and mutate the same instance of), you need Objective-C interop, or you need reference-counted lifetime management explicitly (Module 7).

**`mutating`.** Because structs are value types, a method that changes `self` must be marked `mutating` — the compiler needs to know it's rewriting the value in place. Classes never need this; their methods can always mutate instance state.

**`==` vs `===`.** `==` is value equality — "do these represent the same value" — and you implement it via `Equatable`. `===` is *identity* — "are these literally the same object in memory" — and it only applies to classes (reference types), since value types don't have a stable identity to compare.

### 4. Syntax Cheatsheet

```swift
struct Point {
    var x: Double
    var y: Double

    mutating func moveBy(dx: Double, dy: Double) {
        x += dx
        y += dy
    }
}

var p1 = Point(x: 0, y: 0)       // free memberwise initializer
var p2 = p1                       // COPY
p2.moveBy(dx: 5, dy: 5)
print(p1.x, p2.x)                 // 0.0 5.0 — independent

class Counter {
    var value = 0
    func increment() { value += 1 }   // no `mutating` needed
}

let c1 = Counter()
let c2 = c1                        // SAME instance (let just means you can't reassign c2 itself)
c2.increment()
print(c1.value, c2.value)          // 1 1 — shared

print(c1 === c2)                   // true: same instance
print(c1 === Counter())            // false: different instance, even if value equal

struct Money: Equatable {
    let amount: Double
    let currency: String
}
print(Money(amount: 5, currency: "USD") == Money(amount: 5, currency: "USD"))  // true, synthesized
```

### 5. Exercises

1. Convert the `Point` struct above to a `class` and predict which lines of behavior change. Verify.
2. Write a `struct BankAccount` with a `mutating func deposit(_:)` and explain in a comment why it needs `mutating`.
3. Write a `class BankAccount` with the same method — no `mutating` needed. Write one sentence explaining why.
4. Create two structs conforming to `Equatable` manually (don't use synthesized conformance) and implement `==` yourself.
5. Predict-then-run: pass a struct into a function by value, mutate a *local copy* inside the function, return nothing — does the caller's original change? Verify.
6. Do the same with a class passed into a function — mutate a property on it inside the function. Does the caller see the change?
7. Write a function `func resetIfNegative(_ account: inout BankAccount)` using `inout` on a struct, and explain what `inout` is really doing (hint: it's not "pass by reference" in the C# sense — read up on "copy-in copy-out").
8. **Harder:** implement a minimal copy-on-write wrapper around an array (a class holding an array, with a struct wrapper that copies the class only on mutation) to understand how `Array` achieves value semantics without literally copying on every assignment.
9. **Harder:** write a `struct Matrix` (2D array wrapper) and benchmark (using `Date()` timestamps) copying a large matrix vs. mutating in place, to feel COW's performance behavior.
10. **Harder:** explain, then demonstrate with code, a real bug that reference semantics can cause in a shared model object across two SwiftUI-like "screens" (you can simulate with two functions holding the same class instance).

### 6. Mini Project: Habit Tracker (CLI)

Build a CLI habit tracker where `Habit` is a **struct**:
- `Habit { let name: String; var completedDates: [Date] }`
- Store an array of habits in your CLI's main loop
- Because `Habit` is a value type, when you "update" a habit, you must replace it in the array (e.g., find the index, mutate a local copy, write it back) — implement this correctly and explain why you can't just do `habits.first { $0.name == name }?.complete()`.

### 7. Reflection Questions

- An interviewer asks: "Why does `Array` use `struct` instead of `class`, given that classes seem more powerful?" Answer in 2–3 sentences.
- What specifically does `mutating` tell the compiler to do differently, mechanically?
- Give a concrete example (not from this doc) where reference semantics is the *correct* choice, and explain why value semantics would be wrong there.

### 8. Common Mistakes

- **Defaulting to `class` out of Python/C# habit.** In Swift, that's a code smell unless justified.
- **Trying to mutate a struct through a `let` collection element** (`let habits = [...]; habits[0].complete()` on a mutating method) — won't compile, and understanding *why* (the whole array element would need to be replaced, and `let` forbids that) is a real interview question.
- **Believing `inout` is "pass by reference" the way C# `ref` is.** It's closer, but Swift's actual semantics (copy-in, copy-out) matter for how overlapping `inout` arguments behave — know the difference exists even if you don't need the deep mechanics daily.
- **Forgetting synthesized `Equatable`/`Hashable`** only works if all stored properties are themselves `Equatable`/`Hashable`.

### 9. Challenge

Design a small "shopping cart" system with **both** a value type and a reference type on purpose: `CartItem` as a `struct` (safe to copy around) and `Cart` as a `class` (a single source of truth multiple parts of a hypothetical app would share). Justify each choice in a comment, and write code that demonstrates a bug that *would* occur if the choices were swapped.

---

## Module 5: Enums, Protocols & Extensions

### 1. Goal

Model state precisely with enums (including associated values), and use protocols to write flexible, testable code instead of leaning on class inheritance.

### 2. Concepts

- `enum`, associated values, raw values
- pattern matching on enums (`switch`, `if case`)
- `protocol` (requirements, protocol as a type)
- protocol extensions (default implementations)
- protocol-oriented programming vs. class inheritance

### 3. Short Explanation

**Swift enums are not C#/Java enums.** A C# `enum` is basically a named integer. A Swift enum can carry **associated values** — different data attached per case — which makes it closer to a Rust `enum`, an F# discriminated union, or (functionally) a small sealed class hierarchy in Python/C#, but exhaustively checked and far lighter-weight:

```swift
enum NetworkResult {
    case success(data: Data)
    case failure(error: Error)
}
```

There is no clean Python or C# one-liner equivalent to this — in C# you'd normally build a small class hierarchy or use a discriminated-union library; in Python you'd use a base class or `Union` types with runtime checks. Swift bakes it into the language and the `switch` statement forces you to handle every case.

**Protocols ≈ interfaces, but more.** A Swift `protocol` is like a C# `interface` or a Python `Protocol`/ABC — a contract of required methods/properties. The twist: **protocol extensions** let you provide a *default implementation* directly on the protocol, which every conforming type gets for free unless it overrides it. This is Swift's answer to multiple inheritance and mixins, and it's why Apple pushes "protocol-oriented programming" (POP) as an alternative to deep class hierarchies — compose behavior via small protocols instead of inheriting from a fat base class.

**Why this matters for interviews.** "Protocol-oriented vs object-oriented" is a signature Apple interview topic, because it's genuinely different from how most candidates coming from Java/C#/Python think about code reuse.

### 4. Syntax Cheatsheet

```swift
enum Direction { case north, south, east, west }

enum HTTPStatus: Int {          // raw value backing
    case ok = 200
    case notFound = 404
}
HTTPStatus(rawValue: 404)        // HTTPStatus.notFound (returns Optional!)

enum LoadState<T> {              // enum + associated value + generic (preview of Module 6)
    case idle
    case loading
    case loaded(T)
    case failed(Error)
}

func describe(_ state: LoadState<String>) -> String {
    switch state {
    case .idle: return "idle"
    case .loading: return "loading"
    case .loaded(let value): return "loaded: \(value)"
    case .failed(let error): return "failed: \(error.localizedDescription)"
    }
}

if case .loaded(let value) = state {   // pattern match a single case without full switch
    print(value)
}

protocol Flyable {
    var maxAltitude: Double { get }
    func fly()
}

extension Flyable {
    func fly() { print("Flying up to \(maxAltitude)m") }  // default implementation
}

struct Bird: Flyable {
    let maxAltitude: Double = 3000
    // gets fly() for free from the extension
}

protocol Named { var name: String { get } }
func greet(_ thing: Named) { print("Hello, \(thing.name)") }  // protocol as a type
```

### 5. Exercises

1. Write an enum `TrafficLight` with `red`, `yellow`, `green`, and a computed property `next` that returns the following light.
2. Write an enum `Shape` with associated values (`circle(radius: Double)`, `rectangle(w: Double, h: Double)`) and a function `area(_ shape: Shape) -> Double` using `switch`.
3. Write a `protocol Describable { var description: String { get } }`, conform two different structs to it, and write a function that accepts `[any Describable]` and prints each.
4. Add a protocol extension to `Describable` that provides a default `description` based on some other property, then override it in one conforming type.
5. Write an enum with a raw value of `String` (e.g., `enum Suit: String { case hearts, spades, clubs, diamonds }`) and demonstrate `rawValue` and `init?(rawValue:)`.
6. Predict-then-run: what does `switch` do if you forget a case in a non-`default`-having switch over your own enum? Try it and read the compiler error.
7. Refactor a small class-inheritance hierarchy (e.g., `Animal` → `Dog`, `Cat`, with a `makeSound()` override) into protocol-oriented code with protocol extensions instead.
8. Write `if case` pattern matching (not full `switch`) to check a single enum case with an associated value.
9. **Harder:** design a `protocol Cache { associatedtype Key: Hashable; associatedtype Value; func get(_ key: Key) -> Value?; func set(_ key: Key, _ value: Value) }` and implement it with a struct wrapping a dictionary. (This previews generics/associated types from Module 6.)
10. **Harder:** model a vending machine's state (`idle`, `awaitingPayment(item: String, price: Int)`, `dispensing(item: String)`, `outOfStock(item: String)`) as an enum with associated values, and write a function that transitions between states via `switch`, rejecting invalid transitions.

### 6. Mini Project: Quiz Game (CLI)

Build a CLI quiz game:
- `enum Answer { case a, b, c, d }` and a `struct Question { let text: String; let choices: [String]; let correct: Answer }`
- Define a `protocol Scorable { var score: Int { get } mutating func recordAnswer(correct: Bool) }`, conform a `struct QuizSession` to it
- Loop through questions, read user input, track score, print a summary at the end using a `switch` over score ranges for a final grade message

### 7. Reflection Questions

- Why can a Swift enum with associated values *not* be represented as a raw-value enum (e.g., backed by `Int`)? What's fundamentally different about the two?
- Explain "protocol-oriented programming" to someone who only knows class inheritance, using a concrete example that inheritance handles awkwardly but protocols handle cleanly.
- What's the difference between a protocol *requirement* and a protocol *extension default implementation*, in terms of what conforming types are forced to do?

### 8. Common Mistakes

- **Treating Swift enums like C# enums** and reaching for a class hierarchy when an enum with associated values would be simpler and exhaustively checked.
- **Forgetting `switch` exhaustiveness breaks your build the moment you add a new enum case** — this is a *feature*: the compiler tells you every place that needs updating. Don't silence it with a lazy `default:`.
- **Confusing a protocol requirement with a default implementation** — if a conforming type implements a method that matches a protocol extension's default, understand which one actually gets called (this depends on static vs dynamic dispatch — a real gotcha worth reading up on once you hit it).
- **Over-using protocols with associated types (`PATs`) before understanding generics** — revisit exercise 9 after Module 6 if it felt shaky.

### 9. Challenge

Model a simplified parser for arithmetic expressions using an indirect enum:

```swift
indirect enum Expr {
    case number(Double)
    case add(Expr, Expr)
    case multiply(Expr, Expr)
}
```

Write a function `evaluate(_ expr: Expr) -> Double` using `switch`, and construct `(2 + 3) * 4` as a value of this type manually. (Look up why `indirect` is required — it connects directly to Module 7's ARC concepts.)

---

## Module 6: Error Handling & Generics

### 1. Goal

Write functions that fail safely and explicitly, and write reusable code that works across types without sacrificing type safety.

### 2. Concepts

- `Error` protocol, `throw`/`try`/`catch`
- `try?` and `try!`
- `Result<Success, Failure>`
- generics (generic functions, generic types)
- generic constraints (`where`, protocol bounds)

### 3. Short Explanation

**Swift error handling is checked, not exceptions-as-control-flow.** Python's `try/except` and C#'s `try/catch` both let *any* code throw *anything* at *any time* — the compiler doesn't track it. Swift requires functions that can fail to be marked `throws` in their signature, and callers must use `try` — the compiler enforces that you've acknowledged the possibility of failure at every call site. It's closer in spirit to Java's checked exceptions, but far lighter-weight syntactically, and Swift errors are values (`Error`-conforming enums, typically), not a special stack-unwinding class hierarchy the way C#/Python exceptions are.

**`try` / `try?` / `try!`.** `try` propagates the error to your own `throws` function or a `catch`. `try?` converts a throw into `nil` (turns `throws` into `Optional`, discarding the specific error) — useful when you only care "did it work." `try!` crashes if it throws — same risk profile as force-unwrap, treat it the same way.

**`Result<Success, Failure>`** predates Swift's built-in `throws` ergonomics for async contexts and is still common in completion-handler-based APIs: `Result<T, Error>` is an enum with `.success(T)` / `.failure(Error)` — directly comparable to Rust's `Result` or a hand-rolled "either" type you might build in Python/C#.

**Generics** are Swift's answer to C# generics (`List<T>`) and are more powerful than Python's duck typing (which needs no generics syntax at all, but also gives you zero compile-time guarantees). `func firstElement<T>(_ array: [T]) -> T?` works for any type `T`, and the compiler still checks everything at compile time — you get Python-like reuse with C#-like safety.

**Constraints (`where`, protocol bounds).** `func sum<T: Numeric>(_ values: [T]) -> T` restricts `T` to types conforming to `Numeric` — comparable to C#'s `where T : IComparable`. This is how Swift gets generic code that can still call meaningful methods on the generic type, rather than treating it as a total black box.

### 4. Syntax Cheatsheet

```swift
enum ValidationError: Error {
    case tooShort
    case tooLong(maxLength: Int)
}

func validate(_ password: String) throws -> Bool {
    guard password.count >= 8 else { throw ValidationError.tooShort }
    guard password.count <= 64 else { throw ValidationError.tooLong(maxLength: 64) }
    return true
}

do {
    try validate("abc")
} catch ValidationError.tooShort {
    print("Too short")
} catch {
    print("Other error: \(error)")
}

let isValid = try? validate("longenoughpassword")   // Bool?, nil if it threw

func fetchLocal() -> Result<String, Error> {
    .success("cached data")
}
switch fetchLocal() {
case .success(let data): print(data)
case .failure(let error): print(error)
}

func firstElement<T>(_ array: [T]) -> T? {
    array.first
}

func sum<T: Numeric>(_ values: [T]) -> T {
    values.reduce(0, +)
}

func printAllIfEqual<T: Equatable>(_ a: T, _ b: T) {
    if a == b { print("equal: \(a)") }
}

struct Stack<Element> {           // generic type, not just generic function
    private var items: [Element] = []
    mutating func push(_ item: Element) { items.append(item) }
    mutating func pop() -> Element? { items.popLast() }
}
```

### 5. Exercises

1. Write a custom `Error` enum for a "file not found / permission denied / unknown" trio and a `throws` function that simulates each.
2. Write a `do/catch` that handles each specific error case differently, plus a catch-all.
3. Convert a `throws` function to return `Result<T, Error>` instead, and write the calling code both ways to compare ergonomics.
4. Write a generic function `func swapValues<T>(_ a: inout T, _ b: inout T)` (reimplement Swift's own `swap`).
5. Write a generic `Stack<Element>` (shown above) fully, plus a `peek()` method and an `isEmpty` computed property.
6. Add a constraint: write `func findDuplicates<T: Hashable>(_ items: [T]) -> Set<T>`.
7. Predict-then-run: what error does the compiler give if you write a generic function and try to use `==` on values of the generic type without constraining it to `Equatable`? Read the message carefully.
8. Write a function that takes a throwing closure: `func retry<T>(times: Int, _ operation: () throws -> T) -> T?`, catching failures and retrying.
9. **Harder:** implement a generic `Queue<Element>` using two stacks internally (a classic interview question), with `enqueue`/`dequeue`.
10. **Harder:** write a generic `BinaryTree<T: Comparable>` with `insert` and `contains`, no library help.

### 6. Mini Project: Expense Tracker (CLI)

Build a CLI expense tracker with real error handling:
- Custom `enum ExpenseError: Error { case negativeAmount, emptyCategory, dateInFuture }`
- A `throws` function `addExpense(amount:category:date:) throws -> Expense` that validates and throws specific errors
- A generic `struct Repository<T>` wrapping an in-memory `[T]` with `add`, `all`, and `filter(where:)` — used to store expenses generically (so the same `Repository` type could later store any model)
- Menu loop with `do/catch` printing user-friendly messages per error case

### 7. Reflection Questions

- Why does Swift require `throws` in a function's signature instead of letting any function throw silently like Python/C#? What does that buy you as a caller?
- When would you choose `Result<T, Error>` over a plain `throws` function, given that both represent "this can fail"? (Hint: think about storing the outcome, or completion-handler-based APIs.)
- What does `<T: Equatable>` actually do to the set of types you're allowed to call this generic function with, mechanically?

### 8. Common Mistakes

- **Using `try!` in code that reads external input** (files, network, user input) — that's exactly the data most likely to be malformed, and `try!` turns "malformed input" into "app crash."
- **Swallowing errors with a bare `catch {}`** instead of at least logging what went wrong — silent failure is a code review red flag in every language, Swift included.
- **Writing generic code with no constraints when you actually need one** — e.g., trying to compare two generic values with `<` without constraining to `Comparable`, and being confused by the compiler error.
- **Confusing `try?` "swallows the specific error" with "handles the error."** `try?` is for when you truly don't care *why* it failed — it's not a substitute for real error handling.

### 9. Challenge

Write a generic `func parse<T: LosslessStringConvertible>(_ strings: [String]) -> (values: [T], errors: [String])` that attempts to convert each string to `T`, collecting successes and the original strings that failed — no force unwraps, no crashes on bad input, works for `Int`, `Double`, or any other `LosslessStringConvertible` type without changes.

---

## Milestone 2: Type System Check

1. **(Coding)** Implement a generic `LinkedList<T>` with `append`, `removeFirst`, and a way to iterate it.
2. **(Coding)** Model a traffic light system as an enum with a `mutating` function `advance()` that cycles states, and a computed property for duration in seconds per state.
3. **(Conceptual)** An interviewer says: "Tell me about a time protocol-oriented programming solved a problem class inheritance couldn't." Prepare a real (even if small/hypothetical) example and explain it out loud.
4. **(Conceptual)** Explain the difference between throwing an error and returning `nil` from a function — when is each the right design choice?
5. **(Debug)** You're given a generic function that fails to compile because it calls `.sorted()` on a generic array parameter. Fix it with the correct constraint and explain the fix.

---

## Module 7: ARC, Memory & Concurrency Basics

### 1. Goal

Explain how Swift manages memory without a garbage collector, spot and fix retain cycles, and understand basic thread safety.

### 2. Concepts

- Automatic Reference Counting (ARC)
- `strong`, `weak`, `unowned`
- retain cycles (especially in closures)
- `[weak self]` / `[unowned self]`
- `DispatchQueue` basics (main vs background)
- thread safety basics (data races, why they matter)

### 3. Short Explanation

**This is the biggest conceptual gap coming from Python or C#**, because both of those languages use *tracing garbage collection* — an automatic process that periodically scans for unreachable objects and frees them, with no programmer involvement in the common case. Swift uses **ARC** instead: every class instance carries a reference count; every strong reference increments it; when it hits zero, the instance is deallocated **immediately and deterministically** — not on some GC's schedule. This means Swift memory management is closer to C++ smart pointers (`shared_ptr`/`weak_ptr`) than to anything in Python or C#.

**Only classes are reference-counted.** Structs, enums, and other value types aren't — they don't need to be, because they don't have shared identity (Module 4). ARC is purely a class-instance concern.

**The retain cycle problem.** If object A holds a strong reference to B, and B holds a strong reference back to A, neither's count ever reaches zero — both leak forever, even though nothing outside can reach either. The single most common real-world cause: a closure stored on an object that captures `self` strongly, while the object also stores the closure:

```swift
class ViewModel {
    var onUpdate: (() -> Void)?
    func setup() {
        onUpdate = {
            self.refresh()   // captures self strongly — if self also owns onUpdate, that's a cycle
        }
    }
}
```

**`weak` vs `unowned`.** Both break a retain cycle by not incrementing the reference count. `weak` is always `Optional` (becomes `nil` automatically if the referenced object is deallocated — safe). `unowned` assumes the referenced object will *always* outlive the reference and is *not* optional — faster, but crashes if you're wrong. Default to `weak` unless you can prove the lifetime relationship (e.g., a child that can never outlive its parent).

**Why interviewers love this topic.** It's where "have you shipped real Swift" separates from "have you read the syntax." Nearly every senior Swift interview includes a retain-cycle debugging question.

**Concurrency basics.** `DispatchQueue.main` runs on the UI thread — all UI updates must happen there. `DispatchQueue.global()` gives you a background queue for expensive work. A **data race** happens when two threads read/write the same mutable state without coordination — undefined behavior, not a clean crash, which makes it far worse than a null-unwrap crash. (Module 8 introduces `async`/`await` and Swift's modern structured concurrency, which is now generally preferred over raw GCD for new code — but GCD is still everywhere in production codebases and interview questions.)

### 4. Syntax Cheatsheet

```swift
class Person {
    let name: String
    var pet: Pet?
    init(name: String) { self.name = name }
    deinit { print("\(name) deallocated") }
}

class Pet {
    let name: String
    weak var owner: Person?          // weak breaks the cycle: Person -> Pet -> Person
    init(name: String) { self.name = name }
    deinit { print("\(name) deallocated") }
}

var person: Person? = Person(name: "Ada")
var pet: Pet? = Pet(name: "Rex")
person?.pet = pet
pet?.owner = person
person = nil
pet = nil                             // both deinit fire — no leak, thanks to `weak`

class Downloader {
    var completion: (() -> Void)?
    func start() {
        completion = { [weak self] in     // capture list: breaks the retain cycle
            guard let self else { return }
            self.finish()
        }
    }
    func finish() { print("done") }
}

DispatchQueue.global().async {
    let result = heavyComputation()
    DispatchQueue.main.async {
        updateUI(with: result)            // always hop back to main for UI
    }
}
```

### 5. Exercises

1. Write the `Person`/`Pet` example above *without* `weak`, run it, and observe (via `print` in `deinit`) that neither deallocates.
2. Fix it with `weak`, confirm both `deinit`s fire.
3. Rewrite using `unowned` instead of `weak` where appropriate, and explain in a comment why `unowned` is safe in that specific case (or why it isn't, if you can construct a crash).
4. Write a class with a closure property that captures `self` strongly and causes a leak; fix it with `[weak self]` and a `guard let self else { return }`.
5. Predict-then-run: add a `deinit` with a `print` to a class, create an instance in a function's local scope, and observe when it's printed relative to the function returning.
6. Write a small program dispatching work to `DispatchQueue.global()` and printing a result on `DispatchQueue.main` — verify (via `Thread.isMainThread`) which thread each closure runs on.
7. Deliberately create a data race: two `DispatchQueue.global()` tasks incrementing a shared `var counter` a large number of times concurrently. Run it multiple times and observe the count is *not* reliably correct.
8. Fix exercise 7 using a `DispatchQueue` used as a serial lock (`queue.sync { counter += 1 }`), or research and use `NSLock`.
9. **Harder:** build a three-object retain cycle (A → B → C → A) and fix it by breaking exactly one link with `weak`.
10. **Harder:** explain (in comments) why `unowned` is a performance micro-optimization over `weak`, and identify a specific real scenario (e.g., a parent-child view relationship) where the lifetime guarantee genuinely holds.

### 6. Mini Project: Stopwatch (CLI)

Build a CLI stopwatch that uses a repeating `Timer` (or `DispatchSourceTimer`) with a closure callback:
- `class Stopwatch { var onTick: ((TimeInterval) -> Void)?; ... }`
- **Intentionally** write it first with a strong `self` capture in the tick closure, add a `deinit` print, create and discard a `Stopwatch` instance, and confirm (by absence of the `deinit` print) that it leaked
- Then fix it with `[weak self]`, confirm the `deinit` print now appears
- Print elapsed time to the console once per second while running

### 7. Reflection Questions

- Why can't ARC, on its own, detect and break retain cycles the way a tracing garbage collector's mark-and-sweep can?
- Give the precise rule for choosing `weak` vs `unowned` — not "weak is safer" (true but incomplete), but *why* structurally.
- Why must UI updates happen on the main thread specifically, rather than any thread being fine as long as it's consistent?

### 8. Common Mistakes

- **Capturing `self` strongly in a closure stored as a property**, the single most common source of real-world Swift memory leaks.
- **Using `unowned` defensively "because it's faster" without proving the lifetime relationship** — this trades a safe crash-free leak risk for an unsafe crash risk, backwards from what you want.
- **Updating UI from a background queue** — causes undefined/flaky behavior, not a clean error.
- **Assuming Swift "doesn't need to think about memory" because it's "not manual like C++."** ARC is automatic *reference counting*, not garbage collection — cycles are a real, common bug class you must actively design against.

### 9. Challenge

Build a small pub/sub `EventBus` class where multiple `Subscriber` objects register closures to be called on events. Design it so subscribers can be deallocated freely without leaking and without the `EventBus` calling a dead subscriber's closure (hint: store subscriptions as `weak` references, or hand back a "cancellable" token). Prove correctness with `deinit` print statements.

---

## Module 8: Async/Await & Networking

### 1. Goal

Fetch real data from a network API using Swift's structured concurrency, and decode JSON safely.

### 2. Concepts

- `async`/`await`
- `Task`
- structured concurrency (vs. completion handlers/GCD)
- `URLSession`
- `Codable` (`Decodable`/`Encodable`)
- error propagation through `async throws`

### 3. Short Explanation

**`async`/`await` is directly comparable to C#'s `async`/`await`** — if you know C# Tasks, you already have 80% of the mental model. It's a large step up in readability from Python's `asyncio` (which requires an event loop you manage explicitly) and from older Swift code (which used nested completion-handler closures, similar to pre-`async` JavaScript callback hell). A function marked `async` can `await` other async work without blocking the thread — the runtime suspends and resumes it.

```swift
func fetchUser() async throws -> User { ... }   // can fail AND suspends
let user = try await fetchUser()                 // read top-to-bottom, no nested closures
```

**Structured concurrency.** A `Task { ... }` creates a new unit of concurrent work with a defined lifetime — unlike a raw `DispatchQueue.global().async { }` block, a `Task` is trackable, cancellable, and its errors don't just vanish silently. This is Swift's modern replacement for most everyday GCD usage (Module 7's `DispatchQueue` knowledge is still essential for understanding *why* — main-thread rules don't change).

**`Codable`.** Swift's answer to Python's `json.loads` + manual dict access, or C#'s `System.Text.Json`/`Newtonsoft` deserialization — except it's compiler-verified. You define a struct matching the JSON shape, conform it to `Decodable` (often just `: Codable` for both directions), and `JSONDecoder` does the rest, throwing a specific, inspectable error if the shape doesn't match:

```swift
struct User: Decodable { let id: Int; let name: String }
let user = try JSONDecoder().decode(User.self, from: data)
```

**Error propagation.** `async throws` functions propagate errors exactly like synchronous `throws` functions — `try await` at the call site, `do/catch` around it. No separate "rejected promise" handling path to learn, unlike some completion-handler-based or Promise-based APIs.

### 4. Syntax Cheatsheet

```swift
struct Repo: Decodable {
    let name: String
    let stargazers_count: Int
}

func fetchRepos(for user: String) async throws -> [Repo] {
    let url = URL(string: "https://api.github.com/users/\(user)/repos")!
    let (data, response) = try await URLSession.shared.data(from: url)

    guard let http = response as? HTTPURLResponse, http.statusCode == 200 else {
        throw URLError(.badServerResponse)
    }
    return try JSONDecoder().decode([Repo].self, from: data)
}

Task {
    do {
        let repos = try await fetchRepos(for: "apple")
        print(repos.map(\.name))
    } catch {
        print("Failed: \(error)")
    }
}

// Concurrent (not sequential) awaits with async let:
async let repos = fetchRepos(for: "apple")
async let user = fetchUser(named: "apple")
let (repoResult, userResult) = try await (repos, user)
```

### 5. Exercises

1. Write a `struct` matching a small public API's JSON shape (e.g., a free weather API) and decode a sample JSON string (hardcoded, no network yet) with `JSONDecoder`.
2. Write an `async throws` function that fetches from a real URL and decodes it; call it from a `Task { }` and print the result.
3. Add proper error handling: what happens if the URL is unreachable? Catch and print a specific message.
4. Add a `CodingKeys` enum to a `Decodable` struct to map a `snake_case` JSON field to a `camelCase` Swift property.
5. Write two independent `async` fetches and run them concurrently with `async let` instead of two sequential `await`s — verify (via timestamps) that they overlap.
6. Predict-then-run: what happens if `JSONDecoder().decode` is given JSON missing a required (non-optional) field? Read the actual decoding error.
7. Make a struct field optional to gracefully handle a sometimes-missing JSON field, and confirm decoding no longer throws for that case.
8. Write a function that retries a failed network call up to 3 times with `Task.sleep` between attempts.
9. **Harder:** implement a simple in-memory cache in front of your fetch function so a second call for the same key returns instantly without hitting the network.
10. **Harder:** write a custom `Decodable init(from decoder:)` by hand (not relying on synthesized conformance) for a type whose JSON shape doesn't match its Swift shape (e.g., flattening a nested JSON object into flat Swift properties).

### 6. Mini Project: Weather CLI

Build a CLI that fetches real weather data (Open-Meteo's free API needs no key: `https://api.open-meteo.com/v1/forecast?latitude=..&longitude=..&current_weather=true`):
- `Decodable` structs matching the response shape
- An `async throws` fetch function
- Print temperature and windspeed for a hardcoded location, with clear error output if the network call fails
- Handle the "no internet" case without crashing

### 7. Reflection Questions

- What does `await` actually suspend, and what is free to keep running while it's suspended?
- Why is `async let` different from writing two sequential `try await` calls, in terms of actual wall-clock behavior?
- Why does `Codable` throw a specific, structured error on mismatched JSON instead of just returning `nil`, unlike many optional-returning parsing APIs?

### 8. Common Mistakes

- **Blocking the main thread waiting on a `Task` synchronously** (e.g., misusing semaphores) instead of embracing `async`/`await` end to end — reintroduces the exact problems structured concurrency exists to solve.
- **Force-unwrapping `URL(string:)`** on a dynamically constructed URL (e.g., with user input) instead of handling the `nil` case — safe for a hardcoded literal URL, unsafe otherwise.
- **Forgetting that `Codable` property names must match JSON keys exactly** (or need `CodingKeys`) — a very common source of "why is this always nil" bugs.
- **Writing two sequential `await`s when the calls are independent**, leaving free concurrency on the table.

### 9. Challenge

Build a small async pipeline: fetch a list of items from one endpoint, then concurrently fetch details for *all* items (not sequentially) using `withThrowingTaskGroup`, aggregate the results, and handle partial failure (some detail fetches succeed, some fail) by returning both the successes and a list of errors rather than failing the whole operation on one bad item.

---

## Milestone 3: Memory & Concurrency Check

1. **(Coding)** Given a class with a closure property that leaks, fix it and prove the fix with `deinit`.
2. **(Coding)** Write an `async throws` function chain: fetch a user, then fetch that user's posts, handling failure at each step distinctly.
3. **(Conceptual)** Explain ARC to someone who only knows Python's garbage collector — what do they get "for free" in Python that they must actively manage in Swift, and why?
4. **(Conceptual)** What's the difference between a data race and a retain cycle? Both are concurrency/memory bugs, but they're not the same category — explain what makes each dangerous.
5. **(Debug)** Given a `Task` that fetches data and updates a UI-facing `@Published` property (previewed in Module 10) directly from a background context, identify the bug and fix it.

---

## Module 9: SwiftUI Fundamentals

### 1. Goal

Build a real, interactive SwiftUI screen: layout, basic state, and navigation between two screens.

### 2. Concepts

- the `View` protocol and `body`
- declarative UI (vs. imperative UIKit/WinForms/Tkinter)
- layout: `VStack`, `HStack`, `ZStack`, `Spacer`, padding/frame modifiers
- `@State` (local, private view state)
- basic navigation (`NavigationStack`, `NavigationLink`)
- previews (`#Preview`)

### 3. Short Explanation

**SwiftUI is declarative — you describe *what* the UI should look like for a given state, not the sequence of calls to *build* it.** This is a real paradigm shift if your only UI experience is imperative (Tkinter, WinForms, or even UIKit): instead of "create a label, set its text, add it to a view, position it," you write `Text("Hello")` and the *state* determines what's shown. The closest mental model from your existing knowledge is React (if you've seen it) — components are functions of state, and the framework figures out the diff. If that's unfamiliar too, think of it like this: a `View`'s `body` is re-evaluated any time its state changes, similar to how a template engine re-renders from a data context, except it happens automatically and efficiently.

**`View` is a protocol, not a base class.** Every SwiftUI screen you build conforms to `View` and implements one computed property, `body`, returning `some View` — this directly uses Module 5's protocol knowledge and Module 6's generics knowledge (`some View` is an *opaque type*, meaning "a specific concrete type conforming to `View`, which the caller doesn't need to know exactly").

**`@State`** is a property wrapper (fully covered in Module 10) marking a value as owned and watched by this specific view — mutating it triggers a `body` re-evaluation. It's the SwiftUI-native equivalent of a component's local state in a UI framework, always `private` to the view that owns it.

### 4. Syntax Cheatsheet

```swift
import SwiftUI

struct CounterView: View {
    @State private var count = 0

    var body: some View {
        VStack(spacing: 16) {
            Text("Count: \(count)")
                .font(.title)
            HStack {
                Button("−") { count -= 1 }
                Button("+") { count += 1 }
            }
            .buttonStyle(.bordered)
        }
        .padding()
    }
}

struct DetailView: View {
    let itemName: String
    var body: some View {
        Text(itemName)
            .navigationTitle(itemName)
    }
}

struct ListScreen: View {
    let items = ["Alpha", "Beta", "Gamma"]
    var body: some View {
        NavigationStack {
            List(items, id: \.self) { item in
                NavigationLink(item, destination: DetailView(itemName: item))
            }
            .navigationTitle("Items")
        }
    }
}

#Preview {
    ListScreen()
}
```

### 5. Exercises

1. Build a view with a `Text` and a `Button` that toggles the text between "Hello" and "Goodbye" using `@State`.
2. Build a layout using nested `VStack`/`HStack` that resembles a simple profile card (image placeholder, name, subtitle).
3. Add `.padding()`, `.background()`, and `.cornerRadius()` modifiers to style a view; explain modifier *order* mattering (predict-then-run: does `.padding().background()` look different from `.background().padding()`?).
4. Build a `List` from a hardcoded `[String]` array with `NavigationLink`s to a detail screen showing the tapped item.
5. Add a `TextField` bound to `@State` and display the live-typed text elsewhere on screen.
6. Build a form-like screen with a `Toggle`, a `Slider`, and a `Stepper`, all driving visible `@State`-backed output.
7. Use `ZStack` to overlay a badge/label on top of an image placeholder (`Color` or `Rectangle` is fine as a stand-in).
8. Predict-then-run: what happens to a `List`'s scroll position and identity if you don't provide a stable `id`? Test with a mutable, reorderable array.
9. **Harder:** build a two-screen flow (`NavigationStack`) where the second screen sends data *back* to the first on a button tap (hint: this previews `@Binding` from Module 10 — you can pass a closure for now).
10. **Harder:** recreate the layout of a real app screen you use daily (e.g., a settings screen) using only stacks, text, and system SF Symbols (`Image(systemName:)`) — no custom assets.

### 6. Mini Project: Movie Database App (v1 — static)

Build a SwiftUI app (not CLI — real App target now) with a hardcoded `[Movie]` array (`struct Movie { let title: String; let year: Int; let rating: Double }`):
- A `List` screen showing all movies
- Tapping a movie navigates (`NavigationStack`) to a detail screen with title, year, rating laid out with stacks and modifiers
- Use SF Symbols for a star rating indicator
- No networking yet — that's Module 12, once MVVM is introduced properly

### 7. Reflection Questions

- What does "declarative" actually mean in SwiftUI, precisely — not "less code," but what's structurally different about *how* you describe the UI compared to an imperative framework?
- Why is `body` a computed property instead of a method you call manually to "draw" the screen?
- Why does `@State` need to be `private`, as a design convention (not a compiler requirement, though the compiler will warn) — what would go wrong if a parent view could set another view's `@State` from outside?

### 8. Common Mistakes

- **Fighting the layout system** by over-using fixed `.frame()` sizes instead of letting stacks and `Spacer()` do the work — leads to UI that breaks on different screen sizes.
- **Putting business logic directly in `body`** — `body` should be close to pure rendering; logic belongs elsewhere (a real problem Module 12's MVVM solves).
- **Not understanding modifier order** — `.padding().background(.red)` pads first, then colors the padded area; `.background(.red).padding()` colors first, then adds transparent padding outside it. These look different and it trips up everyone at first.
- **Forgetting `List` needs stable identity** (`id: \.self` or `Identifiable` — Module 12) for correct diffing, especially with reorderable/mutable data.

### 9. Challenge

Build a small "settings screen" with grouped sections (`Form` + `Section`), each containing a mix of `Toggle`, `Picker`, and `NavigationLink` rows, all driven by `@State`, styled to plausibly resemble a real iOS Settings app screen.

---

## Module 10: Property Wrappers & State Management

### 1. Goal

Understand how data flows and stays in sync across SwiftUI views — local state, shared state, and observable model objects.

### 2. Concepts

- property wrappers (what they are, mechanically)
- `@State` vs `@Binding`
- `ObservableObject`, `@Published`
- `@StateObject` vs `@ObservedObject`
- `@EnvironmentObject`

### 3. Short Explanation

**A property wrapper is a struct that wraps a value and intercepts reads/writes** — mechanically similar in *spirit* to a C# property with custom `get`/`set` logic, or a Python `@property` decorator, but generalized into a reusable, attachable type (`@State`, `@Published`, `@AppStorage`, and your own custom ones all use the same underlying mechanism: a type conforming to specific wrapper protocols). Knowing this demystifies SwiftUI's "magic" — it's ordinary Swift underneath.

**`@State` vs `@Binding`.** `@State` is *ownership* — this view created and owns this piece of data. `@Binding` is a *reference* to state owned by someone else — a two-way connection so a child view can read *and write* a parent's `@State` without owning it. This is exactly the "lift state up, pass a setter down" pattern from React, formalized into the type system: you can't accidentally treat someone else's state as your own.

**`ObservableObject` + `@Published`.** For state that's more complex than a single view's local concern — usually a class (Module 4's "reference semantics" is *why* it must be a class: multiple views need to share and observe the *same* instance) — you conform to `ObservableObject`, mark properties `@Published`, and SwiftUI automatically re-renders any view observing it when a `@Published` property changes.

**`@StateObject` vs `@ObservedObject`.** Both let a view observe an `ObservableObject`. The difference is *ownership*, same distinction as `@State`/`@Binding`: use `@StateObject` where the object is *created* (its lifetime is tied to this view), use `@ObservedObject` where it's *passed in* from elsewhere. Get this backwards and you'll recreate your view model on every re-render — a classic, hard-to-spot SwiftUI bug.

**`@EnvironmentObject`.** A way to inject a shared `ObservableObject` down an entire view hierarchy without manually threading it through every initializer — similar in purpose to React Context or C#'s dependency injection container, scoped to the SwiftUI view tree.

### 4. Syntax Cheatsheet

```swift
struct ParentView: View {
    @State private var isOn = false
    var body: some View {
        ToggleRow(isOn: $isOn)     // $ projects @State into a Binding
    }
}

struct ToggleRow: View {
    @Binding var isOn: Bool        // doesn't own it, can still read+write it
    var body: some View {
        Toggle("Enabled", isOn: $isOn)
    }
}

class CartViewModel: ObservableObject {
    @Published var items: [String] = []
    @Published var total: Double = 0

    func add(_ item: String, price: Double) {
        items.append(item)
        total += price
    }
}

struct CartScreen: View {
    @StateObject private var viewModel = CartViewModel()   // OWNS it, created here
    var body: some View {
        VStack {
            Text("Total: \(viewModel.total, specifier: "%.2f")")
            SubtotalView(viewModel: viewModel)               // pass down
        }
    }
}

struct SubtotalView: View {
    @ObservedObject var viewModel: CartViewModel             // does NOT own it, passed in
    var body: some View { Text("\(viewModel.items.count) items") }
}

// Environment injection:
struct RootView: View {
    @StateObject private var session = UserSession()
    var body: some View {
        MainTabView().environmentObject(session)
    }
}
struct ProfileTab: View {
    @EnvironmentObject var session: UserSession               // no manual passing needed
    var body: some View { Text(session.username) }
}
```

### 5. Exercises

1. Build a parent view with `@State` and a child view receiving a `@Binding` to it — verify a toggle in the child updates text in the parent.
2. Build an `ObservableObject` view model with two `@Published` properties, and two sibling views both observing it (one `@StateObject`-owning parent, both children `@ObservedObject`) — verify both update together.
3. Predict-then-run: create a view model with `@ObservedObject` instead of `@StateObject` at the point it's *created* (not passed in), trigger a parent re-render some other way, and observe the view model's state unexpectedly resetting. This is the classic bug — reproduce it on purpose.
4. Fix exercise 3 by switching to `@StateObject` and confirm state now survives re-renders.
5. Build a 3-level-deep view hierarchy sharing one `ObservableObject` via `@EnvironmentObject` instead of manually passing it through every initializer.
6. Write a computed property inside an `ObservableObject` that derives from `@Published` properties (e.g., `total` computed from `items`) — does reading it trigger updates the same way? Investigate and explain.
7. Build a simple custom property wrapper (`@propertyWrapper struct Clamped`) that clamps an `Int` to a range on every set — not SwiftUI-specific, just to understand the mechanism.
8. Predict-then-run: what happens if two different views create two *separate* `@StateObject` instances of a view model that's supposed to represent shared state? Reproduce the bug of "changes in one don't show in the other."
9. **Harder:** refactor the Habit Tracker CLI from Module 4 into a SwiftUI app with an `ObservableObject` view model managing the habit array, replacing manual array index lookups with `@Published`-driven UI updates.
10. **Harder:** build a settings object using `@AppStorage` (a property wrapper backed by `UserDefaults` — a preview of Module 11) alongside `@Published` state, and explain the difference in persistence behavior between the two.

### 6. Mini Project: Workout Tracker (SwiftUI)

Build a SwiftUI workout tracker:
- `class WorkoutViewModel: ObservableObject` owning `@Published var workouts: [Workout]` and `@Published var activeWorkout: Workout?`
- A list screen (`@StateObject`-owned view model) showing all workouts
- A detail/logging screen (`@ObservedObject`, passed in) where you can add sets/reps to the active workout, with changes reflected live back on the list screen
- Share the view model via `@EnvironmentObject` if you add a third screen (e.g., a stats summary)

### 7. Reflection Questions

- In one sentence: what's the actual rule for choosing `@StateObject` vs `@ObservedObject`? Not "StateObject is for creating" — *why* does getting this wrong cause the specific bug it causes?
- Why must `ObservableObject` conformance be on a `class`, never a `struct`? Tie this back to Module 4.
- What problem does `@EnvironmentObject` solve that manually passing the object through every initializer doesn't — and what's the cost (hint: think about what happens if you forget to inject it)?

### 8. Common Mistakes

- **Using `@ObservedObject` at the point of creation** instead of `@StateObject` — the single most common SwiftUI state bug, causing silent, hard-to-diagnose data loss on re-render.
- **Making a view model a `struct`** — won't compile against `ObservableObject`, and even if it could, it would defeat the entire point (no shared identity to observe).
- **Forgetting `.environmentObject(...)` at the injection point** — causes a runtime crash ("No ObservableObject of type X found") that's confusing until you know exactly what to look for.
- **Putting too much into one giant `ObservableObject`** — causes unrelated views to re-render on unrelated state changes; prefer focused, small view models per screen/feature.

### 9. Challenge

Build a shared "favorites" system: an `EnvironmentObject`-injected `FavoritesStore` that any screen in a multi-screen app can add/remove items from, with a dedicated "Favorites" tab that live-updates as items are toggled from anywhere else in the app — no manual refresh, no passing the store explicitly through every screen's initializer.

---

## Milestone 4: SwiftUI State Check

1. **(Coding)** Build a two-screen SwiftUI counter app where the count is owned by a shared `ObservableObject`, correctly using `@StateObject` at the root and `@ObservedObject` everywhere else.
2. **(Coding)** Reproduce, on purpose, the "@ObservedObject created at the wrong level" bug, screenshot/describe the broken behavior, then fix it.
3. **(Conceptual)** Explain property wrappers to a C# developer using the closest C# analog you can think of (custom property accessors, or an attribute-based approach) — where does the analogy break down?
4. **(Conceptual)** When would you choose `@EnvironmentObject` over passing a view model explicitly through initializers, and what's the tradeoff in testability/explicitness?
5. **(Debug)** Given a SwiftUI view that doesn't update when a `@Published` array's *element* is mutated in place (e.g., `viewModel.items[0].isDone.toggle()` on a struct array), diagnose why and fix it (ties back to Module 4's value semantics).

---

## Module 11: Persistence

### 1. Goal

Save data so it survives app relaunch — from simple key-value settings to structured, queryable local storage.

### 2. Concepts

- `UserDefaults`
- `Codable` to/from disk (`FileManager`, `Data`)
- `@AppStorage`
- intro to `SwiftData` (modern Core Data replacement)

### 3. Short Explanation

**`UserDefaults`** is a simple, persistent key-value store baked into iOS — closest to a browser's `localStorage`, or a lightweight `.ini`/settings file you'd hand-roll in Python/C#, except the OS manages it for you. Good for small settings (a theme preference, a flag, a small string), **wrong tool** for structured app data (a list of hundreds of objects) — it's not designed or optimized for that, and interviewers will flag using it that way as a red flag.

**`Codable` to disk.** For structured data, you `JSONEncoder().encode(myModel)` to get `Data`, write that `Data` to a file via `FileManager`, and reverse the process with `JSONDecoder` on launch — the same `Codable` machinery from Module 8's networking, just writing to disk instead of over the network. This is roughly equivalent to `json.dump`/`json.load` in Python or `System.Text.Json` file I/O in C#.

**`@AppStorage`** is a property wrapper that reads/writes `UserDefaults` *and* triggers a SwiftUI view update on change — it's `@State` semantics backed by persistent storage, for simple values only (the same size/complexity limits as raw `UserDefaults` apply).

**`SwiftData`** (introduced alongside Swift 5.9/iOS 17) is Apple's modern, `Codable`-adjacent persistence framework — you annotate a class with `@Model` and get a queryable, relational local database (built on Core Data under the hood) without writing SQL or Core Data's older, more verbose API. Think of it as an ORM (SQLAlchemy in Python, Entity Framework in C#) purpose-built for SwiftUI apps. It's the right tool once your data is genuinely relational or large; for a handful of small, simple objects, `Codable`-to-disk is often simpler and sufficient.

### 4. Syntax Cheatsheet

```swift
// UserDefaults — simple values
UserDefaults.standard.set(true, forKey: "hasOnboarded")
let hasOnboarded = UserDefaults.standard.bool(forKey: "hasOnboarded")

// @AppStorage — SwiftUI-integrated
struct SettingsView: View {
    @AppStorage("isDarkMode") private var isDarkMode = false
    var body: some View { Toggle("Dark Mode", isOn: $isDarkMode) }
}

// Codable to disk — structured data
struct Recipe: Codable, Identifiable { let id: UUID; let title: String }

func save(_ recipes: [Recipe]) throws {
    let data = try JSONEncoder().encode(recipes)
    let url = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
        .appendingPathComponent("recipes.json")
    try data.write(to: url)
}

func loadRecipes() throws -> [Recipe] {
    let url = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
        .appendingPathComponent("recipes.json")
    let data = try Data(contentsOf: url)
    return try JSONDecoder().decode([Recipe].self, from: data)
}

// SwiftData — modern local database
import SwiftData

@Model
class RecipeModel {
    var title: String
    var isFavorite: Bool
    init(title: String, isFavorite: Bool = false) {
        self.title = title
        self.isFavorite = isFavorite
    }
}

// In app setup:
// .modelContainer(for: RecipeModel.self)
// In a view:
// @Query var recipes: [RecipeModel]
// @Environment(\.modelContext) var context
// context.insert(RecipeModel(title: "Pasta"))
```

### 5. Exercises

1. Use `UserDefaults` to persist a simple onboarding-seen flag; verify it survives an app relaunch (or Playground/process restart for a CLI equivalent).
2. Build an `@AppStorage`-backed dark mode toggle in a small SwiftUI view.
3. Write `save`/`load` functions for a `[Codable]` array to disk, with proper `throws` error handling (Module 6) rather than force-unwrapping file operations.
4. Predict-then-run: what happens if you try to load from disk before ever saving (file doesn't exist)? Handle it gracefully.
5. Add a `SwiftData` `@Model` class, insert a few instances, and query them back with `@Query` in a SwiftUI list.
6. Add a computed/derived property to a `@Model` class and use it in a SwiftUI view.
7. Delete a `@Model` instance via the `modelContext` and confirm the SwiftUI list updates automatically.
8. **Harder:** migrate the Codable-to-disk recipe storage (exercise 3) to SwiftData, and compare the amount of boilerplate for basic CRUD.
9. **Harder:** implement a simple "export to JSON / import from JSON" feature on top of a SwiftData-backed app, converting between `@Model` instances and plain `Codable` structs.
10. **Harder:** research (briefly) what Core Data is and how SwiftData relates to it — write 3–4 sentences comparing them, since "Core Data vs SwiftData" is a live interview topic given how recent SwiftData is.

### 6. Mini Project: Recipe App

Build on Module 9's list/detail SwiftUI pattern:
- `Recipe` model with title, ingredients, favorite flag
- Persist favorites so they survive app relaunch — pick `Codable`-to-disk **or** `SwiftData`, and write one sentence justifying the choice for this app's data shape
- A "Favorites" filtered view alongside "All Recipes"
- Use `@AppStorage` for one small setting (e.g., a "sort by name vs date added" preference)

### 7. Reflection Questions

- Why is `UserDefaults` the wrong tool for storing "all of a user's saved recipes," even though it's *technically* capable of storing arbitrary `Codable` data?
- What does `@Model` do under the hood, roughly, that a plain `Codable` struct doesn't?
- If you were designing an app with 5 small settings and an app with 10,000 relational records, would you make the same persistence choice for both? Justify.

### 8. Common Mistakes

- **Storing large or complex data in `UserDefaults`** — works at small scale, degrades badly at scale, and isn't its intended purpose.
- **Force-unwrapping file read/write operations** — disk I/O fails constantly in the real world (permissions, missing files, full disk); this is exactly Module 6's `throws`/`guard` territory.
- **Not handling the "first launch, no saved data yet" case** — a very common crash in real apps that skip this edge case.
- **Reaching for SwiftData/Core Data for trivial data** — adds real complexity (schema, migrations, model containers) that a simple `Codable` file doesn't need.

### 9. Challenge

Add a data migration path: simulate a "v1" `Codable` struct shape already saved to disk, then change the model (add a required field with a sensible default for old data), and write loading logic that upgrades old saved data to the new shape without crashing or losing data — a real problem every shipping app eventually faces.

---

## Module 12: Networking + MVVM in SwiftUI

### 1. Goal

Structure a real, API-backed SwiftUI app using MVVM — the architecture pattern you'll be expected to know and use in almost any Apple engineering interview or job.

### 2. Concepts

- MVVM (Model–View–ViewModel) in a SwiftUI context
- separating networking, business logic, and view code
- loading/error/empty UI states
- `Identifiable`, dependency injection basics (protocol-based, for testability)

### 3. Short Explanation

**MVVM in SwiftUI isn't optional ceremony — it directly maps onto the tools you already have.** The **Model** is your `Codable` data (Module 8/11). The **View** is your SwiftUI `body` (Module 9) — ideally close to pure rendering. The **ViewModel** is an `ObservableObject` (Module 10) that owns state, talks to networking/persistence, and exposes `@Published` properties the View reads — the View never calls `URLSession` directly.

This is the same separation of concerns you'd recognize from ASP.NET MVC/MVVM in C#, or a Flask/Django "views shouldn't contain business logic" convention in Python — Apple's ecosystem just formalizes it tightly around SwiftUI's data-binding.

**Why it matters for interviews specifically:** almost every take-home project and system-design-style iOS interview question expects MVVM (or a clear justification for something else, like TCA or MV). Putting `URLSession` calls directly inside a SwiftUI `View`'s `body` or button action is one of the fastest ways to signal "hasn't worked on a real app" in a code review.

**Protocol-based dependency injection for testability.** Define a `protocol RecipeServicing { func fetchRecipes() async throws -> [Recipe] }`, have your real networking class conform to it, and have your ViewModel depend on the *protocol*, not the concrete class. In tests (Module 14), you inject a fake conforming to the same protocol — no real network calls needed. This directly reuses Module 5's protocol knowledge for a very concrete, practical payoff.

**Loading/error/empty states.** A real screen isn't just "here's the data" — it's "loading… / here's the data / here's an error / there's nothing here yet," modeled cleanly with Module 5's enum-with-associated-values pattern (`LoadState<T>` from that module's cheatsheet is exactly this).

### 4. Syntax Cheatsheet

```swift
struct Movie: Codable, Identifiable {
    let id: Int
    let title: String
    let voteAverage: Double
}

protocol MovieServicing {
    func fetchMovies() async throws -> [Movie]
}

struct MovieAPIService: MovieServicing {
    func fetchMovies() async throws -> [Movie] {
        let url = URL(string: "https://example.com/movies")!
        let (data, _) = try await URLSession.shared.data(from: url)
        return try JSONDecoder().decode([Movie].self, from: data)
    }
}

enum LoadState<T> {
    case idle, loading, loaded(T), failed(String)
}

@MainActor
class MovieListViewModel: ObservableObject {
    @Published private(set) var state: LoadState<[Movie]> = .idle
    private let service: MovieServicing

    init(service: MovieServicing = MovieAPIService()) {   // injected, defaults to real impl
        self.service = service
    }

    func load() async {
        state = .loading
        do {
            let movies = try await service.fetchMovies()
            state = .loaded(movies)
        } catch {
            state = .failed(error.localizedDescription)
        }
    }
}

struct MovieListView: View {
    @StateObject private var viewModel = MovieListViewModel()

    var body: some View {
        Group {
            switch viewModel.state {
            case .idle, .loading:
                ProgressView()
            case .loaded(let movies):
                List(movies) { movie in Text(movie.title) }
            case .failed(let message):
                Text("Error: \(message)")
            }
        }
        .task { await viewModel.load() }   // runs once when the view appears
    }
}
```

### 5. Exercises

1. Build the `MovieServicing` protocol + real implementation + `MovieListViewModel` + `MovieListView` chain above end-to-end against a real free API.
2. Write a `FakeMovieService: MovieServicing` returning hardcoded data (no network) and swap it into the ViewModel via its initializer — confirm the UI works identically with zero network access.
3. Add a `.failed` state path deliberately (point the real service at a bad URL) and confirm the error UI renders correctly.
4. Add pull-to-refresh (`.refreshable`) that re-triggers `load()`.
5. Add a search/filter `TextField` that filters the *loaded* movies client-side via `@Published` computed filtering — without a new network call per keystroke.
6. Refactor a "detail" screen to also use MVVM (its own small ViewModel), fetching additional detail data for a tapped movie.
7. Predict-then-run: what happens if `.task { await viewModel.load() }` runs every time the view re-renders vs. only on first appearance? Investigate `.task` vs `.onAppear` semantics.
8. **Harder:** add `@MainActor` isolation (shown above) to your ViewModel and explain, in a comment, what specific bug class it prevents (ties to Module 7's thread-safety concepts).
9. **Harder:** add pagination — load the first page, then load more as the user scrolls near the bottom of the list.
10. **Harder:** write your ViewModel so it depends on *two* injected protocols (e.g., a movie service and a favorites/persistence service from Module 11) and combine both into one coherent `state`.

### 6. Mini Project: Movie Database App (v2 — API-backed, MVVM)

Rebuild Module 9's static Movie Database as a real, networked, testable app:
- A public movie API (TMDB requires a free API key; OMDb is a lighter-weight alternative) behind a `MovieServicing` protocol
- `MovieListViewModel` with `LoadState<[Movie]>`, injected service, `@MainActor`
- Loading spinner, error view with a retry button, and the real list on success
- A detail screen fetching (or receiving) extended info, following the same MVVM shape
- A `FakeMovieService` used in at least one place to prove the architecture is testable without hitting the network

### 7. Reflection Questions

- Why does the View in MVVM never call `URLSession` or `JSONDecoder` directly — what specifically goes wrong (for testing, for reuse, for reasoning about the code) if it does?
- What does depending on `MovieServicing` (a protocol) instead of `MovieAPIService` (a concrete type) actually buy you, concretely, beyond "it's good practice"?
- Why model loading/error/success as one `LoadState<T>` enum instead of three separate `Bool`/`Optional` properties (`isLoading`, `error`, `data`)? What invalid states does the enum make impossible that the three-properties version doesn't?

### 8. Common Mistakes

- **Calling networking code directly from a `Button` action or `body`** — no separation of concerns, untestable, and an immediate red flag in review.
- **Modeling loading state as separate `isLoading`/`error`/`data` properties** instead of one enum — allows impossible states like "isLoading is true AND error is set AND data is populated" simultaneously, which then has to be defensively handled everywhere.
- **Depending on the concrete service type instead of a protocol** — makes the ViewModel untestable without a real network call.
- **Forgetting `@MainActor`** on ViewModels that publish UI-facing state, risking Module 7's data-race-adjacent bugs when background work updates `@Published` properties directly.

### 9. Challenge

Add offline support: cache the last successfully loaded movie list to disk (Module 11), and on `load()` failure (no network), fall back to showing cached data with a visible "showing cached results" banner instead of a bare error screen — combining Modules 8, 11, and 12 into one coherent feature.

---

## Milestone 5: Architecture Check

1. **(Coding)** Build a small MVVM screen from scratch against any free public API of your choosing, with a protocol-based service layer and a `FakeService` proving testability.
2. **(Coding)** Given a "God ViewModel" that does networking, persistence, and validation all in one 300-line class, refactor it into smaller, focused, protocol-injected pieces.
3. **(Conceptual)** Compare MVVM to plain MVC (as you'd know it from C#/Python web frameworks) — what problem does the ViewModel specifically solve that a SwiftUI View talking straight to a Model doesn't?
4. **(Conceptual)** Explain `@MainActor` to someone who understands Module 7's `DispatchQueue.main` but hasn't seen actors — what's the relationship?
5. **(Debug)** Given a ViewModel whose `@Published` state updates but the UI doesn't visibly reflect it, work through a debugging checklist (Is it `@StateObject` at the right level? Is the property actually `@Published`? Is the mutation happening on the main actor? Is the View actually observing this instance?).

---

## Module 13: Combine Basics

### 1. Goal

Understand reactive streams well enough to read Combine-based code and use it for the one or two problems it solves cleanly (like search debouncing) — without over-adopting it where `async`/`await` is simpler.

### 2. Concepts

- `Publisher`, `Subscriber`, `Subscription`
- `@Published` as a Combine publisher (the connection to Module 10)
- operators: `map`, `filter`, `debounce`, `combineLatest`
- `sink`, `assign`, `AnyCancellable`
- Combine vs. `async`/`await` — when to reach for which

### 3. Short Explanation

**Combine is Apple's reactive streams framework** — conceptually close to RxPy (Python) or Rx.NET/`IObservable<T>` (C#) if you've encountered either, or to a spreadsheet: a `Publisher` emits values over time, and a `Subscriber` reacts to each one, with operators (`map`, `filter`, `debounce`) transforming the stream in between, similar in *shape* to the `map`/`filter`/`reduce` you already know from Module 3 — except operating on a *stream over time* instead of a fixed collection.

**`@Published` already gives you a publisher for free.** Every `@Published var x` exposes `$x` as a `Publisher<T, Never>` — this is the exact same `$` projection syntax as `@State`'s `Binding` projection (Module 10), just producing a different type. This is why Combine and SwiftUI compose so naturally: SwiftUI's own state system *is* built on Combine's `ObservableObject` protocol.

**Where Combine still earns its keep after `async`/`await` exists:** anything that's genuinely a *stream* of multiple values over time reacting to each other — live search-as-you-type with debouncing, combining multiple live form fields' validity into one "is the form valid" boolean, or reacting to `@Published` property changes elsewhere in the app. For a single request/response ("fetch this, then use it"), Module 8's `async`/`await` is simpler and is now generally preferred for new code — knowing *when not* to reach for Combine is as important as knowing its operators.

**`AnyCancellable`.** Subscriptions must be retained (stored somewhere) or they're cancelled immediately when they go out of scope — usually collected into a `Set<AnyCancellable>` stored as a property, similar in spirit to needing to keep an event subscription (`+=` in C#) alive by not letting the subscriber get garbage collected, except explicit here since Swift doesn't silently keep things alive for you.

### 4. Syntax Cheatsheet

```swift
import Combine

class SearchViewModel: ObservableObject {
    @Published var query = ""
    @Published private(set) var results: [String] = []
    private var cancellables = Set<AnyCancellable>()

    init() {
        $query
            .debounce(for: .milliseconds(300), scheduler: RunLoop.main)  // wait for typing to pause
            .removeDuplicates()
            .sink { [weak self] text in
                self?.performSearch(text)
            }
            .store(in: &cancellables)      // keep the subscription alive
    }

    private func performSearch(_ text: String) {
        results = text.isEmpty ? [] : ["\(text) result 1", "\(text) result 2"]
    }
}

// combineLatest — react to two publishers together
class FormViewModel: ObservableObject {
    @Published var email = ""
    @Published var password = ""
    @Published private(set) var isValid = false
    private var cancellables = Set<AnyCancellable>()

    init() {
        Publishers.CombineLatest($email, $password)
            .map { email, password in email.contains("@") && password.count >= 8 }
            .assign(to: &$isValid)   // directly assigns into another @Published property
    }
}
```

### 5. Exercises

1. Build the debounced search example above in a SwiftUI view with a `TextField` bound to `$query`, and observe (via `print`) how many times `performSearch` fires while typing quickly vs. slowly.
2. Remove `.debounce` and observe the difference — how many searches fire per keystroke now?
3. Build the `combineLatest` form-validation example with a SwiftUI form, disabling a submit button when `isValid` is `false`.
4. Add a `.map` operator to transform a `Publisher<String, Never>` into a `Publisher<Int, Never>` (e.g., string → character count) before `.sink`.
5. Predict-then-run: what happens if you forget `.store(in: &cancellables)`? Observe the subscription being cancelled immediately and the sink never firing.
6. Add `.filter` to a pipeline so only queries longer than 2 characters trigger a search.
7. Convert an `async`/`await` fetch (Module 8) to expose its result as a `Publisher` using `Future`, and explain in a comment when you'd actually want to do this (hint: bridging into an existing Combine pipeline) versus when it's unnecessary complexity.
8. **Harder:** chain three `@Published` properties together with `combineLatest3` (or nested `CombineLatest`) into one derived validity flag.
9. **Harder:** implement retry-with-backoff on a Combine publisher chain using `.retry` and `.delay`, and compare the code's readability to Module 8's `async` retry exercise.
10. **Harder:** write one paragraph arguing which of your Module 8 (async/await) or Module 13 (Combine) solutions you'd actually ship in a real app for the search-debounce problem, and why.

### 6. Mini Project: Chat App (local/mock real-time)

Build a SwiftUI chat screen without a real backend:
- A `ChatViewModel` with `@Published var messages: [Message]`
- A `Timer`-driven or manually-triggered `PassthroughSubject<Message, Never>` simulating "incoming messages" from another user, piped through `.sink` into `messages`
- A debounced "typing indicator" driven by the local text field's `@Published` value (show "typing…" only after a pause, hide it once a message is sent)
- This project deliberately stays backend-free — the point is the reactive plumbing, not networking

### 7. Reflection Questions

- What's the actual difference between a Combine `Publisher` and a Swift `AsyncSequence` (the `async`/`await`-native equivalent for streams, briefly previewed here for Module 15)? When would each be the better fit?
- Why does `@Published` need `.store(in:)` for its derived subscriptions to keep working, when the `@Published` property itself doesn't need that?
- Give a concrete scenario where `combineLatest` is meaningfully better than manually checking multiple `@Published` properties inside `body` or a computed property.

### 8. Common Mistakes

- **Reaching for Combine for simple one-shot async work** where plain `async`/`await` reads more clearly — a common "resume-driven" over-engineering mistake once developers learn Combine.
- **Forgetting to store `AnyCancellable`s**, silently losing subscriptions and being confused why a `sink` "never fires."
- **Not debouncing user-input-driven pipelines** (search, validation) and accidentally firing expensive work on every keystroke.
- **Mixing Combine and `async`/`await` inconsistently within the same feature** without a clear reason — pick one per feature/layer unless bridging genuinely requires both.

### 9. Challenge

Build a live form with three fields (username, email, password) where a `combineLatest`-based pipeline produces field-specific error messages *and* an overall "can submit" boolean, all debounced so errors don't flash while the user is still typing — then write one sentence on whether you'd keep this in Combine or rewrite it with plain `@Published` + computed properties, and why.

---

## Module 14: Testing & Performance

### 1. Goal

Write real unit tests for a SwiftUI app's logic layer, and reason concretely about performance and memory implications of the choices made throughout this roadmap.

### 2. Concepts

- `XCTest` (or Swift Testing, the newer `@Test`-based framework)
- testing ViewModels via protocol-injected fakes (direct payoff of Module 12)
- `async` test functions
- Instruments basics (Time Profiler, Allocations, Leaks)
- Big-O awareness of Swift's core collection types

### 3. Short Explanation

**Testing a SwiftUI app means testing the ViewModel and Model layers, rarely the View itself** — this is exactly why Module 12's protocol-based dependency injection exists. If your `MovieListViewModel` depends on `MovieServicing` (a protocol) rather than `MovieAPIService` directly, a test can inject a `FakeMovieService` returning known data instantly, with no real network call, no flakiness, and no waiting.

**`XCTest`** is close in spirit to `pytest` or C#'s `xUnit`/`NUnit` — `XCTAssertEqual`, `XCTAssertTrue`, `setUp()`/`tearDown()` all map directly onto concepts you already know. Newer projects increasingly use **Swift Testing** (`@Test`, `#expect`), a more modern macro-based framework — know both exist; you'll likely encounter `XCTest` in most existing production codebases for now.

**Testing async code** is straightforward: mark your test function `async`, `await` the code under test directly — no special "wait for callback" ceremony like older completion-handler-based testing needed.

**Instruments** is Xcode's profiler suite — Time Profiler (where is CPU time going, closest Python analog `cProfile`/`py-spy`), Allocations (what's using memory), and Leaks (literally finds retain cycles from Module 7 at runtime, empirically, instead of by code reading alone). Knowing Instruments exists and roughly what each tool is for is itself an interview-relevant fact, even before you're fluent using it.

**Big-O of Swift collections**, worth having memorized cold for interviews: `Array` — append amortized O(1), insert/remove at front O(n), subscript access O(1). `Dictionary`/`Set` — insert/lookup/delete average O(1) (hash-based), worst case O(n). This is identical in shape to Python's `list`/`dict` or C#'s `List<T>`/`Dictionary<K,V>` — the underlying data structure reasoning transfers directly; only the syntax is new.

### 4. Syntax Cheatsheet

```swift
import XCTest
@testable import YourAppModule

final class MovieListViewModelTests: XCTestCase {
    func test_load_success_updatesStateToLoaded() async {
        let fake = FakeMovieService(result: .success([Movie(id: 1, title: "Dune", voteAverage: 8.1)]))
        let viewModel = MovieListViewModel(service: fake)

        await viewModel.load()

        guard case .loaded(let movies) = viewModel.state else {
            return XCTFail("Expected .loaded, got \(viewModel.state)")
        }
        XCTAssertEqual(movies.count, 1)
        XCTAssertEqual(movies.first?.title, "Dune")
    }

    func test_load_failure_updatesStateToFailed() async {
        let fake = FakeMovieService(result: .failure(URLError(.notConnectedToInternet)))
        let viewModel = MovieListViewModel(service: fake)

        await viewModel.load()

        guard case .failed = viewModel.state else {
            return XCTFail("Expected .failed, got \(viewModel.state)")
        }
    }
}

struct FakeMovieService: MovieServicing {
    let result: Result<[Movie], Error>
    func fetchMovies() async throws -> [Movie] {
        try result.get()
    }
}

// Newer Swift Testing syntax, for reference:
// import Testing
// @Test func loadSuccessUpdatesState() async {
//     #expect(movies.count == 1)
// }
```

### 5. Exercises

1. Write `XCTest` tests for Module 6's `Stack<Element>`: push/pop order, `isEmpty`, popping an empty stack.
2. Write `async` `XCTest` tests for Module 8's weather-fetching function using a fake/injected URL session or protocol, not a real network call.
3. Write tests for Module 12's `MovieListViewModel` covering `.loading` → `.loaded` and `.loading` → `.failed` transitions, exactly as shown above.
4. Write a test that deliberately fails first (red), then make it pass (green) — practice literal TDD red/green/refactor on one small function.
5. Use Instruments' Leaks tool (or Xcode's Memory Graph Debugger) on Module 7's intentionally-leaky Stopwatch project; confirm it visually shows the leak, then confirm the fixed version doesn't.
6. Write a test asserting a `Codable` model round-trips correctly (encode then decode equals the original) using `Equatable` conformance.
7. Benchmark (via `XCTest`'s `measure { }` or manual `Date` timestamps) inserting 10,000 elements at the front of an `Array` vs. appending 10,000 to the end — relate the result to the Big-O claims above.
8. **Harder:** write a test for a Combine-based pipeline (Module 13) using `XCTestExpectation` to wait for an async `sink` to fire.
9. **Harder:** identify one function in any of your mini projects so far that's *not* currently testable (tightly coupled to `URLSession`, `UserDefaults`, or similar), and refactor it to be testable via protocol injection.
10. **Harder:** write a stress test that adds 100,000 items to your Module 11 persistence layer and measure save/load time — is your chosen approach (`Codable`-to-disk vs. `SwiftData`) still reasonable at that scale? Write a sentence with your conclusion.

### 6. Mini Project: Full Test Suite

Pick your Module 11 Recipe App or Module 12 Movie Database App and bring it to real test coverage:
- Unit tests for every ViewModel's state transitions (loading/success/failure)
- Unit tests for any pure business logic (filtering, sorting, validation)
- At least one test using a fake/injected dependency, proving no real network or disk I/O happens during the test run
- Run the suite and confirm all green before moving on

### 7. Reflection Questions

- Why is "testing the View" usually the wrong instinct in a well-architected SwiftUI app, and what should you test instead?
- What specifically does protocol-based dependency injection (Module 12) enable here that a hardcoded `URLSession.shared` call inside the ViewModel would prevent?
- Given `Array`'s O(1) amortized append but O(n) front-insert, when would you reach for a different data structure entirely (and which one) if front-insertion were a frequent operation in a real app?

### 8. Common Mistakes

- **Testing implementation details instead of behavior** (e.g., asserting a private helper was called, rather than asserting the resulting public state) — makes tests brittle to harmless refactors.
- **Hitting the real network or real disk in unit tests** — makes the suite slow and flaky; almost always a sign a dependency should have been protocol-injected.
- **Not testing the unhappy path** — every ViewModel touched in this roadmap has a `.failed`/error state; untested error paths are exactly where production bugs hide.
- **Ignoring Big-O until it's a production problem** — knowing `Array` front-insertion is O(n) *before* you build a feature that does it in a hot loop is cheaper than profiling it after users complain.

### 9. Challenge

Take any mini project from Modules 9–13 and get it to a state where you could confidently say, in an interview, "this is fully unit tested, has no force unwraps, has no retain cycles (verified in Instruments), and every ViewModel is protocol-injected for testability." Fix whatever's missing to make that true.

---

## Milestone 6: Full Mock Interview

Simulate a real 60-minute Apple interview loop. Do this without AI assistance, ideally with a timer, and ideally read aloud/typed as if explaining to an interviewer, not just solved silently.

**Coding (30 min):**
1. Given an array of integers, find the longest strictly increasing subsequence's length.
2. Implement an LRU cache using a `Dictionary` + doubly linked list (or `NSCache` if you want to compare against the "just use the platform" answer) — a very common Apple-adjacent systems question.

**Swift-specific (15 min):**
3. Explain the differences between `struct` and `class` with a real example of when each is correct — you should be able to do this without hesitation by now.
4. Explain what happens, step by step, when a `weak var` reference's underlying object is deallocated.
5. Given a code snippet with a subtle retain cycle in a closure, find it and fix it on sight.

**System/architecture (15 min):**
6. "Design a simple iOS app that shows a list of items fetched from a network, with offline caching and pull-to-refresh." Talk through your MVVM structure, your persistence choice, and your error/loading states out loud, referencing Modules 8, 11, and 12.

Grade yourself honestly. Any question you couldn't answer cleanly is exactly where to spend extra time before the capstone.

---

## Module 15: Advanced Generics & Streaming (AI Client)

### 1. Goal

Go beyond basic generics into associated types and protocol composition, and build a client that streams data incrementally — the shape of a real LLM/chat API integration.

### 2. Concepts

- `associatedtype` and protocols with associated types (PATs)
- generic `where` clauses (advanced constraints)
- `AsyncSequence` / `AsyncStream`
- streaming HTTP responses
- building a small, reusable networking layer

### 3. Short Explanation

**`associatedtype`** lets a protocol declare "I need *some* type here, decided by whoever conforms" without pinning it down — Module 5's `Cache` exercise previewed this. It's the protocol-world equivalent of a generic type parameter, and it's what makes `Sequence`/`Collection` (the protocols underlying `Array`) work generically across wildly different element types. The key interview-relevant subtlety: a protocol with an associated type can't be used as a plain existential type the way a normal protocol can (`any Cache` alone doesn't fully work if `Cache` has an associated type without additional constraints) — this trips up even experienced developers and is worth understanding at least at a "why does this error happen" level.

**`AsyncSequence`** is `async`/`await`'s native answer to a stream of values over time — where Module 13's Combine `Publisher` is the reactive-framework version, `AsyncSequence` lets you `for try await item in stream { }` directly, reading like a normal `for-in` loop over Module 3's collections, but each element arrives asynchronously. This is exactly the shape of a streaming LLM API response — tokens arriving one at a time rather than one big JSON blob at the end.

**Building a small networking layer.** By this point you've written ad hoc `URLSession` calls in Modules 8 and 12. A real client factors this into a reusable piece: a generic `func request<T: Decodable>(_ endpoint: Endpoint) async throws -> T`, plus a streaming variant for incremental responses — this is genuinely how production API clients (including Anthropic's and OpenAI's own SDK internals) are shaped.

### 4. Syntax Cheatsheet

```swift
protocol DataStore {
    associatedtype Item
    func save(_ item: Item)
    func fetchAll() -> [Item]
}

struct InMemoryStore<T>: DataStore {
    private var items: [T] = []
    mutating func save(_ item: T) { items.append(item) }
    func fetchAll() -> [T] { items }
}

// AsyncStream: bridge a callback-based or manual producer into AsyncSequence
func countdown(from n: Int) -> AsyncStream<Int> {
    AsyncStream { continuation in
        Task {
            for i in stride(from: n, through: 0, by: -1) {
                continuation.yield(i)
                try? await Task.sleep(nanoseconds: 500_000_000)
            }
            continuation.finish()
        }
    }
}

Task {
    for await tick in countdown(from: 3) {
        print(tick)
    }
}

// Streaming chat response shape
struct ChatChunk: Decodable { let delta: String }

func streamChatResponse(prompt: String) -> AsyncThrowingStream<String, Error> {
    AsyncThrowingStream { continuation in
        Task {
            do {
                var request = URLRequest(url: URL(string: "https://api.example.com/chat")!)
                request.httpMethod = "POST"
                // ... encode prompt into request.httpBody ...

                let (bytes, response) = try await URLSession.shared.bytes(for: request)
                guard let http = response as? HTTPURLResponse, http.statusCode == 200 else {
                    throw URLError(.badServerResponse)
                }
                for try await line in bytes.lines {
                    guard let data = line.data(using: .utf8),
                          let chunk = try? JSONDecoder().decode(ChatChunk.self, from: data) else { continue }
                    continuation.yield(chunk.delta)
                }
                continuation.finish()
            } catch {
                continuation.finish(throwing: error)
            }
        }
    }
}

// Generic reusable request layer
struct Endpoint { let url: URL; let method: String = "GET" }

func request<T: Decodable>(_ endpoint: Endpoint) async throws -> T {
    var req = URLRequest(url: endpoint.url)
    req.httpMethod = endpoint.method
    let (data, response) = try await URLSession.shared.data(for: req)
    guard let http = response as? HTTPURLResponse, 200..<300 ~= http.statusCode else {
        throw URLError(.badServerResponse)
    }
    return try JSONDecoder().decode(T.self, from: data)
}
```

### 5. Exercises

1. Build the `countdown(from:)` `AsyncStream` above and consume it with `for await`.
2. Write a protocol with an `associatedtype`, two different conforming types with different concrete types for it, and a generic function that works across both.
3. Refactor Module 8 and Module 12's separate `URLSession` calls into the single generic `request<T: Decodable>(_:)` function shown above; update both call sites to use it.
4. Build an `AsyncThrowingStream` that simulates streamed text (yield one word at a time from a hardcoded sentence, with a small delay) before attempting a real streaming API.
5. Consume a streaming response with `for try await` and append each chunk to a `@Published var responseText: String` so a SwiftUI view updates live, token by token.
6. Predict-then-run: what happens if a consumer of an `AsyncStream` stops iterating early (`break`)? Does the producer's `Task` get cancelled? Investigate.
7. Add cancellation support: let the user tap "stop" mid-stream and confirm the underlying `Task`/network request actually stops.
8. **Harder:** write a generic retry wrapper `func withRetry<T>(times: Int, operation: () async throws -> T) async throws -> T` and apply it to your generic `request` function.
9. **Harder:** compare, in a short paragraph, `AsyncSequence`/`AsyncStream` against Module 13's Combine `Publisher` for this exact streaming-chat use case — which would you actually ship, and why?
10. **Harder:** implement basic error-typed responses — if the API returns a non-2xx status with a JSON error body, decode *that* into a specific `Error` type instead of a generic `URLError`.

### 6. Mini Project: AI Client (SwiftUI)

Build a small SwiftUI chat client that streams responses from a real LLM API (use whichever provider you have API access to; keep the key out of source control):
- MVVM structure (Module 12): a `ChatServicing` protocol, a real implementation using `AsyncThrowingStream`, and a `FakeChatService` for tests
- `@Published var messages: [ChatMessage]` where the in-progress assistant message's text grows live as chunks arrive
- A "stop generating" button that cancels the in-flight `Task`
- Basic error handling: network failure, API error responses, and a retry action
- Persist chat history using Module 11's approach of choice

### 7. Reflection Questions

- Why can't you always use `any DataStore` directly as a variable's type when `DataStore` has an `associatedtype`, the way you could with a plain protocol? What's the compiler protecting you from?
- What's structurally different between consuming an `AsyncStream` with `for await` and consuming a Combine `Publisher` with `sink`, beyond just syntax?
- Why does factoring `URLSession` calls into one generic `request<T: Decodable>` function (rather than repeating similar code in every service) matter beyond "less typing" — think about what happens when you need to add a shared auth header or logging later.

### 8. Common Mistakes

- **Buffering an entire streaming response before displaying anything** — defeats the entire purpose of streaming; make sure chunks actually render incrementally.
- **Not handling stream cancellation** — leaves network requests running (and burning quota/cost) after a user navigates away or taps stop.
- **Hardcoding API keys directly in source** — even for a learning project, practice keeping secrets out of version control (a `.gitignore`d config file or environment variable) as the default habit.
- **Treating `AsyncSequence` and Combine as interchangeable everywhere** — they overlap but aren't identical; know when bridging between them is actually necessary versus just picking one and staying consistent.

### 9. Challenge

Extend the AI Client with "function calling"-style structured output: define a generic decoder path that can interpret either a plain text streamed response *or* a structured JSON tool-call response arriving in the same stream, using an enum with associated values (Module 5) to represent "this chunk is text" vs. "this chunk is a tool call" — a realistic shape for modern LLM API integrations.

---

## Capstone: App Store-Quality SwiftUI App

Everything up to this point was a mini project. This is the real thing: pick your own app idea (or extend the AI Client from Module 15 into something more complete) and build it to a standard you'd be comfortable submitting to the App Store and showing an Apple interviewer as your portfolio piece.

### Requirements Checklist

**Architecture**
- [ ] Clean MVVM throughout — no networking/persistence logic inside Views
- [ ] Protocol-based dependency injection for every external dependency (network, disk, system services)
- [ ] A clear folder/module structure separating Models, Views, ViewModels, Services, and Persistence

**Networking**
- [ ] A reusable, generic networking layer (Module 15's `request<T>` pattern, extended with shared headers/auth/logging)
- [ ] Proper error typing — distinct handling for no-connection, bad-response, decode-failure, and server-error-body cases
- [ ] Retry/backoff where appropriate

**Persistence**
- [ ] A deliberate, justified persistence choice (`UserDefaults`/`@AppStorage` for settings, `Codable`-to-disk or `SwiftData` for structured data)
- [ ] Offline-capable: the app is usable (at least read-only) with no network connection
- [ ] A data migration path if your model shape changes during development (Module 11)

**Testing**
- [ ] Unit tests for every ViewModel's state transitions, including failure paths
- [ ] Fakes/mocks for every external dependency — the test suite runs with zero real network or disk access
- [ ] At least one performance/stress test on a realistic data volume

**Accessibility**
- [ ] Every interactive element has a meaningful `accessibilityLabel`
- [ ] The app is fully usable with VoiceOver (test this for real, not just in theory)
- [ ] Dynamic Type support — text scales correctly at larger accessibility text sizes without breaking layout
- [ ] Sufficient color contrast; the app doesn't rely on color alone to convey state

**Animations**
- [ ] At least one meaningful (not gratuitous) animation using `withAnimation` or `.animation(_:value:)`
- [ ] Loading/transition states feel intentional, not abrupt

**Widgets**
- [ ] At least one WidgetKit widget showing live data from your app (a small/medium home screen widget is enough)

**App Icons & Polish**
- [ ] A real app icon (all required sizes) — even a simple, deliberate design beats a placeholder
- [ ] A consistent visual identity: color scheme, typography, spacing applied consistently across every screen
- [ ] Empty states, loading states, and error states are all designed, not just functional afterthoughts

**Deployment**
- [ ] Signing configured correctly (development and distribution certificates/profiles)
- [ ] App builds and archives successfully for release (`Product > Archive`)
- [ ] Uploaded to App Store Connect via Xcode or Transporter

**TestFlight**
- [ ] Internal testing group set up, build distributed, and installed on a real device (not just simulator)
- [ ] At least one round of feedback incorporated

**App Store Submission**
- [ ] App Store listing complete: screenshots (real device sizes), description, keywords, privacy policy URL, app privacy nutrition label filled out accurately
- [ ] Submitted for review (you don't have to actually publish it — getting through the submission process and review is the learning goal)

### Reflection

Once this is done, write a short retrospective (a few paragraphs, for yourself, not for grading):
- Which module's concepts did you end up leaning on most in the capstone?
- What would you do differently architecturally if you started this app over today?
- Which Milestone question, in hindsight, do you now understand at a genuinely different level than when you first answered it?

If you can answer all three of those with real specificity, you're at the level this roadmap was built to get you to.

---

## Appendix: Apple Interview Question Bank

A running list — return here throughout the roadmap, not just at the end. You should be able to answer every one of these cleanly by the time you reach the Capstone.

**Language fundamentals**
- What is an optional, really, under the hood?
- `struct` vs `class` — give the full picture: value vs reference semantics, mutability, performance, when to choose each.
- What does `mutating` do, mechanically?
- Explain `guard` vs `if` for unwrapping — when is each the right call?
- What's the difference between `==` and `===`?

**Memory & concurrency**
- Explain ARC without saying the words "garbage collection."
- `weak` vs `unowned` — give the precise rule, not just "weak is safer."
- Describe a retain cycle you've actually created and fixed (have a real example ready, from Module 7).
- What's a data race, and how is it different from a retain cycle?
- What does `@MainActor` do, and why does it matter for `ObservableObject`s?

**Type system**
- What's a protocol with an associated type, and why can't you always use it as `any SomeProtocol`?
- Explain protocol-oriented programming with a concrete example inheritance handles worse.
- When would you use `Result<T, Error>` over `throws`?
- Generic constraints — write one from memory (`<T: Comparable>` or similar) and explain what it unlocks.

**SwiftUI & architecture**
- `@State` vs `@Binding` vs `@StateObject` vs `@ObservedObject` vs `@EnvironmentObject` — the ownership rule for each, from memory.
- Why MVVM in SwiftUI specifically — what does the ViewModel do that the View shouldn't?
- How do you make a ViewModel testable without hitting the real network?
- Combine vs `async`/`await` — when does each win?

**Data structures & algorithms (language-agnostic, but answer in Swift)**
- Implement a hash map from scratch (conceptually — you don't need to reimplement `Dictionary`, but explain how it achieves O(1) average lookup).
- Two Sum, in O(n).
- Reverse a linked list, iteratively and recursively.
- Binary search, and the exact conditions under which it's valid to use.
- Explain Big-O for `Array` append/insert/remove and `Dictionary` insert/lookup/delete.

**Systems / design (lite)**
- Design an iOS app that lists items from a network with offline support — talk through architecture out loud.
- How would you handle a slow or flaky network in a production app's UX, not just its code?
- How would you structure a codebase so five iOS engineers can work on the same app without constant merge conflicts?
