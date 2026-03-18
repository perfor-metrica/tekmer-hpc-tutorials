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
#SBATCH -N 1
#SBATCH --ntasks=4
#SBATCH --cpus-per-task=4
#SBATCH --time=04:00:00

ml GROMACS/2025.4-gompi

export OMP_NUM_THREADS=4

srun gmx_mpi mdrun -ntmpi 4 -ntomp 4 -s topol.tpr -deffnm md
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
grep Performance md.log
```

---

## Notlar

- Login node üzerinde çalıştırmayın

