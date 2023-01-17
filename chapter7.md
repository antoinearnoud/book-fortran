# Appendix: Clusters

To use Yale cluster (Grace) for compiling with Fortran you don't need to load anything if you are using gfortran compiler. If you want to use Intel compiler you need to load it with

```bash
module load Langs/Intel/...
```

where `...` has to be replaced by the version of intel to use.

Yale Cluster (Grace) uses SLURM to manage the job submissions. The command to submit a job is

```bash
sbatch name_of_file.sh
```

The file must be a bash file (see the _Appendix: Bash_ chapter for a _very_ short introduction to Bash).

To verify the jobs that have been submitted, on uses the following command

```bash
squeue -u id_of_user
```

The head of the script file (sh file) must be

`#!/bin/bash`

One can add some option (before ANY other text):

```bash
#SBATCH --job-name=myjob
#SBATCH --partition=nameofthepartition
#SBATCH --time=80:00:00
#SBATCH --output=job_output.txt
```

Time is in HH:MM:SS. To add days: DD-HH:MM:SS.
