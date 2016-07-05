# Fourth Chapter: Parallelization using OpenMP


## What is paralelization ?

Parallelizing a code in fortran allows sometimes to gain much high time. It is not too difficult but one needs to be careful.

## Using OpenMP

On easy way to parallelize is to use OpenMP. On Unix machines OpenMP is included (if not go here).

To use OpenMP you must first load the module in the files that will use OpenMP command. 
```
program myprogram
  use openmp
  implicit none
  real :: a
  some code here with parallelization
end program
```