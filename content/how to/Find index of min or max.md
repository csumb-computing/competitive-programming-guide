---
title: Find index of min or max
---

## Python

```python
nums = [3, 1, 2]
nums.index(min(nums))  # 1
nums.index(max(nums))  # 0
```

Empty list raises `ValueError` (from `min`/`max`).

## C++

```c++
vector<int> nums = {3, 1, 2};
int i = min_element(nums.begin(), nums.end()) - nums.begin();  // 1
int j = max_element(nums.begin(), nums.end()) - nums.begin();  // 0

// C++20.
int k = ranges::min_element(nums) - nums.begin();
```

Empty list returns `end()`, so guard before subtracting:

```c++
if (!nums.empty()) {
    int i = ranges::min_element(nums) - nums.begin();
}
```

## Java

Java has no builtin for the index; loop manually.

```java
int[] nums = {3, 1, 2};
int minIdx = 0, maxIdx = 0;
for (int i = 1; i < nums.length; i++) {
    if (nums[i] < nums[minIdx]) minIdx = i;
    if (nums[i] > nums[maxIdx]) maxIdx = i;
}
// minIdx == 1, maxIdx == 0
```

For a `List`, use `indexOf` with `Collections.min`/`max`.

```java
List<Integer> list = List.of(3, 1, 2);
int i = list.indexOf(Collections.min(list));  // 1
int j = list.indexOf(Collections.max(list));  // 0
```

Empty list: `Collections.min`/`max` throw `NoSuchElementException`, so guard first.
