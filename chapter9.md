# Optimization

## Flags

Code in Fortran can be made faster by using optimization flags. These are indications that one wants the compiler to figure out how it can "improve" the code in order to have it run faster. There are many different ways the compiler can improve the code. For example, once a funcion or subroutine is called, the compiler might not know in advance the size it needs to allocate the different local variables of the subroutine. By asking the compiler to optimize the code, the compiler will look at this when compiling and make sure it knows the requirements needed at runtime. The only drawback is that optimizing the code means imposing more constraints on all the objects of the code, and it can end up breaking the code, i.e. make it not work anymore. The usual recommendation is to work out one's code without optimizers and only turn the optimizers at the end, one the code is not supposed to change much but will be run possibly many times.

The most comong optimizer flag is \`-O'

`gfortran -O myfile.f90`

This let the compiler choose which lelvel of optimization it seems adequate. One can also impose a level of optimization with `-O1` , `-O2` or `-O3`.

Besides the flag to optimize code, you should also make sure of the following:

1.  loop over your matrices using outside index first, i.e.

    ```
    do j=1,1000
     do i=1,5
      a(i,j) = (i+j)/2.0
     end do
    end do
    ```
2. avoid using a module if it is used many times. Use inline code instead. There is an overhead cost at calling a module many times.
3. **Profiling: How to improve code**

Use a profiler to see where the code is spending most of the time. However, never use the O3 optimization flag when profiling (it rearranges the code very agressively).
