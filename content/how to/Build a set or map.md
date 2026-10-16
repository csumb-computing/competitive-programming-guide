---
title: Build a set or map
---

## Python

```python
s = {1, 2, 3}
s = set([1, 2, 2])  # {1, 2}

m = {"a": 1, "b": 2}
m = dict([("a", 1), ("b", 2)])
```

## C++

```c++
unordered_set<int> s = {1, 2, 3};
set<int> sorted_s = {1, 2, 3};  // ordered

unordered_map<string, int> m = {{"a", 1}, {"b", 2}};
map<string, int> sorted_m = {{"a", 1}};  // ordered
```

`unordered_*` is average O(1) but unsorted; `set`/`map` is O(log n) and sorted.
