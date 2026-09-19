# C++ — From Zero to Solid Intermediate

> A 26-lesson self-study track, organised into 5 blocks.
> One domain throughout: cars, garage and fleet management (the same as the Python track).
> Every lesson is a `.cpp` file that compiles and runs clean. One commit per lesson.

**Mandatory checks for every lesson (C++20, GCC 13+ or Clang 17+):**

```bash
g++ -std=c++20 -Wall -Wextra -Wpedantic -Werror -g lessonNN.cpp -o lessonNN
./lessonNN
```

From Lesson 13 onwards, also build and run with sanitizers:

```bash
g++ -std=c++20 -Wall -Wextra -Wpedantic -g -fsanitize=address,undefined lessonNN.cpp -o lessonNN_san
./lessonNN_san
```

From Lesson 25 onwards, every change runs `ctest` before the commit.

> `-Wall -Wextra -Wpedantic` turn on the compiler's warnings; `-Werror` turns
> them into errors so you cannot ignore them. The sanitizers catch at runtime
> what the compiler cannot see: leaks, out-of-bounds reads, dangling pointers,
> undefined behaviour. They are non-negotiable in this language.

---

## BLOCK I — Foundations

*You have never written C++. By the end you write terminal programs that work.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 1 | First program and variables | `#include`, `int main()`, `return 0`, `std::cout` and `<<`, the basic types (`int`, `double`, `bool`, `char`, `std::string`), static typing, `const`, `7/2` vs `7/2.0` | `lesson01.cpp` |
| 2 | Operators and expressions | arithmetic, comparison, logical, `+=` and `++`, precedence, implicit conversions and why they bite, `static_cast` | `lesson02.cpp` |
| 3 | Conditionals | `if` / `else if` / `else`, `switch` and fallthrough, ternary, `if` with initialiser | `lesson03.cpp` |
| 4 | Loops | `for`, `while`, `do...while`, `break`, `continue`, range-based `for`, nested loops | `lesson04.cpp` |
| 5 | Functions I | declaration vs definition, parameters, return types, `void`, scope, lifetime of locals | `lesson05.cpp` |
| 6 | **Passing arguments** | by value vs `&` vs `const&`, when to use each, what actually gets copied, overloading, default arguments | `lesson06.cpp` |

> **Lesson 6 is the most important of this block.** "Who owns this, and is it
> being copied?" is the question C++ makes you answer on every single line. It
> is the C++ equivalent of names-and-objects in Python. Do not rush it.

**Block I checkpoint:** you can write a looping terminal menu, built from
functions, that never crashes on bad input.

---

## BLOCK II — Data and structure

*You stop juggling loose variables and start modelling the problem.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 7 | `std::string` | methods, `.substr()`, `.find()`, `[]` vs `.at()`, iterating characters, `std::string_view`, why never `char*` | `lesson07.cpp` |
| 8 | `std::vector` | dynamic growth, `push_back`, `.size()`, `reserve`, iteration, passing to functions, out-of-bounds is UB not an error | `lesson08.cpp` |
| 9 | Input and files | `std::cin` and its failure states, `clear` / `ignore`, `getline`, `ifstream` / `ofstream`, always checking the file opened, CSV parsing | `lesson09.cpp` |
| 10 | `struct` and aggregates | grouping data, `std::vector<Car>`, free functions over structs, aggregate initialisation | `lesson10.cpp` |
| 11 | **Your first class** | `class` vs `struct`, `public` / `private`, encapsulation, constructors, member functions, `const` methods, invariants | `lesson11.cpp` |
| 12 | Multiple files and the build | `.h` vs `.cpp`, `#pragma once`, what goes where, compiler errors vs linker errors, the ODR, `namespace`, Makefile | `lesson12/` |

**Block II checkpoint — Mini-Garage project:**
a `Car` class and a `Garage` class holding a `std::vector<Car>`, a full menu,
CSV persistence, input validation, code split across `include/` and `src/`,
built with a Makefile, zero warnings under `-Werror`.

> **End of the beginner level.** If you stopped here, you can program in C++.
> What follows is what makes C++ *C++* — and what separates it from every
> other language you know.

---

## BLOCK III — Memory and ownership

*The heart of the language. This block is the reason C++ exists.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 13 | Pointers and references | memory addresses, `&x` and `*p`, `nullptr`, pointers vs references, stack vs heap, what a segfault actually is | `lesson13.cpp` |
| 14 | `new`, `delete` and what goes wrong | manual allocation, leaks, dangling pointers, double free, reading a sanitizer report, why modern C++ avoids both keywords | `lesson14.cpp` |
| 15 | **RAII** | the resource lives in the object, constructor acquires, destructor releases, why this makes leaks structurally impossible, writing your own RAII wrapper | `lesson15.cpp` |
| 16 | Object lifetime | construction and destruction order, members and bases, scope exit, temporaries, why leaving a block cleans up for free | `lesson16.cpp` |
| 17 | **Copy, move and the Rule of 5** | shallow vs deep copy, copy constructor and `operator=`, move constructor and move assignment, what `std::move` really does, `noexcept`, Rule of 0 | `lesson17.cpp` |
| 18 | Smart pointers | `unique_ptr` and `make_unique`, `shared_ptr` and its cost, `weak_ptr` for reference cycles, which one by default and why | `lesson18.cpp` |

> **Lessons 15 and 17 are the watershed.** Someone who understands RAII and move
> semantics knows C++. Someone who does not writes Java with C++ syntax and
> leaks memory they cannot find.

