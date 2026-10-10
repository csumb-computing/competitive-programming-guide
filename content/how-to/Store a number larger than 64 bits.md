# Store a number larger than 64 bits

## Python

`int` is arbitrary precision; no special type needed.

```python
x = 2**100  # 1267650600228229401496703205376
```

## C++

Use `__int128` (GCC/Clang only, up to 128 bits).

```c++
__int128 x = (__int128)1 << 100;

// No builtin printing; print digit by digit.
void print(__int128 n) {
    if (n < 0) { cout << '-'; n = -n; }
    if (n > 9) print(n / 10);
    cout << (int)(n % 10);
}
```

For truly arbitrary size, use `boost::multiprecision::cpp_int`.
