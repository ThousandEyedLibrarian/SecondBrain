It's a list of numbers, dumbass. (2,1) is a vector.

Dimensionality is the number of elements in the vector. We describe this in terms of dimensions, eg the vector above is 2d, (1,2,3,4,5) would be 5D etc.

2D and 3D are obviously easy to draw, above that is not.

A vector is typically used as a coordinate in space but really can represent a collection of most sorts.

Represented in code as vec = (v1, v2, v3) where the v's are values, normally x, y and z.

Vectors are normally represented using [[Arrays]].

## Vector Operations

1. Sum: Add all elements together -> outputs a [[Scalar]] (single number)
2. [[Dot Product]] ($x \cdot y$): Add the elements of two vectors element-wise -> outputs a [[Scalar]] (single number)
	1. But what *is this doing*?? It tells us how aligned two vectors are, it projects vector 2 onto vector 1. Imagine a sun as below, the blue line is the shadow per se of vector 2 on vector 1, ie the area of alignment.
		1. If the dot product is 0 the vectors are perfectly aligned, orthagonal.

![[Screenshot 2025-12-15 at 16.17.45.png]]

Note: sum and dot product can be done regardless of the dimensionality of the two vectors

You can also think of [[Functions]] as Vectors and same with their operations, see the Functions page. Sneak preview below.

![[Screenshot 2025-12-15 at 16.39.42.png]]

3. Vector Norm: Takes one n-Dimen. vector -> outputs [[Scalar]]

![[Screenshot 2025-12-15 at 16.51.17.png]]



See also:
- [[Functions]]
- [[Functions (Mathematics)]]
- [[Mathematics]]