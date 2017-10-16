# Fourth Chapter: Parallelization using OpenMP

## What is paralelization ?

Parallelizing a code in FORTRAN can allow to gain much time. It is not too difficult but one needs to be careful.

## Using OpenMP

On easy way to parallelize is to use OpenMP. On Unix machines OpenMP is included \(if not go here\).

All the commands that refer to OpenMP must be preceeded by `!$`.

To use OpenMP you must first load the module in the files that will use OpenMP commands. For example

```fortran
program myprogram
  !$ use omp_lib
  implicit none
  real :: a
  some code here with parallelization (see below)
end program
```

When compiling with gfortran \(on Unix machines\), you will need to use a flag `-fopenmp`:

```
gfortran -fopenmp -o myexec myprogram.f90
```

## Do-loop with OpenMP

The most commonly use of OpenMP is in do-loop. Imagine you have a the following simple code:

```fortran
program myprogram
  implicit none
  real :: a(100)
  do i=1,100
    a(i) = 2*i
  end do
end program
```

In the above code, the loop computes something at each iteration, independently of previous iterations. This is the perfect environment to use parallilization with OpenMP. OpenMP will execute the computation of different iterations on different cores at the same time. Without OpenMP each iteration would have to be finished before the next one starts, i.e. it will all be computed sequenially. To compute using OpenMP, you can write:

```fortran
program myprogram
  !$ use omp_lib
  implicit none
  real :: a(100)
  !$omp parallel do
  do i=1,100
    a(i) = 2*i
  end do
  !$omp end parallel do
end program
```

This way, OpenMP will automatically choose the number of cores at disposal and send to each of them approximately the same number of tasks. Here by default the variable `a` is shared \(see below\).

You can know the number of threads by using the OpenMP subroutine `omp_get_num_threads()` \(returns an integer\) before entering the parallel region \(do-loop\). You can get the thread number by using `omp_get_thread_num()` inside the parallel region \(do-loop\).

Note that to break lines in an OpenMP instruction you need `,&` at the end of the line and `!$openmp&` at the beginning of the next line.

## Other loops with OpenMP

Important instructions in OpenMP are `single`\(where only one instance executes the code, for example to print something\), `critical`\(where only one instance at a time executes the code\) and `barrier`\(where all instances must meet before continuing the code\).

```fortran
program myprogram
!$ use omp_lib
implicit none
...
...
!$omp single
 print*, "this will only be printed one time"
!$omp end single

!$omp critical (nameofcriticalsection)
 print*, "this is gonna print one instance at a time"
!$omp end critical (nameofcriticalsection)

!$omp barrier

end program
```



## Private / Shared Variables with OpenMP

Note that each core \(thread\) will write its own value on the variables. It is therefore important to indicate if the variable is to be shared by each thread or not. If shared, each thread reads the value that has been potentially given by another thread. If private, each variable is duplicated in each thread at the beginning \(with no value assigned to it!\) and lives its own life. At the end of the parallel block, the variable has no value anymore.

The dummy integer of the loop is necessarily private \(no need to indicate it is private\).

Parameters cannot be declared as shared or private because their value cannot change. In some sense, they are necessarily shared.

An example of code using private and shared indicators \[code to be checked by running it\]:

> ```fortran
> program myprogram
>   !$ use omp_lib
>   implicit none
>   real, parameter : pi = 3.1416
>   real :: sharedvar = 2.0
>   real :: privatevar
>   real :: a(100)
>   !$omp parallel default(none) shared(sharedvar, a) private(privatevar) do
>   do i=1,100
>     $! privatevar = omp_get_thread_num()
>     a(i) = sharedvar*pi*i
>   end do
>   !$omp end parallel do
> end program
> ```

The `default(none)` indicates that all variables must be specified as either `shared` or `private`, except the dummy for the loop, `i` and the parameters, here `pi` \(I think - to check\).

## OpenMP with modules

Module variables can only be shared, unless you use a special trick. The trick is that you need to declare them as `threadprivate` in the module where they are defined. Note that you need to have the line `!$ use omp_lib` at the beginning of the module.

```fortran
module mymodule
  !$ use omp_lib
  implicit none
  real :: a
  !$ threadprivate(a)
end mymodule
```

## Caution

Do not use `print*`, when parallelizing. It causes crashes. Write your stuff in a file, using the critical command for example.

