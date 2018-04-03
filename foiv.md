# First Order Initial Value Problem

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** double foiv(double alpha, double sigma, double t)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This method will solve the differential equation `du/dt = sigma * u` given an initial value, alpha, at the point `t`.

**Input:** The user needs to enter the values for alpha, sigma, and t.

**Output:** This will output the solution of the initial value problem.

**Usage/Example:**
Suppose our equation was `du/dt = 2 * u` with alpha = 5 and at t = 2.
```
int main()
{
  double val = foiv(5, 2, 2);
  return 0;
}
```
The solution will be
```
val = 22026.5
```

**Implementation/Code:** The following is the code for `foiv(double alpha, double sigma, double t)`
```
double foiv(double alpha, double sigma, double t)
{
	return std::exp(t * alpha);
}
```
**Last Modified:** February/2018
