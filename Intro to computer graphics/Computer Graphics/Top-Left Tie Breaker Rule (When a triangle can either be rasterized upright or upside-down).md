

#### Finding the top left edges and bottom edge of a triangle (Counter-clockwise)
![[Pasted image 20260722123819.png|432]]

![[Pasted image 20260722123835.png|472]]
> [!note]
> Find the line that is horizontally straight and see if the line is being drawn from left to right or right to left. (Top Edge if line is drawn right to left and Bottom Edge for line drawn left to right)

#### Back-Face Culling CCW or CW traversals (for 3D)

![[Pasted image 20260722124107.png|531]]

$$
\text{Signed Area} = \frac{1}{2} \begin{vmatrix} x_0 & x_1 & x_2 \\ y_0 & y_1 & y_2 \\ 1 & 1 & 1 \end{vmatrix} = \frac{1}{2} \Big[ (x_1 - x_0)(y_2 - y_0) - (x_2 - x_0)(y_1 - y_0) \Big]
$$
> [!attention] Cull Rule:
> If signed area≤ 0, the triangle is back-facing or completely flat and is instantly dropped before traversal begins.



![[Pasted image 20260722123904.png|535]]

**Find point normal equation of <font color="#ff0000">P0 to P1 if boundary is L2</font>**
**Find point normal equation of <font color="#ff0000">P1 to P2 if boundary is L0</font>**
**Find point normal equation of <font color="#ff0000">P2 to P0 if boundary is L1</font>**

`// Pre-calculated during triangle setup`
`bool tl = (E.a > 0) || (E.a == 0 && E.b < 0);`

`// Fast bitwise/conditional check inside the pixel loop`
`bool FragmentInTriangle(Edge E0, Edge E1, Edge E2, double hEval0, double hEval1, double hEval2) {`
    `return (hEval0 > 0.0 || (hEval0 == 0.0 && E0.tl)) &&`
           `(hEval1 > 0.0 || (hEval1 == 0.0 && E1.tl)) &&`
           `(hEval2 > 0.0 || (hEval2 == 0.0 && E2.tl));`
`}`

