# Iterate over two lists at once

## Python

```python
for a, b in zip([1, 2], ["a", "b"]):
    print(a, b)  # 1 a, 2 b

# Stops at the shortest list.
list(zip([1, 2, 3], ["a"]))  # [(1, "a")]
```

## C++

```c++
vector<int> a = {1, 2};
vector<string> b = {"a", "b"};
for (int i = 0; i < min(a.size(), b.size()); i++) {
    cout << a[i] << " " << b[i] << "\n";
}
```

Both stop at the shorter list; no out-of-bounds access.
