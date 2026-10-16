---
title: Store a number larger than 64 bits
---

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

## Java

Use [`BigInteger`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/math/BigInteger.html) for arbitrary-precision integers and [`BigDecimal`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/math/BigDecimal.html) for arbitrary-precision decimals.

```java
BigInteger x = BigInteger.valueOf(2).pow(100);  // 1267650600228229401496703205376
BigInteger y = new BigInteger("123456789012345678901234567890");

x.add(y);       // Addition, does NOT mutate x.
x.multiply(y);  // Multiplication.
x.mod(y);       // Modulo.
```

`BigInteger` is immutable, so every operation returns a new object; there is no `+` operator. It is much slower than `long`, so only reach for it when the values genuinely exceed 64 bits.
