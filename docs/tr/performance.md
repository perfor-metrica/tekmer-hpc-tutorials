# HPC Performans Optimizasyon İpuçları (Slurm Tabanlı İş Yükleri)

[![Documentation Status](https://readthedocs.org/projects/su-hpc-tutorials/badge/?version=latest)](https://su-hpc-tutorials.readthedocs.io/en/latest/?badge=latest)

---

## Genel Bakış

Yüksek Başarımlı Hesaplama (HPC) ortamlarında performans iki temel faktöre bağlıdır:

1. Uygulamanın **çalışma süresi**
2. İşin başlatılana kadar **kuyrukta bekleme süresi**

Sadece hızlı çalışan bir uygulama yeterli değildir; uzun süre kuyrukta bekleyen iş de verimsizdir.

Kodun doğru çalışmasından sonra **performans optimizasyonu en kritik adımdır**.

---

## Temel Kavramlar

HPC performansı, iş yükünüzün donanımla ne kadar uyumlu olduğuna bağlıdır:

- Aynı cache’i paylaşan task’ler → **düşük gecikme**
- Bellek yoğun işler → **NUMA farkındalığı kritik**
- Yanlış yerleşim → **CPU ve bellek kaynaklarının verimsiz kullanımı**

Bu davranışlar **Slurm scheduler parametreleri ile kontrol edilir**.

---

## Kapsam

> Bu doküman yalnızca **Linux batch (Slurm) işleri** için geçerlidir.

---

## 1. Uygulama Tipini Belirleyin

Öncelikle uygulamanızın türünü belirleyin:

- **Tek thread (single-thread)**
- **Multi-thread (OpenMP, shared memory)**
- **Dağıtık (MPI)**

Yanlış sınıflandırma = yanlış kaynak kullanımı.

---

## 2. Multi-thread (Shared Memory) Uygulamalar

Multi-thread uygulamalarda en kritik nokta:

👉 Thread’leri aynı CPU/socket içinde tutmak

### Avantajları:
- Cache locality artar
- NUMA gecikmesi azalır
- Bellek bant genişliği daha verimli kullanılır

---

### Örnek: Tek CPU üzerinde 24 core kullanımı

#### Komut satırı:

```bash

--ntasks=1 --cpus-per-task=24
```

####Batch script:

```bash
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=24
```

####Dikkat

Büyük kaynak talebi → daha uzun queue bekleme süresi

###Ölçekleme

Eğer uygulamanız iyi ölçekleniyorsa:

```bash
--cpus-per-task=N
```

arttırılabilir.

Slurm davranışı:

Önce aynı socket içindeki core’ları doldurur

Sonra diğer socket’e geçer.

##3. Kritik Pratik Ayarlar
###3.1 CPU Binding 

```bash
#SBATCH --cpu-bind=cores
```

Alternatif:

```bash
#SBATCH --hint=nomultithread
```

Amaç:

Thread’lerin farklı core’lara sabitlenmesi

Scheduler jitter ve migration engelleme

###3.2 Thread Sayısını Eşitleyin

```bash
export OMP_NUM_THREADS=24
```

Slurm ile uygulama uyuşmazsa:

→ CPU boşa gider

→ Performans düşer

###3.3 Oversubscription’dan Kaçının

Yanlış:

```bash
--ntasks=24 --cpus-per-task=24
```

Bu durumda:
→ 576 CPU talep ediyorsunuz

Doğru:

```bash
--ntasks=1 --cpus-per-task=24
```

###4. Bu Yöntemi Ne Zaman Kullanmayın

Aşağıdaki durumlarda kullanmayın:

- MPI uygulamaları

- Bağımsız task’ler (embarrassingly parallel)

- Multi-node workload

Bunun yerine:

```bash
--ntasks=N
```

kullanın.

## 5. Performans vs Kuyruk Süresi

| Strateji                      | Sonuç                                  |
|------------------------------|----------------------------------------|
| Büyük kaynak (çok core)      | Hızlı runtime, uzun bekleme            |
| Küçük kaynak                 | Hızlı başlama, uzun runtime            |

Gerçek optimizasyon:

👉 Toplam turnaround time = queue + runtime


