# Sixth Chapter: Using Libraries

To use library you need to have a library available on your computer. That's complicated. Most of the time you don't need libraries. One library you can use to optimize \(i.e. find the global optimum of\) functions is NLopt.

To compile with a library named mylibrary, use

```
gfortran myprogram.f90 -lmylibrary
```

Note the `-l` before the name of the library \(where `l`is lower case of **L** and stands for library\).

The compiler must know where to find the library.

