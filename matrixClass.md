# Matix Class

[Math 5620 Software Manual](https://tannerwheeler.github.io/math5620/main)

**Routine Name:** class Matrix

**Author:** Tanner Wheeler

**Language:** C++. The code can be compiled using the cMake compiler.

**Description/Purpose:** This class will create a matrix in which you can initialize it personally or using the different functions.  It also initializes the 5-point stencil and 9-point stencil if needed.

**Input:** 
Matrix(std::vector<double> initializer) - turns a vector into an mx1 matrix.
Matrix(int M, int N, bool doLayout) - creates an mxn matrix. To initialize it yourself put true for the bool.
Matrix() - Creates a 5x5 hilbert matrix.
Matrix(int mesh) - Creates the 5 point stencil with the mesh.
Matrix(int mesh, bool point_9) - Creates the 9 point stencil with the mesh.  The bool does nothing.
Matrix(int M, int N) - Creates a tridiagonal matrix with a mxn matrix.

**Output:** No output only creates a matrix you can manipulate.

**Usage/Example:** You must include the file in your file.
```
#include "Matrix.hpp"
```
Choose the type of Matrix you want to initialize.  Here we will use the Hilbert Matrix.
```
Matrix myMatrix();
```
You can now use the functions how you need.

**Implementation/Code:** The following is the code for 
```
#ifndef _MATRIX_HPP_
#define _MATRIX_HPP_

#include <iostream>
#include <vector>
#include <iomanip>
#include <string>

class Matrix
{
public:

	//
	// This will initialize your matrix from a vector.
	//
	Matrix(std::vector<double> initializer) : M(initializer.size()), N(1)
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		for (unsigned int i = 0; i < M; i++)
		{
			layout[i][0] = initializer[i];
		}
	}
	
	//
	//Regular Matrix
	//
	Matrix(int M, int N, bool doLayout) : M(M), N(N) 
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		std::string typing;

		if (doLayout)
		{
			for (unsigned int i = 0; i < M; i++)
			{
				std::cout << "Row " << i + 1 << "-- " << std::endl;

				for (unsigned int j = 0; j < N; j++)
				{
					std::cout << "\tPlace " << j + 1 << ": ";
					std::cin >> typing;

					layout[i][j] = std::stod(typing);
				}
			}
		}
	}

	// Creates the hilbert matrix
	Matrix() : M(5), N(5)
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		for (unsigned int i = 0; i < M; i++)
		{
			for (unsigned int j = 0; j < N; j++)
			{
				double value = 1 / static_cast<double>(i + j + 1);
				layout[i][j] = value;
			}
		}
	}

	// Creates the hilbert matrix
	Matrix(int M, int N, int value) : M(M), N(N)
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		for (unsigned int i = 0; i < M; i++)
		{
			for (unsigned int j = 0; j < N; j++)
			{
				layout[i][j] = value;
			}
		}
	}


	// 5 point stencil matrix
	Matrix(int mesh) : M(mesh * mesh), N(mesh * mesh)
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		initDiagonal(-4);

		for (unsigned int i = 0; i < M - 1; i++)
		{
			if ((i + 1) < N && (i + 1) % mesh != 0)
			{
				layout[i][(i + 1)] = 1;
			}

			if ((i + mesh) < N)
			{
				layout[i][(i + mesh)] = 1;
			}
		}


		for (unsigned int i = 0; i < M - 1; i++)
		{
			if (i < N && (i + 1) % mesh != 0)
			{
				layout[(i + 1)][i] = 1;
			}

			if ((i + mesh) < M)
			{
				layout[(i + mesh)][i] = 1;
			}
		}

	}


	// 9 point stencil matrix
	Matrix(int mesh, bool point_9) : M(mesh * mesh), N(mesh * mesh)
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		initDiagonal(-20);

		for (unsigned int i = 0; i < M - 1; i++)
		{
			if ((i + 1) < N && (i + 1) % mesh != 0)
			{
				layout[i][(i + 1)] = 4;
			}

			if ((i + mesh) < N)
			{
				layout[i][(i + mesh)] = -4;
			}

			if ((i + mesh) < M && (i + mesh + 1) % mesh != 0)
			{
				layout[i + 1][i + mesh] = 1;
			}

			if ((i + mesh + 1) < N && (i + mesh + 1) % mesh != 0)
			{
				layout[i][i + mesh + 1] = 1;
			}
		}


		for (unsigned int i = 0; i < M - 1; i++)
		{
			if (i < N && (i + 1) % mesh != 0)
			{
				layout[(i + 1)][i] = 4;
			}

			if ((i + mesh) < M)
			{
				layout[(i + mesh)][i] = -4;
			}

			if ((i + mesh) < M && (i + mesh + 1) % mesh != 0)
			{
				layout[i + mesh][i + 1] = 1;
			}

			if ((i + mesh + 1) < M && (i + mesh + 1) % mesh != 0)
			{
				layout[i + mesh + 1][i] = 1;
			}
		}
	}


	
	//Creates a matrix with the -2 down the diagonal and 1 on the diagonals
	//above and below it.
	Matrix(int M, int N) : M(M), N(N)
	{
		std::vector<std::vector<double>> test(M, std::vector<double>(N));
		layout = test;

		initDiagonal(-2);
		initLowDiagonal(1);
		initUpDiagonal(1);
	}

	//
	// Copy constructor.
	//
	Matrix(const Matrix& error)
	{
		M = error.M;
		N = error.N;
		layout = error.layout;
	}


	//
	// Special Values of the class.  Probably should be private values.
	//
	int M;
	int N;

	int getM() { return M; }

	int getN() { return N; }

	std::vector<std::vector<double>> layout;

	//
	// Prints the Matrix.
	//
	void print()
	{
		for (unsigned int i = 0; i < M; i++)
		{
			std::cout << "|  ";
			for (unsigned int j = 0; j < N; j++)
			{
				std::cout << std::setw(7) << std::setprecision(4) << layout[i][j] << "  ";
			}
			std::cout << "|" << std::endl;
		}
		
		std::cout << "=======================================" << std::endl;
	}


	//
	// Initializes the Matrix's main diagonal
	//
	void initDiagonal(double d)
	{
		for (unsigned int i = 0; i < M; i++)
		{
			if (i < N)
			{
				layout[i][i] = d;
			}
		}
	}

	//
	// This initializes the matrix's diagonal above the main diagonal
	//
	void initUpDiagonal(double u)
	{
		for (unsigned int i = 0; i < M - 1; i++)
		{
			if ((i + 1) < N)
			{
				layout[i][(i + 1)] = u;
			}
		}
	}

	//
	// This initializes the matrix's diagonal below the main diagonal
	//
	void initLowDiagonal(double l)
	{
		for (unsigned int i = 0; i < M - 1; i++)
		{
			if (i < N)
			{
				layout[(i + 1)][i] = l;
			}
		}
	}

	Matrix operator*(const Matrix& rhs)
	{
		if (this->N == rhs.M)
		{
			Matrix matrix(this->M, rhs.N, false);

			for (int i = 0; i < this->M; i++)
			{
				for (int j = 0; j < rhs.N; j++)
				{
					double sum = 0.0f;
					for (int k = 0; k < this->N; k++)
					{
						sum += static_cast<double>(this->layout[i][k]) * static_cast<double>(rhs.layout[k][j]);
					}

					matrix.layout[i][j] = (double)sum;  // Got rid of [(double)i][(double)j]
				}
			}

			return matrix;
		}
		else
		{
			std::cout << "Dimensions aren't compatible.  Left hand matrix returned. No multiplication performed." << std::endl;

			return *this;
		}
	}


	Matrix operator*(const double& rhs) 
	{
		Matrix matrix(this->M, this->N, false);

		for (int i = 0; i < this->M; i++)
		{
			for (int j = 0; j < this->N; j++)
			{
				double mult = this->layout[i][j];
				mult *= rhs;
				matrix.layout[i][j] = mult;
			}
		}

		return matrix;
	}



	Matrix operator/(const double& rhs)
	{
		for (unsigned int i = 0; i < this->M; i++)
		{
			for (unsigned int j = 0; j < this->N; j++)
			{
				this->layout[i][j] /= rhs;
			}
		}

		return *this;
	}



	Matrix operator/(const Matrix& rhs)
	{
		if(rhs.M == 1 && rhs.N == 1)
		for (unsigned int i = 0; i < this->M; i++)
		{
			for (unsigned int j = 0; j < this->N; j++)
			{
				this->layout[i][j] /= rhs.layout[0][0];
			}
		}

		return *this;
	}




	Matrix operator+(const Matrix& rhs)
	{
		if (this->M == rhs.M && this->N == rhs.N)
		{
			Matrix matrix(this->M, this->N, false);

			for (unsigned int i = 0; i < M; i++)
			{
				for (unsigned int j = 0; j < N; j++)
				{
					matrix.layout[i][j] = ((double)this->layout[i][j] + (double)rhs.layout[i][j]);
				}
			}

			return matrix;
		}
		else
		{
			std::cout << "Dimensions aren't compatible. Left hand matrix returned. No addition performed." << std::endl;

			return *this;
		}
	}

	

	Matrix operator-(const Matrix& rhs)
	{
		if (this->M == rhs.M && this->N == rhs.N)
		{
			Matrix matrix(this->M, this->N, false);

			for (unsigned int i = 0; i < M; i++)
			{
				for (unsigned int j = 0; j < N; j++)
				{
					matrix.layout[i][j] = ((double)this->layout[i][j] - (double)rhs.layout[i][j]);
				}
			}

			return matrix;
		}
		else
		{
			std::cout << "Dimensions aren't compatible. Left hand matrix returned. No addition performed." << std::endl;

			return *this;
		}
	}

	

	Matrix transpose()
	{
		Matrix newMatrix(N, M, false);

		for (unsigned int i = 0; i < M; i++)
		{
			for (unsigned int j = 0; j < N; j++)
			{
				newMatrix.layout[j][i] = layout[i][j];
			}
		}

		return newMatrix;
	}



	bool operator!=(const Matrix& rhs)
	{
		if (this->M == rhs.M && this->N == rhs.N)
		{
			for (unsigned int i = 0; i < M; i++)
			{
				for (unsigned int j = 0; j < N; j++)
				{
					if(this->layout[i][j] != rhs.layout[i][j])
					{
						return true;
					}
				}
			}

			return false;
		}
		else
		{
			return true;
		}
	}




	bool operator==(const Matrix& rhs)
	{
		if (this->M == rhs.M && this->N == rhs.N)
		{
			for (unsigned int i = 0; i < M; i++)
			{
				for (unsigned int j = 0; j < N; j++)
				{
					if (this->layout[i][j] != rhs.layout[i][j])
					{
						return false;
					}
				}
			}

			return true;
		}
		else
		{
			return false;
		}
	}
	

	float infiMatrixNorm()
	{
		double maxSum = 0.0f;
		double sum = 0.0f;

		for (unsigned int i = 0; i < M; i++)
		{
			for (unsigned int j = 0; j < N; j++)
			{
				sum += layout[i][j];
			}

			if (sum > maxSum)
			{
				maxSum = sum;
			}
			
			sum = 0.0f;
		}

		return maxSum;
	}


	float oneMatrixNorm()
	{
		double maxSum = 0.0f;
		double sum = 0.0f;

		for (unsigned int j = 0; j < N; j++)
		{
			for (unsigned int i = 0; i < M; i++)
			{
				sum += layout[i][j];
			}

			if (sum > maxSum)
			{
				maxSum = sum;
			}

			sum = 0.0f;
		}

		return maxSum;
	}

};

#endif
```
**Last Modified:** February/2018
