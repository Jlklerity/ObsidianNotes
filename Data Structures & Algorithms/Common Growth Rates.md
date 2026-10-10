# Common Growth Rates

## Notation: lg means log base 2

> [!info] Throughout this course, $\lg n = \log_2 n$ (binary logarithm).

Inside $O$, $\Omega$ and $\Theta$ the base is **irrelevant**, because
changing base only multiplies by a constant. Elsewhere it is not: a
recursion tree that halves the problem has $\lg n$ levels, not $\log_{10} n$.

> [!note] $o$ and $\omega$
> Cormen et al. also define little-o and little-omega, for bounds that are
> **not** asymptotically tight. This course uses only $O$, $\Omega$ and
> $\Theta$ — the other two are not examinable, but you will meet them in the
> textbook.

## The ordering

For sufficiently large $n$, each row grows faster than the one above it:

| Function | Name |
|---|---|
| $1$ | constant |
| $\lg n$ | logarithmic |
| $(\lg n)^k$, $k > 0$ | polylogarithmic |
| $n^z$, $0 < z < 1$ | sublinear power law |
| $n$ | linear |
| $n \lg n$ | linearithmic |
| $n^k$, $k > 1$ | polynomial |
| $a^n$, $a > 1$ | exponential |
| $n!$ | factorial |

> [!tip] Reading the plots
> On **linear** axes the gaps look dramatic only for large $n$. On
> **log-log** axes, each power $n^k$ becomes a straight line of slope $k$,
> which makes polynomial degrees easy to compare by eye — and exponentials
> still curve upward.

## Checkpoint (graded)

Rank by order of growth, slowest to fastest: $\lg n$, $n^2$, $n \lg n$, $n$.

Submitted in *Week 02 Lecture: Checkpoint* on xSITe. Unlike Week 01's
practice checkpoint, **this one is graded**.

---
Related: [[Asymptotic Notation (O, Omega, Theta)]]
Next: [[Divide and Conquer]]
