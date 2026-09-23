# C++ — From Zero to Solid Intermediate (v2)

> A 27-lesson self-study track, organised into 5 blocks.
> One domain throughout: cars, garage and fleet management (the same as the Python track).
> Every lesson is a `.cpp` file that compiles and runs clean. One commit per lesson.

**Mandatory build for every lesson, from Lesson 1 (C++20, GCC 13+ or Clang 17+):**

```bash
g++ -std=c++20 -Wall -Wextra -Wpedantic -Werror -g \
    -fsanitize=address,undefined -fno-sanitize-recover=all \
    -D_GLIBCXX_ASSERTIONS \
    lessonNN.cpp -o lessonNN
./lessonNN
```

What each part does:

- `-Wall -Wextra -Wpedantic` turn on the compiler's warnings; `-Werror` turns them into errors so you cannot ignore them.
- `-g` keeps debug information, so every error report points to a file and a line.
- `-fsanitize=address,undefined` adds runtime checks that catch what the compiler cannot see: leaks, out-of-bounds reads, dangling pointers, undefined behaviour.
- `-fno-sanitize-recover=all` stops the program at the first undefined behaviour instead of printing a message and carrying on, so you cannot miss it.
- `-D_GLIBCXX_ASSERTIONS` makes GCC's standard library check things like `v[i]` being in range. On other standard libraries it does nothing, so it is harmless to leave in.

> Sanitizers are on from day one because undefined behaviour does not wait for
> pointers: an uninitialised variable in Lesson 1 or `v[10]` on a 5-element
> vector in Lesson 9 already triggers it.
>
> On Windows, work inside WSL. The sanitizers do not work with MinGW.

From Lesson 14 the build moves to CMake, with the same flags.
From Lesson 26 onwards, every change runs `ctest` before the commit.

---

## BLOCK I — Foundations

*You have never written C++. By the end you write terminal programs that work.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 1 | First program and variables | `#include`, `int main()`, `return 0`, `std::cout` and `<<`, the basic types (`int`, `double`, `bool`, `char`, `std::string`), static typing, `const`, `7/2` vs `7/2.0`, **always initialise** (`int x{};`): reading an uninitialised variable is your first undefined behaviour | `lesson01.cpp` |
| 2 | Operators and expressions | arithmetic, comparison, logical, `+=` and `++`, precedence, implicit conversions and why they bite, brace initialisation refusing narrowing, `static_cast` | `lesson02.cpp` |
| 3 | Conditionals | `if` / `else if` / `else`, `switch` and fallthrough, `[[fallthrough]]` and why `-Wextra` complains without it, ternary, `if` with initialiser | `lesson03.cpp` |
| 4 | Loops | `for`, `while`, `do...while`, `break`, `continue`, range-based `for`, nested loops | `lesson04.cpp` |
| 5 | Reading keyboard input | `std::cin` and `>>`, what happens when the user types letters where a number is expected (the failure state), `clear` / `ignore`, `std::getline`, the `>>`-then-`getline` trap, end of input (Ctrl+D) and the infinite-loop trap, a validation loop you will reuse everywhere | `lesson05.cpp` |
| 6 | Functions I | declaration vs definition, parameters, return types, `void`, scope, lifetime of locals | `lesson06.cpp` |
| 7 | **Passing arguments** | by value vs `&` vs `const&`, when to use each, what actually gets copied, returning by value (and why it is cheap — explained in Lesson 19), overloading, default arguments | `lesson07.cpp` |

> **Lesson 7 is the most important of this block.** "Who owns this, and is it
> being copied?" is the question C++ makes you answer on every single line. It
> is the C++ equivalent of names-and-objects in Python. Do not rush it.

**Block I checkpoint:** you can write a looping terminal menu, built from
functions, that never crashes on bad input: letters where a number is expected,
empty lines, or Ctrl+D.

---

## BLOCK II — Data and structure

