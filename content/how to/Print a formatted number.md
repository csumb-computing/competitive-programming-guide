---
title: Print a formatted number
---

## Python

```python
f"{3.14159:.2f}"  # "3.14", 2 decimals
f"{42:05d}"       # "00042", zero-padded to width 5
f"{1234567:,}"    # "1,234,567", thousands separators

print(f"{3.14159:.2f}")
```

## C++

```c++
cout << fixed << setprecision(2) << 3.14159 << "\n";  // 3.14
cout << setw(5) << setfill('0') << 42 << "\n";        // 00042
```

`fixed`/`setprecision` and `setfill` are sticky; reset with `cout << defaultfloat;` if needed.

## Java

Use [`System.out.printf`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/PrintStream.html#printf(java.lang.String,java.lang.Object...)) or [`String.format`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/String.html#format(java.lang.String,java.lang.Object...)).

```java
System.out.printf("%.2f%n", 3.14159);  // 3.14, 2 decimals
System.out.printf("%05d%n", 42);       // 00042, zero-padded to width 5
System.out.printf("%,d%n", 1234567);   // 1,234,567, thousands separators

String s = String.format("%.2f", 3.14159);  // "3.14"
```

`%n` is the platform line separator; use `\n` if you want a literal newline. Unlike C++'s `setprecision`, the format specifier is per-call, so there is nothing sticky to reset.
