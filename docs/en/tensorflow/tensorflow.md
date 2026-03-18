# TensorFlow on Tekmer HPC

[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Overview

TensorFlow is an open-source machine learning framework developed by Google. It is widely used for:

- Deep learning (CNN, RNN, Transformers)
- Training and inference
- Scientific computing with GPU acceleration

---

## Availability on Tekmer HPC

TensorFlow is available on the Tekmer HPC cluster through environment modules.

Load available versions:

    module avail tensorflow

Load a specific version:

    module load TensorFlow

---

## Recommended Usage

TensorFlow workloads should typically run on:

- GPU nodes (preferred for training)
- CPU nodes (for lightweight inference or preprocessing)

---

## Example: Running TensorFlow (CPU)

```bash
#!/bin/bash
#SBATCH --job-name=tf_cpu
#SBATCH --partition=defq
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=16G
#SBATCH --time=02:00:00

module load TensorFlow

python script.py
```

---

## Performance Recommendations

- Use GPU for training whenever possible
- Match CPU threads with TensorFlow settings:

```bash
      export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
```

- Avoid oversubscribing CPU resources
- Monitor memory usage (TensorFlow can consume large memory)

---

## Provider

Google

---

## Licensing

Apache License 2.0 (Open Source)

