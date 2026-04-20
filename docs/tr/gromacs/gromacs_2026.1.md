# GROMACS 2026.1 Kullanım Kılavuzu

## Genel Bilgiler
GROMACS, biyomoleküler simülasyonlar için tasarlanmış yüksek performanslı bir moleküler dinamik (MD) yazılımıdır.

Aşağıdaki teknolojiler için optimize edilmiştir:

- MPI paralelliği
- OpenMP thread kullanımı
- SIMD vektörizasyonu (AVX)

TEKMER HPC üzerinde:

- MPI: OpenMPI 5.0.3
- OpenMP: Etkin (maksimum 128 thread)
- FFT: FFTW 3.3.10

Çalıştırılabilir dosya yolu:
`/perf/papps/GROMACS/2026.1-gompi-2024a/bin/gmx_mpi`

---

## Modül Yükleme

```bash
ml GROMACS/2026.1-gompi
```

---

## Kurulum Doğrulama

```bash
gmx --version
gmx_mpi --version
```

---

## Derleme Detayları

- Sürüm: 2026.1
- Hassasiyet: Mixed
- Bellek modeli: 64-bit
- SIMD: AVX_256
- Derleyici: GCC 13.3.0
- MPI: OpenMPI 5.0.3
- OpenMP: Etkin (maksimum 128 thread)
- GPU: Devre dışı
- FFT: FFTW 3.3.10 (CPU)
- PLUMED: Etkin
- Colvars: Etkin

---

## Çalıştırma Modları

### Hibrit MPI + OpenMP

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

ml GROMACS/2026.1-gompi

export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK}

echo "Job started on $(hostname)"
echo "Node list: $SLURM_JOB_NODELIST"
echo "Start time: $(date)"

srun gmx_mpi mdrun -ntomp ${OMP_NUM_THREADS} -s topol.tpr -deffnm md

echo "End time: $(date)"
```

---

## Performans İpuçları

- ntmpi × ntomp = toplam çekirdek sayısı olmalı
- Küçük testlerle başlayın
- Aşırı kaynak tahsisinden kaçının
- En iyi performans için hibrit modu kullanın
- squeue ile izleme yapın

---

## Loglar

```bash
grep Performance *.log
```

---

## Notlar

- Bu derlemede GPU desteği yoktur
- Login node üzerinde çalıştırmayın

