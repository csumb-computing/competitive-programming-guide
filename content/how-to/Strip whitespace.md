# Strip whitespace

## Python

```python
"  hi  ".strip()   # "hi", both ends
"  hi  ".lstrip()  # "hi  ", left only
"  hi  ".rstrip()  # "  hi", right only
```

## C++

No builtin; trim manually.

```c++
string s = "  hi  ";
size_t start = s.find_first_not_of(" \t\n\r");
size_t end = s.find_last_not_of(" \t\n\r");
string trimmed = (start == string::npos) ? "" : s.substr(start, end - start + 1);
```

All-whitespace (or empty) input gives `start == npos`, so the result is `""`.
