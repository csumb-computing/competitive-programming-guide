# Sort a list

There are two forms:

- Sorting the list in place (mutating it)
- Returning a new sorted list, leaving the original untouched

## Python

In Python, use the builtins [sorted](https://docs.python.org/3/library/functions.html#sorted) or [`list.sort`](https://docs.python.org/3/library/stdtypes.html#list.sort).

```python
sorted([3, 1, 2]) // [1, 2, 3], returns a NEW list
[3, 1, 2].sort() // None, sorts the list IN PLACE
```

By default both sort ascending. To sort descending, pass `reverse=True`:

```python
sorted([3, 1, 2], reverse=True) // [3, 2, 1]
```

To sort by something other than the value itself, use the `key` parameter:

```python
sorted([(2, "b"), (1, "a")], key=lambda x: x[0]) // [(1, "a"), (2, "b")]
sorted(["bb", "a", "ccc"], key=len) // ["a", "bb", "ccc"]
```

#### Python Errors

`sorted` and `sort` raise an exception if the values are not comparable.

```python
sorted([1, "a"]) // Raises TypeError: '<' not supported between instances of 'str' and 'int'
sorted([]) // Returns [], no exception is raised
```

## C++

In C++, use [`std::sort`](https://en.cppreference.com/w/cpp/algorithm/sort) for random-access containers (arrays, `vector`, `string`) or [`std::stable_sort`](https://en.cppreference.com/w/cpp/algorithm/stable_sort) when equal elements must keep their relative order.

```c++
vector<int> nums = {3, 1, 2};
sort(nums.begin(), nums.end()); // {1, 2, 3}, sorts IN PLACE

// C++20, no iterators needed.
ranges::sort(nums);
```

To sort descending or by a custom rule, pass a comparator:

```c++
vector<int> nums = {3, 1, 2};
sort(nums.begin(), nums.end(), greater<int>()); // {3, 2, 1}

// C++20.
ranges::sort(nums, ranges::greater());

// Custom comparator.
ranges::sort(nums, [](int a, int b) { return a < b; });
```

Note that sorting does NOT return a new container, it mutates the one you passed in. If you need the original preserved, copy it first (`vector<int> copy = nums;`) or use `std::ranges::to` to build a new one.

Note that sorting an empty container is valid and does nothing; no exception and no undefined behavior.

The comparator must provide a strict weak ordering. If it does not (for example, a comparator using `<=` instead of `<`), the behavior is undefined.
