# Slurm İş Gönderim Rehberi (Tekmer HPC)

[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Genel Bakış

Bu doküman, Tekmer HPC kümesinde Slurm kullanarak iş (job) gönderme, izleme ve hata ayıklama süreçlerini açıklar.

---

## Job Script Hazırlama

Örneğin scriptler şu dizinde bulunmaktadır:

**/perf/shared/**

Kopyalayın ve düzenleyin. 

```bash
mkdir -p $HOME/workfolder
cd $HOME/workfolder
cp /perf/shared/example_submit.sh my_experiment.sh
vi my_experiment.sh
```

---

## Job Gönderme

```bash
sbatch my_experiment.sh
```

---

## Minimal Örnek 
(En son geçerli örnekleri **/perf/shared/** klasöründe bulabilirsiniz.)

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

echo "Çalıştığı node: $(hostname)"
```
---

## Temel Komutlar

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

## Tekmer HPC Notları

- Varsayılan partition: defq
- Gereksiz kaynak talep etmeyin
- Output için %x-%j.out kullanın

---

## OpenMP Örneği

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

## MPI Örneği

```bash
#!/bin/bash
#SBATCH --partition=defq
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=8
#SBATCH --time=01:00:00

srun ./my_mpi_program
```
---

## İzleme

```bash
squeue -u $USER
sacct -j <jobid>
```

---

## En İyi Uygulamalar

- ntasks ve cpus-per-task doğru kullanılmalı
- OMP_NUM_THREADS ayarlanmalı
- Toplam süre optimize edilmeli

---

## Yazılım Listesi

```bash
module avail
```

