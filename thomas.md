# Thomas Algorithm

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** thomas()

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will use the Thomas algorithm to solve the System of linear equations given the input provided to the class Init.

**Input:** There is no input needed for this function.

**Output:** This return a vector of type double values.  These values will not be printed to the console.

**Usage/Example:**
This function is to be used inside of the [class Init](https://tannerwheeler.github.io/math5620/init).  After creating and Init class you can then call the function by
```
<Init_class_name>.thomas();
```

**Implementation/Code:** The following is the code for std::vector<double> thomas()
```
std::vector<double> thomas()
	{
		std::vector<double> gamma;
		std::vector<double> beta;

		gamma.push_back(upper[0]/diagonal[0]);
		beta.push_back(base[0]/diagonal[0]);

		for (unsigned int i = 1; i < n - 2; i++)
		{
			gamma.push_back(upper[i] / (diagonal[i] + (gamma[i-1]*lower[i-1])));// changed - to +
			beta.push_back((base[i]-(beta[i-1]*lower[i-1]))/(diagonal[i]+(gamma[i-1]*lower[i-1])));
		}

		beta.push_back((base[n-2]-(beta[n-3]*lower[n-3])) / (diagonal[n-2] + (gamma[n-3] * lower[n-3])));

		std::vector<double> f;

		for (unsigned int t = 0; t < n - 1; t++)
		{
			f.push_back(0);
		}

		f[n - 2] = beta[n-2]; ///////
		for (int i = n - 3; i >= 0; i--)
		{
			f[i] = beta[i] + gamma[i] * f[i + 1];// changed - to +
		}

		return f;
	}
```
**Last Modified:** February/2018
