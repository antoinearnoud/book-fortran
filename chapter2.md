# Second Chapter: Simple programming in FORTRAN

FORTRAN is a bit different from Matalab. It is a low level language. Concretely this means that the steps needed to run some code are distinct:
1. writing the code
2. compiling the code
3. executing the code

## How to start
### 1. Writing the code

To write the code use any text editor. It might be more convenient to use an editor specialized in FORTRAN such as Atom. In Atom the syntax is colored according to FORTRAN conventions. You can for example use Atom. Open a file and call it```myprogram.f90```. That's your *main* file. It has the following structure.

```
program main
  the code here
end program
```
You do not need to call the program```main```. You can also call it ```myprogram``` or any other name, as long as the file starts with```program``` and ends with ends with```end program```.

The ```the code here``` part is some FORTRAN code that we will cover later. For now, note that the code must be *closed* meaning that the whole structure must be consistent. In this case it means that we start with a key word ```program``` and ends with the key words ```end program```. This is different from Matlab where your code might only contains something like
```
a = 3
b = 2
c = a + b
```

### 2. Compiling the code

To compile the code one needs a compiler (see Chapter 1). On Unix machine, open the terminal and type
```
gfortran myprogram.f90
```
This will produce a new file (an executable). By default the new file is called ```a```. You can change this to give the file a more convenient name, for example ```myprog_exec``` using
```
gfortran -o myprogr_exe myprogramf90
```
This tells the compiler to call the output file ```myprog_exe```. It uses the *flag* (or option) ```-o``` followed by the argument to this flag. You can use any name you want for the executable file.

### 3. Executing the code

It is only when executing the file that the code will be executed and the computations run. To execute the file type in the 
```
./a
```
Or, if you used the ```-o``` flag:
```
./myprog_exe
```
## Declaring variables

You need to declare all the variables you will use. For example, putting together the code written above:
```
program myprogram
  implicit none
  real :: a, b, c
  the code here
end program
```
The key words ```implicit none``` means that you want all the variables used to be first declared. Hence if in the ```the code here``` part you use other letters, such that ```d```, the code will return an error when you try to compile it. It is possible no to use ```implicit none```, which allows you to use variables not declared, but you should *never* to this (mostly because then the variables have some default types). Note that here we declared the variables as ```real```. There are other types, and the most usual are
```
integer
double
character
```
The type ```character``` is for strings.

## Functions and Subroutines

In FORTRAN you can use two types of blocs of code which you provide with input: the function and the subroutine. Consider these two as quite similar. The function is defined as follows:
```
function myfunction(a,b,c)
  implicit none
  real :: a,b,c, myfunction
  the code here
end function
```
As you can see, one needs to declare all the variables that are passed as arguments (here ```a```, ```b``` and ```c```) as well as the output variable which *has the same name as the function*. For example, the function could do
```
function myfunction(a,b,c)
  implicit none
  real :: a,b,c, myfunction
  myfunction = a + b + c
end function
```
To call this function into the main program you would write alltogether
```
program myprogram
  implicit none
  real :: x1,x2,x3, easy_sum
  easy_sum = myfunction(x1,x2,x3)
  
  contains
  function myfunction(a,b,c)
    implicit none
    real :: a,b,c, myfunction
    myfunction = a + b + c
  end function
end program
```
The key word ```contains``` tells the compiler that the code following this key word contains the definitions of functions and subroutines. 

In the definition of the function, if you used as an argument a variable that has already been defined (such as ```x1```, ```x2``` or ```x3```), the variable should still be re-declared in the function. True?