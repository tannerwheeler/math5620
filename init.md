# Initializing an Elliptic Ordinary Differential Equation

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** Init(double a, double b, double u_a, double u_b, int nv)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This class constructor will initialize the arrays of data that you need in order to solve the DE. 

**Input:** You need to include a value for a, b, u_a, u_b, and n in 
```
Init(double a, double b, double u_a, double u_b, int nv).
```

**Output:** There is no output.  However you can call the print function ```print()``` to see what your data looks like.

**Usage/Example:**
In order to use this class you must add
```
#include "Init.hpp"
```
to your .cpp file.  In order to call and use this class you write:
```
Init <variable_name_here>(0, 0, 2.5, 5, 100)
```
this will create your class with these specific parameters.  In order to change the function that is used in the code you must manually
rewrite what you want the code to compute in the function method.

**Implementation/Code:** The following is the code for 
```
#include <iostream>
#include <vector>

class Init
{
public:

	Init(double a, double b, double u_a, double u_b, int nv)
	{
		h = (b - a) / nv;
		n = (double)nv;
		std::cout << h << std::endl;

		for (unsigned int i = 0; i < n - 1; i++)
		{
			diagonal.push_back(-2);
		}

		for (unsigned int i = 0; i < n - 2; i++)
		{
			upper.push_back(1);
			lower.push_back(1);
		}

		base.push_back((h*h) * function(1) - u_a);
		for (unsigned int i = 1; i < n - 2; i++)
		{
			base.push_back((h*h) * function(i + 1));
		}
		base.push_back((h*h) * function(n - 1) - u_b);

		print();
	}


	std::vector<double> diagonal;
	std::vector<double> upper;
	std::vector<double> lower;
	std::vector<double> base;
	double h;
	double n;

	double function(double x)
	{
		//
		//
		// Write your function here.
		//
		//

		return std::sin(3.141592653589793238 * x);
	}

	void print()
	{
		for (unsigned int i = 0; i < diagonal.size(); i++)
		{
			std::cout << "|  " << diagonal[i] << "  |" << std::endl;
		}

		std::cout << "====================" << std::endl;

		for (unsigned int i = 0; i < upper.size(); i++)
		{
			std::cout << "|  " << upper[i] << "  |" << std::endl;
		}

		std::cout << "====================" << std::endl;

		for (unsigned int i = 0; i < lower.size(); i++)
		{
			std::cout << "|  " << lower[i] << "  |" << std::endl;
		}

		std::cout << "====================" << std::endl;

		for (unsigned int i = 0; i < base.size(); i++)
		{
			std::cout << "|  " << base[i] << "  |" << std::endl;
		}

		std::cout << "====================" << std::endl;
	}
};
```
**Last Modified:** February/2018
