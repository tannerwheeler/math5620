# Machine Epsilon

**Function Name:**           find_machine_epsilon<T>()

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

For example,

    gfortran smaceps.f

will produce an executable **./a.exe** than can be executed. If you want a different name, the following will work a bit
better

    gfortran -o smaceps smaceps.f

**Description/Purpose:** After choosing a type of number desired in C++ this function will print the precision value that
can be represented on a computer.

**Input:** No input is needed, but you do however have to specify what type of number you want to use in your code.  This
is a template.  It will find the machine epsilon for whatever type of number you specify in the function call
find_machine_epsilon<_type here_>().

**Output:** This function returns a single precision value for the number of decimal digits that can be represented on the
computer with the digit type specified.  The main function prints out this value.

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

**Implementation/Code:** The following is the code for smaceps()

```
template <class T>
T find_machine_epsilon()
{	
	return std::numeric_limits<T>::epsilon();
}

int main()
{
	std::cout << find_machine_epsilon<float>() << std::endl;

	return 0;
}

```

**Last Modified:** September/2017
