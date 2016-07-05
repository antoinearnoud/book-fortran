# Third Chapter: Full FORTRAN programming using modules

## What's a module?

A module is a way to store variables and functions/subroutines that are available everywhere in the program and modifiable from anywhere in the program.

## How write a module

To store variables that must be accessible everywhere in a program, you need to create a file called (for example) ```mymodule.f90```.
```
module mymodule
  implicit none
  real :: a
  real :: b
  a = 5
  b = 6
  contains
  functionInModule(x,y)
    implicit none
    real :: x, y, functionInModule
    functionInModule = x-y
end module
```
And the main program becomes
```
program myprogram
  use mymodule
  implicit none
  real :: w, z
  some code here
  w = a + b
  z = functionInModule(w,w)
end program
```
  