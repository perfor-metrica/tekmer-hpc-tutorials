[![Documentation Status](https://readthedocs.org/projects/performetrica-hpc-tutorials/badge/?version=latest)](https://performetrica-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

# PERFORMETRICA HPC CLUSTER QUICKSTART GUIDE

## Scope of This Guide

This guide explains how to access and run jobs on the Performetrica HPC Cluster.

It does NOT cover:

- Basic Linux usage

- Programming models such as MPI, OpenMP or CUDA

Users are expected to have:

- Basic Linux command-line knowledge

- Familiarity with their applications

---

## Getting an HPC Account

Access to Performetrica HPC is managed via the user portal:

👉 [https://portal.superbilgisayar.tr/](https://portal.superbilgisayar.tr/)

### Steps

1. Register via the portal (**Online Registration**)  
2. Verify your email and complete activation  
3. Wait for approval (if required)  
4. Your HPC account will be automatically provisioned  

Accounts may be:

- Individual (R&D users)

- Organization-based (universities, companies)

---

## Important Usage Rules (Read Carefully)

Improper usage can negatively impact all users on the system.

Failure to follow these rules may result in account suspension.

### Do NOT

- Run computational jobs on login nodes  
- Submit large-scale jobs without testing  
- Abuse shared resources  

### Always

- Start with small test jobs  
- Use the scheduler (Slurm)  
- Monitor your jobs  

---

## HPC System Architecture

The Performetrica HPC cluster consists of:

- **Login Nodes** → login, job submission, light tasks  
- **Compute Nodes** → actual computation  
- **Storage Systems** → shared high-performance storage  

Login nodes are NOT for computation.

---

## Connecting to the System

### Windows

Use an SSH client such as:

- MobaXterm  

- PuTTY  

After installing the client, connect using:
**username@login.superbilgisayar.tr**


### Linux and macOS

Use SSH from terminal:

**ssh username@login.superbilgisayar.tr**


---

## File System Basics

When you login, you start in your home directory (`~`).

### Basic Commands

```bash
pwd # current directory
ls # list files
cd dir # change directory
cd .. # parent directory
```

### File Operations

```bash
mv file1 file2 # rename/move
cp file1 dir/ # copy
```

---

## Data Transfer

### Upload (local → cluster)

```bash
scp file username@login.superbilgisayar.tr:/path/
```

### Download (cluster → local)

```bash
scp username@login.superbilgisayar.tr:/path/file
```

---

## Editing Files

Use terminal-based editors:

- vi  
- nano  
- emacs  

---

## Software Environment

Available software is managed via modules:

```bash
module avail
module load <software>
```

For additional software:

Submit a request via the portal.

---

## Job Scheduling (Slurm)

All computations MUST be submitted via Slurm.

### Example Job Submission

```bash
sbatch job.sh
```

### Useful Commands

```bash
squeue # list jobs
scancel JOBID # cancel job
sinfo # cluster status
```

Jobs are scheduled based on:

- Resource availability  

- Fair usage policies  

- Priority  

---

## Storage Policy (Critical)

- HPC is NOT for long-term storage  
- Always backup your data externally  
- Remove unnecessary files after completion  

Old or unused data may be deleted by administrators.

---

## Best Practices

- Test jobs before scaling  
- Use appropriate resources (CPU, memory)  
- Avoid unnecessary large I/O operations  
- Keep your directories organized  

---

## Support

For help and support:

📧 [contact@performetrica.com](mailto:contact@performetrica.com)  
🌐 [Performetrica HPC Portal](https://portal.superbilgisayar.tr/)

