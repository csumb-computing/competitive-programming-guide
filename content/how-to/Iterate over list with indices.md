# Iterate over list with indices

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
