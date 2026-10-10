# Store a 64 bit number

## Python

No need to worry about this! `int` is "arbitrary precision", which means that its size will grow to whatever number you need to store.

If you use Java or C++, it's often recommended to switch to Python for some problems just to get this behavior.

## C++

In C++, use `long long`, which will always be _at least_ 64 bits.

```c++
long long x = 9;
```

For large [integer literals](https://en.cppreference.com/cpp/language/integer_literal), you'll have to use a type suffix like `LL`.

```c++
long long int x = 9223372036854775807LL;
```

The suffix `ll` is also valid and means the same thing, but `LL` is the convention for competitive programming; it's also easier to read.

Another option is the [fixed-width integer type](https://en.cppreference.com/cpp/types/integer) `int64_t`. This will have _exactly_ 64 bits.

```c++
int64_t z = 1LL << 62;
```

This is ill-advised. On some platforms, the program will fail to program if it's not possible to use a 64-bit type (as on a 32-bit computer). I've encountered this with some older graders like UVa.
