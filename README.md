# C++ — From Zero to Solid Intermediate

> A 26-lesson self-study track, organised into 5 blocks.
> One domain throughout: cars, garage and fleet management.
> Every lesson is a `.cpp` file that compiles and runs. One commit per lesson.

**Mandatory flags for every lesson:**

```bash
g++ -std=c++20 -Wall -Wextra -Wpedantic -g lessonNN.cpp -o lessonNN
```

From Lesson 13 onwards, always add `-fsanitize=address,undefined`.

---

## BLOCK I — Foundations

*You have never written C++. By the end of this block you write terminal programs that work.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 1 | First program and variables | `#include`, `main`, `std::cout`, the 5 basic types, `const`, integer division | `lesson01.cpp` |
| 2 | Operators and expressions | arithmetic, comparison, logical, precedence, conversions and `static_cast` | `lesson02.cpp` |
| 3 | Conditionals | `if` / `else if` / `else`, `switch`, ternary, `if` with initialiser | `lesson03.cpp` |
| 4 | Loops | `for`, `while`, `do...while`, `break`, `continue`, range-based `for` | `lesson04.cpp` |
| 5 | Functions I | declaration vs definition, parameters, return values, scope, lifetime | `lesson05.cpp` |
| 6 | **Functions II — argument passing** | by value vs `&` vs `const&`, overloading, default arguments | `lesson06.cpp` |

> **Lesson 6 is the most important of this block.** By value vs by reference vs
> `const&` is what separates people who know C++ from people who write C++ as if
> it were Python. Do not rush it.

**Block I checkpoint:** you can write a looping terminal menu, built from
functions, that never crashes.

---

## BLOCK II — Data and structure

*You stop juggling loose variables and start modelling the problem.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 7 | `std::string` | methods, iteration, validation, `[]` vs `.at()`, `std::string_view` | `lesson07.cpp` |
| 8 | `std::vector` | dynamic growth, `push_back`, iteration, passing to functions, bounds | `lesson08.cpp` |
| 9 | Input and files | `cin` and its pitfalls, `getline`, validation, `ifstream` / `ofstream`, CSV | `lesson09.cpp` |
| 10 | `struct` and aggregates | grouping data, vectors of structs, free functions over them | `lesson10.cpp` |
| 11 | **Your first class** | `public` / `private`, encapsulation, constructors, `const` methods, invariants | `lesson11.cpp` |
| 12 | Multiple files | `.h` vs `.cpp`, `#pragma once`, linker errors, ODR, `namespace`, Makefile | `lesson12/` |

**Block II checkpoint — Mini-Garage project:**
a `Car` class, a `Garage` class holding a `std::vector<Car>`, a full menu,
CSV persistence, code split across `include/` and `src/`, zero warnings.

> **End of the beginner level.** If you stopped here, you can program in C++.
> What follows is what makes C++ different from every other language.

---

## BLOCK III — Memory and ownership

*The heart of C++. This block is the reason the language exists.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 13 | Stack, heap and pointers | addresses, `*` and `&`, `nullptr`, references vs pointers | `lesson13.cpp` |
| 14 | `new`, `delete` and what goes wrong | memory leaks, dangling pointers, double free, sanitizers | `lesson14.cpp` |
| 15 | **RAII** | the resource lives in the object, the destructor cleans up, why this solves everything | `lesson15.cpp` |
| 16 | Object lifetime | constructors, destructors, construction and destruction order, scope | `lesson16.cpp` |
| 17 | **Copy, move and the Rule of 5** | copy constructor, `operator=`, `std::move`, `noexcept`, Rule of 0 | `lesson17.cpp` |
| 18 | Smart pointers | `unique_ptr`, `shared_ptr`, `weak_ptr`, `make_unique`, reference cycles | `lesson18.cpp` |

> **Lessons 15 and 17 are the watershed.** Someone who understands RAII and move
> semantics knows C++. Someone who does not writes Java with C++ syntax.

