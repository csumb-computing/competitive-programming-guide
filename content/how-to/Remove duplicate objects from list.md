# Remove duplicate objects from list

## Python

```python
# Order NOT preserved.
list(set([1, 2, 2, 3]))  # [1, 2, 3]

# Order preserved.
list(dict.fromkeys([1, 2, 2, 3]))  # [1, 2, 3]
```

`set` requires hashable elements; unhashable ones (e.g. `list`) raise `TypeError`.

## C++

```c++
vector<int> nums = {1, 2, 2, 3};

// Order NOT preserved.
unordered_set<int> s(nums.begin(), nums.end());

// Order preserved, requires sorted input.
sort(nums.begin(), nums.end());
nums.erase(unique(nums.begin(), nums.end()), nums.end());  // {1, 2, 3}
```

`unique` only removes *consecutive* duplicates, so sort first. Empty list is valid.
