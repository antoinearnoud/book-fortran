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

## Do-loop with OpenMP

The most commonly use of OpenMP is in do-loop. Imagine you have a loop that computes something at each iteration, independently of previous iterations. This is the perfect environment to use openmp. OpenMP will send the computation of different iterations at the same time on different cores instead of waiting that one iteration is done before starting the next one. Instead of using this
```
program myprogram
  implicit none
  real :: a(100)
  do i=1,100
    a(i) = 2*i
  end do
end program
```
You can use
```
program myprogram
  use openmp
  implicit none
  real :: a(100)
  !$omp parallel do
  do i=1,100
    a(i) = 2*i
  end do
  !$omp end parallel do
end program
```
This way, OpenMP will choose automatically the number of cores at disposal and send to each of them approximately the same number of tasks.

## Private / Shared Vairalbes with OpenMP

## OpenMP with modules