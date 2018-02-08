# 2 Norm

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** twoNorm(std::vector<double> computed, std::vector<double> exact)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This will compute the value of the 2 norm for you computed output.

**Input:** You need to include as parameters a vector of your computed values and a vector of your exact values.  This function can be
changed to only need one vector of the differences of the computed and exact values.

**Output:** Returns the 2 norm. However, if there wrong input was given it will give you a -1 as the norm siganlling an error.

**Usage/Example:**
You must include your two vectors and call the function.
```
double norm = twoNorm(computed, exact);
```

**Implementation/Code:** The following is the code for twoNorm(std::vector<double> computed, std::vector<double> exact)
```
double twoNorm(std::vector<double> computed, std::vector<double> exact)
	{
		double sum = -1.0;
		if (computed.size() == exact.size())
		{
			for (unsigned int i = 0; i < computed.size(); i++)
			{
				double value = computed[i] - exact[i];
				if (value < 0)
				{
					value *= -1;
				}

				sum += pow(value, 2);
			}

			sum = sqrt(sum);

			return sum;
		}
		else
		{
			return sum;
		}
	}
```
**Last Modified:** February/2018
