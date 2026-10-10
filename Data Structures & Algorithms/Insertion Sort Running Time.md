

Implementation: [[Insertion Sort Algorithm]]
Method: [[Running Times (n) of non-recursive algorithms]]

## The pseudocode we count

```
1 for i <- 1 to length(ar) - 1 (inclusive)
2     active_key <- ar[i]
3     h <- i
4     while h > 0 and ar[h - 1] > active_key
5         ar[h] <- ar[h - 1]
6         h <- h - 1
7     ar[h] <- active_key
```

`h` is the **hole index**. Invariant: before each outer iteration `i`,
`ar[0 .. i-1]` is already sorted.

## The four basic steps we count

| Step | Line |
|---|---|
| Left-boundary check (`h > 0`) | 4 |
| Comparison with active key (`ar[h-1] > active_key`) | 4 |
| Right shift | 5 |
| Insertion | 7 |

These are the same four the Week 01 insertion-sort animator counts.

## Best case — ascending input

If `ar` is already ascending, `ar[h-1] > active_key` is false immediately,
so the `while` body never runs: **no right shifts at all**.

The outer loop runs $n - 1$ times, and each iteration does:

- 1 left-boundary check (line 4)
- 1 comparison (line 4)
- 1 insertion (line 7)

Total steps grow in proportion to $n$, so $T(n) = \Theta(n)$.

## Worst case — descending input

Every key must travel all the way to the front. When outer iteration $i$
starts, `active_key` is smaller than all $i$ keys to its left, so the loop
shifts all of them right before inserting at index 0. Iteration $i$ does:

| Count | Step | Why |
|---|---|---|
| $i + 1$ | left-boundary checks | one extra check when `h` reaches 0 |
| $i$ | comparisons | none when `h` reaches 0 — **short-circuit evaluation** |
| $i$ | right shifts | |
| $1$ | insertion | |

Summing comparisons over $i = 1, 2, \dots, n-1$:

$$
1 + 2 + \cdots + (n-1) = \frac{n(n-1)}{2}
$$

which grows in proportion to $n^2$. The same reasoning applies to the
boundary checks and right shifts. So $T(n) = \Theta(n^2)$.

> [!important] The same algorithm is $\Theta(n)$ on one input and
> $\Theta(n^2)$ on another. The case is a property of the **input**, not of
> the algorithm — and not of the notation. See
> [[Asymptotic Notation (O, Omega, Theta)]].

> [!tip] Focus on the dominant growth trend
> For large $n$ the leading term outweighs small details like the "+1" in
> the boundary checks, or the $n-1$ insertions beside the $n(n-1)/2$
> comparisons.
