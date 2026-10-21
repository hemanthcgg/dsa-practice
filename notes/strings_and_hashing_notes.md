## 1\. String

### Definition

A string is a sequence of characters arranged in a specific order. It is used to represent and manipulate text.

### Key Concepts

- Characters are arranged in a specific sequence.
- Characters can be accessed by position or index.
- Common operations include traversal, searching, concatenation, comparison, and substring extraction.
- Strings may be mutable or immutable depending on the programming language.

### Example

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s = "hello";

    cout << s[0] << "\n";       // h
    cout << s.size() << "\n";   // 5

    s += " world";
    cout << s << "\n";          // hello world

    reverse(s.begin(), s.end());
    cout << s << "\n";

    return 0;
}
```

### Common Operations

| Operation | C++ Syntax | Complexity |
| --- | --- | --- |
| Get length | `s.size()` | O(1) |
| Access character | `s[i]` | O(1) |
| Append character | `s.push_back('a')` | Amortized O(1) |
| Concatenate | `s += t` | Depends on appended length |
| Extract substring | `s.substr(pos, len)` | O(len) |
| Reverse | `reverse(s.begin(), s.end())` | O(n) |
| Sort characters | `sort(s.begin(), s.end())` | O(n log n) |

---

## 2\. Hash Set

### Definition

A hash set is a data structure that stores a collection of unique elements and uses a hash function to support efficient insertion, deletion, and membership checking.

### Key Concepts

- Duplicate elements are not stored as separate entries.
- Elements are generally not maintained in sorted order.
- A hash function helps locate elements efficiently.
- Average-case insertion, deletion, and lookup are typically O(1).
- Worst-case operations can take O(n), depending on collisions and implementation.

### Example

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    unordered_set<int> st;

    st.insert(10);
    st.insert(20);
    st.insert(10);  // Duplicate ignored

    cout << st.size() << "\n";  // 2

    if (st.count(10)) {
        cout << "Element found\n";
    }

    st.erase(10);

    cout << st.count(10) << "\n";  // 0

    return 0;
}
```

### Common Operations

| Operation | C++ Syntax | Average Complexity |
| --- | --- | --- |
| Insert | `st.insert(x)` | O(1) |
| Search | `st.find(x)` | O(1) |
| Check existence | `st.count(x)` | O(1) |
| Delete | `st.erase(x)` | O(1) |
| Get size | `st.size()` | O(1) |
| Check empty | `st.empty()` | O(1) |

---

## 3\. Hash Map

### Definition

A hash map is a data structure that stores key-value pairs and uses a hash function to support efficient insertion, retrieval, updating, and deletion of values associated with keys.

### Key Concepts

- Each key is unique and is associated with a value.
- Multiple keys can map to the same value.
- A key is used to retrieve its corresponding value.
- Average-case insertion, deletion, and lookup are typically O(1).
- Worst-case operations can take O(n), depending on collisions and implementation.

### Example

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    unordered_map<string, int> mp;

    mp["apple"] = 3;
    mp["banana"] = 2;

    mp["apple"]++;  // Update value to 4

    cout << mp["apple"] << "\n";  // 4

    if (mp.find("banana") != mp.end()) {
        cout << "Key found\n";
    }

    mp.erase("banana");

    return 0;
}
```

### Common Operations

| Operation | C++ Syntax | Average Complexity |
| --- | --- | --- |
| Insert or update | `mp[key] = value` | O(1) |
| Access value | `mp[key]` | O(1) |
| Search key | `mp.find(key)` | O(1) |
| Check existence | `mp.count(key)` | O(1) |
| Delete key | `mp.erase(key)` | O(1) |
| Get number of entries | `mp.size()` | O(1) |

**Important:** Accessing `mp[key]` inserts the key with a default-initialized value if it does not already exist. Use `find()` when checking for a key without inserting it.

---

## 4\. Comparison: String vs Hash Set vs Hash Map

| Feature | String | Hash Set | Hash Map |
| --- | --- | --- | --- |
| Stores | Ordered characters | Unique elements | Key-value pairs |
| Duplicates | Allowed | Not stored separately | Keys must be unique |
| Main purpose | Text processing | Uniqueness and membership | Mapping and lookup |
| Access method | Position or index | Element lookup | Key lookup |
| Average lookup | O(1) by index | O(1) | O(1) |
| Maintains sorted order | Character sequence preserved | No | No |

**Note:** O(1) string lookup refers to accessing a character by index. Searching for a character or substring generally requires additional time.

---

## 5\. Quick Pattern Recognition

| Problem Requirement | Recommended Approach |
| --- | --- |
| Process or compare text | String |
| Check for repeated elements | Hash Set |
| Find unique elements | Hash Set |
| Check whether an element exists | Hash Set |
| Count element occurrences | Hash Map |
| Store values with their indices | Hash Map |
| Find pairs using complements | Hash Set or Hash Map |
| Find a longest substring under constraints | String + Sliding Window + Set/Map |

---

## 6\. Complexity Cheat Sheet

Let:

- `n` = input size
- `k` = number of distinct elements or tracked characters

| Operation or Pattern | Typical Time | Auxiliary Space |
| --- | --- | --- |
| Traverse a string or array | O(n) | O(1) |
| Reverse using two pointers | O(n) | O(1) |
| Sort a string | O(n log n) | Implementation-dependent |
| Frequency counting with a hash map | O(n) average | O(k) |
| Detect duplicates with a hash set | O(n) average | O(n) |
| Two Sum using a hash map | O(n) average | O(n) |
| Sliding window | Often O(n) | Depends on the window and data structure |

Hash-based complexity is generally average-case. Worst-case performance may be slower.

---

### Final Revision Summary

- **String:** Ordered sequence of characters used for text processing.
- **Hash Set:** Collection of unique elements optimized for membership checks.
- **Hash Map:** Collection of key-value pairs optimized for lookup and association.

Choose the data structure based on the operation the problem requires: text manipulation, uniqueness checking, or key-value mapping.