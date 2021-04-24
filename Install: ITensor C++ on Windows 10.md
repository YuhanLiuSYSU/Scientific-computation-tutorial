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
