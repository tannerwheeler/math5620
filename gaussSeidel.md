# Gauss-Seidel Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** Matrix gSeidel(Matrix m, Matrix bValues)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method performs the Gauss-Seidel Method on the equation Ax = b.  It will use the Matrix class in Appendix B.  It will also use the splitting function splitULD(\~~) separating the upper, lower, and diagonal parts of A from each other.  It then will iterate until it converges or a specific number of iterations.  This can be change in the do while loop.  The commented out print() function calls are for debugging purposes.

**Input:** The input of this method consist of a Matrix, A, from Ax = b and a matrix, b, from Ax = b containing the obtained values.

**Output:** This method will return a matrix, x, for Ax = b.  Depending upon if it converged or completed the number of iterations first will cause this matrix to possibly vary.

**Usage/Example:**
If you wanted to use a 5-point stencil, 4 by 4 matrix for A in `Ax = b`.  This is done below in the initialization 
`Matrix i1(size);`.
```
int main()
{
	int size = 4;
	Matrix i1(size);

	std::vector<double> bValues(size * size, 1);
	Matrix b = bValues;

	Matrix gs = gSeidel(i1, b);
	gs.print();
  
	return 0;
}
```

`std::vector<double> bValues(size * size, 1);
Matrix b = bValues;`

This initialization will create the matrix `b` in `Ax=b`.  After calling `gSeidel(i1, b)` `gs` is equal to `x`.
With `gs.print();` it prints the matrix `x` is equal to
```
|  -0.8333  |
|  -1.1667  |
|  -1.1667  |
|  -0.8333  |
|  -1.1667  |
|  -1.6667  |
|  -1.6667  |
|  -1.1667  |
|  -1.1667  |
|  -1.6667  |
|  -1.6667  |
|  -1.1667  |
|  -0.8333  |
|  -1.1667  |
|  -1.1667  |
|  -0.8333  |
```

**Implementation/Code:** The following is the code for 
```
Matrix gSeidel(Matrix m, Matrix bValues)
{
	Matrix l(m.getM(), m.getN(), 0);
	Matrix u(m.getM(), m.getN(), 0);

	Matrix d(m.getM(), m.getN(), 0);
	splitULD(m, d, u, l);
	d = d + u;
	//d.print();

	Matrix b = bValues;
	//b.print();

	std::vector<double> initX(m.getN(), 0);

	Matrix identity(d.getM(), m.getN(), false);
	identity.initDiagonal(1);
	d = Gauss(d, identity);
	//d.print();

	Matrix exNott(initX);
	//exNott.print();
	Matrix exOne = exNott;

	int num = 0;

	do
	{
		exNott = exOne;

		exOne = l;

		exOne = exOne * exNott;
		//exOne.print();

		exOne = b - exOne;
		//exOne.print();

		exOne = d * exOne;
		//exOne.print();

		//exOne.print();
		//exNott.print();
		num++;

	} while (exOne != exNott && num < 600);

	std::cout << num << std::endl << std::endl;

	return exOne;
}
```
**Last Modified:** February/2018
