# Split into L - D - U

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** void splitULD(const Matrix& a, Matrix& d, Matrix& u, Matrix& l)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method is for the for purpose of splitting any matrix into three different parts.  It will take the lower triangular values of the matrix and create a lower triangular matrix.  It will do the same with the upper triangular matrix values and diagonal values.  This is not calculating the LU decomposition it is only splitting the parts of a matrix into three different matrices. This is compatible with the matrix class in Appendix B.

**Input:** You must pass into this function the matrix for which you want the L, D, and U matrices.  The next three matrices need to be matrices with the same dimesions of the first parameter matrix.  These are passed in by reference in the order D, U, and L.

**Output:** This matrix will not print anything to the screen nor will it return anything.  Because the last three values are passed by reference you will have the D, U, and L matrices as they have been modified in the method.

**Usage/Example:**
Suppose you wanted to split the matrix `A` =
```
|1  2  3|
|4  5  6|
|7  8  9|
```
you would then need three 0 matrices with the same dimensions. `D, U, L` =
```
|0  0  0|
|0  0  0|
|0  0  0|
```
You can then pass these into the function.
```
splitULD(A, D, U, L);
```
After this call `A` didn't change, but `D` =
```
|1  0  0|
|0  5  0|
|0  0  9|
```
And `U` =
```
|0  2  3|
|0  0  6|
|0  0  0|
```
And `L` =
```
|0  0  0|
|4  0  0|
|7  8  9|
```


**Implementation/Code:** The following is the code for 
```
void splitULD(const Matrix& a, Matrix& d, Matrix& u, Matrix& l)
{
	for (int i = 0; i < a.M; i++)
	{
		for (int j = 0; j < a.N; j++)
		{
			if (i > j)
			{
				l.layout[i][j] = a.layout[i][j];
			}
		}
	}

	//l.print();

	for (int i = 0; i < a.M; i++)
	{
		for (int j = 0; j < a.N; j++)
		{
			if (j > i)
			{
				u.layout[i][j] = a.layout[i][j];
			}
		}
	}

	//u.print();

	for (int i = 0; i < a.M; i++)
	{
		d.layout[i][i] = a.layout[i][i];
	}

	//d.print();
}
```
**Last Modified:** February/2018
