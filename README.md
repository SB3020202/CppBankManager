# Learning C++

My journey learning C++ from zero, one lesson at a time.

**Build any lesson:**

```bash
g++ -std=c++20 -Wall -Wextra -Wpedantic -g lesson01.cpp -o lesson01
./lesson01
```

---

## Block I — Foundations

### Lesson 1 — First program and variables ☐
- `#include`, `int main()`, `return 0`
- `std::cout` and `<<`
- The 5 basic types: `int`, `double`, `bool`, `char`, `std::string`
- `const`
- Integer division: `7 / 2` is 3, not 3.5

### Lesson 2 — Operators and expressions ☐
- Arithmetic: `+ - * / %`
- Comparison: `== != < > <= >=`
- Logical: `&& || !`
- `+=`, `-=`, `++`, `--`
- Operator precedence
- `static_cast<double>(x)`

### Lesson 3 — Conditionals ☐
- `if`, `else if`, `else`
- `switch` and why you need `break`
- Ternary: `condition ? a : b`
- Nesting conditions

### Lesson 4 — Loops ☐
- `for` loop
- `while` loop
- `do...while` loop
- `break` and `continue`
- Range-based for: `for (int x : numbers)`
- Nested loops

### Lesson 5 — Functions I ☐
- Writing a function: return type, name, parameters
- `return`
- `void` functions
- Declaration (prototype) vs definition
- Local variables and scope

### Lesson 6 — Functions II: passing arguments ☐
- **By value** — the function gets a copy
- **By reference (`&`)** — the function changes the original
- **By const reference (`const&`)** — no copy, no changes
- When to use each one
- Function overloading
- Default arguments

> The most important lesson of this block.

---

## Block II — Data and structure

### Lesson 7 — `std::string` ☐
- Creating, joining with `+`, comparing with `==`
- `.size()`, `.empty()`, `.substr()`, `.find()`
- `[]` vs `.at()`
- Looping over characters
- `std::getline` for reading a full line

### Lesson 8 — `std::vector` ☐
- Creating a vector
- `push_back()`, `pop_back()`
- `.size()`, `.empty()`, `.clear()`
- Access with `[]` and `.at()`
- Looping: index vs range-based
- Passing a vector to a function

### Lesson 9 — Input and files ☐
- Reading with `std::cin`
- Why `cin >>` breaks on bad input, and how to recover
- Mixing `cin >>` and `getline`
- Writing files with `std::ofstream`
- Reading files with `std::ifstream`
- Checking the file actually opened
- Splitting a CSV line

### Lesson 10 — `struct` ☐
- Grouping related data into one type
- Creating and using a struct
- `std::vector<MyStruct>`
- Passing structs to functions
- Functions that work on structs

### Lesson 11 — Your first class ☐
- `class` vs `struct`
- `public` and `private`
- Why hiding data matters (encapsulation)
- Constructors
- Member functions (methods)
- `const` methods
- Getters
- Invariants: rules your class must always keep true

### Lesson 12 — Multiple files ☐
- Header files (`.h`) vs source files (`.cpp`)
- `#pragma once`
- What goes in the header, what goes in the source
- Compiling several files together
- Linker errors vs compiler errors
- `namespace`
- Writing a simple Makefile

**Milestone project — Mini-Garage:** a terminal program to manage cars.
Add, remove, search, drive, refuel, save and load from a file.

---

## Block III — Memory and ownership

### Lesson 13 — Pointers and references ☐
- What memory addresses are
- `&x` gets an address, `*p` reads the value
- Declaring a pointer: `int* p`
- `nullptr` and always checking for it
- References vs pointers
- Stack vs heap

### Lesson 14 — `new`, `delete` and what goes wrong ☐
- Allocating with `new`, freeing with `delete`
- Memory leaks
- Dangling pointers
- Double free
- Running with `-fsanitize=address` to catch all of it
- Why you should avoid `new` and `delete` in modern C++

### Lesson 15 — RAII ☐
- The core idea of C++: the resource lives inside the object
- Constructor takes it, destructor releases it
- Why this makes leaks impossible
- Writing a small RAII class

### Lesson 16 — Object lifetime ☐
- When constructors run
- When destructors run
- Order of construction and destruction
- Objects inside other objects
- Why leaving a scope cleans up automatically

### Lesson 17 — Copy, move and the Rule of 5 ☐
- What happens when you copy an object
- Copy constructor and copy assignment
- Shallow copy vs deep copy
- Move constructor and move assignment
- `std::move` — what it actually does
- `noexcept`
- Rule of 5 and Rule of 0

### Lesson 18 — Smart pointers ☐
- `std::unique_ptr` — one owner
- `std::make_unique`
- `std::shared_ptr` — shared ownership
- `std::weak_ptr` — breaking reference cycles
- Which to use by default

---

## Block IV — Abstraction and the standard library

### Lesson 19 — Inheritance and polymorphism ☐
- Base classes and derived classes
- `virtual` functions
- `override` and `final`
- Abstract classes and pure virtual functions
- **Virtual destructors — and why forgetting one is a bug**
- Object slicing

### Lesson 20 — Errors and exceptions ☐
- `throw`, `try`, `catch`
- Standard exceptions
- Writing your own exception class
- `std::optional` for "maybe there's a value"
- Keeping objects valid when something throws

### Lesson 21 — STL containers ☐
- `std::map` — sorted key-value pairs
- `std::unordered_map` — fast key-value lookup
- `std::set`
- `std::deque`
- Big O of each operation
- How to pick the right one

### Lesson 22 — Algorithms and lambdas ☐
- Lambdas: `[](int x) { return x * 2; }`
- Capturing variables in a lambda
- `std::sort`
- `std::find_if`, `std::count_if`
- `std::accumulate`
- `std::erase_if`
- Why these beat hand-written loops

### Lesson 23 — Templates ☐
- Why write the same function twice for `int` and `double`?
- Function templates
- Class templates
- C++20 `concepts` — restricting what types are allowed
- Reading template error messages

### Lesson 24 — Modern C++ ☐
- `auto`
- Structured bindings: `auto [key, value] : myMap`
- `std::chrono` for time and dates
- `std::filesystem` for files and paths
- `std::format` for clean output
- `std::string_view`

---

## Block V — Going professional

### Lesson 25 — Tooling ☐
- CMake instead of a Makefile
- Writing unit tests with GoogleTest
- Finding bugs with `gdb`
- Sanitizers: address and undefined behaviour
- `clang-format` and `clang-tidy`
- GitHub Actions: building and testing on every push

### Lesson 26 — Capstone: FleetManager ☐
A full fleet management program using everything above:
- Abstract `Vehicle`, with `CombustionCar` and `ElectricCar` derived
- Ownership with `unique_ptr`
- Custom exception hierarchy
- STL containers, chosen deliberately
- A templated repository class
- Save and load from file
- A CLI that never crashes on bad input
- Unit tests
- Zero compiler warnings, zero sanitizer errors

---

## Rules I follow

1. Never commit code I can't explain line by line.
2. Always compile with `-Wall -Wextra -Wpedantic`.
3. From Lesson 13 onwards, always run with `-fsanitize=address,undefined`.
4. A 40-line compiler error? Read **the first line**. The rest is fallout.
5. One commit per lesson.
