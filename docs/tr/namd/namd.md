[![Documentation Status](https://readthedocs.org/projects/performetrica-hpc-tutorials/badge/?version=latest)](https://performetrica-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

# NAMD (Türkçe)

## Genel Bilgi

NAMD (Nanoscale Molecular Dynamics), büyük biyomoleküler sistemlerin simülasyonu için geliştirilmiş yüksek performanslı bir yazılımdır.

Aşağıdaki alanlarda yaygın olarak kullanılır:

- Moleküler dinamik simülasyonları  

- Protein yapı analizi  

- İlaç geliştirme ve hesaplamalı kimya  

- Büyük ölçekli paralel hesaplamalar  

NAMD şu özellikler için optimize edilmiştir:

- Paralel çalışma (MPI)  

- HPC kümelerinde yüksek ölçeklenebilirlik  

- CPU ve GPU hızlandırma  

Performetrica HPC üzerinde NAMD compute node’lar üzerinde çalıştırılır ve hem küçük hem de büyük ölçekli simülasyonlar için uygundur.

---

## Erişim

NAMD, Performetrica HPC kümesinde kurulu olup yetkili tüm kullanıcıların erişimine açıktır.

Ayrıca:

- İş istasyonlarında  

- Yerel Linux ortamlarında  

kullanılabilir.

---

## Lisans

NAMD akademik ve araştırma amaçlı kullanım için ücretsizdir.

---

## Platform

- Linux (HPC ortamı)

---

## Performetrica HPC Üzerinde NAMD Kullanımı

NAMD işlemleri Slurm job scheduler üzerinden çalıştırılmalıdır.

### Örnek Slurm Script

```bash
#!/bin/bash
#SBATCH -J namd_job
#SBATCH -N 1
#SBATCH -n 16
#SBATCH --time=02:00:00

module load namd

srun namd2 input.conf > output.log
```

### Gönderim:

```bash
sbatch job.sh
```

##Performans Önerileri

- Daha iyi performans için çok çekirdek kullanın

- Büyük job’lardan önce küçük testler yapın

- Input dosyalarını optimize edin


## İyi Uygulamalar

- Login node üzerinde çalıştırmayın

- squeue ile job’ları izleyin

- Gereksiz çıktı dosyalarını silin

- Geçici dosyaları temizleyin

## Destek

Kurulum, kullanım ve optimizasyon desteği için:

📧 [contact@performetrica.com](mailto:contact@performetrica.com)  
