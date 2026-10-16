---
title: Finding min or max
---

## With Scalar

### Python Scalar

In Python, use the builtins [min](https://docs.python.org/3/builtins/functions.html#min) or [max](https://docs.python.org/3/builtins/functions.html#max).
```python
min(2, 4) // 2
```

### C++ Scalar

In C++, you must use a different function depending on whether or not the value is like a list.

If it is not a list, `min` and `max`.

```python
min(2, 4);
```


## With List

### Python List

In Python, use the builtins [min](https://docs.python.org/3/builtins/functions.html#min) or [max](https://docs.python.org/3/builtins/functions.html#max), like with scalar.

```python
min([1, 3]) // 1
```

If the aggregate value cannot be computed, then an exception is raised.

```python
min([]) // Raises "ValueError: min() iterable argument is empty"
```

### C++ List

If it is a list, there are two different ways to handle it.

The cleanest way requires C++20.

```c++
vector<int> nums = {1, 3};
int val = ranges::max(nums);

// If array empty.
vector<int> nums2 = {};
if (!nums.empty()) {
	int val2 = ranges::max(nums2);
}
```

Note that if the array is empty, an exception is NOT thrown; instead the behavior is undefined.

If you can't use C++20 or want to check to see if there was a min or max after calling the function, use `max_element`.

```c++
int val = *std::max_element(nums.begin(), nums.end());
int val2 = *ranges::max_element(nums);

// If empty, can check after
auto it = ranges::max_element(nums);
if (it != numbers.end()) {
	// Array was actually empty, no max found.
}
```

Note that like above, if the input array is empty, and you try to dereference the retrned pointer, it is ALSO undefined behavior.
