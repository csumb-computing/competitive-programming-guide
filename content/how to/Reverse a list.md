---
title: Reverse a list
---

## Python

```python
[1, 2, 3][::-1]  # [3, 2, 1], returns a NEW list

nums = [1, 2, 3]
nums.reverse()   # None, reverses IN PLACE
```

## C++

```c++
vector<int> nums = {1, 2, 3};
reverse(nums.begin(), nums.end());  // {3, 2, 1}, IN PLACE

// C++20.
ranges::reverse(nums);
```

Empty or single-element lists are valid and unchanged.
