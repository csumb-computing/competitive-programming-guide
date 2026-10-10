# Split and join strings

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
