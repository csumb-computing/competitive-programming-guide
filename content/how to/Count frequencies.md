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

## Java

```java
int[] arr = {9, 9, 9, 5};

Map<Integer, Integer> freqs = new HashMap<>();
for (int val : arr) {
    freqs.merge(val, 1, Integer::sum);
}
// {9: 3, 5: 1}
```

`merge` inserts `1` when the key is absent and otherwise combines with the existing value. If you prefer to be explicit, use `getOrDefault`.

```java
freqs.put(val, freqs.getOrDefault(val, 0) + 1);
```

For a sorted map, use `TreeMap`; for insertion order, use `LinkedHashMap`.
```
