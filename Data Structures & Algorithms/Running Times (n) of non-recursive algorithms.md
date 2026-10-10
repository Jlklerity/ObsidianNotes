

![[Pasted image 20260907141850.png]]

> [!question] What is it for
> $T(n)$ is the **number of basic steps** an algorithm performs on an input
> of size $n$ — not seconds. Seconds depend on the CPU, the compiler and
> implementation details; counting basic steps is machine-independent.
> See [[Basic Steps and Input Size]].


## Going from T(n) to an asymptotic bound

Dropping the constant multipliers and all but the highest power of $n$ gives
the **tight** bound, $\Theta$ — not $O$.

For example, if $T(n) = 3n^2 + 5n + 2$, then $T(n) = \Theta(n^2)$.

> [!warning] Why not "the algorithm is $O(n^2)$"?
> $O(n^2)$ is true, but it is only an **upper** bound, and a weak statement:
> the same function is also $O(n^3)$, $O(n^4)$, $O(n!)$ — all correct.
> $\Theta(n^2)$ says the growth is pinned from **both** sides, so state it
> whenever you can prove it.

> [!danger] Two things to be careful of
> - $O$ is **not** "a simpler version of $T(n)$". It is a *set of functions*
>   defined by $0 \le f(n) \le c\,g(n)$ for all $n \ge n_0$.
> - $O$ is **not** "worst case", and $\Omega$ is **not** "best case". The
>   case is about *which input* you pick; the notation is about *how a
>   function grows*.

Full definitions and the worked proofs:
[[Asymptotic Notation (O, Omega, Theta)]]

---
Applied to a real algorithm: [[Insertion Sort Running Time]]
