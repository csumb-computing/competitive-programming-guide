---
title: cptest
---

A tool I made to automatically run the code. See [cptest.rs](https://github.com/hyperupcall-projects/dev/blob/main/tools/cptest.rs). Use it with [competitive-programming-paste](./competitive-programming-paste.md).

For example, for [romans](https://open.kattis.com/problems/romans), I have this structure:

```
$ ls
in1  in2  out1  out2  romans*  romans.cpp
$ cptest -t
Compiling ./romans.cpp
Running 2 tests

TEST 1
--- Actual
1088
--- Expected
1088
---

TEST 2
--- Actual
22046
--- Expected
22046
---
```

It supports a few useful features:

```
cptest -h
Usage: cptest [OPTIONS] [FILE]

OPTIONS:
  -c    Contest compilation
  -t    Run all tests
  -x    Execute the compiled program
  -h    Show this help message

FILE:
  Source file to compile (auto-detected if not specified)
  Supports C++, Java, Python, and OCaml
```