*You stop juggling loose variables and start modelling the problem.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 8 | `std::string` | methods, `.substr()`, `.find()`, `[]` vs `.at()` (`.at()` checks and throws — you learn to catch it in Lesson 10), iterating characters, `std::to_string` / `std::stoi`, why C++ code uses `std::string` instead of C-style `char` arrays | `lesson08.cpp` |
| 9 | `std::vector` | dynamic growth, `push_back`, `.size()`, `reserve`, iteration, passing to functions by `const&`, out-of-bounds with `[]` is undefined behaviour, not an error — and how your build flags catch it | `lesson09.cpp` |
| 10 | Exceptions and `std::optional` — the basics | `throw` / `try` / `catch`, `std::exception` and `.what()`, catching by `const&`, the ones you have already met (`out_of_range` from `.at()`, `invalid_argument` from `stoi`), what happens when nobody catches, `std::optional` when "not found" is a normal outcome vs an exception when something went wrong | `lesson10.cpp` |
| 11 | Files and CSV | `ifstream` / `ofstream`, always checking the file opened, reading line by line, splitting CSV with `getline` and `std::stringstream`, converting fields with `stoi` / `stod` and handling bad lines without crashing | `lesson11.cpp` |
| 12 | `struct` and aggregates | grouping data, `std::vector<Car>`, free functions over structs, aggregate initialisation | `lesson12.cpp` |
| 13 | **Your first class** | `class` vs `struct`, `public` / `private`, encapsulation, constructors and member initialiser lists, member functions, `const` methods, invariants, a constructor that throws to refuse an invalid `Car` | `lesson13.cpp` |
| 14 | Multiple files and the build | `.h` vs `.cpp`, `#pragma once`, what goes where, compiling and linking by hand (`g++ -c`, then link), compiler errors vs linker errors, the ODR, `namespace`, a minimal `CMakeLists.txt` with warnings and sanitizers | `lesson14/` |

**Block II checkpoint — Mini-Garage project:**
a `Car` class that refuses invalid data, a `Garage` class holding a
`std::vector<Car>`, search by plate returning `std::optional`, a full menu,
CSV persistence that reports bad lines instead of crashing, input validation,
code split across `include/` and `src/`, built with CMake, zero warnings under
`-Werror`, clean under the sanitizers.

> **End of the beginner level.** If you stopped here, you can program in C++.
> What follows is what makes C++ *C++* — and what separates it from every
> other language you know.

---

## BLOCK III — Memory and ownership

*The heart of the language. This block is the reason C++ exists.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 15 | Pointers and references | memory addresses, `&x` and `*p`, `nullptr`, pointers vs references, stack vs heap, what a segfault actually is, **first steps in `gdb`** (`run`, `bt`, `print`, `frame`) to find the crashing line without adding `cout`s | `lesson15.cpp` |
| 16 | `new`, `delete` and what goes wrong | manual allocation, leaks, dangling pointers, double free, reading a sanitizer report line by line, why modern C++ avoids both keywords | `lesson16.cpp` |
| 17 | Object lifetime | construction and destruction order, members and bases, scope exit, temporaries, returning a reference to a local, references into a vector that grows (invalidation), `std::string_view` and why a view must never outlive its string | `lesson17.cpp` |
| 18 | **RAII** | the resource lives in the object, constructor acquires, destructor releases, why this makes leaks structurally impossible, writing your own RAII wrapper, exception safety (basic and strong guarantees) and why RAII is what makes exceptions safe | `lesson18.cpp` |
| 19 | **Copy, move and the Rule of 5** | shallow vs deep copy, copy constructor and `operator=`, move constructor and move assignment, what `std::move` really does, `noexcept`, Rule of 0 | `lesson19.cpp` |
| 20 | Smart pointers | `unique_ptr` and `make_unique`, `shared_ptr` and its cost, `weak_ptr` for reference cycles, which one by default and why | `lesson20.cpp` |

