# Using Pointers from Algorithms

See [undefined behavior](./Undefined behavior.md]) for details.

## Example: dereferencing the result of `min_element` / `max_element`

`min_element` and `max_element` (and the `ranges::` versions) return an
**iterator** pointing at the smallest or largest element. If the range is
empty, there is no such element, so they return the end iterator instead.

Dereferencing that end iterator is undefined behavior.

```c++
vector<int> nums = {};

// UB: the range is empty, so this dereferences end().
int val = *ranges::max_element(nums);
```

Python, by contrast, raises an exception:

```python
min([])  # Raises "ValueError: min() iterable argument is empty"
```

## The fix: guard before you dereference

Check that the range is non-empty before dereferencing, or compare the returned
iterator against `end()`.

```c++
vector<int> nums = {1, 3};

// Check the range first.
if (!nums.empty()) {
    int val = *ranges::max_element(nums);
}

// Or check the iterator after the call.
auto it = ranges::max_element(nums);
if (it != nums.end()) {
    int val = *it;
}
```

The same rule applies to `std::min_element` / `std::max_element`, and to
`ranges::max` / `ranges::min`, which also have undefined behavior on an empty
range.
