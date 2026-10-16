---
title: How to count a single frequency
---

### Value

### Python

```python
arr = [9, 9, 9, 5]
v.count(9) // 3.
```

### C++

Use [std::count](https://en.cppreference.com/cpp/algorithm/count).
```c++
vector<string> vec = {9, 9, 9, 5};
count(vec.begin(), vec.end(), 9) // 3

ranges::count(vec, 9) // 3
```

## Custom Condition/predicate

### Python

Python uses [list comprehension](https://docs.python.org/3.10/tutorial/datastructures.html?highlight=list+comprehension#list-comprehensions):

```python
sum(1 for x in v if x % 2 == 0)
```

C++ uses [`std::ranges::count_if`](https://en.cppreference.com/cpp/algorithm/ranges/count) or [`std::count_if`](https://en.cppreference.com/cpp/algorithm/count):

### C++

```c++
int evens = std::count_if(v.begin(), v.end(), [](int x) { return x % 2 == 0; });
auto evens = std::ranges::count_if(v, [](int x) { return x % 2 == 0; }); // ptr_diff. 64 bits.
```
