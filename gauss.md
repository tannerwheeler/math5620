# Gaussian Elimination

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** Matrix Gauss(Matrix a, Matrix b) 

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will take the equation Ax = b and solve for x using Gaussian Elimination.

**Input:** A matrix a and matrix b must be provided as input.  

**Output:** This will return the matrix x in the equation Ax = b.

**Usage/Example:** If I wanted to find the inverse of a matrix (if it exists). I would enter
```
matrix x = Gauss(a, b);
```
where b is the identity matrix.

**Implementation/Code:** The following is the code for 'Matrix Gauss(Matrix a, Matrix b)'
```
Matrix Gauss(Matrix a, Matrix b)
{
	Matrix clean(a.getM(), a.getN(), false);
	clean.initDiagonal(1);
	Matrix mult(a.getM(), a.getN(), false);
	mult.initDiagonal(1);

	
	for (int j = 0; j < a.getN() - 1; j++)
	{
		for (int i = j+1; i < a.getM(); i++)
		{
			mult.layout[i][j] = -1 * (a.layout[i][j] / a.layout[j][j]);
		}

		b = mult * b;
		a = mult * a;
		mult = clean;
	}

	for (int j = 0; j < a.getN(); j++)
	{
		for (int i = 0; i < j ; i++)
		{
			mult.layout[i][j] = -1 * (a.layout[i][j] / a.layout[j][j]);
		}

		b = mult * b;
		a = mult * a;
		mult = clean;
	}

	for (int i = 0; i < a.getM(); i++)
	{
		mult.layout[i][i] = 1 / a.layout[i][i];
	}

	b = mult * b;
	a = mult * a;

	//b.print();

	return b;
}
```
**Last Modified:** February/2018
