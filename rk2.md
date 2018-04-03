# Runge Kutta 2nd Order Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** rk2(Func f, double x0, double y0, double x1, double n)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method is the Runge Kutta 2nd order iterative method.  This will iteratively find values of the solution with two steps.  First it will estimate a value for `U*` and then apporximate the solution from that value.  This will iteratively use the previous solutions.

**Input:** A function must be defined and implemented to be passed into this method.  An interval start `x0` and end `x1` must be passed into the function.  The function also needs an initial value for the solution `y0` and the number of steps taken in the interval `n`.

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

Suppose our interval is from 0 to 10, `y0 = 1`, and the number of spaces equals 10.
```
int main()
{
  std::vector<double> answers0 = rk2(rkf, 0, 1, 10, 10);
  return 0;
}
```
With this vector the user can then code a way to print out all of the values in the vector.  The output should be
```
1
2.5
6.25
15.625
39.0625
97.65625
244.14063
610.35156
1525.8789
3814.6973
9536.7432
```

**Implementation/Code:** The following is the code for rk2(Func f, double x0, double y0, double x1, double n)
```
std::vector<double> rk2(Func f, double x0, double y0, double x1, double n)
{
	std::vector<double> solutions;
	solutions.push_back(y0);
	double h = (x1 - x0) / n;
	double Ustar;
	double U1;
	
	while (x0 < x1)
	{
		Ustar = y0 + 0.5 * h * f(x0, y0);
		U1 = y0 + h * f(x0 + h / 2, Ustar);

		solutions.push_back(U1);
		y0 = U1;
		x0 += h;
	}

	return solutions;
}
```
**Last Modified:** February/2018
