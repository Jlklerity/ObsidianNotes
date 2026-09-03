

`// AABB for triangle is computed and defined as: min(xmin, ymin) and max(xmax, ymax)`
`// where all four coordinate values are integral`
`Eval0 = DotProduct(E0, P(xmin+0.5, ymin+0.5))`
`Eval1 = DotProduct(E1, P(xmin+0.5, ymin+0.5))`
`Eval2 = DotProduct(E2, P(xmin+0.5, ymin+0.5))`
`for (y{ymin}; y < ymax; ++y) {`
	`// start values [at fragment centers] for horizontal spans`
	`hEval0 = Eval0; hEval1 = Eval1; hEval2 = Eval2;`
	`for (x{xmin}; x < xmax; ++x) {`
		`if (FragmentInTriangle(E0, E1, E2, hEval0, hEval1, hEval2)) {`
		`set_pixel(x, y, color); // fragment shader`
		`}`
	`// incrementally update hEval0, hEval1, hEval2`
	`}`
`// incrementally update Eval0, Eval1, Eval2`
`}`

`// return true if fragment centre is in:`
`// inside half-plane of edge E0 [or on top or left edge E0] AND`
`// inside half-plane of edge E1 [or on top or left edge E1] AND`
`// inside half-plane of edge E2 [or on top or left edge E2];`
`// otherwise return false`
`bool FragmentInTriangle(Edge E0, Edge E1, Edge E2,` 
										`double hEval0, double hEval1, double hEval2) {`
		`return (`
		`(hEval0 > 0. || (hEval0==0. && E0.tl)) &&`
		`(hEval1 > 0. || (hEval1==0. && E1.tl)) &&`
		`(hEval2 > 0. || (hEval2==0. && E2.tl))`
		`) ? true : false;`
`}`