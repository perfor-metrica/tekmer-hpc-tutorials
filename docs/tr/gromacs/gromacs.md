# GROMACS 2025.4 Kullanım Kılavuzu

## Genel Bilgi
GROMACS, biyomoleküler simülasyonlar için kullanılan yüksek performanslı bir yazılımdır.

Aşağıdaki işlemler için optimize edilmiştir:

- MPI paralelleştirme

- OpenMP thread kullanımı

- SIMD (AVX)

TEKMER HPC üzerinde:

- MPI: OpenMPI 5.0.3

- OpenMP: aktif (128 thread’e kadar)

- FFT: FFTW 3.3.10

Çalıştırılabilir dosya:
`/perf/papps/GROMACS/2025.4-gompi-2024a/bin/gmx_mpi`

---

## Modül Yükleme

```bash
ml GROMACS/2025.4-gompi
```

---

## Kurulum Doğrulama

```bash
gmx --version
gmx_mpi --version
```

---

## Build Detayları

- Versiyon: 2025.4
- Precision: Mixed
- SIMD: AVX_256
- Compiler: GCC 13.3.0
- MPI: OpenMPI 5.0.3

---

## Çalışma Modları

### Hybrid (MPI + OpenMP)

```bash
gmx_mpi mdrun -ntmpi 4 -ntomp 4 -s topol.tpr
```

### Sadece OpenMP

```bash
gmx mdrun -ntomp 8 -s topol.tpr
```

### Sadece MPI

```bash
gmx_mpi mdrun -ntmpi 16 -ntomp 1 -s topol.tpr
```

---

## Slurm Örneği

```bash
#!/bin/bash
#SBATCH -J gromacs_job
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

ml GROMACS/2025.4-gompi

export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK}

echo "Job started on $(hostname)"
echo "Node list: $SLURM_JOB_NODELIST"
echo "Start time: $(date)"

srun gmx_mpi mdrun -ntomp ${OMP_NUM_THREADS} -s topol.tpr -deffnm md

echo "End time: $(date)"

```

---

## Performans Önerileri

- `ntmpi × ntomp = toplam CPU` olacak şekilde ayarlayın
- Küçük testlerle başlayın
- Gereksiz kaynak istemeyin
- Hybrid kullanım genelde en iyi sonucu verir
- `squeue` ile izleyin

---

## Log Analizi

```bash
grep Performance *.log
```

---

## Notlar

- Login node üzerinde çalıştırmayın

