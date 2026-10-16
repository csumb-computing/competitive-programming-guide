---
title: Iterate over list with indices
---

## Python

```python
for i, val in enumerate([1, 2, 3]):
    print(i, val)  # 0 1, 1 2, 2 3

for i, val in enumerate([1, 2, 3], start=1):
    print(i, val)  # 1 1, 2 2, 3 3
```

## C++

```c++
vector<int> nums = {1, 2, 3};
for (int i = 0; i < nums.size(); i++) {
    cout << i << " " << nums[i] << "\n";
}

// C++23.
for (auto [i, val] : views::enumerate(nums)) {
    cout << i << " " << val << "\n";
}
```

Empty list: the loop body never runs.

## Java

```java
int[] nums = {1, 2, 3};
for (int i = 0; i < nums.length; i++) {
    System.out.println(i + " " + nums[i]);
}

// Enhanced for loop, when you only need the value.
for (int val : nums) {
    System.out.println(val);
}
```

For a `List`, use `IntStream.range`.

```java
List<Integer> list = List.of(1, 2, 3);
IntStream.range(0, list.size()).forEach(i -> System.out.println(i + " " + list.get(i)));
```

Empty list: the loop body never runs.
