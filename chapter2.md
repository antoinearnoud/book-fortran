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
or, if you used the ```-o`` flag
```
./myprog_exe
```


