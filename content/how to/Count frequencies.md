---
title: How to count frequencies
---

## Python

### Method 1

If you're new, use this.

```python
arr = [9, 9, 9, 5]
freqs = {}
for val in arr:
    if val in freqs:
        freqs[val] += 1
    else:
        freqs[val] = 1
```

### Method 2

Shorter, customize the value when the element does not exist.

```python3
from collections import defaultdict

freqs = defaultdict(lambda: 0)
for val in arr:
    freqs[val] += 1
```

### Method 3

Most ergonomic.

```python3
from collections import Counter

freqs = Counter(arr)
```

## C++

This is the best C++ has so far. With `operator[]`, if the key does not exist, it calls the type's default constructor.

```c++
vector<string> vec = {9, 9, 9, 5};

unordered_map<string, int> counter;
for (const auto& val : vec) {
      counter[val] += 1;
}
```
