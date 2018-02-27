# Matrix One Norm

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** 'float oneMatrixNorm()'

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will find the one norm for a matrix.  It will sum up all of the values of each column of the matrix.

**Input:** The input must be a matrix from the Matrix class in **Appendix B**.

**Output:** This will output the maximum sum of all the columns of the matrix.

**Usage/Example:**  After creating a matrix call
```
double max = oneMatrixNorm(matrix);
```

**Implementation/Code:** The following is the code for 'float oneMatrixNorm()'.
```
float oneMatrixNorm(Matrix matrix)
	{
		double maxSum = 0.0f;
		double sum = 0.0f;

		for (unsigned int j = 0; j < matrix.getN(); j++)
		{
			for (unsigned int i = 0; i < matrix.getM(); i++)
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
