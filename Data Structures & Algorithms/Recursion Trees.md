# Recursion Trees

> [!info] Definition
> A **recursion tree** visualises a recurrence by expanding the recursive
> calls into a tree. Each node represents one subproblem, labelled with the
> work done **outside** the recursive calls at that call (the "combine"
> cost). The recursive calls are not missing from the accounting: they are
> the node's subtrees, so adding up every node gives the whole running time.

## Expanding merge sort's recurrence

$\Theta(n)$ means dividing and merging $n$ keys takes between two fixed
multiples of $n$ steps. Write that work as $cn$, with $c$ standing for
either multiple:

$$
T(n) = 2\,T(n/2) + cn
$$

> [!note] Why the "=" is safe here
> Strictly there are **two inequalities**: $\le$ with the larger multiple and
> $\ge$ with the smaller. The first gives an upper bound on $T(n)$, the
> second a lower bound. Adding up the tree gives the same two bounds — a
> short induction on the number of levels.

Expanding one level at a time (Cormen et al. 2022, Figure 2.5):

```
(a)      T(n)

(b)       cn
         /  \
    T(n/2)  T(n/2)

(c)       cn
         /  \
      cn/2  cn/2
      /  \  /  \
   T(n/4) ... T(n/4)
```

## The full tree

The tree continues until the subproblem size reaches 1. The size **halves at
every level**, so merge sort needs $\lg n$ levels.

```
level                                              Time spent
  0                    cn                              cn
                     /    \
  1              cn/2      cn/2                        cn
                /   \      /   \
  2         cn/4   cn/4  cn/4  cn/4                    cn
              ...        ...        ...
lg n     T(1) T(1)  ...        T(1)                  Theta(n)
              <-- n nodes at the bottom -->
```

## Time spent per non-leaf level

At level $i$ with $0 \le i < \lg n$, the tree holds $2^i$ subproblems, each
of size $n/2^i$. Merging $m$ keys takes time proportional to $m$
(see [[Merge Sort]]), so one subproblem costs $c\,n/2^i$ and the whole level
costs

$$
2^i \cdot \frac{cn}{2^i} = cn .
$$

> [!important] The two factors cancel: descending the tree shrinks the
> subproblems at exactly the rate their number grows.

With $\lg n$ such levels, the total non-leaf cost is
$cn \lg n = \Theta(n \lg n)$.

## Total time

Every leaf is a subproblem of one key, already sorted, so the base case
returns immediately: $\Theta(1)$ each. With $n$ leaves, the bottom level
costs $n \cdot \Theta(1) = \Theta(n)$ — **negligible** beside the
$cn \lg n$ above it.

$$
\boxed{\;T(n) = \Theta(n \lg n)\;}
$$

> [!note] If $n$ is a power of two, this argument is an exact derivation.
> Otherwise the levels are ragged and the tree gives a well-founded *guess*.

---
Next week: the **Master Theorem**, which reads the answer off a recurrence
with no tree at all.