> **Lessons 17 and 18 are in this order on purpose.** RAII ties a resource to
> an object's lifetime, so you first need to know exactly when objects die.
>
> **Lessons 18 and 19 are the watershed.** Someone who understands RAII and move
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
| 21 | Inheritance and polymorphism | base and derived, `virtual`, `override`, `final`, abstract classes, **virtual destructors**, object slicing, the vtable, your own exception classes deriving from `std::runtime_error` and catching a hierarchy | `lesson21.cpp` |
| 22 | Choosing containers | `map`, `unordered_map`, `set`, `deque`, `array`, complexity of each operation, when a tree beats a hash table | `lesson22.cpp` |
| 23 | Algorithms and lambdas | lambda syntax, captures by value and by reference, `sort`, `find_if`, `accumulate`, `erase_if`, ranges and views | `lesson23.cpp` |
| 24 | Templates | function and class templates, why they exist, C++20 `concepts`, `if constexpr`, reading a 40-line template error | `lesson24.cpp` |
| 25 | Modern C++ in practice | `auto` used well, structured bindings, `chrono`, `filesystem`, `format`, `variant` and `visit` | `lesson25.cpp` |

**Block IV checkpoint:** you pick the right container for a problem and justify
it with its complexity, and you can tell whether a class needs a virtual
destructor just by looking at how it is used.

---

## BLOCK V — Going professional

*The difference between code that works and code you ship.*

| # | Lesson | What you learn | Deliverable |
|:--:|---|---|---|
| 26 | Tooling | CMake in depth (a library target for the core, separate executables), GoogleTest (fixtures, parametrised tests), `gdb` beyond the basics (breakpoints, watchpoints), sanitizers as a build option, `clang-format`, `clang-tidy`, GitHub Actions CI. Optional: `valgrind` on a separate build without sanitizers (the two cannot be combined) | `lesson26/` |
| 27 | **Capstone project** | full FleetManager: vehicles, trips, maintenance, CLI + file persistence, with tests, CI, documented | repository |

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
- [ ] Get a non-trivial program to run clean under ASan and UBSan
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

Domain tracks are also left out of the core. They come after Lesson 27:

- **Concurrency:** `thread`, `mutex`, `atomic`, `condition_variable`, ThreadSanitizer
- **Embedded and hardware:** no-heap / no-exception code, bit manipulation, memory layout, reading assembly
- **Performance:** Google Benchmark, `perf`, cache locality, profiling
- **Computer vision and robotics:** OpenCV, ROS 2, CUDA

---

## Pace

| Block | Lessons | Realistic time |
|---|---|---|
| I — Foundations | 1–7 | 1–1.5 weeks |
| II — Data and structure | 8–14 + project | 2–3 weeks |
| III — Memory and ownership | 15–20 | 2–3 weeks |
| IV — Abstraction and STL | 21–25 | 2–3 weeks |
| V — Going professional | 26–27 | 2 weeks |

**Total: roughly 11–12 weeks** at 1–2 hours per day. With coursework alongside,
count on 3 to 4 months. It is not a race — Blocks III and IV are what matter.

> Slower than the Python track, and that is expected. In Python the runtime
> handles memory for you; in C++ that responsibility is yours, and learning to
> carry it is most of the work.

---

## Ground rules

1. Never commit code you cannot explain line by line.
2. Always compile with `-Wall -Wextra -Wpedantic -Werror`. A warning is a deferred bug.
3. Always build with the sanitizers, from Lesson 1. Code that "works" can still be broken.
4. A 40-line compiler error? Read **the first line** — the rest is fallout. A crash? Read the sanitizer report first; from Lesson 15, reach for `gdb`, not `cout`.
5. One commit per lesson. The history is the proof of the journey.

---

## What changed from v1

- **Keyboard input moved into Block I** (new Lesson 5), so the Block I checkpoint only asks for what you have already learned.
- **Exception basics and `std::optional` moved to Lesson 10**, before the first code that throws (`.at()`, `stoi`, constructors enforcing invariants). Custom exception hierarchies went to Lesson 21 (inheritance) and exception safety to Lesson 18 (RAII).
- **Object lifetime now comes before RAII** (Lessons 17 and 18 were swapped).
- **`std::string_view` moved** from the strings lesson to object lifetime, where dangling views make sense.
- **Sanitizers and library assertions from Lesson 1**, and UBSan now stops the program at the first error.
- **Basic `gdb` in Lesson 15**, when segfaults first appear, instead of Lesson 25.
- **CMake from Lesson 14**, instead of learning a Makefile and switching to CMake later.
- **`valgrind` removed from the checklist**; it is now optional in Lesson 26, on a separate build.
- 26 → 27 lessons.
