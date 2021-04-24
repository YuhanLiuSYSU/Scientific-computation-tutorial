**Ingredients: Windows 10 + Cygwin + ITensor + Eclipse**

### Short introduction
[ITensor](https://itensor.org/) is a powerful package for tensor network computation. It offers Julia and C++ versions. Here are some helpful(?) tips if you want to install C++ version on Windows 10 and decide not to use a virtual machine, and are new to programming. 

## Installation note
Windows system with Cygwin. Use:
```
CCCOM=g++ -std=c++17 -Wa,-mbig-obj -O2 -fPIC

PLATFORM=lapack
BLAS_LAPACK_LIBFLAGS=-lpthread -L/usr/lib -lblas -llapack 
```
(We can open the Cygwin terminal and see what is in /usr/lib. It is actually `C:\cygwin64\lib`)

### Bug one
In the Makefile in itensor folder, replace `@echo "THIS_DIR=$(PWD)"` by
```
@echo "THIS_DIR=$(shell pwd)"
```

### Bug two
In the `algs.cc` in `itensor\tensor`, replace `_N` and `_Rrows` by names that don't contain underscore. The error is
```
In file included from /usr/lib/gcc/x86_64-pc-cygwin/10/include/c++/cctype:42,
                 from /usr/lib/gcc/x86_64-pc-cygwin/10/include/c++/bits/localefwd.h:42,
                 from /usr/lib/gcc/x86_64-pc-cygwin/10/include/c++/string:43,
                 from /usr/lib/gcc/x86_64-pc-cygwin/10/include/c++/stdexcept:39,
                 from tensor/algs.cc:17:
tensor/algs.cc: In function 'int itensor::detail::hermitianDiag(int, itensor::Real*, itensor::Real*)':
tensor/algs.cc:37:20: error: expected unqualified-id before numeric constant
   37 |         LAPACK_INT _N = N;
      |                    ^~
```

#### minor bug
Need to add `C:\cygwin64\lib\lapack` to system path separately. Otherwise the file `dmrg.exe` cannot be executed.

## Work with Eclipse
1. Create a [new makefile c++ project](https://mcuoneclipse.com/2017/07/22/tutorial-makefile-projects-with-eclipse/) with eclipse.
2. [Import resources from file system](https://help.eclipse.org/2021-03/index.jsp?topic=%2Forg.eclipse.cdt.doc.user%2Fgetting_started%2Fcdt_w_existing_code.htm&cp=13_1_8). It makes a copy of the files that you wish to import to your assigned folder of the new project.
3. In Eclipse, go to `Project-> Build targets -> Create`. If you only want to build `dmrg.cc` file, change the `build command` from `make` to `make dmrg`
4. Build your newly created target. When it is done, you should see a `dmrg.exe` file in the `sample` folder.
5. Run the `dmrg.exe` file.
6. Tada!

-- Yuhan Liu
