---
title: Use a regex
---

Regexes, or regular expressions are commonly used to parse and extract information from strings. Different languages have different parsing engines for regexes.

Check out [this quickstart](https://www.regular-expressions.info/quickstart.html) or [this one](https://www.rexegg.com/regex-quickstart.php). Here is a [cheat sheet](https://cheatography.com/davechild/cheat-sheets/regular-expressions/).

Be careful, some features may not have widespread support, so when in doubt, check the language documentation.

Common tokens you'll reach for:

- `.` any character, `\d` digit, `\w` word character, `\s` whitespace
- `*` zero or more, `+` one or more, `?` optional, `{n,m}` between `n` and `m`
- `[...]` character class, `[^...]` negated class
- `^` start of string, `$` end of string
- `|` alternation, `(...)` capturing group

## Python

Use the [`re`](https://docs.python.org/3/library/re.html) module. Use raw strings (`r"..."`) so backslashes are interpreted as a backslash, rather than the start of an escape sequence.

```python
import re

s = "abc 123 def 456"

# search: first match anywhere, returns a Match or None.
m = re.search(r"\d+", s)
m.group()  # "123"

# match: only matches at the start of the string.
re.match(r"\d+", s)  # None, s starts with "abc"

# fullmatch: the entire string must match.
re.fullmatch(r"\d+", "123")  # <re.Match ...>

# findall: every match. With groups, returns tuples instead of strings.
re.findall(r"\d+", s)  # ["123", "456"]

# finditer: every match with positions.
for m in re.finditer(r"\d+", s):
    m.group(), m.start(), m.end()  # ("123", 4, 7), then ("456", 12, 15)

# Groups.
m = re.search(r"(\w+)\s+(\d+)", s)
m.group(1)  # "abc"
m.group(2)  # "123"

# sub: replace every match.
re.sub(r"\d+", "#", s)  # "abc # def #"

# split: split on a regex.
re.split(r"\s+", "a  b   c")  # ["a", "b", "c"]
```

#### Python Errors

`search`, `match`, and `fullmatch` return `None` when there is no match, so calling `.group()` on the result raises.

```python
re.search(r"\d+", "abc").group()  # Raises AttributeError: 'NoneType' object has no attribute 'group'
```

## C++

Use [`<regex>`](https://en.cppreference.com/w/cpp/regex). The default grammar is ECMAScript, which is close to Python's. Raw string literals (`R"(...)"`) avoid escaping backslashes.

```c++
#include <regex>

string s = "abc 123 def 456";

// regex_search: first match anywhere.
smatch m;
if (regex_search(s, m, regex(R"(\d+)"))) {
    m.str();  // "123"
}

// regex_match: the ENTIRE string must match.
regex_match("123", regex(R"(\d+)"));  // true
regex_match(s, regex(R"(\d+)"));      // false

// Iterate every match.
for (sregex_iterator it(s.begin(), s.end(), regex(R"(\d+)")), end; it != end; ++it) {
    it->str();  // "123", then "456"
}

// Groups.
if (regex_search(s, m, regex(R"((\w+)\s+(\d+))"))) {
    m[1].str();  // "abc"
    m[2].str();  // "123"
}

// regex_replace: replace every match.
regex_replace(s, regex(R"(\d+)"), "#");  // "abc # def #"
```

Note that `regex_match` anchors both ends, unlike Python's `re.match`, which only anchors the start. Use `regex_search` when you want Python's `re.search` behavior.

Note that `std::regex` is slow and can be a bottleneck on large inputs. If a pattern is simple (a fixed delimiter, a run of digits), hand-rolled parsing is usually faster and worth it in a tight loop.

In Python, `re` caches recently used patterns, but if you reuse one in a loop, compile it once with `re.compile(r"...")` and call methods on the compiled object.
