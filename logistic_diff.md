# Logistic Differential Equation

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Function Name:** double logistic(double alpha, double beta, double gamma, double t)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This function will compute the value of `P(t)` from the function `dP/dt = gamma*P - beta*P^2`.

**Input:** You need to input the values for alpha(`P(0)`), gamma, beta, and the value `t`.

**Output:** This calculates the value of P(t) given the expressed input.  This only will return a decimal value to the function call.

**Usage/Example:**
With an initial value alpha = 4, beta = 1, gamma = 2, and t = 5.
```
int main()
{
	double val = logistic(4, 1, 2, 5);
	return 0;
}
```
This will then return the value
```
val = 2.00005
```

**Implementation/Code:** logistic(double alpha, double beta, double gamma, double t)
```
double logistic(double alpha, double beta, double gamma, double t)
{
	if (beta == 0)
	{
		return foiv(alpha, gamma, t);
	}
	else if (gamma == 0)
	{
		return 1 / ((beta * t) + (1 / alpha));
	}
	else
	{
		return (alpha * gamma * exp(gamma * t)) / (gamma + (alpha * beta * (exp(gamma * t) - 1)));
	}
}
 ```
 
 **Last Modified:** January/2018
