# Conjugate Gradient Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** Matrix conjGrad(Matrix a, Matrix f, double tol)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method will perform the Conjugate Gradient method for the matrix `Ax = b`.  It will use the matrix class in Appendix B.  This will continue to iterate until `r1 < tolerance`.  

**Input:** You will need to pass into this method a matrix for `A` as the first parameter.  The second parameter is a matrix for `b`.  The last parameter is the tolerance that will help determine the number of iterations performed.

**Output:** This matrix will output the matrix `x` in `Ax = b`.

**Usage/Example:**
If you wanted to use a 5-point stencil, 4 by 4 matrix for A in `Ax = b`.  This is done below in the initialization 
`Matrix i1(size);`.
```
  int size = 4;
	double tol = 0.00000000000000000000001;
	Matrix i1(size);

	std::vector<double> bValues(size * size, 1);
	Matrix b = bValues;
  
	Matrix cg = conjGrad(i1, b, 0.00000000000000000000001);
	cg.print();
```
`std::vector<double> bValues(size * size, 1);
Matrix b = bValues;`

This initialization will create the matrix `b` in `Ax=b`.  After calling `conjGrad(i1, b)` `cg` is equal to `x`.
With `cg.print();` it prints the matrix `x` is equal to
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
Matrix conjGrad(Matrix a, Matrix f, double tol)
{
	std::vector<double> initX(a.getN(), 0);
	Matrix u0(initX);
	Matrix u1 = u0;

	Matrix r0 = f - (a * u0);
	Matrix r1 = r0;
	Matrix p0 = r0;
	Matrix p1 = p0;

	Matrix alpha = u0;
	Matrix beta = u0;
	Matrix w = u0;

	bool exit = false;
	int iter = 0;

	while (!exit && iter < 500)
	{
		w = a*p0;
		//w.print();

		alpha = (r0.transpose() * r0) / (p0.transpose() * w);
		//p0.print();
		//alpha.print();

		u1 = u0 + (p0 * alpha.layout[0][0]);
		//u1.print();


		r1 = r0 - (w * alpha.layout[0][0]);
		//r1.print();


		if (std::abs(r1.infiMatrixNorm()) < tol)
		{
			exit = true;
		}

		beta = (r1.transpose() * r1) / (r0.transpose() * r0);

		p1 = r1 + (p0 * beta.layout[0][0]);

		u0 = u1;
		p0 = p1;
		r0 = r1;
		
		iter++;
	}

	std::cout << iter << std::endl << std::endl;

	return u1;
}
```
**Last Modified:** February/2018
