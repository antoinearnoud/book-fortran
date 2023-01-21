# Recursive functions

Fortran 90can deal with recursive functions. It requires to use a few additional keywords: recursive and result.  here is an example to compute a factorial.



```
RECURSIVE FUNCTION Factorial(n)  RESULT(Res)

IMPLICIT NONE
INTEGER :: Res
INTEGER, INTENT(IN) :: n

IF (n == 0) THEN
   Res = 1
ELSE
   Res = n * Factorial(n-1)
END IF

END FUNCTION Factorial
```

The keyword RESULT\( \) is necessary to let the program know what to return when the recursion is finished.

