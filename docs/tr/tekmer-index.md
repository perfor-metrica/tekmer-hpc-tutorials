# Tekmer HPC – Erişim ve Sistem Genel Bilgileri

[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Tekmer HPC'ye Erişim

### Yerel ağdan erişim
```bash
ssh <kullanıcı_adı>@login.tekmer.performetrica.com
```

### Dış ağdan erişim
```bash
ssh <kullanıcı_adı>@login.tekmer.performetrica.com
```

---

## Sistem Genel Bakış

Tekmer HPC, CPU tabanlı bir yüksek başarımlı hesaplama kümesidir.

Kullanım alanları:

- Bilimsel hesaplama
- Paralel işler (MPI / OpenMP)
- Simülasyon ve veri işleme

---

## Kaynakları Görüntüleme

Node ve partition listesi:

```bash
sinfo --long --Node "%#N %.6D %#P %6t"
```

Detaylı node bilgisi:

```bash
scontrol show node <node>
```

---

## CPU Özellikleri

Performans CPU özelliklerine bağlıdır:

- AVX / AVX2 / AVX-512
- FMA
- SIMD
- NUMA mimarisi

Kontrol etmek için:

```bash
lscpu
```

---

## Performans Optimizasyonu

### 1. İş tipini doğru seçin

- OpenMP → shared memory
- MPI → distributed

---

### 2. CPU Binding

```bash
#SBATCH --cpu-bind=cores
```

---

### 3. NUMA Farkındalığı

- Thread’leri aynı socket içinde tutun
- Cross-socket erişimden kaçının

---

### 4. Thread Ayarı

```bash
export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
```

---

### 5. Bellek Kullanımı

- Gerektiği kadar isteyin
- Fazla bellek → uzun queue süresi

---

### 6. I/O Optimizasyonu

- Mümkünse `/tmp` kullanın
- Küçük sık yazımlardan kaçının

---

## İş Tipleri

| İş Tipi | Slurm Ayarı |
|--------|------------|
| Serial | ntasks=1 |
| OpenMP | cpus-per-task=N |
| MPI    | ntasks=N |

---

## Örnek Job

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

## Referanslar

- https://slurm.schedmd.com/

