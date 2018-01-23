# Machine Epsilon

**Function Name:**           find_machine_epsilon<T>()

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** After choosing a data type desired in C++ this function will print the precision value that
can be represented on a computer.

**Input:** No input is needed, but you do however have to specify what data type you want to use in your code.  This
is a template.  It will find the machine epsilon for whatever data type you specify in the function call
find_machine_epsilon<_type here_>().

**Output:** This function returns a single precision value for the number of decimal digits that can be represented on the
computer with the data type specified.  The main function prints out this value.

**Usage/Example:** 
With this function all that must be specified is the data type of the function.  If we choose to use the data type _float_ as our data type we would call the function like:
```
find_machine_epsilon<float>();
```
If we would have chosen the data type _double_ we would have put:
```
find_machine_epsilon<double>();
```
In the case with the _double_ data type we would get a result of 
```
2.22045e-16
```
This is the precision that this machine can arrive at for _double_ s on this computer.

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
