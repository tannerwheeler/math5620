# Implicit Euler Method
## Backward Euler Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** std::vector<double> impEuler(Func f, Func df, double a, double y0, double b, double dt)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method is to iteratively find the solutions to a differential equation.  It uses the backward Euler Method to accomplish this, with the Newton Method used to find the Implicit value.

**Input:** For this method you must have two functions defined and implemented.  These functions are the original function and the function's derivative.  You then need to pass in the inital condition of the function `y0`.  The starting `a` and ending `b` points of an interval should be past into the method.  You also establish a tolerance for the iterations here along with the number of steps in the interval.  The tolerance needs to be set in the newton method variable.  The size of the time steps `dt` is the last variable that needs to be passed into the function.

**Output:** The output of this function is a vector of double values for each time step.

**Usage/Example:**
Let's start by defining our function we want to pass into the method.
```
typedef double Func(double, double);

double fun(double t, double y)
{
	return 1 * y;
}
```
This is the function `du/dt = u(t)`.

Suppose our interval is from 0 to 10, `y0 = 1`, and the number of spaces equals 10.
```
int main()
{
	std::vector<double> answers1 = impEuler(rkf, drkf, 0, 1, 10, size);
	return 0;
}
```
With this vector the user can then code a way to print out ten values of the vector.  The output should be
```
1
2.86797
8.22526
23.5898
67.655
194.033
556.48
1595.97
4577.19
13127.3
```

**Implementation/Code:** The following is the code for impEuler(Func f, Func df, double a, double y0, double b, double dt)
```
double newtonMethod(Func f, Func df, double a, double y0, double h, double dt)
{
	double x1 = 1.0f;
	double x0 = 0.0f;
	double tol = 0.000000001;  // Set your tolerance here
	int iter = 0;

	while (x1 != x0 && std::abs(x1 - x0) > tol && iter < 10000)
	{
		x0 = x1;
		x1 = x0 - ((x0 - y0 - (h*f(a, x0))) / (1 - (h * df(a, x0))));

		iter++;
	}

	return x1;
}

std::vector<double> impEuler(Func f, Func df, double a, double y0, double b, double dt)
{
	std::vector<double> solutions;
	solutions.push_back(y0);

	double h = (b - a) / dt;  // This is just implementing the change in t.  
	h = (b - a) / h;	// It can be changed to h = dt.  This just helps me.

	while (a <= b)
	{
		y0 = newtonMethod(f, df, a, y0, h, dt);
		a += h;

		solutions.push_back(y0);
	}

	return solutions;
}
```
**Last Modified:** February/2018