**Block III checkpoint:** you can explain to a colleague, without notes, why
destructors exist and why `std::vector` needs `noexcept` on the move constructor.

---

## BLOCK IV — Abstraction and the standard library

*You stop reinventing the wheel and start using the language as it was designed.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 19 | Inheritance and polymorphism | `virtual`, `override`, `final`, abstract classes, **virtual destructors**, slicing | `lesson19.cpp` |
| 20 | Errors and exceptions | `try` / `catch`, custom hierarchies, exception safety, `std::optional` | `lesson20.cpp` |
| 21 | STL containers | `map`, `unordered_map`, `set`, `deque`, complexity and how to choose | `lesson21.cpp` |
| 22 | Algorithms and lambdas | `sort`, `find_if`, `accumulate`, `erase_if`, lambda captures, ranges | `lesson22.cpp` |
| 23 | Templates | function and class templates, C++20 `concepts`, `if constexpr` | `lesson23.cpp` |
| 24 | Modern C++ in practice | `auto`, structured bindings, `chrono`, `filesystem`, `format`, `variant` | `lesson24.cpp` |

**Block IV checkpoint:** you pick the right container for a problem and justify
the choice with its algorithmic complexity.

---

## BLOCK V — Going professional

*The difference between code that works and code you ship.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 25 | Tooling | CMake, GoogleTest, `gdb`, sanitizers, `clang-format`, `clang-tidy`, CI | `lesson25/` |
| 26 | **Capstone project** | full FleetManager, with tests, CI and documentation | repository |

---

## How you know you have reached solid intermediate

You can answer all of these without looking anything up:

- [ ] Why must a base class destructor be `virtual`?
- [ ] What is the difference between `std::vector<T>` and `std::vector<std::unique_ptr<T>>`, and when do you use each?
- [ ] What exactly happens when you call `std::move(x)`? (Hint: less than you think.)
- [ ] Why is `map` O(log n) and `unordered_map` O(1) on average — and when does `map` win?
- [ ] What is the Rule of 0, and why is it the goal?
- [ ] What is undefined behaviour? Give three examples.
- [ ] Why is `void f(const std::string&)` usually better than `void f(std::string)` — and when is it not?
- [ ] What is the strong exception guarantee and how do you achieve it?

And you can do all of these:

- [ ] Read a 40-line template error and find the actual cause
- [ ] Use `gdb` to track down the source of a segfault
- [ ] Set up a project from scratch with CMake, tests and CI
- [ ] Read someone else's C++ without getting lost

---

## What this track deliberately does **not** cover

Advanced topics, intentionally out of scope. They are not worth the time yet:

- Heavy template metaprogramming (SFINAE, recursive templates)
- Lock-free programming and atomic memory models
- Serious custom allocators
- C++20 modules (compiler support is still uneven)
- Coroutines
- Multiple and virtual inheritance
- Profile-guided optimisation

Concurrency (`thread`, `mutex`, `atomic`) is also left out of the core track.
It is a separate block, to be taken after Lesson 26 — especially if you head
towards embedded systems or backend work.

---

## Pace

| Block | Lessons | Realistic time |
|---|---|---|
| I — Foundations | 1–6 | 1 week |
| II — Data and structure | 7–12 + project | 2 weeks |
| III — Memory and ownership | 13–18 | 2 weeks |
| IV — Abstraction and STL | 19–24 | 2 weeks |
| V — Going professional | 25–26 | 2 weeks |

**Total: roughly 9 weeks** at 1–2 hours per day. With coursework alongside,
count on 3 months. It is not a race — Blocks III and IV are what matter.

---

## Ground rules

1. Never copy code you cannot explain line by line.
2. Always compile with `-Wall -Wextra -Wpedantic`. A warning is a deferred bug.
3. From Lesson 13 onwards, always run with `-fsanitize=address,undefined`.
4. A 40-line compiler error? Read **the first line**. The rest is fallout.
5. One commit per lesson. The history is the proof of the journey.
