# Third Chapter: Full FORTRAN programming using modules

## What is a module?

A module is a way to store variables and functions/subroutines that are available everywhere in the program and modifiable from anywhere in the program.

## How to write a module

To store variables that must be accessible everywhere in a program, you need to create a file called (for example) ```mymodule.f90``` which would contains
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
Note the ```use mymodule``` at the begining of the program before the ```implicit none```. Because of this line, all the variables and functions/subroutines declared in the module can be used in the program.

One can also use ```use mymodule, only: variable/function/subroutine``` to make only part of the variables or functions available. For example
```
program myprogram
  use mymodule, only: functionInModule
  implicit none
  real :: w,z
  z = functionInModule
end program
```
Why would you want to do that?
