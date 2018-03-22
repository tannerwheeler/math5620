# Jacobi Iteration

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** Matrix jacobi(Matrix m, std::vector<double> bValues)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This function takes the given parameters as input and computes the analytic solutions of y(t) at any time t.  This will continue to interate until the matrix converges.  If you want to set an iteration limit to the method it must be added.

**Input:** You must pass into the function a matrix that is diagonally dominant. This can be created using the Matrix class in **Appendix B**.  You also need to pass in a matrix with the results (b in the equation Ax=b).

**Output:** This will return a matrix equal to the x in the Ax=b linear equation.

**Usage/Example:** This code is used by passing in your desired matrix and conditions.  It can be called as:
```
Matrix xValues = jacobi(matrix, b);
```


**Implementation/Code:** The following is the code for 
```
Matrix jacobi(Matrix matrix, Matrix b)
{
	Matrix l(m.getM(), m.getN(), 0);
	Matrix u(m.getM(), m.getN(), 0);
	//Matrix d(m.getM(), m.getN, false);

	//std::vector<double> initd(m.getN(), -0.5);

	Matrix d(m.getM(), m.getN(), 0);

	splitULD(m, d, u, l);

	d.initDiagonal(1 / m.layout[0][0]);
	//d.print();

	Matrix b = bValues;
	//b.print();

	std::vector<double> initX(m.getN(), 0);

	//Matrix exOne(initX);
	Matrix exNott(initX);
	//exNott.print();
	Matrix exOne = exNott;

	int num = 0;

	do
	{
	exNott = exOne;

	exOne = l;

	exOne = exOne + u;
	//exOne.print();

	exOne = exOne * exNott;
	//exOne.print();

	exOne = b - exOne;
	//exOne.print();

	exOne = d * exOne;
	//exOne.print();

	num++;

	} while (exOne != exNott);
	//exOne = d * (b - (l + u) * exNott);

	std::cout << num << std::endl << std::endl;

	return exOne;
}
```
**Last Modified:** February/2018
