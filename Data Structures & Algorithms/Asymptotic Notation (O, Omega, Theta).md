# Asymptotic Notation (O, Omega, Theta)

To describe the dominant growth trend of $T(n)$ for large $n$, we compare it
to a simpler function $g(n)$, and ask whether a **constant multiple** of
$g(n)$ bounds it from above, below, or both — once $n$ is large enough.

| Notation | Pronunciation | Bound provided by $g(n)$ |
|---|---|---|
| $O(g(n))$ | Big O | Upper |
| $\Omega(g(n))$ | Big Omega | Lower |
| $\Theta(g(n))$ | Theta | Tight (upper and lower) |

## Definitions

All three assume $f$ and $g$ are asymptotically nonnegative.

> [!info] $O$ — upper bound
> $O(g(n)) = \{ f(n)$ : there exist positive constants $c$ and $n_0$ such
> that $0 \le f(n) \le c\,g(n)$ for all $n \ge n_0 \}$
>
> Beyond some point $n_0$, $f$ never exceeds a fixed multiple of $g$.

> [!info] $\Omega$ — lower bound
> $\Omega(g(n)) = \{ f(n)$ : there exist positive constants $c$ and $n_0$
> such that $0 \le c\,g(n) \le f(n)$ for all $n \ge n_0 \}$
>
> Beyond some point $n_0$, $f$ is never below a fixed multiple of $g$.

> [!info] $\Theta$ — tight bound
> $\Theta(g(n)) = \{ f(n)$ : there exist positive constants $c_1$, $c_2$ and
> $n_0$ such that $0 \le c_1 g(n) \le f(n) \le c_2 g(n)$ for all
> $n \ge n_0 \}$
>
> Beyond some point $n_0$, $f$ is squeezed between two fixed multiples of $g$.

Every definition has **its own** $n_0$, and none of them says anything about
what $f$ does to the left of $n_0$ — it may cross the bound there freely.

## The "=" is not equality

The definitions make $O(g(n))$ a **set of functions**, so the exact
statement is $f(n) \in O(g(n))$. Following Cormen et al. (2022) we write
$f(n) = O(g(n))$ instead — here "=" means set membership.

> [!warning] Consequences of the shorthand
> - Not symmetric: you may **not** write $O(g(n)) = f(n)$. The right-hand
>   side is always the coarser one.
> - You may **not** cancel a common right-hand side: from $f(n) = O(n^2)$
>   and $h(n) = O(n^2)$ it does **not** follow that $f(n) = h(n)$.

## Relationship between the three

> [!info] Theorem
> $f(n) = \Theta(g(n))$ **if and only if** $f(n) = O(g(n))$ and
> $f(n) = \Omega(g(n))$.

Example: insertion sort's worst case satisfies $T(n) = O(n^2)$ and
$T(n) = \Omega(n^2)$, therefore $T(n) = \Theta(n^2)$.
See [[Insertion Sort Running Time]].

## Worked example: $T(n) = qn^2 + rn + s$, with $q > 0$

$r$ and $s$ may be negative (the comparison count $n(n-1)/2$ has
$r = -1/2$), so we bound them by $|r|$ and $|s|$.

**Upper bound.** Take $n_0 = 1$:

$$
T(n) = qn^2 + rn + s \le qn^2 + |r|n + |s| \le qn^2 + |r|n^2 + |s|n^2
= (q + |r| + |s|)\,n^2
$$

using $x \le |x|$, then $1 \le n \le n^2$. So $c = q + |r| + |s|$ works and
$T(n) = O(n^2)$.

**Lower bound.** Take $n_0 = \max\{1,\ 2(|r| + |s|)/q\}$:

$$
T(n) \ge qn^2 - |rn + s| \ge qn^2 - (|r|n + |s|) \ge qn^2 - (|r| + |s|)n
\ge qn^2 - \tfrac{q}{2}n^2 = \tfrac{q}{2}n^2
$$

using $x \ge -|x|$, the triangle inequality, $1 \le n$, then
$n \ge 2(|r|+|s|)/q$. So $c = q/2$ works and $T(n) = \Omega(n^2)$.

Together: $T(n) = \Theta(n^2)$.

> [!note] What matters is that such constants **exist**, not the particular
> values chosen. A larger $n_0$ works just as well.

## $O$ is not "worst case"; $\Omega$ is not "best case"

The two ideas are independent:

- **Best/worst case** is about *which input* of size $n$ you consider.
- **$O$, $\Omega$, $\Theta$** are about *how a function grows*, whichever
  function you chose.

Any of the three notations can be applied to any case:

| Case | Input | Tight bound | Also true |
|---|---|---|---|
| Best | ascending | $\Theta(n)$ | $O(n)$ and $\Omega(n)$ |
| Worst | descending | $\Theta(n^2)$ | $O(n^2)$ and $\Omega(n^2)$ |

So "insertion sort is $O(n^2)$" and "insertion sort is $\Omega(n)$" are both
true, and **neither names a case**.

> [!danger] Saying $O$ when you mean worst case is the mistake to avoid.

## Style rules

- If you can prove $\Theta(g(n))$, state $\Theta(g(n))$ — don't use $O$ or
  $\Omega$ instead.
- Otherwise state the **tightest** bound you can justify. Anything $O(n^2)$
  is also $O(n^3)$, but $O(n^2)$ is more informative.
- Use the **simplest** function. If it is $\Theta(n^2)$ it is also
  $\Theta(9n^2 - 2n)$, but $\Theta(n^2)$ is clearer.
- Never treat the "=" as algebraic equality.

---
Next: [[Common Growth Rates]]
