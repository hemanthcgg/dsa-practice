## 1. What is Sliding Window?

A technique for working with a **contiguous** part of an array or string (a subarray or substring). Move the window across the input and update its state instead of recalculating everything from scratch.

## 2. When should I think of Sliding Window?

- The problem asks about a **contiguous subarray or substring**.
- Find a maximum/minimum sum or length for a window of size `k`.
- Find the longest or shortest valid subarray/substring.
- Count contiguous windows that satisfy a condition.

## 3. Two common patterns

### Pattern 1: Fixed-Size Window

The window must always have exactly `k` elements.

**Steps**
1. Calculate the result for the first `k` elements.
2. Move the window right by one: remove the outgoing element and add the incoming element.
3. Update the best answer at each step.

**Example:** Maximum sum of any subarray of size `3` in `[2, 1, 5, 1, 3, 2]`.

| Window | Sum |
|---|---:|
| `[2, 1, 5]` | 8 |
| `[1, 5, 1]` | 7 |
| `[5, 1, 3]` | 9 |
| `[1, 3, 2]` | 6 |

Maximum sum = **9**, from `[5, 1, 3]`.

```cpp
int sum = 0;

// Sum the first k elements
for (int i = 0; i < k; i++) {
    sum += arr[i];
}

int best = sum;

for (int right = k; right < n; right++) {
    sum += arr[right];       // Add incoming element
    sum -= arr[right - k];   // Remove outgoing element
    best = max(best, sum);
}
```

### Pattern 2: Variable-Size Window

The window grows and shrinks to satisfy a condition.

**General steps**
1. Move `right` forward and include the new element.
2. While the window is invalid, move `left` forward and remove elements from the window.
3. Update the answer at the appropriate point.

**Example:** Longest subarray with sum `<= 7` in `[2, 1, 3, 2, 1]` (all values are positive).

- Expand to `[2, 1, 3, 2]`; sum = `8`, which is too large.
- Move `left` once, removing `2`; window becomes `[1, 3, 2]`, sum = `6`.
- Add the final `1`; window becomes `[1, 3, 2, 1]`, sum = `7`, length = `4`.
- Longest valid length = **4**.

```cpp
int left = 0;
int sum = 0;
int best = 0;

for (int right = 0; right < n; right++) {
    sum += arr[right];

    while (sum > 7) {         // Window is invalid
        sum -= arr[left];
        left++;
    }

    best = max(best, right - left + 1);
}
```

This sum-based shrinking example relies on **non-negative values** (and is most commonly taught with positive values). With negative numbers, expanding or shrinking does not change the sum predictably, so this template may not work.

## 4. How do I move the pointers?

- `right++`: expand the window by adding a new element.
- `left++`: shrink the window by removing its leftmost element.
- Keep the window's running state updated whenever an element enters or leaves.
- For a **longest valid window**, usually shrink while invalid, then update the maximum length.
- For a **shortest valid window**, once the window becomes valid, record the answer and keep shrinking while it remains valid.

## 5. Complexity

- **Time:** Usually `O(n)` because each pointer moves forward at most `n` times.
- **Extra space:** Often `O(1)` for a running sum; may be `O(k)` or `O(character set)` when maintaining a deque, map, or set.

## 6. Quick recognition rules

- **Contiguous + fixed length `k`** → fixed-size sliding window.
- **Contiguous + longest/shortest valid range** → consider variable-size sliding window.
- **Longest substring without repeating characters** → variable window + set/map.
- **Sum condition with negative numbers** → don't blindly use the usual expand/shrink sum template; consider prefix sums and hashing instead.

**Remember:** Two pointers are the indices; sliding window is the technique of maintaining the elements and state between those indices.
