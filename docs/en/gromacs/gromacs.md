# GROMACS 2025.4 Usage Guide

## General Information
GROMACS is a high-performance molecular dynamics (MD) software designed for biomolecular simulations.

It is optimized for:

- MPI parallelism

- OpenMP threading

- SIMD vectorization (AVX)

On TEKMER HPC:

- MPI: OpenMPI 5.0.3

- OpenMP: Enabled (max 128 threads)

- FFT: FFTW 3.3.10

Executable path:
`/perf/papps/GROMACS/2025.4-gompi-2024a/bin/gmx_mpi`

---

## Load Module

```bash
ml GROMACS/2025.4-gompi
```

---

## Verify Installation

```bash
gmx --version
gmx_mpi --version
```

---

## Build Details

- Version: 2025.4
- Precision: Mixed
- SIMD: AVX_256
- Compiler: GCC 13.3.0
- MPI: OpenMPI 5.0.3

---

## Running Modes

### Hybrid MPI + OpenMP

```bash
gmx_mpi mdrun -ntmpi 4 -ntomp 4 -s topol.tpr
```

### OpenMP only

```bash
gmx mdrun -ntomp 8 -s topol.tpr
```

### MPI only

```bash
gmx_mpi mdrun -ntmpi 16 -ntomp 1 -s topol.tpr
```

---

## Slurm Example

```bash
#!/bin/bash
#SBATCH -J gromacs_job
#SBATCH -N 1
#SBATCH --ntasks=4
#SBATCH --cpus-per-task=4
#SBATCH --time=04:00:00

ml GROMACS/2025.4-gompi

export OMP_NUM_THREADS=4

srun gmx_mpi mdrun -ntmpi 4 -ntomp 4 -s topol.tpr -deffnm md
```

---

## Performance Tips

- Ensure `ntmpi × ntomp = total cores`
- Start with small tests
- Avoid over-allocation
- Use hybrid mode for best performance
- Monitor with `squeue`

---

## Logs

```bash
grep Performance md.log
```

---

## Notes

- Do not run on login nodes

