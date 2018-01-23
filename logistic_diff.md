# Logistic Differential Equation

**Routine Name:**           Logistic Differential Equation

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

For example,

    gfortran smaceps.f

will produce an executable **./a.exe** than can be executed. If you want a different name, the following will work a bit
better

    gfortran -o smaceps smaceps.f

**Description/Purpose:** This function will compute the value of P(t) from the function dP/dt = alpha*P - beta*P^2.

**Input:** The values of alpha, beta, P_0 (P(t) when t = 0), and t.

**Output:** This calculates the value of P(t) given the expressed input.

**Usage/Example:**

The routine has two arguments needed to return the values of the precision in terms of the smallest number that can be
represented. Since the code is written in terms of a Fortran subroutine, the values of the machine machine epsilon and
the power of two that gives the machine epsilon. Due to implicit Fortran typing, the first argument is a single precision
value and the second is an integer.

      call smaceps(sval, ipow)
      print *, ipow, sval

Output from the lines above:

      24   5.96046448E-08

The first value (24) is the number of binary digits that define the machine epsilon and the second is related to the
decimal version of the same value. The number of decimal digits that can be represented is roughly eight (E-08 on the
end of the second value).

**Implementation/Code:** The following is the code for analytic_sol(double p_0, double alpha, double beta, double point_t)
- The main() function can be ignored if only the analytic_sol(...) function is used.

```
#include <iostream>
#include <cmath>


double numerator(double p_0, double alpha, double beta, double point_t)
{
	double top = p_0 / (alpha - (beta * p_0));

 	top *= alpha;

 	top *= exp(alpha * point_t);

 	return top;
}

double denominator(double p_0, double alpha, double beta, double point_t)
{
 	double bottom = p_0 / (alpha - (beta * p_0));

 	bottom *= beta;

 	bottom *= exp(alpha * point_t);

 	return bottom + 1;
}

double analytic_sol(double p_0, double alpha, double beta, double point_t)
{
 	double solution = 0.0;

	if (alpha == 0 && beta == 0)
 	{
    solution = p_0;
	}
  else if (alpha == 0 && beta != 0)
  {
  	solution = 1 / ((beta * point_t) + (1 / p_0));
  }
 	else if (alpha != 0 && beta == 0)
 	{
 		solution = (p_0 * exp(alpha * point_t));
 	}
 	else
 	{
 		solution = numerator(p_0, alpha, beta, point_t) / denominator(p_0, alpha, beta, point_t);
 	}
  
  return solution;
}


int main()
{
	double p_0 = 0.0f;
	double alpha = 0.0f;
	double beta = 0.0f;
	double point_t = 0.0f;

	std::cout << "Alpha = ";
	std::cin >> alpha;
	std::cout << std::endl;

	std::cout << "Beta = ";
	std::cin >> beta;
	std::cout << std::endl;

	std::cout << "P_0 = ";
	std::cin >> p_0;
	std::cout << std::endl;

	std::cout << "t = ";
	std::cin >> point_t;
	std::cout << std::endl;

	std::cout << "P(" << point_t << ") = " << analytic_sol(p_0, alpha, beta, point_t) << std::endl;

	return 0;
}
 ```
 
 **Last Modified:** January/2018
