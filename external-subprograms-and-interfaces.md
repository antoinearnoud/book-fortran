---
description: This is a slightly more advanced topic.
---

# External subprograms and Interfaces

To call a function (or subroutine) from another file, we saw that we can use modules with the syntax

```fortran
use moduleName
```

The Interface statement is used when one needs to use an external function as an input into another function. It works the following way

```fortran
program main
implicit none
use moduleName, only: subroutine_one
real :: a,b,c,n, px, result

main_subroutine(subroutine_one,a,b,c,n, px, result)

print(result)

include
subroutine main_subroutine(func, a,b,c,n, px, result)
implicit none
real :: result
interface
function func(a,b,c,n)
		   real, intent(in) :: a(:),b(:),n
		   real vector_add(size(a))
		   end function vector_add
		end interface

result = px * func(a,b,c,n)
end subroutine
```
