

## Hypothesis: $f$ must be **continuous** on $[a, b]$

> Everything below fails without this.

---

## FTC Part 1 — differentiating an integral gives back the function

Define
$$g(x) = \int_a^x f(t)\, dt \qquad a \le x \le b$$

Then $g$ is:
- continuous on $[a, b]$
- differentiable on $(a, b)$
- and $$g'(x) = f(x)$$

### Why $t$ and not $x$ inside?
$t$ is a <font color="#c00000">dummy variable</font>. $x$ is already used as the upper limit, so it cannot also be the variable being integrated over.

---

## FTC Part 2 — evaluating a definite integral

$$\int_a^b f(x)\, dx = F(b) - F(a)$$
where $F$ is **any** antiderivative of $f$.

> [!hint]
> FTC2 is what turns integration from "compute a limit of infinitely many rectangles" into "find one antiderivative and subtract".

> [!question] Why "any" antiderivative?
> If $F$ and $G$ are both antiderivatives of $f$, then $F = G + C$. Compute $(G(b)+C) - (G(a)+C)$ — what happens to $C$?
