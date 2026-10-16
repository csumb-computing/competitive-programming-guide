---
title: Size of integers
---

## Python

Python integers have **arbitrary precision**. They grow as large as needed,
limited only by memory, so they never overflow.

```python
x = 2 ** 100  # Works fine.
```

## C++

In C++, the size of an integer type is **not fixed by the standard**. The
standard only guarantees a *minimum* size, so the same code can behave
differently on different platforms.

### Minimum sizes guaranteed by the standard

| Type | Minimum bits | Minimum range |
| --- | --- | --- |
| `signed char` | 8 | -127 to 127 |
| `short` | 16 | -32767 to 32767 |
| `int` | 16 | -32767 to 32767 |
| `long` | 32 | -2147483647 to 2147483647 |
| `long long` | 64 | -9223372036854775807 to 9223372036854775807 |

The standard also guarantees the ordering of the sizes:

```
sizeof(char) <= sizeof(short) <= sizeof(int) <= sizeof(long) <= sizeof(long long)
```

Note that `sizeof` returns the number of *bytes*, and a byte is `CHAR_BIT` bits
(at least 8). On virtually every modern platform a byte is 8 bits.

### The data model

Because the standard leaves the exact sizes open, each platform picks a **data
model** that fixes the sizes of `int`, `long`, and pointers. The name encodes
which types are 64-bit.

| Model | `int` | `long` | pointer | Examples |
| --- | --- | --- | --- | --- |
| LP64 | 32 | 64 | 64 | Linux, macOS (64-bit) |
| LLP64 | 32 | 32 | 64 | Windows (64-bit) |
| ILP32 | 32 | 32 | 32 | 32-bit systems |

So `long` is 64 bits on Linux but 32 bits on Windows — the same program can
overflow in one place and not the other.

### Fixed-width types

When you need an exact size, use the fixed-width types from `<cstdint>`:

```c++
int32_t a;   // Exactly 32 bits.
int64_t b;   // Exactly 64 bits.
uint64_t c;  // Exactly 64 bits, unsigned.
```

These are only defined if the platform has a type of that exact width, which
every contest judge does.

### What this means for competitive programming

- `int` is 32 bits on every judge you will meet, so it holds values up to about
  2.1 × 10^9.
- If a value can exceed that (or you are summing many values), use `long long`
  or `int64_t`.
- Signed integer overflow is [undefined behavior](/explanations/undefined-behavior/),
  so an overflow can silently produce a wrong answer.
