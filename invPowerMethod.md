# Inverse Power Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** double findInverseEigenvalue(Matrix matrix)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** After receiving a matrix it will find the inverse of it and then take then perform the power method.  This will perform an iteration either 750 times or until the results matrix hasn't changed since the last iteration.  The number of times the matrix iterates can be changed.

**Input:** You must enter a nxn matrix from the Matrix class in **Appendix B**.  This method also uses the Matrix class during the computation.

**Output:** This will return 1 divided by the smallest eigenvalue of the Matrix which can be used for the Inverse Matrix 2 Norm.

**Usage/Example:** If you were trying to find the Inverse Matrix 2 Norm on a matrix you could find the absolute value of
```
double max = findEigenvalues(matrix);

max = abs(max);
```

**Implementation/Code:** The following is the code for 'double findInverseEigenvalue(Matrix matrix)'
```
double findInverseEigenvalue(Matrix imatrix)
{
  Matrix identity(imatrix.getM(), imatrix.getN(), false);
  identity.initDiagonal(1);
  Matrix matrix = Gauss(imatrix, identity);
	std::vector<double> initStart(matrix.getN(), 1);
	std::vector<double> initEnd(matrix.getN(), 0);

	Matrix xStart(initStart);
	Matrix xEnd(initEnd);

	bool end = false;
	int times = 0;

	std::cout << "init 2" << std::endl;

	while (!end && times < 750)
	{
		xEnd = (matrix * xStart);// / (xStart.transpose() * xStart);
		xEnd = xEnd / xEnd.layout[matrix.M - 1][0];

		if (xEnd == xStart)
		{
			end = true;
		}
		else
		{
			xStart = xEnd;
		}

		std::cout << "run" << times << std::endl;

		times = times + 1;
	}

	std::cout << "init 3" << std::endl;

	xStart = matrix * xEnd;
	xStart = xStart.transpose() * xEnd;
	xStart = xStart / (xEnd.transpose() * xEnd);

	return xStart.layout[0][0];
}
```
**Last Modified:** February/2018
