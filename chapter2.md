# Simple code in FORTRAN

FORTRAN is a bit different from, say, Matalab. It is a low level language. Concretely this means that the steps needed to run some code are distinct:  
1. writing the code  
2. compiling the code  
3. executing the code

## How to start

### 1. Writing the code

To write the code use any text editor. It might be more convenient to use an editor specialized in FORTRAN such as _Atom _\(from _Github\)_ or _SublimeText_. In these editors the syntax is colored according to FORTRAN conventions.

To start writing code, create a new a file and call it`myprogram.f90`. That's your _main_ file. It has the following structure.

```fortran
program main
  the code here
end program
```

You do not need to call the program`main`. You can also call it `myprogram` or any other name, as long as the file starts with`program` and ends with`end program`.

The `the code here` part is some FORTRAN code that we will cover later. For now, note that the code must be _closed,_ meaning that the whole structure must be consistent. In this case it means that we start with a keyword `program` and ends with the keywords `end program`. This is different from Matlab where your code might only contains something like

```
a = 3
b = 2
c = a + b
```

### 2. Compiling the code

To compile the code one needs a compiler \(see Chapter 1\). On Unix machine, open the terminal and type

```bash
gfortran myprogram.f90
```

This will produce a new file \(an executable\). By default, the new file is called `a`. You can change this to give the file a more convenient name, for example `myprog_exe`. To do so, use the option `-o`:

```bash
gfortran -o myprogr_exe myprogram.f90
```

This tells the compiler to name the output file `myprog_exe`. It uses the _flag_ \(or option\) `-o` followed by the argument to this flag.

To compile a program with modules or a library, see next chapters.

### 3. Executing the code

It is only when executing the file that the code will be executed and the computations run. To execute the file, type in the terminal

```bash
./a
```

Or, if you used the `-o` flag with a different output name:

```
./myprog_exe
```

## Declaring variables

You need to declare all the variables you will use. ere is how

```fortran
program myprogram
  implicit none
  real :: a, b, c
  the code that uses a b and c here
end program
```

The key words `implicit none` means that you want that all the variables used in the code have to be first declared. Hence, if in the `the code here` part you use other letters, such as `d`, the code will return an error when you try to compile it. It is possible no to use `implicit none` which allows you to use variables not declared. However, you should _never_ do this \(mostly because each letter of the alphabet has a default type if not declared\). Note that here we declared the variables as `real`. There are other types, and the most usual types are

```fortran
real
integer
character
```

The type `character` is for strings.

You can specify the number of bytes to be used for your variables \(hence the precision\) by using the `kind`specifier.

```fortran
integer(kind=2) :: shortinteger
integer(kind=4) :: longinteger
integer(kind=16) :: verylonginteger
```

## Functions and Subroutines

In FORTRAN you can use two types of blocs of code which you provide with input: the function and the subroutine. They both work the same way but with slight differences.

### Functions

A function is defined as follows:

```fortran
function myfunction(a,b,c)
  implicit none
  real :: a,b,c, myfunction
  the code here
end function
```

As you can see, one needs to declare all the variables that are passed as arguments \(here `a`, `b` and `c`\) as well as the output variable which must _have the same name as the function_. For example, the function could be

```fortran
function myfunction(a,b,c)
  implicit none
  real :: a,b,c, myfunction
  myfunction = a + b + c
end function
```

To call this function into the main program you would write altogether

```fortran
program myprogram
  implicit none
  real :: x1,x2,x3, easy_sum
  x1 = 1
  x2 = 2
  x3 = 3
  easy_sum = myfunction(x1,x2,x3)

  contains
  function myfunction(a,b,c)
    implicit none
    real :: a,b,c, myfunction
    myfunction = a + b + c
  end function
end program
```

The key word `contains` tells the compiler that the code following this key word contains the definitions of functions and subroutines.

In the definition of the function, the variables passed as argument are local: they can have the same name as variables in the main part \(above `contains`\), this will not affect them. One can however  use variables defined above `contains`inside the function, such as:

