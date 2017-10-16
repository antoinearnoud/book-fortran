# Eigth Chapter: Debugging Errors

## Simple Thoughts

One problem with FORTRAN is that sometimes, when you try to use a variable to which you haven't given any initialization, it will still be able to use it. However, it will use the previous value stored at this place in the system. This value can be whatever crazy thing you can think about, since what was stored can be any type of data. That's how you can get crazy result.

First step of debugging is to make sure that all the variable you used have been initialized / given a value before using them.

## Debugging Tools

You can use gdb. When compiling, add the option `-g`. This allows you to run your program normally once it is compiled or to run it with gdb. Just type `gdb myprogram_exe`. Then you can type different things. For example

```
break main
run
```

and then follow the execution of the program step by step by using

```
step
```

To go faster one can use `step 50` which will automatically apply steep 50 times \(50 can be changed to any integer\).

Instead of typing `break main` \(which puts break at each step of the program\), you can instead create a break point anywhere in the code \(source file\) by using `break sourcefile.f90:lineofbreak`. After creating all the breaks needed, just use `run`.

Then, at any time you can use the

```
print name_of_variable
```

to see what is the value stored in a given variable.

`list`is used to see a few lines of code around the step that has just ran. Similarly, `where`tells you where you are in the program.

To quit gdb type

```
quit
y
```



