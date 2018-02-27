# Matrix Infinity Norm

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** float infiMatrixNorm(Matrix matrix)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will find the infinity norm of a matrix.

**Input:** You can pass in a matrix from the Matrix Class in **Appendix B**.

**Output:** This will return the maximum of the sum of all the rows in the matrix.

**Usage/Example:** After creating a matrix call
```
double infiMatrixNorm(matrix);
```

**Implementation/Code:** The following is the code for 'float infiMatrixNorm(Matrix matrix)'.
```
double infiMatrixNorm(Matrix matrix)
	{
		double maxSum = 0.0f;
		double sum = 0.0f;

		for (unsigned int i = 0; i < matrix.getM(); i++)
		{
			for (unsigned int j = 0; j < matrix.getN(); j++)
			{
				sum += matrix.layout[i][j];
			}

			if (sum > maxSum)
			{
				maxSum = sum;
			}
			
			sum = 0.0f;
		}

		return maxSum;
	}
```
**Last Modified:** February/2018
