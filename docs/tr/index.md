[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)
# TEKMER HPC HIZLI BAŞLANGIÇ KILAVUZU

## Kapsam

Bu doküman, TEKMER HPC Kümesine erişim ve iş çalıştırma süreçlerini açıklar.

Şunları kapsamaz:

- Temel Linux kullanımı  
- MPI, OpenMP, CUDA gibi paralel programlama konuları  

Kullanıcıların:

- Temel Linux bilgisine  
- Kullanacakları yazılıma hakim olması beklenir  

---

## HPC Hesabı Alma

TEKMER HPC erişimi kullanıcı portalı üzerinden sağlanır:

👉 <a href="https://tekmer.performetrica.com/" target="_blank" rel="noopener noreferrer">
 TEKMER HPC Portal
</a>

### Adımlar

1. Portal üzerinden kayıt olun (**Online Kayıt**)  
2. E-posta doğrulamasını tamamlayın  
3. Gerekirse onay sürecini bekleyin  
4. HPC hesabınız otomatik oluşturulur  

---

## Önemli Kullanım Kuralları

Yanlış kullanım tüm sistemi olumsuz etkileyebilir.

Kurallara uyulmaması durumunda hesap askıya alınabilir.

### Yapmayın

- Login node üzerinde hesaplama çalıştırmayın  
- Test etmeden büyük işler göndermeyin  
- Kaynakları kötüye kullanmayın  

### Yapın

- Küçük testlerle başlayın  
- Slurm kullanın  
- Job’larınızı takip edin  

---

## Sistem Mimarisi

TEKMER HPC aşağıdaki bileşenlerden oluşur:

- **Login Node** → giriş ve job gönderimi  
- **Compute Node** → hesaplama  
- **Depolama Sistemleri** → paylaşımlı yüksek performanslı disk  

Login node hesaplama için kullanılmaz.

---

## Sisteme Bağlantı

### Windows

SSH istemcisi kullanın:

- MobaXterm  
- PuTTY  

Bağlantı:

**username@login.tekmer.performetrica.com**


### Linux ve macOS


**ssh username@login.tekmer.performetrica.com**


---

## Dosya Sistemi

Giriş yaptığınızda home dizininizdesiniz (`~`).

### Temel Komutlar

```bash
pwd
ls
cd klasor
cd ..
```

### Dosya İşlemleri

```bash
mv dosya1 dosya2
cp dosya1 dizin/
```

---

## Veri Transferi

### Yükleme

```bash
scp dosya username@login.tekmer.performetrica.com:/path/
```

### İndirme

```bash
scp username@login.tekmer.performetrica.com:/path/dosya
```

---

## Dosya Düzenleme

- vi  
- nano  
- emacs  

---

## Yazılım Kullanımı

```bash
module avail
module load <yazilim>
```

Yeni yazılım için portal üzerinden talep oluşturun.

---

## Job Çalıştırma (Slurm)

Tüm işler Slurm üzerinden gönderilmelidir.

### Job Gönderimi

```bash
sbatch job.sh
```

### Komutlar

```bash
squeue
scancel <JOBID>
sinfo
```

---

## Depolama Politikası

- Sistem uzun süreli veri saklama için değildir (30 gün)
- Verilerinizi yedekleyin  
- Gereksiz dosyaları silin  

---

## İyi Uygulamalar

- Küçük testlerle başlayın
- Size tahsis edilen kaynağı seçin  
- Gereksiz I/O işlemlerinden kaçının  
- Dizinlerinizi düzenli tutun  

---

## Destek


📧 [contact@performetrica.com](mailto:contact@performetrica.com)  
🌐 [https://tekmer.performetrica.com/](https://tekmer.performetrica.com/)

