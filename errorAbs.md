# Absolute Error

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Function Name:**           errorAbs(double ex, double exBar)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** Calling errorAbs(double ex, double exBar) will calculate the absolute value of the difference between the calculated value and the actual value.

**Input:** In order to find the absolute error you need to know x and x-bar.  These are the two input values for errorAbs(...).

**Output:** This function will return a double value of the calculated absolute error.  The function does not print this value out.

**Usage/Example:**
If we were given the values of x = 2 and x-bar = 2.5 we would call the function as:
```
errorAbs(2, 2.5)
```
This will return the value 0.5 to the function call.

**Implementation/Code:** The following is the code for smaceps()

```
double errorAbs(double ex, double exBar)
{
	double solution = 0.0f;

	solution = ex - exBar;

	if (solution < 0)
	{
		solution *= -1;
	}

	return solution;
}

int main()
{
	std::cout << errorAbs(2, 2.5) << std::endl;

	return 0;
}
```
**Last Modified:** January/2018
