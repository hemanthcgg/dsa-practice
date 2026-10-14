# Array: Study Notes 

## 1. Array Traversal and Manipulation

An array is a linear data structure consisting of a collection of elements, each identified by at least one array index or key, stored in contiguous memory locations.

### Key Concepts:

* **Traversal:** Visiting every element in the array sequentially (typically $O(N)$ time complexity).

* **Manipulation:** Inserting, deleting, updating, or transforming elements within the collection.

### Code Example: Traversal and Basic Manipulation

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    // Initializing a vector (dynamic array)
    vector<int> nums = {10, 20, 30, 40, 50};

    // 1. Traditional Index-based Traversal
    cout << "Index-based: ";
    for (size_t i = 0; i < nums.size(); ++i) {
        cout << nums[i] << " ";
    }
    cout << "\n";

    // 2. Range-based For Loop - Read/Write (Doubling each element)
    for (int &val : nums) {
        val *= 2;
    }

    // 3. Range-based For Loop - Read-only
    cout << "After doubling: ";
    for (const auto &val : nums) {
        cout << val << " ";
    }
    cout << "\n";

    return 0;
}
```

## 2. In-Place Modifications

In-place algorithms modify data structure elements within the original memory space without requiring extra auxiliary arrays (achieving $O(1)$ auxiliary space complexity).

### Common In-Place Patterns:

1. **Two Pointers:** Moving pointers from both ends towards the center (e.g., Reversing an array, Palindrome check).

2. **Read/Write Pointers (Fast & Slow):** Filtering elements or removing duplicates on the fly.

### Code Example 1: Reversing an Array In-Place

```cpp
#include <iostream>
#include <vector>
#include <utility> // for std::swap

using namespace std;

void reverseArray(vector<int>& arr) {
    int left = 0;
    int right = arr.size() - 1;

    while (left < right) {
        swap(arr[left], arr[right]);
        left++;
        right--;
    }
}

int main() {
    vector<int> data = {1, 2, 3, 4, 5};
    reverseArray(data);
    
    cout << "Reversed: ";
    for (int x : data) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Code Example 2: Removing Duplicates from a Sorted Array (In-Place)

```cpp
#include <iostream>
#include <vector>

using namespace std;

int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;
    
    int slow = 0; // Slow pointer for unique elements position
    for (int fast = 1; fast < nums.size(); ++fast) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    return slow + 1; // New length of unique elements
}

int main() {
    vector<int> nums = {1, 1, 2, 2, 3, 4, 4};
    int newLength = removeDuplicates(nums);
    
    cout << "Unique elements: ";
    for (int i = 0; i < newLength; ++i) {
        cout << nums[i] << " ";
    }
    cout << "\n";
    return 0;
}
```

## 3. Sorting Fundamentals

Sorting arranges elements in a specific order (ascending or descending). While writing custom sorting algorithms (like Bubble, Selection, Insertion, Merge, or Quick sort) is crucial for algorithmic foundations, modern programming environments provide highly optimized sorting functions.

### Basic Comparison Sorting Algorithms Overview:

* **Bubble Sort:** Repeatedly swaps adjacent elements if they are in the wrong order. ($O(N^2)$ time)

* **Insertion Sort:** Builds the final sorted array one item at a time (efficient for small or nearly sorted data). ($O(N^2)$ worst, $O(N)$ best time)

* **Selection Sort:** Repeatedly finds the minimum element from the unsorted part and puts it at the beginning. ($O(N^2)$ time)

* **IntroSort / Hybrid Sorts:** Algorithms combining QuickSort, HeapSort, and InsertionSort for optimal performance ($O(N \log N)$ average time).

### Code Example: Using Sorting Utilities and Implementing Bubble Sort

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Custom implementation of Bubble Sort
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    bool swapped;
    for (int i = 0; i < n - 1; ++i) {
        swapped = false;
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;
    }
}

int main() {
    vector<int> nums = {64, 34, 25, 12, 22, 11, 90};

    // Using custom bubble sort
    bubbleSort(nums);
    cout << "Bubble Sorted: ";
    for (int x : nums) cout << x << " ";
    cout << "\n";

    // Using C++ STL sort (Descending order using lambda)
    sort(nums.begin(), nums.end(), [](int a, int b) {
        return a > b;
    });

    cout << "STL Sorted (Desc): ";
    for (int x : nums) cout << x << " ";
    cout << "\n";

    return 0;
}
```

## 4. C++ Specific Array Types & Best Practices

In C++, you have multiple ways to represent and handle arrays. Choosing the right type depends on memory requirements and whether the size is known at compile-time or runtime.

### A. Raw C-Style Arrays (`T arr[N]`)

* **Characteristics:** Inherited from C. Fixed size determined at compile-time. No bounds checking. Decays to pointers easily, leading to potential security vulnerabilities or bugs (e.g., buffer overflows).

* **Usage:** Generally avoided in modern C++ unless interfacing with legacy C-APIs.

```cpp
int rawArr[5] = {1, 2, 3, 4, 5};
```

### B. `std::array<T, N>` (Introduced in C++11)

* **Characteristics:** A container that encapsulates fixed-size arrays. It lives on the stack, has zero overhead compared to raw arrays, but provides standard container benefits (like `.size()`, iterators, and bounds-checking via `.at()`).

* **Usage:** When the size is fixed and known at compile-time, and you want stack allocation with container safety.

```cpp
#include <array>
// Note: If using 'using namespace std;', you can write 'array<int, 5>'
std::array<int, 5> fixedArr = {1, 2, 3, 4, 5};
```

### C. `std::vector<T>` (Dynamic Array)

* **Characteristics:** A sequence container that encapsulates dynamic size arrays. It handles its own memory management, automatically resizing (allocating and deallocating on the heap) as elements are added or removed.

* **Usage:** The default choice for most sequences in C++ where the size can change dynamically at runtime.

```cpp
#include <vector>
// Note: If using 'using namespace std;', you can write 'vector<int>'
std::vector<int> dynamicArr = {1, 2, 3};
dynamicArr.push_back(4); // Automatically resizes
```