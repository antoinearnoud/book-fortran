# Makefile

## What is a Makefile

A Makefile is a file that automatically compiles your program. When there are many different files \(modules\) and that these files call each other, it might be helpful to automate the process of generating the program. The structure of a Makefile is the following

```makefile
# Start of the Makefile

# Defining variables
FC = ifort #gfortran
FFLAGS = -openmp #-fopenmp
LFLAGS = 
OBJECTS = main.o params.o nrtype.o nrutil.o grid.o preference.o demographics.o labor.o gridtax.o evaluate.o output.o tauchenhussey.o newton.o euler_eqn.o household.o resid.o taxfn.o distribution.o zbrent.o
MODULES = nrtype.mod nrutil.mod params.mod
.PHONY: clean

# Makefile
exec : $(OBJECTS)
	$(FC) $(FFLAGS) -o replication_parallel $(OBJECTS)


nrtype.o : nrtype.f90
	$(FC) -c $(FFLAGS) $<
nrutil.o : nrtype.mod nrutil.f90
	$(FC) -c $(FFLAGS) nrutil.f90
params.o : nrtype.mod params.f90
	$(FC) -c $(FFLAGS) params.f90

# below: to replace with: %.o : params.mod %.f90
#			$(FC) -c $(FFLAGS) %.f90 ??
# not sure it works

main.o : params.mod nrtype.mod main.f90
	$(FC) -c $(FFLAGS) main.f90
grid.o : params.mod grid.f90
	$(FC) -c $(FFLAGS) grid.f90
preference.o : params.mod preference.f90
	$(FC) -c $(FFLAGS) preference.f90
demographics.o : params.mod demographics.f90
	$(FC) -c $(FFLAGS) demographics.f90
labor.o : params.mod labor.f90
	$(FC) -c $(FFLAGS) labor.f90
gridtax.o : params.mod gridtax.f90
	$(FC) -c $(FFLAGS) gridtax.f90
evaluate.o : params.mod evaluate.f90
	$(FC) -c $(FFLAGS) evaluate.f90
output.o : params.mod output.f90
	$(FC) -c $(FFLAGS) output.f90
tauchenhussey.o : params.mod tauchenhussey.f90
	$(FC) -c $(FFLAGS) tauchenhussey.f90
newton.o : params.mod newton.f90
	$(FC) -c $(FFLAGS) newton.f90
euler_eqn.o : params.mod euler_eqn.f90
	$(FC) -c $(FFLAGS) euler_eqn.f90
household.o: params.mod household.f90
	$(FC) -c $(FFLAGS) household.f90
resid.o : params.mod resid.f90
	$(FC) -c $(FFLAGS) resid.f90
taxfn.o : params.mod taxfn.f90
	$(FC) -c $(FFLAGS) taxfn.f90
distribution.o : params.mod distribution.f90
	$(FC) -c $(FFLAGS) distribution.f90

# this one is different
zbrent.o : nrtype.mod nrutil.mod zbrent.f90
	$(FC) -c $(FFLAGS) zbrent.f90


nrtype.mod : nrtype.f90
	$(FC) -c $(FFLAGS) $<
nrutil.mod : nrutil.f90
	$(FC) -c $(FFLAGS) $<
params.mod : params.f90
	$(FC) -c $(FFLAGS) $<

clean:
	rm -f $(OBJECTS) $(MODULES)

#END OF MAKEFILE
```

## How to use a Makefile

use the following command

```
make -f Makefile
```

You can also only run the clean part of the Makefile by

```
make clean -f Makefile
```



