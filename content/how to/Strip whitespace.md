---
title: Strip whitespace
---

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

## Java

```java
"  hi  ".trim();   // "hi", both ends
"  hi  ".strip();  // "hi", both ends (Java 11+, Unicode-aware)
"  hi  ".stripLeading();   // "hi  ", left only
"  hi  ".stripTrailing();  // "  hi", right only
```

`trim` only removes characters with code point `<= U+0020`, while `strip` uses `Character.isWhitespace`, so prefer `strip` on modern Java. Use `stripLeading`/`stripTrailing` (Java 11+) to trim only one side.

All-whitespace (or empty) input gives `""`.
