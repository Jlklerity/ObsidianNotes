# [[Merge Sort Code]]

The paradigmatic [[Divide and Conquer|divide-and-conquer]] algorithm.

> [!note] Indexing
> The textbook and the video tutorial index arrays from **1**. C++ and the
> merge-sort animator index from **0**. The pseudocode below indexes from 0.

## The top-level algorithm

```
1 sort(ar, 0, length(ar) - 1)

  procedure sort(ar, lo, hi)
  // lo, hi are the low and high boundary indices; md is the midpoint.
  // Postcondition: ar[lo .. hi] sorted.
2   if lo < hi
3     md <- floor((lo + hi) / 2)
4     sort(ar, lo, md)
5     sort(ar, md + 1, hi)
6     merge(ar, lo, md, hi)
```

| Line | Step | Note |
|---|---|---|
| 2 | base case | nothing to do when `lo >= hi` (at most one key) |
| 3 | **divide** | split the range in half |
| 4–5 | **conquer** | 2 recursive calls, each on half the keys |
| 6 | **combine** | merge, $\Theta(m)$ for $m$ keys |

All the combine work happens inside `merge`.

## The merge step

`merge(ar, lo, md, hi)` assumes `ar[lo .. md]` and `ar[md+1 .. hi]` are
sorted, and leaves `ar[lo .. hi]` sorted.

> [!note] The two temporary arrays below are a **storage choice**. Merging
> itself does not require them.

### 1 of 3 — copy out the two halves

```
1  n_left  <- md - lo + 1
2  n_right <- hi - md
3  left  <- array of length n_left
4  right <- array of length n_right
5  for j <- 0 .. n_left - 1
6      left[j] <- ar[lo + j]
7  for k <- 0 .. n_right - 1
8      right[k] <- ar[md + 1 + k]
9  i <- lo
10 j <- 0
11 k <- 0
```

Three positions: `i` in the destination `ar`, and `j`, `k` in the sources.

### 2 of 3 — the main loop

```
1 while j < n_left and k < n_right
2     if left[j] <= right[k]
3         ar[i] <- left[j]
4         j <- j + 1
5     else
6         ar[i] <- right[k]
7         k <- k + 1
8     i <- i + 1
```

Each iteration writes **exactly one key**, after **exactly one comparison**.
The loop stops as soon as either source runs out.

### 3 of 3 — the cleanup loops

```
1 while j < n_left
2     ar[i] <- left[j]
3     i <- i + 1
4     j <- j + 1
5 while k < n_right
6     ar[i] <- right[k]
7     i <- i + 1
8     k <- k + 1
```

At most one of these does any work in a given call, but **both are needed**,
because either half may empty first.

No comparison is required once one half is empty: what remains in the other
half is already sorted among itself, and every one of those keys is at least
as large as every key already written.

## Merge without any arrays named

Strip the storage away and the algorithm is six lines. It needs three
positions: how far each source has been consumed, and how far the
destination has been filled.

```
1 while both sources still hold an unprocessed key
2     compare the two unprocessed heads
3     write the smaller one to the destination
4     advance the source it came from
5     advance the destination
6 append whatever remains of the source that is not yet empty
```

Nothing here says *where* the sources or destination live. The
implementation above is one arrangement of storage, not the only one, and
these six lines do not change when the arrangement does.

## [[Merge Invariant]] 

> [!important] Invariant
> The output produced so far consists of **exactly the smallest keys already
> taken** from the two source sequences, in ascending order. Every key not
> yet taken is at least as large as every key already written.

Why it matters — the invariant is what makes a merge correct:

- it holds before the first key is written;
- every write preserves it;
- when both sources are empty, it says the whole output is sorted.

> [!warning] Debugging test for the lab
> Ascending output *so far* is **not** enough. Take a key while a smaller one
> still waits, and the error surfaces only later — when that smaller key has
> to be written after a larger one.

## Why merging a segment takes linear time

Let $m$ be the number of keys being merged; count iterations of the main
loop and both cleanup loops together.

- Every key has to be written, so the work is **at least** proportional to $m$.
- Each iteration writes exactly one key, so there are **exactly $m$** iterations.
- Only the main loop compares, once per iteration, so **at most $m$** comparisons.
- One iteration costs a constant number of basic steps — one write, two
  index increments, at most one comparison — none depending on $m$.

$$
\text{Merging } m \text{ keys takes } \Theta(m) \text{ time.}
$$

Different implementations move the keys differently, but $\Theta(m)$ survives
all of them: each touches every key a constant number of times.

## The recurrence

A **recurrence** is an equation describing a function in terms of its value
at smaller arguments. Taking the three steps in turn on $n$ keys (assuming
for simplicity that $n$ is a power of two):

| Step | Cost |
|---|---|
| Divide: compute the midpoint | $\Theta(1)$ |
| Conquer: two recursive calls on $n/2$ keys | $2\,T(n/2)$ |
| Combine: merge two sorted halves | $\Theta(n)$ |

Absorbing $\Theta(1)$ into the larger $\Theta(n)$:

$$
T(n) = 2\,T(n/2) + \Theta(n)
$$

> [!note] Anonymous function
> That $\Theta(n)$ is an *anonymous function*, not a set: inside a larger
> expression it stands for some unnamed function that is $\Theta(n)$. This
> convention is what lets us write the recurrence without knowing the
> merge's exact cost — only that it grows linearly.

## What if n is odd?

Real inputs are not obliging: five keys split into two and three. The honest
recurrence uses floors and ceilings:

$$
T(n) = T\!\left(\left\lfloor \tfrac{n}{2} \right\rfloor\right)
     + T\!\left(\left\lceil \tfrac{n}{2} \right\rceil\right) + \Theta(n)
$$

These can be shown to leave the answer unchanged: the solution is still
$\Theta(n \lg n)$.

> [!danger] Keep two things apart
> - *Assume $n$ is a power of two* is a simplification **for the analysis**.
>   It keeps the recursion tree balanced and the algebra readable.
> - **An implementation may never assume it.** Real code has to handle five
>   keys, or seven, or one. A merge sort that quietly assumes a power of two
>   is wrong on most inputs.

---
Next: [[Recursion Trees]]
