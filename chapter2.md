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

To compile a program with modules or a library, see next chapters.

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
To call this function into the main program you would write altogether
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

In the definition of the function, the variables passed as argument are local: they can have the same name as variables in the main part (above ```contains```), this will not affect them. One can however  use variables defined above ```contains```inside the function, such as:

```
program myprogram
  implicit none
  real :: x1,x2,x3, easy_sum, big_number
  big_number = 1000
  easy_sum = myfunction(x1,x2,x3)
  
  contains
  function myfunction(a,b,c)
    implicit none
    real :: a,b,c, myfunction
    myfunction = a + b + c + bignumber
  end function
end program
```
In this example, ```easy_sum``` will be equal to ```1000 + x1 + x2 + x3```.

A subroutine is similar to a function but it does not return a variable. Instead, it executes the code inside it. Declaring a subroutine goes as follows
```
subroutine mysubroutine(a,b,c)
  implicit none
  real :: a, b, c
  a = a + b + c
  b = 0
  c = -1000
end subroutine
```
This subroutine will change the value of the three variables. You use a subroutine into your program with the following code:
```
program myprogram
  implicit none
  real :: x1,x2,x3, easy_sum
  call mysubroutine(x1,x2,x3)
  
  contains
  subroutine mysubroutine(a,b,c)
    implicit none
    real :: a, b, c
    a = a + b + c
    b = 0
    c = -1000
  end subroutine
end program
```

# More on functions and subroutines

In both function and subroutine, one can specify is the arguments of the function/subroutine are to be altered by using the keywords ```intent(in)```, ```intent(out)``` and ```intent(inout)```. ```intent(in)``` means that the variable should not be altered inside the function (input only). ```intent(out)``` means that whatever the value given to the variable before it enters the function as an argument, this value is ignored. With ```intent(inout)``` the variable can be altered and the value it has before entering the function is still assigned to it at the beginning of the function. For example
```
function myfunction(a,b,c)
  implicit none
  real, intent(in) :: b, c
  real :: myfunction
  real, intent(inout) :: a
  a = a + b + c
  myfunc = a
end function
```
 Note that you **should not** have an ```intet(out)``` before the return of the function (here ```myfunction```).
 
A function can also be a ```pure function```. This implies that the function will only change he behavior of the output (i.e. the variable ```myfunction``` above). It is a key word to be sure that nothing else is altered.
```
pure function myfunction(a,b,c)
  implicit none
  real, intent(in) :: b, c
  real :: myfunction
  real, intent(inout) :: a
  a = a + b + c
  myfunc = a + b + c
end function
```
 This will not work (check) because ```a``` is an argument of a pure function, but the function tries to modify it (one should change the ```intent(inout) :: a``` into ```intent(in) :: a``` as well as delete ```a = a + b + c```.

# Types and arrays, parameters

To declare an array (vector) ```a``` and a matrix ```b``` use
```
real :: a(5)
real :: b(5,4)
```
or, equivalently
```
real, dimension(5) :: a
real, dimension(5,4) :: b
```
The first way is convenient to declare arrays of different dimensions on the same line
```
real :: a(5), b(5,4)
```
You can also use the keyword ```p[arameter```. This means that the variable *cannot* change value. You must therefore initialize it at the same time you declare it.
```
real, parameter :: a = 5
real, dimension(5,4), parameter :: b = (5, 4, 3)
```
(check if this works)

# ```Save``` keyword, initialization-declaration

The keyword ```save``` is used to make a variable global (see next chapter). 
Another way to make a variable global is to assigns it a value at the same time as the declaration.
```
real, save :: a
real :: b =5
```

# Comments
To write a comment in FORTRAN just use ```!``` at the beginning of the sentence.

# Break lines

To break a line in FORTRAN, use ```&``` at the end of the line you want to break, and start the next line right below.
Isnt'it ```, &```?


