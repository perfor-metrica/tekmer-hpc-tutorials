# Slurm Job Submission Guide (Tekmer HPC)

[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Overview

This guide explains how to submit, monitor, and troubleshoot jobs on the Tekmer HPC cluster using Slurm.

---

## Preparing a Job Script

Example scripts may be located under:

**/perf/shared/**

Copy and modify:

```bash
mkdir -p $HOME/workfolder
cd $HOME/workfolder
cp /perf/shared/example_submit.sh my_experiment.sh
vi my_experiment.sh
```

---

## Submitting a Job

```bash
sbatch my_experiment.sh
```

---

## Minimal Example

```bash
#!/bin/bash
#SBATCH --job-name=test_job
#SBATCH --partition=defq
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --time=01:00:00
#SBATCH --output=%x-%j.out

echo "Running on $(hostname)"
```
---

## Basic Commands


```bash
sbatch job.sh
squeue
squeue -u $USER
scancel <jobid>
sinfo
scontrol show job <jobid>
sacct -j <jobid>
```
---

## Important Notes for Tekmer HPC

- Default partition: defq
- QoS is NOT used in this cluster
- Always request only necessary resources
- Prefer %x-%j.out for outputs

---

## OpenMP Example

```bash
#!/bin/bash
#SBATCH --partition=defq
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=16G
#SBATCH --time=02:00:00

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
./my_openmp_program
```

---

## MPI Example

```bash
#!/bin/bash
#SBATCH --partition=defq
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=8
#SBATCH --time=01:00:00

srun ./my_mpi_program
```

---

## Monitoring

```bash
squeue -u $USER
sacct -j <jobid>
```

---

## Best Practices

- Match ntasks vs cpus-per-task correctly
- Set OMP_NUM_THREADS
- Avoid oversubscription
- Optimize total time (queue + runtime)

---

## Available Software

```bash
module avail
```
