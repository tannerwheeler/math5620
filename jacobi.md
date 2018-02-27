# Jacobi Iteration

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** Matrix jacobi(Matrix m, std::vector<double> bValues)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This function takes the given parameters as input and computes the analytic solutions of y(t) at any time t.

**Input:** You must pass into the function that is diagonally dominant. This can be created using the Matrix class in **Appendix B**.  You also need to pass in a vector with the results (b in the equation Ax=b).

**Output:** This will return the a Matrix equal to the x in the Ax=b linear equation.

**Usage/Example:** This code is used by passing in your desired matrix and conditions.  It can be called as:
```
Matrix xValues = jacobi(matrix, b);
```


**Implementation/Code:** The following is the code for 
```
Matrix jacobi(Matrix m, std::vector<double> bValues)
{
	Matrix l(m.getM(), m.getN(), false);
	Matrix u(m.getM(), m.getN(), false);

	l.initLowDiagonal(1);

	u.initUpDiagonal(1);

	std::vector<double> initd(m.getN(), -0.5);

	Matrix d(m.getM(), m.getN(), false);
	d.initDiagonal(-0.5)

	Matrix b(bValues);

	std::vector<double> initX(m.getN(), 0);
	
	Matrix exNott(initX);
	exNott.print();
	Matrix exOne = exNott;
  
  int time = 0;

	do
	{
	exNott = exOne;

	exOne = l;

	exOne = exOne + u;
	
	exOne = exOne * exNott;

	exOne = b - exOne;

	exOne = d * exOne;
  
  time++;

	} while (exOne != exNott && time < 500);

	return exOne;
}
```
**Last Modified:** February/2018
