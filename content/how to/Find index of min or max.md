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
