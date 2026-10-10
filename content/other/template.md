# Template

It's important to have a template to ease reading and writing code. Mine may be of some inspiration:

```c++
#include <bits/stdc++.h>
#define ISDEBUG
#ifdef ISDEBUG
   #define debug(s) cout << s << endl
   #define vdebug(s) debug(#s << ": " << s)
#else
   #define debug(s)
   #define vdebug(s)
#endif
using namespace std;
namespace rg = ranges;
using ll = long long;
using pri = pair<int, int>;
using prl = pair<ll, ll>;
using vi = vector<int>;
using vll = vector<ll>;
#define say(s) cout << s << endl
#define loop(i, a, b) for (int i = a; i < (b); ++i)
#define loopt(i, a, b, T) for (T i = a; i < (b); ++i)
#define be(x) (x).begin(), (x).end()
template <class T> static ostream &operator<<(ostream &os, const vector<T> &v) {
   os << '[';
   for (auto i = 0; i < v.size(); ++i) {
      os << v[i];
      if (i + 1 < v.size()) os << ", ";
   }
   os << ']';
   return os;
}
template <class M, class = enable_if_t<is_same_v<typename M::key_type, typename M::key_type>>>
static ostream &operator<<(ostream &os, const M &m) {
   os << '{';
   for (auto it = m.begin(); it != m.end(); ++it) {
      os << it->first << ": " << it->second;
      if (next(it) != m.end()) os << ", ";
   }
   os << '}';
   return os;
}

int main() {
   cin.tie(nullptr)->sync_with_stdio(false);
   // cin.exceptions(cin.failbit);
}
```

## Features

### Printing Variables.

Easily debug values and variables:

```c++
int a = 5;

// Before.
cout << a << endl;
cout << a << endl;
cout << "a: " << a << endl;

// After.
say(a);   // Prints "5"
debug(a); // Prints "5"
vdebug(a) // Prints "a: 5"
```

Note the `ISDEBUG` macro. If it is set, then `debug` and `vdebug` print as shown above. If it is commented out, then those print statements are not compiled in. `say` always prints.

### Namespace Shortcuts

Although the namespace pollution is generally frowned upon, it's great for reducing typing in competitive programming.

```c++
using namespace std;

// Before.
std::max(1, 2); // 1

// After.
min(1, 2);      // 1
```

Similarly, do this with `std::ranges`

```c++
namespace rg = ranges;
vector<int> arr{1, 2};

// Before.
std::ranges::min(arr) // 1

// After.
std::rg::min(arr);    // 1

// After (with using namespace std).
rg::min(arr);         // 1
```

### Loops

Python's `range` is powerful. C++ has [iota](https://en.cppreference.com/cpp/ranges/iota_view), but it can behave in unexpected ways and more difficult to debug.

This improves readability and makes it easy to identify loops that are different from the typical array-looping.

```c++
int n; cin >> n;

// Before.
for (int i = 0; i < n; ++i) {
	
}

// After.
loop (i, 0, n) {
	
}
```

`loopt` is useful when you may want to use `ll`.

## Begin and End Shortcut

```c++
vector<int> arr{1, 2};

// Before.
sort(arr.begin(), arr.end());

// After.
sort(be(arr));
```

If C++20 is supported, consider exclusively using [`std::ranges`](https://cppreference.com/cpp/ranges).

## Template Stuff

The template stuff at the end allows for printing arrays and maps. It leverages SFINAE instead of Concepts for broader compatability. 

```c++
vector<string> arr = {1, 2, 3};
map<string, int> m;
m.insert("a", 2);
m.insert("b", 3);

// After.
cout << arr << endl; // [1, 2, 3]
cout << m << endl;   // {a: 2, b: 3}

// After (with say()).
say(arr); // [1, 2, 3]
say(m);   // {a: 2, b: 3}
```
