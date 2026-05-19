# Performetrica HPC – Getting Started & System Overview

[![Documentation Status](https://readthedocs.org/projects/performetrica-hpc-tutorials/badge/?version=latest)](https://performetrica-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Accessing Performetrica HPC

### From inside Performetrica / local network
```bash
ssh <username>@login.superbilgisayar.tr
```

### From outside (internet)
```bash
ssh <username>@login.superbilgisayar.tr
```

> If VPN or firewall restrictions apply, follow Performetrica access policy.

---

## Cluster Overview

Performetrica HPC is a CPU-based high performance computing cluster designed for:

- Scientific computing
- Parallel workloads (MPI / OpenMP)
- Simulation, modeling, and data processing

---

## Inspecting Cluster Resources

To list nodes and partitions:

```bash
sinfo --long --Node "%#N %.6D %#P %6t"
```

To check detailed node info:

```bash
scontrol show node <nodename>
```

---

## Understanding CPU Capabilities

Performance depends heavily on CPU features.

Example CPU capabilities (Intel Xeon class CPUs):

- AVX / AVX2 / AVX-512
- FMA (Fused Multiply-Add)
- SIMD vectorization
- NUMA architecture

You can inspect CPU flags:

```bash
lscpu
```

or:

```bash
cat /proc/cpuinfo
```

### Why this matters

- AVX/AVX512 → faster vector math
- NUMA → memory locality is critical
- Cache hierarchy → affects scaling

---

## Performance Optimization Guidelines

### 1. Match workload to architecture

- Use **OpenMP** for shared memory scaling
- Use **MPI** for distributed scaling

---

### 2. CPU Binding (Critical)

Avoid CPU migration:

```bash
#SBATCH --cpu-bind=cores
```

---

### 3. NUMA Awareness

- Keep threads on same socket if possible
- Avoid cross-socket memory traffic

---

### 4. Thread Configuration

```bash
export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
```

---

### 5. Memory Optimization

- Request realistic memory
- Avoid over-allocation (increases queue time)
- Monitor usage with:

```bash
sacct -j <jobid> --format=MaxRSS
```

---

### 6. I/O Considerations

- Use local `/tmp` when possible
- Avoid heavy I/O on shared storage
- Batch writes instead of frequent small writes

---

## Typical Workload Types

| Workload Type | Recommended Slurm Settings |
|--------------|---------------------------|
| Serial       | ntasks=1, cpus-per-task=1 |
| OpenMP       | ntasks=1, cpus-per-task=N |
| MPI          | ntasks=N                  |
| Hybrid       | ntasks + cpus-per-task    |

---

## Example CPU Job

```bash
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --partition=defq
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=32G
#SBATCH --time=02:00:00

export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

./my_application
```

---

## Key Takeaways

- Use correct Slurm parameters
- Respect NUMA and cache locality
- Optimize total runtime (queue + execution)

---

## References

- https://slurm.schedmd.com/
- https://hpc-wiki.info/

