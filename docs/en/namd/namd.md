[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

# NAMD

## General Information

NAMD (Nanoscale Molecular Dynamics) is a high-performance simulation software designed for large biomolecular systems.

It is widely used for:

- Molecular dynamics simulations  

- Protein structure analysis  

- Drug discovery and computational chemistry  

- Large-scale parallel simulations  

NAMD is optimized for:

- Parallel execution (MPI)  

- High scalability on HPC clusters  

- CPU and GPU acceleration  

On TEKMER HPC, NAMD is available on compute nodes and can be used for both small-scale and large-scale simulations.

---

## Availability

NAMD is installed on the TEKMER HPC cluster and is available to all authorized users.

It can also be used on:

- Workstations  

- Local Linux environments  

---

## Licensing

NAMD is free for academic and research use.

---

## Platform

- Linux (HPC cluster environment)

---

## Running NAMD on TEKMER HPC

NAMD should be executed via the job scheduler (Slurm).

### Example Slurm Job Script


```bash
#!/bin/bash
#SBATCH -J namd_job
#SBATCH -N 1
#SBATCH -n 16
#SBATCH --time=02:00:00

module load namd

srun namd2 input.conf > output.log
```

###Submit the job:

```bash
sbatch job.sh
```

##Performance Considerations

- Use multiple cores for better performance

- Test small runs before large simulations

- Optimize input configuration files


##Best Practices

- Avoid running NAMD directly on login nodes

- Monitor jobs using squeue

- Store only necessary output data

- Clean temporary files after execution

##Support

For installation, optimization, or usage support:

📧 [contact@performetrica.com](mailto:contact@performetrica.com)

