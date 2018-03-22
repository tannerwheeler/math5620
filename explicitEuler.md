# Explicit Euler Method

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** void expEuler(Func f, double y0, double a, double b, double h)

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** 

**Input:** This method will need five inputs.  The first is a function that must be declared.  An example of this is shown in the implementation/code section below with the `typedef double Func(double)`.  The second parameter is the initial value at `y(0) = y0`.  Third is the initial input to the function.  Fourth is where the input values end.  It will iterate until `a > b`.  The last is the amount that `a` will increase by.

**Output:** This will not return any values from the method.  This will print out each step as it is iterated through the method, `ex: 12: 2355` where the first value is the step and the second is the output.

**Usage/Example:**
If you had the function `f(x0=) = x^2`, you can define it as
```
typedef double Func(double);

double func(double y)
{
  return std::sin(y);
}
```
In the main function you can call the method as

```
int main()
{
	expEuler(func, 1, 1, 5, .5);

  return 0;
}
```


The values printed will be:

```
1.000:  1.000
1.500:  1.421
2.000:  1.915
2.500:  2.386
3.000:  2.729
3.500:  2.929
4.000:  3.035
4.500:  3.088
5.000:  3.115
```

**Implementation/Code:** The following is the code for `void expEuler(Func f, double y0, double a, double b, double h)`
```
typedef double Func(double);

double func(double y)
{
	return std::sin(y);
}



void expEuler(Func f, double y0, double a, double b, double h)
{
	while (a <= b)
	{
		std::cout << std::fixed << std::setprecision(3) << a << ":  " << y0 << std::endl;

		y0 += h * f(y0);
		a += h;
	}
}
```
**Last Modified:** February/2018
