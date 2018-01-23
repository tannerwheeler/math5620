# Relative Error

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:**           errorRel(double ex, double exBar)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This function will caluclate the relative error between a calculated value and actual value.

**Input:** There are two inputs for this function.  You need to know x and x-bar.  x is your actual value and x-bar is your calculated value.

**Output:** This function does not print out the relative error, but returns it to the function call.

**Usage/Example:**
Give the values of x = 1000 and x-bar = 1000.1, we would call the function as:
```
errorRel(1000, 1000.1)
```
this would then return the value 9.9999e^-5 to the funciton call.

**Implementation/Code:** The following is the code for errorRel(double ex, double exBar)
```
double errorRel(double ex, double exBar)
{
	double solution = 0.0f;

	solution = ex - exBar;

	if (solution < 0)
	{
		solution *= -1;
	}

	if (exBar < 0)
	{
		solution /= (-1 * exBar);
	}
	else
	{
		solution /= exBar;
	}

	return solution;
}


int main()
{
	std::cout << errorRel(1000, 1000.1) << std::endl;

	return 0;
}
```
**Last Modified:** January/2018
