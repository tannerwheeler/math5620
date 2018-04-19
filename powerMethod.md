# Power Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** double findEigenvalues(Matrix matrix)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will perform an iteration either 750 times or until the results matrix hasn't changed since the last iteration.  The number of times the matrix iterates can be changed.

**Input:** You must enter a nxn matrix from the Matrix class in **Appendix B** (All operations of a matrix can be used with this class).  This method also uses the Matrix class during the computation.

**Output:** This will return the largest eigenvalue of the Matrix which can be used for the Matrix 2 Norm.

**Usage/Example:** If you were trying to find the Matrix 2 Norm on a matrix you could find the absolute value of
```
double max = findEigenvalues(matrix);

max = abs(max);
```

**Implementation/Code:** The following is the code for 'Matrix findEigenvalues(Matrix matrix)'
```
double findEigenvalues(Matrix matrix)
{
	std::vector<double> initStart(matrix.getN(), 1);
	std::vector<double> initEnd(matrix.getN(), 0);

	// Turn the vectors into matrix structure using the Matrix class.
	// This allows the use of all matrix operations needed.
	Matrix xStart(initStart);
	Matrix xEnd(initEnd);

	bool end = false;
	int times = 0;

	while (!end && times < 750)  // Change iterations here
	{
		xEnd = (matrix * xStart);
		xEnd = xEnd / xEnd.layout[matrix.M - 1][0]; // This will normalize the matrix vector.

		if (xEnd == xStart)
		{
			end = true;
		}
		else
		{
			xStart = xEnd;
		}

		// std::cout << "run" << times << std::endl;  // Uncomment to see progress as you run the code.

		times = times + 1;
	}

	// Use old matrix xStart instead of implementing a new matrix vector.
	// These three lines are the computation (A * x * x)/(x * x)
	xStart = matrix * xEnd;
	xStart = xStart.transpose() * xEnd;
	xStart = xStart / (xEnd.transpose() * xEnd);

	return xStart.layout[0][0];
}
```
**Last Modified:** February/2018
