# Undefined behavior

Undefined behavior (UB) is when the C++ standard places **no requirements** on
what your program does. The compiler is allowed to do anything: crash, return
garbage, silently "work", or even delete the surrounding code during
optimization. This is different from Python, which raises an exception when
something goes wrong.

## Why it is dangerous

- **No exception is thrown.** Unlike Python, C++ does not tell you that the
  range was empty.
- **It may not crash.** The program can read a garbage value and produce a
  wrong answer, which is worse in a contest because it can pass the sample
  tests.
- **The compiler may exploit it.** Once the compiler assumes UB never happens,
  it can optimize away checks you were relying on.

## Other common sources of UB

- Dereferencing `end()` from `find`, `lower_bound`, `min_element`, etc.
- Out-of-bounds access, such as `v[v.size()]` or `v[-1]`.
- Signed integer overflow.
- Reading an uninitialized variable.
- Modifying a container while iterating over it.

## How to catch it

Compile and test locally with the sanitizers enabled. They turn many silent UB
bugs into loud errors.

```sh
g++ -std=c++20 -fsanitize=address,undefined -g main.cpp -o main
```