**Block III checkpoint:** you can explain to a colleague, without notes, what
happens to every object when a function returns, and why `std::vector` needs
`noexcept` on the move constructor to use it.

---

## BLOCK IV — Abstraction and the standard library

*You stop reinventing the wheel and start using the language as it was designed.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 19 | Inheritance and polymorphism | base and derived, `virtual`, `override`, `final`, abstract classes, **virtual destructors**, object slicing, the vtable | `lesson19.cpp` |
| 20 | Errors and exceptions | `throw` / `try` / `catch`, standard exceptions, custom hierarchies, RAII as the thing that makes exceptions safe, `std::optional` | `lesson20.cpp` |
| 21 | Choosing containers | `map`, `unordered_map`, `set`, `deque`, `array`, complexity of each operation, when a tree beats a hash table | `lesson21.cpp` |
| 22 | Algorithms and lambdas | lambda syntax, captures by value and by reference, `sort`, `find_if`, `accumulate`, `erase_if`, ranges and views | `lesson22.cpp` |
| 23 | Templates | function and class templates, why they exist, C++20 `concepts`, `if constexpr`, reading a 40-line template error | `lesson23.cpp` |
| 24 | Modern C++ in practice | `auto` used well, structured bindings, `chrono`, `filesystem`, `format`, `variant` and `visit` | `lesson24.cpp` |

**Block IV checkpoint:** you pick the right container for a problem and justify
it with its complexity, and you can tell whether a class needs a virtual
destructor just by looking at how it is used.

---

## BLOCK V — Going professional

*The difference between code that works and code you ship.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 25 | Tooling | CMake, GoogleTest (fixtures, parametrised tests), `gdb`, sanitizers in the build, `clang-format`, `clang-tidy`, GitHub Actions CI | `lesson25/` |
| 26 | **Capstone project** | full FleetManager: vehicles, trips, maintenance, CLI + file persistence, with tests, CI, documented | repository |

> Optional capstone extension: port the core to an ESP32 with real sensor
> input. It is the natural bridge to embedded work.

---

## How you know you have reached solid intermediate

You can answer all of these without looking anything up:

- [ ] Why must a base class destructor be `virtual`, and what happens if it isn't?
- [ ] What exactly does `std::move(x)` do? (Hint: less than the name suggests.)
- [ ] What is the difference between `std::vector<T>` and `std::vector<std::unique_ptr<T>>`, and when do you use each?
- [ ] What is the Rule of 0, and why is it the goal rather than the Rule of 5?
- [ ] What is undefined behaviour? Give three examples you have personally caused.
- [ ] Why is `map` O(log n) and `unordered_map` O(1) on average — and when does `map` still win?
- [ ] Why is `void f(const std::string&)` usually better than `void f(std::string)` — and when is it not?
- [ ] What is object slicing, and how do you prevent it?
- [ ] What is the strong exception guarantee, and how does RAII help you get it?
- [ ] When does a `shared_ptr` leak, and what fixes it?

And you can do all of these:

- [ ] Read a 40-line template error and find the actual cause
- [ ] Use `gdb` to track down a segfault instead of adding `cout`s
- [ ] Set up a project from scratch with CMake, tests, formatting and CI
- [ ] Get a non-trivial program to run clean under ASan, UBSan and valgrind
- [ ] Read someone else's C++ without getting lost

---

## What this track deliberately does **not** cover

Advanced topics, intentionally out of scope. They are not worth the time yet:

- Heavy template metaprogramming (SFINAE, recursive templates, type erasure)
- Lock-free programming and the atomic memory model
- Custom allocators beyond a toy pool
- C++20 modules (compiler support is still uneven)
- Coroutines
- Multiple and virtual inheritance
- Profile-guided optimisation and hand-tuned SIMD

Domain tracks are also left out of the core. They come after Lesson 26:

- **Concurrency:** `thread`, `mutex`, `atomic`, `condition_variable`, ThreadSanitizer
- **Embedded and hardware:** no-heap / no-exception code, bit manipulation, memory layout, reading assembly
- **Performance:** Google Benchmark, `perf`, cache locality, profiling
- **Computer vision and robotics:** OpenCV, ROS 2, CUDA

---

## Pace

| Block | Lessons | Realistic time |
|---|---|---|
| I — Foundations | 1–6 | 1 week |
| II — Data and structure | 7–12 + project | 2 weeks |
| III — Memory and ownership | 13–18 | 2–3 weeks |
| IV — Abstraction and STL | 19–24 | 3 weeks |
| V — Going professional | 25–26 | 2 weeks |

**Total: roughly 11 weeks** at 1–2 hours per day. With coursework alongside,
count on 3 to 4 months. It is not a race — Blocks III and IV are what matter.

> Slower than the Python track, and that is expected. In Python the runtime
> handles memory for you; in C++ that responsibility is yours, and learning to
> carry it is most of the work.

---

## Ground rules

1. Never commit code you cannot explain line by line.
2. Always compile with `-Wall -Wextra -Wpedantic -Werror`. A warning is a deferred bug.
3. From Lesson 13 onwards, always run under `-fsanitize=address,undefined`. Code that "works" can still be broken.
4. A 40-line compiler error? Read **the first line** — the rest is fallout. A segfault? Reach for `gdb`, not `cout`.
5. One commit per lesson. The history is the proof of the journey.
