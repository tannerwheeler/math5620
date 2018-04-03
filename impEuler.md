# Implicit Euler Method
## Backward Euler Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** void impEuler(Func f, Func df, double y0, const double a, const double b, const double dt, const double tol)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method is to iteratively find the solutions to a differential equation.  It uses the backward Euler Method to accomplish this, with the Newton Method used to find the Implicit value.

**Input:** For this method you must have two functions defined and implemented.  These functions are the original function and the function's derivative.  You then need to pass in the inital condition of the function `y0`.  The starting `a` and ending `b` points of an interval should be past into the method.  You also establish a tolerance for the iterations here along with the number of steps in the interval.

**Output:** The output of this function is just a double value for the solution of the final step in the interval.

**Usage/Example:**
There are no examples as the code still needs some modifications.

**Implementation/Code:** The following is the code for impEuler(Func f, Func df, double y0, const double a, const double b, const double dt, const double tol)
```
double newtonMethod(Func f, Func df, double y0, const double a, const double b, const double dt, const double tol)
{
	int iter = 0;
	double x1 = 2.0f;
	double x0 = 2.0f;

	do
	{
		x0 = x1;
		x1 = x0 - (x0 - y0 - (dt*f(1, x0))) / (1 - (dt*df(1, x0)));

		iter++;
	  //std::cout << tol;
	} while (std::abs(x1 - x0) > tol && iter < 750);

	std::cout << std::endl << std::endl;
	return x1;
}



/*std::vector<double>*/void impEuler(Func f, Func df, double y0, const double a, const double b, const double dt, const double tol)
{
	std::vector<double> solutions;
	solutions.push_back(y0);

	int iter = 0;

	for (int i = a; i < b;)
	{
		i += dt;

		double next = newtonMethod(f, df, solutions[iter], a, b, dt, tol);
		solutions.push_back(next);

		//std::cout << next << std::endl << std::endl;

		iter++;
	}

	for (int i = 0; i < solutions.size(); i++)
	{
		std::cout << "y" << i << " = " << solutions[i] << std::endl;
	}
}
```
**Last Modified:** February/2018
