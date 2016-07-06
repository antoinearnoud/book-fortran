# Fourth Chapter: Parallelization using OpenMP


## What is paralelization ?

Parallelizing a code in FORTRAN can allow to gain much time. It is not too difficult but one needs to be careful.

## Using OpenMP

On easy way to parallelize is to use OpenMP. On Unix machines OpenMP is included (if not go here).

To use OpenMP you must first load the module in the files that will use OpenMP command. For example
```
program myprogram
  use openmp
  implicit none
  real :: a
  some code here with parallelization (see below)
end program
```

When compiling with gfortran (on Unix machines), you will need to use a flag ```-fopenmp```:
```
gfortran -fopenmp -o myexec myprogram.f90
```

## Do-loop with OpenMP

The most commonly use of OpenMP is in do-loop. Imagine you have a the following simple code:
```
program myprogram
  implicit none
  real :: a(100)
  do i=1,100
    a(i) = 2*i
  end do
end program
```
In the above code, the loop that computes something at each iteration, independently of previous iterations. This is the perfect environment to use openmp. OpenMP will execute the computation of different iterations on different cores at the same time. Without OpenMP each iteration would have to been done before the next one starts. Instead of using this
You can use
```
program myprogram
  use omp_lib
  implicit none
  real :: a(100)
  !$omp parallel do
  do i=1,100
    a(i) = 2*i
  end do
  !$omp end parallel do
end program
```
This way, OpenMP will choose automatically the number of cores at disposal and send to each of them approximately the same number of tasks. Here by default the variable ```a``` is shared (see below).

You can know the number of threads by using the OpenMP subroutine ```omp_get_num_threads()``` (returns an integer) before entering the parallel region. You can get the thread number by using ```omp_get_thread_num()```.

Note that to break lines in an OpenMP instruction you need ```,&``` at the end of the line and ```!$openmp&``` at the beginning of the next line.

## Private / Shared Variables with OpenMP

Note that each core (thread) will write its own value on the variables. It is therefore important to indicate if the variable is to be shared by each thread or not. If shared, each thread reads the value that has been potentially given by another thread. If private, each variable is duplicated in each thread at the beginning (with no value assigned to it!) and lives its own life. At the end of the parallel block, the variable has no value anymore.

The dummy integer of the loop is necessarily private (no need to indicate it is private).

Parameters cannot be declared as shared or private because their value cannot change. In some sense, they are necessarily shared.

## OpenMP with modules

Module variables can only be shared, unless you use a special trick. The trick is that you need to declare them as ```threadprivate``` in the module where they are defined. Note that you need to ```use``` the ```openmp``` module.
```
mymodule
  !$ use omp_lib
  implicit none
  real :: a
  !$ threadprivate(a)
end mymodule
```

