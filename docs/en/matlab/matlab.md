[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

# MATLAB

## General Information

MATLAB is a high-level programming and numerical computing environment used for:

- Mathematical modeling and simulation  

- Data analysis and visualization  

- Algorithm development  

- Engineering and scientific computing  

On TEKMER HPC, MATLAB can be used in:

- **Interactive mode** (for testing and development)

- **Batch mode** (for large-scale jobs via Slurm)

- **Parallel mode** using the Parallel Computing Toolbox

---

## Installation / Help

Detailed installation and usage instructions are available at **Installation Tutorial** or with the link below:

👉 https://tekmer-hpc-tutorials.readthedocs.io/en/latest/matlab/pdf/matlab-tutorial.pdf

Includes:

- Windows installation guide  

- HPC (Slurm) integration examples  

For additional help:  
📧 [contact@performetrica.com](mailto:contact@performetrica.com)

---

## Minimum System Requirements

| OS       | Architecture | RAM |
|----------|-------------|-----|
| Windows  | 64-bit      | 4 GB |
| macOS    | 64-bit      | 4 GB |
| Linux    | 64-bit      | 4 GB |

---

## Using MATLAB on TEKMER HPC

### Load MATLAB

```bash
module load matlab
```

Run Interactive Session (short tests only)

```bash
matlab
```
⚠️ Do NOT run heavy workloads interactively on login nodes.

Run Batch Job (Recommended)

###Example Slurm script:

```bash
#!/bin/bash
#SBATCH -J matlab_job
#SBATCH -N 1
#SBATCH -n 4
#SBATCH --time=01:00:00

module load matlab

matlab -nodisplay -r "my_script; exit"
```

Submit with:

```bash
sbatch job.sh
```

Parallel Computing

MATLAB supports parallel execution via:

- Parallel Computing Toolbox

- parpool / parfor

- Distributed jobs


Example:

```bash
parpool(4);
parfor i=1:100
    A(i) = heavy_function(i);
end
```

##Toolbox Information

The following toolboxes are available (subset shown):

- MATLAB

- Simulink

- Parallel Computing Toolbox

- Deep Learning Toolbox

- Signal Processing Toolbox

- Optimization Toolbox

- Statistics and Machine Learning Toolbox

- Computer Vision Toolbox

- Control System Toolbox

- Image Processing Toolbox

- Symbolic Math Toolbox

- GPU Coder

(Additional toolboxes may be available depending on licensing.)

##Usage Policy

MATLAB is licensed software and must be used in compliance with license terms

Parallel usage may be limited by available licenses

Excessive resource usage may result in job termination

Users must follow [TEKMER HPC Usage Policy](HPC_Kullanim_Politikasi.md)

Servers Installed

MATLAB is available on the TEKMER HPC cluster.

For campus-wide or institutional access requests:

📧 [contact@performetrica.com](mailto:contact@performetrica.com)

Provider

MathWorks Inc.

Supported Platforms

Windows

Linux

macOS
