## General instructions

Here are brief instructions for accessing and using LUMI, see [LUMI Documentation](https://docs.lumi-supercomputer.eu/) for more details.

LUMI is accessed with `ssh` (note that only ssh keys can be used, so key needs to be uploaded to 
user portal):
```
ssh -Y my-user-name@lumi.csc.fi
```

For editing program source files you can use e.g. *nano* editor: 

```
nano prog.f90 &
```
(`^` in nano's shortcuts refer to **Ctrl** key, *i.e.* in order to save file and exit editor press `Ctrl+X`)
Also other popular editors (emacs, vim, gedit) are available.

### Disk areas

All the exercises in the supercomputers should be carried out in the
**scratch** disk area. The name of the scratch directory can be
queried with the command `lumi-workspaces`. As the base directory is
shared between members of the project, you should create your own
directory:
```
cd /scratch/project_465000424 
mkdir -p $USER
cd $USER
```

### Running applications in LUMI

In LUMI, programs need to be executed via the batch job system. Simple job running with 
8 MPI tasks and 8 GPUs in a single node can be submitted with the following batch job script:
```
#!/bin/bash
#SBATCH --job-name=example
#SBATCH --account=project_465000424
#SBATCH --partition=standard-g
#SBATCH --reservation=tau_training
#SBATCH --time=00:05:00
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=8
#SBATCH --gpus-per-node=8

export MPICH_GPU_SUPPORT_ENABLED=1 # needed for applications using GPU aware MPI

srun my_exe
```

Save the script *e.g.* as `job.sh` and submit it with `sbatch job.sh`. 
The output of job will be in file `slurm-xxxxx.out`. You can check the status of your jobs with `squeue -u $USER` and kill possible hanging applications with
`scancel JOBID`.

The reservation `tau_training` is available during the course days and it
is accessible only for the members of the `project_465000424`.

### Using TAU

After loggin into Lumi using ssh, run:

```bash
module use /appl/local/csc/courses/tau_prof_march23/modules/
```

After this you can use tau by loading the module:

```bash
module load tau
```

For running `paraprof` (GUI for investigating profiles) it is recommended to use VNC, 
details for setting up VNC are provided in [separate instructions](vnc-instructions.md)

