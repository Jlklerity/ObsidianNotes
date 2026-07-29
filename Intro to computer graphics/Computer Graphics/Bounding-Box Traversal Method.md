

`struct Point {`
    `int x, y;`
`};`
`// Edge function: returns positive if (px, py) is to the left of the edge from a to b,`
`// negative if to the right, and zero if exactly on the edge.`
`// This is the cross product of (b - a) and (p - a).`
`int edge_function(Point a, Point b, int px, int py) {`
    `return (b.x - a.x) * (py - a.y) - (b.y - a.y) * (px - a.x);`
`}`
`void rasterize_triangle(Point& p1, Point& p2, Point& p3) {`
    `// 1. Compute the bounding box of the triangle from its three vertices.`
    `int x_min = std::max(0,         std::min({p1.x, p2.x, p3.x}));`
    `int x_max = std::min(WIDTH - 1, std::max({p1.x, p2.x, p3.x}));`
    `int y_min = std::max(0,         std::min({p1.y, p2.y, p3.y}));`
    `int y_max = std::min(HEIGHT - 1,std::max({p1.y, p2.y, p3.y}));`
`}`

#### Incremental Evaluation of Edge Equations Method
`w0 += A0; 
`w1 += A1;`
`w2 += A2;`

> [!warning]
> Incremental evaluation on its own does not tell you which pixels to visit. It only tells you how to cheaply compute the edge function as you move. It still needs some iteration domain, and the bounding box provides that.