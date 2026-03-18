# İletişim ve Destek

TEKMER HPC hizmetleri ile ilgili aşağıdaki konularda destek almak için:

- Sistem kullanımı
- Teknik destek
- Paralel programlama desteği
- Performans optimizasyonu
- Yazılım kurulum talepleri
- Hata ve problem bildirimi

Lütfen aşağıdaki adres ile iletişime geçiniz:

📧 **[contact@performetrica.com](mailto:contact@performetrica.com)**

---

## Destek Kapsamı

Destek ekibi aşağıdaki konularda yardımcı olabilir:

- Slurm job gönderim problemleri

- Yazılım ve modül kullanımı

- Çalışma zamanı hatalarının analizi

- Performans iyileştirme (CPU, bellek, I/O)

- Paralelleştirme yöntemleri (MPI, OpenMP)

- Ortam (environment) yapılandırması

---


## Destek Talebi Öncesi

Destek talebi oluşturmadan önce:

- [**SSS (FAQ)**](faq.md) bölümünü inceleyiniz

- İlgili [**dokümantasyon ve eğitimleri**](tekmer-index.md) kontrol ediniz

- Job çıktılarınızı ve hata loglarını gözden geçiriniz

Birçok yaygın problem bu kaynaklarda açıklanmıştır.

---

## Problem Bildirimi

Hızlı ve doğru destek alabilmek için aşağıdaki bilgileri mutlaka ekleyiniz:

### Gerekli Bilgiler
- Kullanıcı adınız
- Problemin oluştuğu tarih ve saat
- Kullanılan login veya compute node (varsa)

### Job Bilgileri
- Job ID (Slurm kullanıldıysa)
- Job scripti (`sbatch` / `srun`)
- Çalıştırılan komut veya uygulama

### Hata Bilgileri
- Tam hata mesajı (kopyala-yapıştır, ekran görüntüsü değil)
- Çıktı ve hata dosyaları (`.out`, `.err`)

### Dosya ve Dizin Bilgileri
- Aşağıdakilerin tam yolları:
  - Girdi dosyaları
  - Script dosyaları
  - Çıktı dizinleri

---

## İyi ve Kötü Örnek

**Kötü:**
> İş çalışmıyor.

**İyi:**
> Kullanıcı: user01  
> Job ID: 123456  
> Komut: sbatch run.sh  
> Hata: "MPI_Init failed"  
> Çıktı dosyası: /perf/defq/user01/job.out  

---

## Yanıt Süresi

- İlk geri dönüş genellikle **1 iş günü içinde** yapılır
- Karmaşık problemler daha uzun sürebilir
- Ek bilgi veya log talep edilebilir

---

## En İyi Uygulamalar

Daha hızlı destek almak için:

- Tekrarlanabilir (reproducible) örnekler sağlayın

- Büyük işlerden önce küçük testler yapın

- Job scriptlerinizi düzenli ve açıklamalı tutun

- Desteklenen yazılım ve modülleri kullanın

---

## Ek Destek Kanalları

- Ticket sistemi: [tekmer.performetrica.com](https://tekmer.performetrica.com/)
- Telefon 

