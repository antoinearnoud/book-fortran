# Installing FORTRAN

I recommend using Unix systems. On Unix machines \(such as Linux\), FORTRAN is already installed. If one does not have a Unix system, one can use Oracle Virtual Box to create one.

## FORTRAN on Windows 

### using Oracle Virtual Box

Windows machines do not use the same protocols than Unix machines, and it is common to encounter issues with Windows when using library or writing scripts to automate some code. For example, Windows does not use bash scripting. As most libraries and scripting codes are developped on unix system, and most of the clusters I have encountered use bash commands, I recommend to simulate a Unix environment on a Windows computer in order to use Fortran. It is very easy to do.

Download and install Oracle Virtual Box from Oracle website. Create a new virtual machine with unix operating system.  This will install unix on your computer. Then install Dropbox on both your computer and the virtual system. On the virtual system, only sync the Dropbox folder of your program's code \(for example myproject/code\). This way the code is downloaded automatically on Dropbox servers. One can also use a control version system like git. It requires a bit of reading and practice to use a system like git so one can postpone this until after one has a good grasping of FORTRAN. For more information on git, checkout git for Economists.

### using Intel Visual

One can install Intel Visual \(free for academics\) on Windows. This installs Intel compiler  and a convenient interface to use write and compile code. However instructions in this manual on scripting \(used to automate tasks or to parallelize work\) needsto be adapted to Windows environment \(using batch instead of bash language\). 

## FORTRAN on Mac

Max machines are close to Unix systems, so there should not be much to install on Macs. GCC Compiler \(gfortran\) is already installed.

## FORTRAN on Unix

Fortran is already ready to use on unix machines. The compiler is _gfortran_ \(see below for explanations on compilers\).

