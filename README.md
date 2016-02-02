# MLPACK_for_MSVC
The releases include MLPACK build using MSVC 2015. To build for other versions of MSVC, try the instructions below (keep in mind that older compilers may not work since MLPACK relies on some modern features)
Files for building MLPACK and it's dependencies using the Microsoft Visual Studio Compiler.
Instructions:
Build the following libraries:
  * OpenBLAS (optimized BLAS) (http://www.openblas.net/)
  * LAPACK (http://www.netlib.org/lapack/)
  * ARPACK (http://www.caam.rice.edu/software/ARPACK/)

To build the above, you will need a fortran compiler. I use GFortran from MinGW-w64 on Cygwin.

You can link ARPACK to LAPACK and OpenBLAS. Compile ARPACK and LAPACK as if you were on a Unix system 20 years ago. These instructions will help: http://www.recheliu.org/memo/buildarpackonwindowsforvisualstudio.

You can use CMake to configure OpenBLAS for Visual Studio.

You can use CMake to configure Armadillo for Visual Studio, but you should modify your config.hpp file before compiling and installing. Make sure to explicitly link the libraries in the armadillo project.

You can download the Boost libraries here: http://sourceforge.net/projects/boost/files/boost-binaries/1.60.0/

You will have to modify CMakeLists.txt to prevent an error declaring MSVC as non C++-11 compliant. The patched file is included in the repo.
You will have to modify any file containing OpenMP for loops, as MSVC 2015 supports OpenMP 2.5, which requires signed integer indices. GCC and Clang already support OpenMP 3.0 with unsigned indices. Replace "size_t" with "maxint_t".
For 2.0.0 only src/mlpack/methods/det/dt_utils.cpp needs this fix.
