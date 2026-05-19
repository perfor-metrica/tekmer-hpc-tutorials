# HPC Performance Optimization Tips (Slurm-Based Workloads)

[![Documentation Status](https://readthedocs.org/projects/performetrica-hpc-tutorials/badge/?version=latest)](https://performetrica-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

### Overview

Performance in High Performance Computing (HPC) environments is defined by two key factors:

1. **Execution time** of your application  
2. **Queue wait time** before your job starts running  

Optimizing both is critical. A fast application that waits hours in the queue is still inefficient.

After ensuring correctness, **performance optimization is the most important step** in HPC usage.

---

### Key Concepts

Efficient HPC usage depends on how well your workload matches the underlying hardware:

- Tasks sharing CPU cache → **lower latency**
- Memory-intensive workloads → **benefit from NUMA awareness**
- Poor placement → **wasted CPU cycles and longer runtimes**

Proper use of **Slurm scheduler parameters** allows you to control this behavior.

---

### Scope

> **This guide applies to Linux batch jobs executed via Slurm**

---

## 1. Understand Your Application Type

Before tuning anything, determine:

### Is your application:
- **Single-threaded?**
- **Multi-threaded (OpenMP, shared memory)?**
- **Distributed (MPI)?**

This determines everything.

---

## 2. Multi-threaded Workloads (Shared Memory)

If your application is multi-threaded:

### Best Practice

Keep all threads **within the same CPU socket** to:

- Maximize cache usage

- Avoid NUMA penalties

- Reduce memory latency

### Example: Use 24 cores on a single CPU

#### Command line:

```bash
--ntasks=1 --cpus-per-task=24
```

####Batch script:

```bash
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=24
```

###Important Considerations


This request may increase queue wait time.

You are asking for a large contiguous resource block.

##Scaling Strategy

If your application scales well:

Gradually increase:

```bash
--cpus-per-task=N
```

Slurm default behavior:

Expands CPUs within the same socket first

Then spills over to next socket if needed

##Recommended Additions (Critical in Practice)
###1. Explicit CPU Binding

Avoid scheduler ambiguity:

```bash
#SBATCH --cpu-bind=cores
```

or:

```bash
#SBATCH --hint=nomultithread
```

###2. Control Thread Count in Application

Set environment variables:

```bash
export OMP_NUM_THREADS=24
```

Mismatch between Slurm and application = performance loss

###3. Avoid Oversubscription

Wrong:

```bash
--ntasks=24 --cpus-per-task=24   # 576 logical CPUs requested
```

Correct (for OpenMP):

```bash
--ntasks=1 --cpus-per-task=24
```

##3. When NOT to Use This Approach

Do NOT use **--cpus-per-task** if:

Your workload is MPI-based

- Tasks are independent

- You need multi-node scaling

Instead use:

```bash
--ntasks=N
```

## 4. Trade-off: Performance vs Queue Time

| Strategy             | Result                             |
|----------------------|------------------------------------|
| Large CPU block      | Faster execution, longer wait      |
| Smaller allocation   | Faster start, longer runtime       |

Best practice:

- Benchmark both approaches

- Optimize total turnaround time, not just runtime


