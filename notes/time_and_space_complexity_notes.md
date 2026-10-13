# Time and Space Complexity: Study Notes

Welcome to your study notes on algorithmic complexity. This guide covers the fundamental concepts needed to analyze how efficiently algorithms run and how much memory they consume.

---

## 1. Asymptotic Notations: Big O, Big Omega, and Big Theta

Asymptotic notation is a mathematical way to describe the limiting behavior of a function—specifically, how an algorithm's resource usage grows as the input size ($n$) grows very large.

*   **Big O Notation ($O$): Upper Bound**
    *   Describes the **worst-case** scenario (or upper bound) for growth.
    *   It guarantees that the algorithm will not take *longer* than the specified order of growth.
    *   *Mathematical intuition:* $f(n) = O(g(n))$ means there exist positive constants $c$ and $n_0$ such that $0 \le f(n) \le c \cdot g(n)$ for all $n \ge n_0$.

*   **Big Omega Notation ($\Omega$): Lower Bound**
    *   Describes the **best-case** scenario (or lower bound) for growth.
    *   It guarantees that the algorithm will take *at least* as long as the specified order of growth.
    *   *Mathematical intuition:* $f(n) = \Omega(g(n))$ means there exist positive constants $c$ and $n_0$ such that $0 \le c \cdot g(n) \le f(n)$ for all $n \ge n_0$.

*   **Big Theta Notation ($\Theta$): Tight Bound**
    *   Describes the **exact** asymptotic behavior (both upper and lower bounds).
    *   An algorithm is $\Theta(g(n))$ if it is both $O(g(n))$ and $\Omega(g(n))$.

---

## 2. Best, Average, and Worst Case Scenarios

When analyzing an algorithm, input characteristics often dictate performance beyond just the size ($n$).

*   **Best Case:**
    *   The scenario where the algorithm takes the minimum amount of resources (time or space) for an input of size $n$.
    *   *Example:* Searching for an element that is located at the very first index of an array using Linear Search results in a best-case time complexity of $\Theta(1)$.

*   **Average Case:**
    *   The expected resource consumption averaged across all possible inputs of size $n$ (assuming a certain probability distribution, usually uniform).
    *   *Example:* In standard randomized QuickSort, the average-case time complexity is $O(n \log n)$.

*   **Worst Case:**
    *   The scenario that forces the algorithm to take the maximum amount of resources for an input of size $n$.
    *   This is the most commonly analyzed metric in competitive programming and systems engineering because it provides a reliable performance guarantee.
    *   *Example:* Searching for an element that does not exist in an array using Linear Search results in a worst-case time complexity of $O(n)$.

---

## 3. Analyzing Loops and Nested Loops

Code blocks executed sequentially or repeatedly can be analyzed using basic counting and summation rules.

*   **Single Loops:**
    *   A loop that runs $n$ times typically has a time complexity of $O(n)$.
    *   If the loop variable increments or decrements by multiplying or dividing by a constant factor $c$ (e.g., $i = i \times 2$), the complexity is logarithmic: $O(\log n)$.

    ```text
    // O(n) example
    for (int i = 0; i < n; i++) {
        // Constant time operation O(1)
    }

    // O(log n) example
    for (int i = 1; i < n; i *= 2) {
        // Constant time operation O(1)
    }
    ```

*   **Nested Loops:**
    *   When loops are nested, you multiply the complexities of each loop if the inner loop depends on the outer loop, or use summations.
    *   *Independent nested loops:* If loop 1 runs $n$ times and loop 2 runs $m$ times independently, complexity is $O(n \times m)$.
    *   *Dependent nested loops:* If the inner loop runs based on the current value of the outer loop (e.g., $j$ from $0$ to $i$), the total operations equal $1 + 2 + 3 + \dots + n = \frac{n(n+1)}{2}$, which simplifies to $O(n^2)$.

    ```text
    // O(n^2) example
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i; j++) {
            // Constant time operation O(1)
        }
    }
    ```

---

## 4. Recursion and Recursion Stack Complexity

Recursive functions call themselves, creating active frames on the call stack until a base case is reached.

*   **Time Complexity of Recursion:**
    *   Determined by: **(Number of recursive calls) $\times$ (Work done per recursive call)**.
    *   Can often be solved using recursion trees, substitution method, or the **Master Theorem** for divide-and-conquer recurrences of the form $T(n) = aT(n/b) + f(n)$.

*   **Space Complexity (Call Stack) of Recursion:**
    *   The space complexity is proportional to the **maximum depth of the recursion tree** (i.e., the maximum height of the call stack at any given moment).
    *   Even if a function creates local variables, if the stack depth reaches $n$, the auxiliary stack space is $O(n)$.

*   *Example:* Factorial Function
    ```text
    int factorial(int n) {
        if (n <= 1) return 1;          // Base case
        return n * factorial(n - 1);   // Recursive call
    }
    ```
    *   **Time Complexity:** $O(n)$ because there are $n$ recursive calls, each doing $O(1)$ work.
    *   **Space Complexity:** $O(n)$ because the recursion stack grows to a depth of $n$ before hitting the base case.

---
*Tip: Always distinguish between Auxiliary Space (extra space used by the algorithm) and Total Space (auxiliary space + input space).*