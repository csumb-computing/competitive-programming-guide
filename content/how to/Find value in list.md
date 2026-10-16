---
title: Finding value in list
---

There are two forms:

- Checking whether or not a value exists in a list
- Getting the index of the value in the list

## Python

In Python, use the `in` operator or [`index`](https://docs.python.org/3/library/array.html#array.array.index)..

```python
3 in [1, 3] // True
[1, 3].index(3) // 1
```

Note that strings have `''.find`.

#### Python Errors

`index` raises an exception.

```python
[1, 3].index(5) // Raises ValueError: list.index(x): x not in list""
```

## C++

```c++
vector<int> nums = {1, 3};

if (nums.contains)
```

If you only care whether the value exists, and not where it is, you can use `count`.
```c++
vector<int> nums = {1, 3};

ranges::contains(nums, 3); // True
nums.contains(3) // True
```
Note that `count` returns `0` when the value is not found, so no exception is thrown and there is nothing to dereference.



```c++
vector<int> nums = {1, 3};

if (auto it = find(nums.begin(), nums.end(), 3); it != nums.end()) {
	int idx = it - nums.begin(); // 1
}

// C++20.
if (auto it = ranges::find(nums, 3); it != nums.end()) {
	int idx = it - nums.begin(); // 1
}

Note that like above, if the value is not found, the returned iterator is the end iterator, and dereferencing it is ALSO undefined behavior.
