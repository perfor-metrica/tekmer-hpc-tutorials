# Performetrica HPC Üzerinde TensorFlow

[![Documentation Status](https://readthedocs.org/projects/performetrica-hpc-tutorials/badge/?version=latest)](https://performetrica-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Genel Bakış

TensorFlow, Google tarafından geliştirilen açık kaynaklı bir makine öğrenmesi kütüphanesidir.

Kullanım alanları:

- Derin öğrenme (CNN, RNN, Transformer)
- Model eğitimi ve çıkarım (inference)
- GPU hızlandırmalı hesaplama

---

## Performetrica HPC Üzerinde Kullanım

TensorFlow, Performetrica HPC kümesinde module sistemi üzerinden kullanılabilir.

Mevcut sürümleri görmek için:

    module avail tensorflow

Yüklemek için:

    module load TensorFlow

---

## Önerilen Kullanım

TensorFlow işleri genellikle:

- GPU node'larda (eğitim için)
- CPU node'larda (küçük işler için)

çalıştırılmalıdır.

---

## Örnek: CPU Üzerinde Çalıştırma

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

## Performans Önerileri

- CPU thread sayısını ayarlayın:
```bash
      export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
```
- Oversubscription yapmayın
- Bellek kullanımını izleyin

---

## Sağlayıcı

Google

---

## Lisans

Apache License 2.0 (Açık Kaynak)

