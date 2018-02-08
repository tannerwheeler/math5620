# LU Factorization

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** LUFactorization()

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** To calculate the values of a linear system of equations using LU Factorization.

**Input:** You do not need input for this method.

**Output:** The console will not print anything from this function, but a vector of type doubles will be returned.

**Usage/Example:**
To implement this code you will want to include it inside of the [class Init](https://tannerwheeler.github.io/math5620/init).  After
calling the function through
```
LUFactorization();
```
you will be given a vector of type double values.

**Implementation/Code:** The following is the code for LUFactorization()
```
	std::vector<double> LUFactorization()
	{
		std::vector<double> ld;
		for (unsigned int i = 0; i < n - 1; i++)
		{
			ld.push_back(1);
		}

		std::vector<double> ll;
		std::vector<double> ud;
		std::vector<double> uu;

		uu = upper;

		ud.push_back(diagonal[0]);

		for (unsigned int i = 1; i < n - 1; i++)
		{
			ll.push_back(lower[i-1] / ud[i - 1]);
			ud.push_back(diagonal[i] - (ll[i-1] * uu[i - 1]));
		}

		std::vector<double> y;

		y.push_back(base[0]);
		for (unsigned int i = 1; i < n - 1; i++)
		{
			y.push_back(base[i] - (ll[i-1] * y[i - 1]));
		}

		for (unsigned int i = 0; i < y.size(); i++)
		{
			std::cout << y[i] << std::endl;
		}

		std::vector<double> u;

		for (unsigned int i = 0; i < n - 1; i++)
		{
			u.push_back(0);
		}

		u[n - 2] = y[n - 2] / ud[n - 2];
		for (int i = n - 3; i >= 0; i--)
		{
			u[i] = (y[i] - (uu[i] * u[i + 1])) / uu[i];
		}

		return u;
	}
```
**Last Modified:** February/2018
