# Predictor Corrector Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** 
std::vector<double> predCorMethod(Func f, double x0, double y0, double x1, double n)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This function uses to methods to estimate the value of the solutions.  It starts with the Adams-Bashforth 4th order method that predicts the first three values given an initial value.  This value is then corrected by the Adams-Moulton 3rd order method.

**Input:** A function must be defined and implemented to be passed into this method.  An interval start `x0` and end `x1` must be passed into the function.  The function also needs an initial value for the solution `y0` and the change in step taken in the t values `n`.

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

Suppose our interval is from 0 to 10, `y0 = 1`, and time steps of 1.
```
int main()
{
  std::vector<double> answers0 = preCorMethod(rkf, 0, 1, 10, 1);
  return 0;
}
```
With this vector the user can then code a way to print out all of the values in the vector.  The output should be
```
1
2
4.5
10.875
28.921224
77.733626
208.6456
559.91094
1502.6124
4032.5373
10822.048
```

**Implementation/Code:** The following is the code for predCorMethod(Func f, double x0, double y0, double x1, double n)
```
std::vector<double> predCorMethod(Func f, double x0, double y0, double x1, double n)
{
	std::vector<double> solutions;
	double h = n;
	double U0 = y0;
	solutions.push_back(y0);
	x0 += h;
	double U1 = U0 + h * f(x0, U0);
	solutions.push_back(U1);
	x0 += h;
	double U2 = U1 + (h/2) * (-1*f(x0, U0) + 3*f(x0, U1));
	solutions.push_back(U2);
	x0 += h;
	double U3 = U2 + (h/12)*(5*f(x0, U0) - 16*f(x0, U1) + 23*f(x0, U2));
	solutions.push_back(U3);
	x0 += h;
	double U4;

	while (x0 <= x1)
	{
    		//Adams-Bashforth method used here and above
		U4 = U3 + (h / 24)*(-9 * f(x0, U0) + 37 * f(x0, U1) - 59 * f(x0, U2) + 55 * f(x0, U3));
		//Adams-Moulton method used here
		U4 = U3 + (h / 24)*(f(x0, U1) - 5 * f(x0, U2) + 19 * f(x0, U3) + 9 * f(x0, U4));

		solutions.push_back(U4);
		x0 += h;
		U0 = U1;
		U1 = U2;
		U2 = U3;
		U3 = U4;
	}

	return solutions;
}
```
**Last Modified:** February/2018
