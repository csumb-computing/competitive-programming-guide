# Print a formatted number

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
