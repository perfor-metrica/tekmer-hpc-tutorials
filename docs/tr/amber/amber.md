# AmberTools 24.10 Kullanım Kılavuzu

## Genel Bilgiler
AmberTools, bağımsız olarak geliştirilen ve hem kendi başına hem de Amber ile birlikte çalışan araçlardan oluşan bir yazılım paketidir.

Aşağıdaki kullanım senaryoları için uygundur:

- Moleküler dinamik (MD) simülasyonları
- Açık su (explicit solvent) simülasyonları
- Genelleştirilmiş Born (implicit solvent) modelleri

---

## Modül Yükleme

AmberTools modülünü kullanmadan önce bağımlılıkları yüklemeniz gerekir:

```bash
ml GCC/13.3.0 OpenMPI/5.0.3 AmberTools
```

---

## Kurulum Doğrulama

```bash
sander --version
which tleap
which parmchk2
which gem.pmemd
```

Beklenen çıktılar:

- sander: Version 24.0
- tleap: /perf/papps/AmberTools/24.10-gompi-2024a/bin/tleap
- parmchk2: /perf/papps/AmberTools/24.10-gompi-2024a/bin/parmchk2
- gem.pmemd: /perf/papps/AmberTools/24.10-gompi-2024a/bin/gem.pmemd

---

## Kurulum Detayları

- Sürüm: AmberTools 24.10
- sander sürümü: 24.0
- Derleyici: GCC 13.3.0
- MPI: OpenMPI 5.0.3
- Kurulum yolu: /perf/papps/AmberTools/24.10-gompi-2024a

---

## Temel Bileşenler

- tleap: Sistem hazırlama (topoloji ve koordinat dosyaları)
- parmchk2: Parametre kontrol ve oluşturma
- sander: CPU tabanlı MD motoru
- pmemd / gem.pmemd: Optimize edilmiş MD motorları

---

## Örnek Kullanım

### Sistem Hazırlama (tleap)

```bash
tleap -f leap.in
```

### Parametre Kontrolü

```bash
parmchk2 -i ligand.mol2 -f mol2 -o ligand.frcmod
```

### MD Çalıştırma (sander)

```bash
sander -O -i md.in -p topol.prmtop -c input.inpcrd -o md.out -r md.rst -x md.nc
```

---

## Slurm Örneği

```bash
#!/bin/bash
#SBATCH -J amber_job
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

ml GCC/13.3.0 OpenMPI/5.0.3 AmberTools

export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK}

echo "Job started on $(hostname)"
echo "Node list: $SLURM_JOB_NODELIST"
echo "CPUs per task: $SLURM_CPUS_PER_TASK"
echo "Start time: $(date)"

srun sander -O \
  -i md.in \
  -p topol.prmtop \
  -c input.inpcrd \
  -o md.out \
  -r md.rst \
  -x md.nc

echo "End time: $(date)"
```

---

## Performans İpuçları

- Küçük testlerle başlayın
- CPU kullanımını `--cpus-per-task` ile kontrol edin
- MPI gerekiyorsa paralel sürümleri kullanın
- Disk I/O performansını izleyin

---

## Log Analizi

```bash
grep "NSTEP" md.out
```

---

## Notlar

- Login node üzerinde çalıştırmayın
- Çalışma dizininde yeterli disk alanı olduğundan emin olun

