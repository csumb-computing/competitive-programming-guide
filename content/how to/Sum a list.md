# Sum a list

## Python

```python
sum([1, 2, 3])        # 6
sum([])               # 0, no exception
sum([1, 2, 3], 10)    # 16, with start value
```

## C++

```c++
vector<int> nums = {1, 2, 3};
accumulate(nums.begin(), nums.end(), 0);  // 6
accumulate(nums.begin(), nums.end(), 0, plus<int>());  // 6

// C++20.
ranges::fold_left(nums, 0, plus<int>());  // 6
```

Empty list returns `0` in both, no exception.

Watch overflow: the accumulator type is the type of the start value, so pass `0LL` for a `long long` sum.