```fortran
program myprogram
  implicit none
  real :: x1,x2,x3, easy_sum, big_number
  big_number = 1000
  x1 = 1
  x2 = 2
  x3 = 3
  easy_sum = myfunction(x1,x2,x3)

  contains
  function myfunction(a,b,c)
    implicit none
    real :: a,b,c, myfunction
    myfunction = a + b + c + bignumber
  end function
end program
```

In this example, `easy_sum` will be equal to `1000 + x1 + x2 + x3,`, i.e. `1+2+3+1000 = 1006`.

### Subroutines

A subroutine is similar to a function but it does not necessarily return a variable. Instead, it executes the code inside it. Declaring a subroutine is done as follows

```fortran
subroutine mysubroutine(a,b,c)
  implicit none
  real :: a, b, c
  a = 0
  b = -1000
  c = a + b
end subroutine
```

This subroutine will change the value of the three variables. You use a subroutine into your program with the following code:

```fortran
program myprogram
  implicit none
  real :: x1,x2,x3
  call mysubroutine(x1,x2,x3)

  contains
  subroutine mysubroutine(a,b,c)
    implicit none
    real :: a, b, c
    a = 0
    b = -1000
    c = a + b
  end subroutine
end program
```

# More on functions and subroutines

In both functions and subroutines, one can specify if the arguments of the function/subroutine are to be altered by using the keywords `intent(in)`, `intent(out)` and `intent(inout)`. `intent(in)` means that the variable should not be altered inside the function \(input only\). `intent(out)` means that whatever the value given to the variable before it enters the function as an argument, this value is ignored. With `intent(inout)` the variable can be altered and the value it has before entering the function is still assigned to it at the beginning of the function. For example

```fortran
function myfunction(a,b,c)
  implicit none
  real, intent(in) :: b, c
  real :: myfunction
  real, intent(inout) :: a
  a = a + b + c
  myfunc = a
end function
```

Note that you **should not** have an `intent(out)` before the return of the function \(here `myfunction`\).

A function can also be a `pure function`. This implies that the function will only change the behavior of the output \(i.e. the variable `myfunction` above\). It is a keyword used to make sure that nothing else is altered.

```fortran
pure function myfunction(a,b,c)
  implicit none
  real, intent(in) :: b, c
  real :: myfunction
  real, intent(inout) :: a
  a = a + b + c
  myfunc = a + b + c
end function
```

This will not work \(to check\) because `a` is an argument of a pure function, but the function tries to modify it \(the `inout `classification is enough to provoke an error as a pure function cannot modify an input argument\). To have something working one needs to change the `intent(inout) :: a` into `intent(in) :: a` as well as to delete `a = a + b + c` \(or create an intermediary variable `intvar = a + b + c` , and not forgetting to declare it with: `real :: intvar`\).

# Types and arrays, parameters

To declare an array \(vector\) `a` and a matrix `b` use

```fortran
real :: a(5)
real :: b(5,4)
```

or, equivalently

```fortran
real, dimension(5) :: a
real, dimension(5,4) :: b
```

The first way is convenient to declare arrays of different dimensions on the same line

```fortran
real :: a(5), b(5,4)
```

You can also use the keyword `parameter`. This means that the variable _cannot_ change value. You must therefore initialize it at the same time you declare it.

```fortran
real, parameter :: d = 5
```

# `Save` keyword, initialization-declaration

The keyword `save` is used to make a variable global \(see next chapter\). More specifically,  `save` is a specification statement which can be used to ensure that variables and arrays used within a procedure \(local variable\) preserve their values between successive calls to the procedure.  
Another way to make a variable global is to assigns it a value at the same time as the declaration.

```fortran
real, save :: a
real :: b = 5
```

That is why it is dangerous to assign a value at the same time on edeclares a variable: at each iterative call, the starting value of the variable is the last one assigned to it, not the one assigned in the declaration \(here b = 5\). Overall, it is preferable to use modules instead of  `save`  \(see next chapter\).

# Comments

To write a comment in FORTRAN, use `!` at the beginning of the comment.

# Break lines

To break a line in FORTRAN, use `&` at the end of the line you want to break, and start the next line right below.

