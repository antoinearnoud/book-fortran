# Eigth Chapter: Debugging Errors

## Simple Thoughts

One problem with FORTRAN is that sometimes, when you try to use a variable to which you haven't given any initialization, it will still be able to use it. However, it will use the previous value stored at this place in the system. This value can be whatever crazy thing you can think about, since what was stored can be any type of data. That's how you can get crazy result.

First step of debugging is to make sure that all the variable you used have been initialized / given a value before using them.

## Debugging Tools

