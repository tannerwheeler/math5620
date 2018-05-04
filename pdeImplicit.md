# Implicit Euler for PDE's

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** implicitPDE(double alpha, double a, double b, double u0, double x0, double xn, double dt, double dx)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** Unlike the Implicit Euler method for ODE's this will solve the Partial Differential Equation with time steps.  This can be used on equations like the heat equation.  It will use the jacobi method as its linear solver.  This uses the Matrix class documented in Appendix B.

**Input:** Alpha is the `a` from your PDE `u_t = a * u_xx`.  The x value range is `a` to `b`.  The initial value is u0.  For `u(x,t)`, `x0` is `u(x,a)` and `xn` is `u(x,b)`.  The change is time is `dt`.  The change in x is `dx`.  These are the parameters for the method.  They need to be entered in that order.

**Output:** The output of the method will be the solution to the PDE at a time step that you decide in the code.  This time step isn't a parameter, but need to be hard coded into the method.

**Usage/Example:**
Given our parameters as explained above and in the code comments.  We can call the function with the these parameters.

```
Matrix answer = implicitPDE(2, 0, 65, 20, 100, 25, 3, 13);
answer.print();
```
This will then print out 
```
|      100  |
|    38.86  |
|    23.12  |
|    20.56  |
|    21.06  |
|       25  |
```
In order for this method to converge `alpha * dt/dx^2 < 1/2`.

**Implementation/Code:** The following is the code for Matrix implicitPDE(double alpha, double a, double b, double u0, double x0, double xn, double dt, double dx)
```
// Alpha is from your PDE. u_t = a * u_xx
// x value range is a to b.  u0 is the initial value of the system.  x0 is u(x,a) and xn is u(x,b).
// dt is the change in t.  dx is the change in x.
Matrix implicitPDE(double alpha, double a, double b, double u0, double x0, double xn, double dt, double dx)
{
	int size = (b - a) / dx; // Determines the number of data points needed.
	std::vector<double> create(size + 1, u0);
	create[0] = x0;
	create[create.size() - 1] = xn;

	Matrix U0(create, false);
	Matrix U1 = U0;

	Matrix B(size + 1, size + 1, 0);
	B.initDiagonal(1);

	//B.print();

	Matrix A(size + 1, size + 1); // Create a tri diagonal matrix

	//A.print();

	double lambda = ((alpha * dt) / (dx * dx));

	B = B - (A * lambda);

	//B.print();
	//U0.print();
	while (a < 30) // Number of time steps decided here
	{
		U1 = jacobi(B, U0);

		// This resets the borders because 
		// they aren't supposed to change.
		U1.layout[0][0] = x0;
		U1.layout[size][0] = xn;

		U0 = U1;
		a += dt;
	}

	return U1;
}
```
**Last Modified:** February/2018
