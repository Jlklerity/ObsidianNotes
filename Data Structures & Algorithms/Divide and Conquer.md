# Divide and Conquer

Non-recursive algorithms are analysed by counting how often each operation
executes — see [[Running Times (n) of non-recursive algorithms]] and
[[Insertion Sort Running Time]]. **Recursive** algorithms need different
techniques. Divide-and-conquer algorithms are a prominent class of recursive
algorithms, and several methods exist for analysing them.

## The three steps

> [!info] 1. Divide
> Partition the problem into one or more subproblems, each a smaller
> instance of the same problem.

> [!info] 2. Conquer
> Solve the subproblems recursively, until they reach a **base case** that
> can be solved directly.

> [!info] 3. Combine
> Integrate the subproblem solutions into a solution to the original problem.

## The general pattern

Every divide-and-conquer algorithm splits into $a$ subproblems of size
$n/b$, and does $f(n)$ work to divide and combine. All three vary:

| Algorithm | $a$ | $n/b$ | $f(n)$ | Recurrence |
|---|---|---|---|---|
| Binary search | 1 | $n/2$ | $\Theta(1)$ | $T(n) = T(n/2) + \Theta(1)$ |
| Ternary search | 1 | $n/3$ | $\Theta(1)$ | $T(n) = T(n/3) + \Theta(1)$ |
| Merge sort | 2 | $n/2$ | $\Theta(n)$ | $T(n) = 2T(n/2) + \Theta(n)$ |
| Strassen's matrix multiplication | 7 | $n/2$ | $\Theta(n^2)$ | $T(n) = 7T(n/2) + \Theta(n^2)$ |

- The searches **discard all but one part**, so only $b$ differs.
- Strassen (1969) cuts each matrix into four half-width blocks and combines
  them using **seven** block products.

Only merge sort is covered in this course; the others are examples.
A [[Recursion Trees|recursion tree]] solves any of them.

---
Next: [[Merge Sort]]
