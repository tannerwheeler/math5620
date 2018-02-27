# 5 Point Stencil

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** void initMesh5(double start, double end, int meshSize)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will define a mesh grid for your 5 point stencil.  A matrix will be initialized from the Matrix class in **Appendix B** from the 5 point stencil constructor.  This will then take the input from the function specified in code below and solve Ax = b using a LU factorization.

**Input:** Input includes: where is your starting point, where is your ending point, and the number of mxm grid size you want between them.

**Output:**  This method will print the solution to the console when finished.  It will not return any values.

**Usage/Example:** If I wanted to find all of the solution of the Laplace equation \Delta u = sin(xy) from starting point -1 and ending point 3 in the x and y directions with a mesh size of 3 I would enter:
```
initMesh5(-1, 3, 3);
```
This would then use the points (0, 0), (0, 1), (1, 0), (0, 2), (1, 1)... to initialize the right hand matrix and solve the equation.

**Implementation/Code:** The following is the code for 'void initMesh5(double start, double end, int meshSize)'.
```
void initMesh5(double start, double end, int meshSize)
{
	double h = (end - start - 1) / static_cast<double>(meshSize);

	int size = meshSize * meshSize;

	Matrix f(size, 1, false);

	for (int i = 0; i < meshSize; i++)
	{
		for (int j = 0; j < meshSize; j++)
		{
			f.layout[(i * meshSize) + j][0] = h * h * std::sin((i * h)*(j * h));   // This is where you declare your function.
		}
	}

	Matrix mesh(meshSize);
	Matrix l(mesh.getM(), mesh.getN(), false);
	Matrix u(mesh.getM(), mesh.getN(), false);

	l_u_factorization(mesh, l, u);

	Matrix x = Gauss(u, Gauss(l, f));

	x.print();
}
```
**Last Modified:** February/2018
