
#### Midpoint Error Derivation Graph

![[Pasted image 20260722122221.png|432]]

#### Symmetry Of Lines

![[Pasted image 20260722122248.png|433]]![[Pasted image 20260722122303.png|606]]


`int dx = x2 - x1, dy = y2 - y1;`
`int sx = (dx > 0) ? 1 : -1;`
`int sy = (dy > 0) ? 1 : -1;`
`dx = abs(dx);`
`dy = abs(dy);`

`bool swapped = false;`
`if (dy > dx) {`
    `std::swap(dx, dy);`
    `swapped = true;`
`}`

`// 1. Initialize the decision variables`
`int d = 2 * dy - dx;`
`int de = 2 * dy;`
`int dne = 2 * (dy - dx);`

`// 2. Loop through every step along the driving axis (runs dx + 1 times)`
`for (int i = 0; i <= dx; ++i) {`
    `set_pixel(x1, y1, color); // Plot the current pixel`

    if (d > 0) {
        d += dne;
        // Conditional step along the passive axis
        if (!swapped) {
            y1 += sy;
        } else {
            x1 += sx;
        }
    } else {
        d += de;
    }

    // 3. Unconditional step along the driving axis
    if (!swapped) {
        x1 += sx;
    } else {
        y1 += sy;
    }
`}`

> [!important] Terms for Triangle Rasterization
> Interior Fragments —> Fragments to be rasterized in the triangle primitive
> Scanline —> Fragments in a row of colorbuffer