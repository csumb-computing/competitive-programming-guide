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

## Java

```java
Set<Integer> s = new HashSet<>(Set.of(1, 2, 3));
Set<Integer> sorted = new TreeSet<>(Set.of(1, 2, 3));  // ordered

Map<String, Integer> m = new HashMap<>(Map.of("a", 1, "b", 2));
Map<String, Integer> sortedM = new TreeMap<>(Map.of("a", 1));  // ordered
```

`HashSet`/`HashMap` are average O(1) but unsorted; `TreeSet`/`TreeMap` are O(log n) and sorted. `LinkedHashSet`/`LinkedHashMap` preserve insertion order. Note that `Set.of`/`Map.of` create immutable collections; wrap them in `new HashSet<>(...)` if you need to mutate.
