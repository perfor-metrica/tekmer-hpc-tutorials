[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)
# MATLAB (Türkçe)

## Genel Bilgi

MATLAB, aşağıdaki alanlarda kullanılan yüksek seviyeli bir programlama ve sayısal hesaplama ortamıdır:

- Matematiksel modelleme ve simülasyon  
- Veri analizi ve görselleştirme  
- Algoritma geliştirme  
- Mühendislik ve bilimsel hesaplamalar  

TEKMER HPC üzerinde MATLAB şu modlarda kullanılabilir:

- **Etkileşimli mod** (test ve geliştirme)  

- **Batch mod** (Slurm ile büyük işler)  

- **Paralel mod** (Parallel Computing Toolbox ile)  

---

## Kurulum / Yardım

Detaylı kurulum ve kullanım dokümanına Kurulum Eğitimi tabından veya buradan ulaşabilirsiniz:

👉 https://tekmer-hpc-tutorials.readthedocs.io/en/latest/matlab/pdf/matlab-tutorial.pdf

İçerik:

- Windows kurulum  

- macOS kurulum  

- Linux kurulum  

- HPC kullanım örnekleri  

Destek için:  
📧 [contact@performetrica.com](mailto:contact@performetrica.com)  

---

## Minimum Sistem Gereksinimleri

| İşletim Sistemi | Mimari | RAM |
|----------------|--------|-----|
| Windows        | 64-bit | 4 GB |
| macOS          | 64-bit | 4 GB |
| Linux          | 64-bit | 4 GB |

---

## TEKMER HPC Üzerinde MATLAB Kullanımı

### MATLAB Yükleme

```bash
module load matlab
Etkileşimli Çalıştırma (sadece kısa testler için)
matlab
```

⚠️ Login node üzerinde yoğun hesaplama çalıştırmayınız.

###Batch Job (Önerilen)

Örnek Slurm script:

```bash
#!/bin/bash
#SBATCH -J matlab_job
#SBATCH -N 1
#SBATCH -n 4
#SBATCH --time=01:00:00

module load matlab

matlab -nodisplay -r "my_script; exit"
```

Gönderim:

```bash
sbatch job.sh
```
###Paralel Hesaplama

MATLAB paralel çalışmayı destekler:

- Parallel Computing Toolbox

- parpool / parfor

- Dağıtık işler

###Örnek:

```bash
parpool(4);
parfor i=1:100
    A(i) = heavy_function(i);
end
```

###Toolbox Bilgisi

Mevcut toolbox’lardan bazıları:

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

(Lisansa bağlı olarak değişebilir.)

###Kullanım Politikası

MATLAB lisanslı bir yazılımdır

Paralel kullanım lisans ile sınırlı olabilir

Aşırı kaynak kullanımı durumunda job durdurulabilir

TEKMER HPC kullanım politikalarına uyulmalıdır

###Kurulu Sistemler

MATLAB, TEKMER HPC kümesinde kuruludur.

Kurum geneli erişim talepleri için:
📧 [contact@performetrica.com](mailto:contact@performetrica.com)  

###Sağlayıcı

MathWorks Inc.

###Desteklenen Platformlar

Windows

Linux

macOS
