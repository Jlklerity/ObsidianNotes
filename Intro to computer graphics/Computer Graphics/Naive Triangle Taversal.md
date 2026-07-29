

`// Checking each pixel individually`
`for (int y{}; y < window_height; ++y) {`
	`for (int x{}; x < window_width; ++x) {`
		`if (PointInEdge(E0, P(x+0.5, y+0.5)) &&`
			`PointInEdge(E1, P(x+0.5, y+0.5)) &&`
			`PointInEdge(E2, P(x+0.5, y+0.5)))`
			`set_pixel(x, y, color);`
	`}`
`}`