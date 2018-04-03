# Explicit Euler Method (Vector Return)

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** expEulerV(Func f, double a, double y0, double b, double dt)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This is the Explicit Euler Method to determine the solution to a differential equation.

**Input:** This method needs to have a function implemented and defined passed into it.  The then take `a` the start of the interval, `y0` the value of the function when `t = 0`, `b` the end of the interval, and `dt` which is the number of changes in `t`.

**Output:** This will return a vector of double type values.  The size of the vector will depend on the length of the interval and the change of value size.

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
  std::vector<double> answers0 = expEulerV(fun, 0, 1, 10, 10);
  return 0;
}
```
With this vector the user can then code a way to print out all of the values in the vector.  The output should be
```
1
2
4
8
16
32
64
128
256
512
1024
2048
```


**Implementation/Code:** The following is the code for `std::vector<double> expEulerV(Func f, double a, double y0, double b, double dt)`
```
std::vector<double> expEulerV(Func f, double a, double y0, double b, double dt)
{
	std::vector<double> solutions;
	solutions.push_back(y0);

	double h = (b - a) / dt;

	while (a <= b)
	{
		y0 += h * f(a, y0);
		a += h;

		solutions.push_back(y0);
	}

	return solutions;
}
```
**Last Modified:** February/2018
