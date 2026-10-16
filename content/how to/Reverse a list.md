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

## Java

```java
List<Integer> nums = new ArrayList<>(List.of(1, 2, 3));
Collections.reverse(nums);  // [3, 2, 1], IN PLACE
```

There is no builtin for arrays; reverse manually.

```java
int[] arr = {1, 2, 3};
for (int i = 0, j = arr.length - 1; i < j; i++, j--) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
```

Empty or single-element lists are valid and unchanged.
