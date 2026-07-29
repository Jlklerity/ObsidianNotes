### Edge-Walking Method

> [!info]
> Checks for a change in the middle vertex’s direction and draws a horizontal line across the vertex to separate the triangle into top half and bottom half.

![[Pasted image 20260722122630.png|303]]

> [!failure] Drawbacks:
> Extremely complicated setup for edge cases (e.g., triangles with already horizontal edges or skinny "slivers"). It is highly serial and cannot be distributed efficiently across parallel GPU cores.