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


### Java Scalar

In Java, use [`Math.min`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Math.html#min(int,int)) or [`Math.max`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Math.html#max(int,int)).

```java
Math.min(2, 4);  // 2
Math.max(2, 4);  // 4
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

### Java List

Use [`Collections.min`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Collections.html#min(java.util.Collection)) or [`Collections.max`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Collections.html#max(java.util.Collection)).

```java
List<Integer> nums = List.of(1, 3);
int val = Collections.min(nums);  // 1
```

If the list is empty, `Collections.min`/`max` throw `NoSuchElementException`.

```java
Collections.min(List.of());  // Raises NoSuchElementException
```

For arrays, use a stream, which returns an `OptionalInt` instead of throwing.

```java
int[] arr = {1, 3};
int val = Arrays.stream(arr).max().getAsInt();  // 3

// Empty array: the OptionalInt is empty, so getAsInt() throws NoSuchElementException.
Arrays.stream(new int[]{}).max().getAsInt();  // Raises NoSuchElementException
```
