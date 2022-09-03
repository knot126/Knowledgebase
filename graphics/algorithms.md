# List of rasterisable and raytraceable primitives with algorithms

This is an *incomplete* list of possible **primitives in computer graphics**, as well as **algorithms** that go with them and links to descriptions of the algorithms if available.

## Rasterisation

### Common for Rasterisaton

These primitives are common &mdash; especailly in 3D graphics &mdash; because they are easy to work with.

 * Points
 * Lines
   * Naïve (solve $y = rx + c$) [[Wikipedia](https://en.wikipedia.org/wiki/Line_drawing_algorithm#A_naive_line-drawing_algorithm)]
   * DDA [[Wikipedia](https://en.wikipedia.org/wiki/Digital_differential_analyzer_(graphics_algorithm))]
   * Midpoint line generation algorithm [[GeeksForGeeks](https://www.geeksforgeeks.org/mid-point-line-generation-algorithm/)]
   * Bresenham's line algorithm [[Wikipedia](https://en.wikipedia.org/wiki/Bresenham%27s_line_algorithm)]
   * Xiaolin Wu's line algorithm (with AA) [[Wikipedia](https://en.wikipedia.org/wiki/Xiaolin_Wu%27s_line_algorithm)]
   * Gupta-Sproull algorithm (with AA)
   * Signed distance function
 * Triangles
   * Edge function [[Scratchapixel](https://www.scratchapixel.com/lessons/3d-basic-rendering/rasterization-practical-implementation/rasterization-stage)]
   * Barycentric coordinates [[Scratchapixel](https://www.scratchapixel.com/lessons/3d-basic-rendering/rasterization-practical-implementation/rasterization-stage)]</li>
   * Scanline rasterisation [[Wikipedia](https://en.wikipedia.org/wiki/Scanline_rendering)]</li>
   * Signed distance function
 * Quadrilaterals
   * Edge function extended

### Rasterisable

Other primitives for which at least one algorithm exists for rasterising explicitly - that is, it doesn't require tesselation and then using some other algorithm. Not every one of these will be easy to use in 3D.

 * Rectangles
   * Naïve
   * Signed distance function
 * Elipses and circles
   * Midpoint circle algorithm [[GeeksForGeeks](https://www.geeksforgeeks.org/mid-point-circle-drawing-algorithm/)]
   * Signed distance function
 * Bézier curves
   * Naïve (find the $y$-values for given $x$-value)
   * Bresenham extended [[Alois Zingl](http://members.chello.at/easyfilter/bresenham.html)]
   * Signed distance function
 * Béziergon and SVG-like paths
   * Loop-Blinn 2005 [[GPU Gems](https://developer.nvidia.com/gpugems/gpugems3/part-iv-image-effects/chapter-25-rendering-vector-art-gpu) | [paper](https://www.microsoft.com/en-us/research/wp-content/uploads/2005/01/p1000-loop.pdf)]
   * Wavelet rasterisation [[paper](https://people.engr.tamu.edu/schaefer/research/wavelet_rasterization.pdf)]
 * Convex polygons
   * Edge function extended
 * Splines
   * Bresenham extended [[paper](http://members.chello.at/~easyfilter/Bresenham.pdf)]
 * Concave polygons
   * Odd-even edge algorithm

## Ray-tracing

### Analytical

Shapes for which ray intersection locations can be found analytically.

 * Points
 * Lines
 * Triangles
 * Planes
 * Quadratic, cubic and quartic surfaces
   * Spheres
 * Discs

Not technically related, but worth mentioning:

 * Constructive solid geometry

### Intersectable

Shapes for which ray intersections can be found, but might require numerical methods. This is often since [their roots cannot be found analytically using reasonable methods](https://en.wikipedia.org/wiki/Abel%E2%80%93Ruffini_theorem).

 * Bézier surfaces
 * B-spline and NURBS surfaces
 * $n$-degree single-variable polynomial surfaces