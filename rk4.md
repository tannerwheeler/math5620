# Runge Kutta 4th Order Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** std::vector<double> rk4(Func f, double x0, double y0, double x1, double n)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method is the Runge Kutta 4th order iterative method.  This will iteratively find values of the solution with 5 steps.  First it will estimate a value for `k1`, then `k2` using `k1`, then `k3` using `k2`, and finally `k4` using `k3`.  Once all of these values have been found `U1` will be solved for using `k1`, `k2`, `k3`, and `k4`.  This will iteratively use the previous solutions for each preceeding solution.

**Input:** A function must be defined and implemented to be passed into this method.  An interval start `x0` and end `x1` must be passed into the function.  The function also needs an initial value for the solution `y0` and the change in t as the parameter `n`.

**Output:** This method will return a vector of all the `U1` solutions approximated during the iterations.  These will be the values of each step of the solution.  They will be in the order found.

**Usage/Example:**
Let's start by defining our function we want to pass into the method.
```
typedef double Func(double, double);

double rkf(double t, double y)
{
	return 1 * y;
}
```
This is the function `du/dt = u(t)`.

Suppose our interval is from 0 to 10, `y0 = 1`, and the time step equal to 1.
```
int main()
{
  std::vector<double> answers0 = rk4(rkf, 0, 1, 10, 1);
  return 0;
}
```
With this vector the user can then code a way to print out all of the values in the vector.  The output should be
```
1
2.7083333
7.3350694
19.865813
53.803244
145.71712
394.65053
1068.8452
2894.789
7840.0536
21233.479
```

**Implementation/Code:** The following is the code for rk4(Func f, double x0, double y0, double x1, double n)
```
std::vector<double> rk4(Func f, double x0, double y0, double x1, double n)
{
	std::vector<double> solutions;
	solutions.push_back(y0);
	double h = n;
	double k1;
	double k2;
	double k3;
	double k4;
	double U1;

	while (x0 < x1)
	{
		k1 = y0;
		k2 = y0 + 0.5 * h * f(x0 + h / 2, k1);
		k3 = y0 + 0.5 * h * f(x0 + h / 2, k2);
		k4 = y0 + h * f(x0 + h / 2, k3);

		U1 = y0 + (h / 6) * (f(x0, k1) + 2 * f(x0 + h / 2, k2) + 2 * f(x0 + h / 2, k3) + f(x0 + h, k4));

		solutions.push_back(U1);

		y0 = U1;
		x0 += h;
	}

	return solutions;
}
```
**Last Modified:** February/2018
