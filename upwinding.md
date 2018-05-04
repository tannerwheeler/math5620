# Upwinding

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** upwinding(double alpha, double a, double b, double u0, double x0, double xn, double dt, double dx)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This performs upwinding for hyperbolic PDE's.  This uses the Matrix class documented in Appendix B.

**Input:** Alpha is the `a` from your PDE `u_t = a * u_xx`.  The x value range is `a` to `b`.  The initial value is u0.  For `u(x,t)`, `x0` is `u(x,a)` and `xn` is `u(x,b)`.  The change is time is `dt`.  The change in x is `dx`.  These are the parameters for the method.  They need to be entered in that order.

**Output:** The output of the method will be the solution to the PDE at a time step that you decide in the code.  This time step isn't a parameter, but need to be hard coded into the method.

**Usage/Example:**
Given our parameters as explained above and in the code comments.  We can call the function with the these parameters.
```
Matrix answer = upwinding(2, 0, 65, 20, 100, 25, 3, 13);
answer.print();
```
This will then print out 
```
|      100       20    20.49    19.75    13.16    3.903  |
```

**Implementation/Code:** The following is the code for Matrix upwinding(double alpha, double a, double b, double u0, double x0, double xn, double dt, double dx)
```
Matrix upwinding(double alpha, double a, double b, double u0, double x0, double xn, double dt, double dx)
{
	int size = (b - a) / dx; // Determines the number of data points needed.
	std::vector<double> create(size + 1, u0);
	create[0] = x0;
	create[create.size() - 1] = xn;

	Matrix U0(create, true); // Use the Matrix class in order to have 
							 // needed matrix operations.  Initialize it
							 // with the vector just created.
	Matrix U1 = U0;

	Matrix A(size + 1, size + 1, 0); // Create a matrix of all 0's
	A.initLowDiagonal(-1);
	A.initDiagonal(1);

	double lambda = ((alpha * dt) / (dx));

	double int_t = 0; // This is the initial value of t for u(x,t).
	double fin_t = 9; // This is the final value of t for u(x,t).

	while (int_t < fin_t)
	{
		U1 = U0 - (U0 * A * lambda);

		// This resets the border because 
		// it isn't supposed to change.
		U1.layout[0][0] = x0;

		U0 = U1;

		int_t += dt;
	}

	return U1;
}
```
**Last Modified:** February/2018
