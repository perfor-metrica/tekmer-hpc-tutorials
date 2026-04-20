# AmberTools 24.10 Usage Guide

## General Information
AmberTools is a suite of independently developed programs that can be used both on their own and together with Amber.

It is suitable for the following use cases:

- Molecular dynamics (MD) simulations
- Explicit solvent simulations
- Generalized Born (implicit solvent) models

---

## Load Module

Before loading AmberTools, you must load its dependencies:

```bash
ml GCC/13.3.0 OpenMPI/5.0.3 AmberTools
```

---

## Verify Installation

```bash
sander --version
which tleap
which parmchk2
which gem.pmemd
```

Expected outputs:

- sander: Version 24.0
- tleap: /perf/papps/AmberTools/24.10-gompi-2024a/bin/tleap
- parmchk2: /perf/papps/AmberTools/24.10-gompi-2024a/bin/parmchk2
- gem.pmemd: /perf/papps/AmberTools/24.10-gompi-2024a/bin/gem.pmemd

---

## Build Details

- Version: AmberTools 24.10
- sander version: 24.0
- Compiler: GCC 13.3.0
- MPI: OpenMPI 5.0.3
- Installation path: /perf/papps/AmberTools/24.10-gompi-2024a

---

## Core Components

- tleap: System preparation (topology and coordinate generation)
- parmchk2: Parameter checking and generation
- sander: CPU-based MD engine
- pmemd / gem.pmemd: Optimized MD engines

---

## Example Usage

### System Preparation (tleap)

```bash
tleap -f leap.in
```

### Parameter Check

```bash
parmchk2 -i ligand.mol2 -f mol2 -o ligand.frcmod
```

### Run MD (sander)

```bash
sander -O -i md.in -p topol.prmtop -c input.inpcrd -o md.out -r md.rst -x md.nc
```

---

## Slurm Example

```bash
#!/bin/bash
#SBATCH -J amber_job
#SBATCH -p defq
#SBATCH -N 1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --time=04:00:00
#SBATCH --output=%x_%j.out
#SBATCH --error=%x_%j.err
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=your_email@example.com

ml GCC/13.3.0 OpenMPI/5.0.3 AmberTools

export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK}

echo "Job started on $(hostname)"
echo "Node list: $SLURM_JOB_NODELIST"
echo "CPUs per task: $SLURM_CPUS_PER_TASK"
echo "Start time: $(date)"

srun sander -O \
  -i md.in \
  -p topol.prmtop \
  -c input.inpcrd \
  -o md.out \
  -r md.rst \
  -x md.nc

echo "End time: $(date)"
```

---

## Performance Tips

- Start with small tests
- Control CPU usage with `--cpus-per-task`
- Use parallel versions if MPI is required
- Monitor disk I/O performance

---

## Log Analysis

```bash
grep "NSTEP" md.out
```

---

## Notes

- Do not run on login nodes
- Ensure sufficient disk space in the working directory

