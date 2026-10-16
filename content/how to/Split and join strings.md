---
title: Split and join strings
---

## Python

```python
"a,b,c".split(",")  # ["a", "b", "c"]
"a b  c".split()    # ["a", "b", "c"], splits on any whitespace

",".join(["a", "b", "c"])  # "a,b,c"
"".join(["a", "b"])        # "ab"
```

## C++

```c++
// Split.
string s = "a,b,c";
stringstream ss(s);
string token;
vector<string> parts;
while (getline(ss, token, ',')) {
    parts.push_back(token);
}

// Join.
string joined;
for (size_t i = 0; i < parts.size(); i++) {
    if (i) joined += ",";
    joined += parts[i];
}
```

Empty input: `split` gives `[""]` in Python; the C++ loop yields no tokens.

## Java

```java
// Split. The argument is a REGEX.
"a,b,c".split(",");     // ["a", "b", "c"]
"a b  c".split("\\s+");  // ["a", "b", "c"], splits on runs of whitespace

// Join.
String.join(",", List.of("a", "b", "c"));  // "a,b,c"
String.join("", List.of("a", "b"));        // "ab"
```

Empty input: `"".split(",")` returns `[""]`, matching Python. Note that `split` takes a regex, so a literal `.` must be escaped as `"\\."`.
