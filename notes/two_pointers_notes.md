## 1. What is Two Pointers?

A technique that uses **two indices (pointers)** to traverse an array or string efficiently, often reducing an `O(n^2)` solution to `O(n)`.

## 2. When should I think of Two Pointers?

- The array is **sorted**, and you need to find a pair satisfying a condition.
- You need to check a **palindrome**.
- You need to remove duplicates or modify an array **in-place**.
- You need to compare or process elements from two positions.

## 3. Common patterns

### Pattern 1: Opposite Directions

Start at both ends: `left = 0`, `right = n - 1`.

**Use for:** Pair sum in a sorted array, palindrome checking.

- If the sum is too small → `left++`
- If the sum is too large → `right--`
- If the sum equals the target → pair found

### Pattern 2: Same Direction (Slow and Fast)

Both pointers move from left to right, but they have different jobs.

- **`fast`** scans the elements one by one.
- **`slow`** marks the position of the last accepted/valid element (or where the next valid element should go).
- Usually, `fast` moves every iteration. `slow` moves only when an element should be kept or written.

**Use for:** Removing duplicates from a sorted array, moving zeroes, and other in-place modifications.

## 4. Example: Find a pair with target sum

Sorted array: `[1, 2, 4, 6, 8]`, target = `10`

```cpp
int left = 0;
int right = 4;

while (left < right) {
    int sum = arr[left] + arr[right];

    if (sum == 10) {
        // Pair found
        break;
    } else if (sum < 10) {
        left++;
    } else {
        right--;
    }
}
```

| Step | Pair | Sum | Action |
|---|---|---:|---|
| 1 | 1, 8 | 9 | Move left |
| 2 | 2, 8 | 10 | Found! |

**Why does it work?** Because the array is sorted, moving `left` right increases the sum, while moving `right` left decreases it.

## 5. Example: Remove duplicates using same-direction pointers

Given the **sorted** array `[1, 1, 2, 2, 3]`, keep each value only once, in-place.

```cpp
int slow = 0;

for (int fast = 1; fast < arr.size(); fast++) {
    if (arr[fast] != arr[slow]) {
        slow++;
        arr[slow] = arr[fast];
    }
}

int uniqueCount = slow + 1;
// The unique values are in arr[0 ... uniqueCount - 1].
```

### How do the pointers move?

Start with `slow = 0` and `fast = 1`.

| `fast` index/value | Compare with `arr[slow]` | What happens? | Pointer movement |
|---|---|---|---|
| `1 / 1` | `1 == 1` | Duplicate; skip it | `fast` moves; `slow` stays |
| `2 / 2` | `2 != 1` | Keep `2` at the next valid position | `slow++`, copy `arr[fast]` to `arr[slow]`, then `fast++` |
| `3 / 2` | `2 == 2` | Duplicate; skip it | `fast` moves; `slow` stays |
| `4 / 3` | `3 != 2` | Keep `3` at the next valid position | `slow++`, copy `arr[fast]` to `arr[slow]`, then `fast++` |

At the end, the first `slow + 1` elements are `[1, 2, 3]`. Values beyond that prefix can be ignored.

**Key idea:** `fast` searches; `slow` builds the valid result. For this example, the array must be sorted so duplicates are next to each other.

## 6. Complexity

| Operation | Complexity |
|---|---|
| Time | `O(n)` |
| Extra space | `O(1)` |

These are typical for the two-pointer patterns above.

## 7. Important rules

- **Sorted array + pair sum?** Consider opposite-direction pointers.
- **Palindrome?** Compare both ends and move inward.
- **Remove duplicates in-place?** Consider slow and fast pointers.
- **Unsorted array + pair sum?** Hashing is often a better direct approach.
- **Can sorting help?** Yes, but sorting typically adds `O(n log n)` time and may change the original index order.
- **Loop condition:** Usually `left < right` for opposite-direction pointers; `fast < n` for the duplicate-removal example.

**Remember:** Two pointers work when you have a clear rule for moving one or both pointers. Don't use them just because a problem contains an array.
