# SoftITo Veri Analitiği - 1. Hafta Notları

Bu döküman, SoftITo Veri Analitiği eğitiminin 1. haftasında işlenen veri mimarisi temellerini, Python programlamaya girişi ve NumPy kütüphanesi ile çok boyutlu veri analizini içermektedir.

---

## 1. Gün: Veri Dünyasına Giriş ve Roller (12 Ekim 2026)

### Temel Kavramlar ve Roller
* **Data Architect / Data Engineer:** Veri kaynaklarından (Sources) veriyi alıp pipeline (veri boru hattı) inşa eden (Build) rollerdir.
* **Solution Developer:** Çözüm geliştirici.
* **Supervisor:** Çalışanlardan ve çalışma alanından sorumlu olan, işleyişin kurallara uygun olmasını denetleyen kişidir.
* **Abstraction (Soyutlama):** Karmaşık ayrıntılardan kaçınarak konuyu veya sistemi temele indirgeme işlemidir.
* **Tabular Data:** Satırlardan ve sütunlardan oluşan, bir ızgara (grid) şeklinde organize edilmiş bilgidir.

### Veri Sistemi Mimarisi (Data System)
Verinin sistemdeki yolculuğu temel olarak 3 aşamadan oluşur:
1. **Bronze (Ingest):** Verinin kaynaklardan ham haliyle sisteme alındığı ilk katman.
2. **Silver (Clean):** Verinin temizlendiği, düzenlendiği ve standartlaştırıldığı orta katman.
3. **Gold (Model):** Verinin iş modellerine göre modellendiği, analize tam anlamıyla hazır olduğu son katman.

### Data Analyst (Veri Analisti) Rolü ve Konumu
* Veri analisti, veri sistemindeki **Gold (Model)** katmanından beslenir.
* Temel araçlarından biri **SQL**'dir.
* Analistin ana odak noktası **Manage & Report** (Yönetmek ve Raporlamak) adımlarıdır.

---

## 2. Gün: Veri Mimarisi ve ML Kavramları (13 Ekim 2026)

### Makine Öğrenmesi (ML) Kavramları
* **Predict (Tahmin Etme):** Karar verme olayı. Veriye dayanarak bir sonucun ne olacağını öngörmek.
* **Data Scientists (Veri Bilimciler):** Daha iyi bir veri için daha çok donanımsal alanla ilgilenirler.
* **ML Engineer (Makine Öğrenmesi Mühendisi):** Biraz daha yazılım ve altyapı ağırlıklı ile ilgilenir.

### Versiyonlama ve Sistem Terimleri
* **Stable (Kararlı):** Versiyonun test edilmiş, hatasız ve güvenilir şekilde çalışan hali.
* **Deprecated (Kullanımdan Kaldırılmış):** Terk edilmek üzere olan, geliştirilmesi durdurulmuş, yakında geçerliliğini yitirecek olan versiyon.
* **Legacy (Eski Sistem):** Çok iyi fonksiyonları olan ama güncellenmeyen, geliştirilme süreci durmuş olan eski dosya/sistem.

### Dosya Uzantıları ve Formatları
* **.ipynb:** Jupyter Notebook dosyası formatı (Genelde JSON tabanlı çalışır).
* **.py:** Python betik (script) dosyası (Genelde text tabanlı çalışır).
* **Path:** Dosya adresi / Yolu.

---

## 3. Gün: Python Temelleri, Veri Yapıları ve İleri Seviyeye Giriş (14 Ekim 2026)

### 1. Geliştirme Ortamı ve Değişkenler
* Kod yazmak ve veri analizlerini test edebilmek için **Jupyter Notebook** ortamı kuruldu.
* **Değişkenler (Variables):** Değerleri saklamak için ayrılmış bellek alanlarıdır. Python değişkenin tipini otomatik algılar.

### Temel Veri Tipleri (Data Types) ve Dönüşümler
Python'da kullanılan temel veri türleri şunlardır:
1. **Integer (Tam Sayı):** `a = 4`
2. **Float (Ondalıklı):** `b = 5.6`
3. **String (Metin):** `x = 'M'` veya `y = "MHM"`
4. **Boolean (Mantıksal):** `x = True` veya `y = False`
5. **Complex (Karmaşık Sayı):** `x = 4+5j`

* **Tip Dönüşümleri (Type Conversions):** Elimizdeki veriyi başka bir tipe dönüştürmek için `float(x)`, `str(x)` veya `bool(x)` gibi fonksiyonlar kullanılır.

### 2. Python Veri Yapıları (Data Structures)
Algoritmik düşüncede veriyi tutma şeklimiz çok önemlidir. Python'da 4 temel veri yapısı işlendi:

* **Tuple (Demet):** `a = (1, 2, 3, 4)` veya parantezsiz `a = 1, 2, 3, 4` şeklinde tanımlanır. İçeriği değiştirilemeyen (immutable) veri yapısıdır.
* **List (Liste):** `a = [1, 2, 3, 4]` şeklinde köşeli parantezle tanımlanır. Sıralıdır ve elemanları daha sonradan değiştirilebilir (mutable).
* **Set (Küme):** `a = {1, 2, 3, 4, 4}` şeklinde süslü parantezle tanımlanır. Matematikteki kümeler gibidir, tekrarlayan (mükerrer) eleman barındırmaz.
* **Dictionary (Sözlük):** `a = {1: 2, 2: 3}` şeklinde tanımlanır. Verileri Anahtar-Değer (Key-Value) çiftleri halinde tutar. Elemanlara indeks numarasıyla değil, anahtar kelimeyle (örn: `a[1]`) erişilir.

### 3. Faydalı Fonksiyonlar ve Kavramlar
* **`range()` Fonksiyonu:** Belirli bir aralıkta sayılar üretmek için kullanılır. Örneğin `range(6)` ile 0'dan 5'e kadar sayılar üretilir. Bu sayılar doğrudan listeye (`list(range(5))`), demete (`tuple(range(5))`) veya kümeye (`set(range(5))`) dönüştürülebilir.
* **Keywords (Anahtar Kelimeler):** Python'un kendi işleyişi için rezerve ettiği kelimelerdir (örn: `None`). Bu kelimeler değişken adı olarak kullanılamaz. Bir kelimenin rezerve edilip edilmediği `import keyword` kütüphanesi kullanılarak `keyword.iskeyword('None')` fonksiyonu ile kontrol edilebilir.

### 4. İleri Seviye Python'a (Advanced Python) Giriş
Günün sonuna doğru ve 4. güne sarkan bölümde, daha ileri seviye Python kütüphanelerine ve dosya okuma işlemlerine giriş yapıldı:
* **Multithreading (Eşzamanlı İşlemler):** Programın farklı parçalarının aynı anda (eşzamanlı) çalışmasını sağlayarak tasarımı basitleştirmek için `import threading` modülü işlendi. `threading.active_count()`, `threading.current_thread()` gibi fonksiyonlar incelendi.
* **CSV Dosyası İşlemleri:** Dışarıdan bir veri setini (`Singapore_Residents.csv`) Python'a aktarmak için standart `import csv` kütüphanesi ile okuma yapıldı.

---

# 4. Gün Notları - Veri Bilimi Ekosistemi ve NumPy Kütüphanesine Giriş (15 Ekim 2026)

Bugün Advanced Python (İleri Python) konularını tamamlayarak Veri Bilimi için Python kütüphaneleri ekosistemine ve çok boyutlu veri manipülasyonu sağlayan NumPy kütüphanesine (`import numpy as np`) giriş yaptık.

## Veri Bilimi İçin Python Kütüphaneleri (Data Science Ecosystem)
Veri bilimi süreçleri ve bu süreçlerde kullanılan temel kütüphaneler şu şekildedir:
* **Extract, Transform, Load (ETL):** pandas, BeautifulSoup, Intake.
* **Data Exploration (Veri Keşfi):** Seaborn, matplotlib.
* **Data Evaluation (Veri Değerlendirme):** NumPy, TensorFlow.
* **Data Modeling (Veri Modelleme):** scikit-learn, SciPy, statsmodels (SM).
* **Data Presentation (Veri Sunumu):** matplotlib, HoloViews, VisPy.

## NumPy Dizileri (Arrays) Oluşturma ve Veri Türleri
Python listelerini doğrudan işlemek yerine hız ve esneklik kazanmak için NumPy dizilerine dönüştürürüz:
* **Listeden Diziye Çevirme:** `np.array(liste_adi)` kullanılarak standart bir Python listesi (örneğin bir Sudoku matrisi) NumPy dizisine dönüştürülür.
* **Sentetik Dizi Oluşturma:** Büyük verilerle çalışmadan önce kodları test etmek için `np.arange()` (belirli aralıklarda dizi oluşturma) veya `np.zeros()` (sıfırlarla dolu dizi oluşturma) gibi fonksiyonlar kullanılır.
* **Veri Tipi Öğrenme (`.dtype` & `type()`):** Standart Python türlerinden (`int`, `float`) farklı olarak NumPy, belleği daha verimli kullanmak için `np.int64`, `np.float32` gibi detaylı tipler sunar. Bir dizinin içindeki elemanların tipini `.dtype` ile, nesnenin kendi tipini ise `type()` ile öğreniriz.

## 2B ve 3B Dizilerde Boyut (Axis) ve Şekil (Shape) Kavramı
Matris yapılarında işlem yaparken eksenlerin (axis) yönünü ve dizinin şeklini bilmek kritik önem taşır:
* **.shape Özniteliği:** Dizinin boyutlarını (satır, sütun, derinlik) verir. Örneğin; `(675, 843, 3)` çıktısı 675 satır, 843 sütun ve 3 renk kanalından (RGB) oluşan bir resmi temsil eder.
* **Birinci Boyut (Axis 0):** Satırları temsil eder (Yukarıdan aşağıya doğru).
* **İkinci Boyut (Axis 1):** Sütunları temsil eder (Soldan sağa doğru).
* **Üçüncü Boyut (Axis 2):** Derinliği (örneğin RGB renk kanallarını) temsil eder.

## NumPy ile Veri Manipülasyonu Fonksiyonları
* **`np.split()` ile Bölme:** Çok boyutlu bir diziyi alt dizilere ayırır. Örneğin, bir RGB resim matrisini kırmızı, yeşil ve mavi kanallarına ayırmak için `axis=2` argümanı kullanılır.
* **`np.where()` ile Filtreleme ve Koşullu Değiştirme:** 
  * Belirli bir koşulu sağlayan verilerin **indekslerini** bulur (Örn: `np.where(agac_verisi[:, 1] == 313879)`).
  * Koşula bağlı **değer değiştirme** işlemi yapar. Örneğin, `np.where(blue_array > blue_array.mean(), 255, blue_array)` kodu ile ortalamadan büyük olan piksel değerleri 255 (maksimum mavi) ile değiştirilerek vurgulanır.
* **`np.delete()` ile Silme:** Eksen belirtilmezse çok boyutlu dizi tek boyuta indirgenir ve belirtilen indeks silinir. `axis=1` verilirse o indeksteki sütun tamamen silinir.
* **`.reshape()` ile Yeniden Şekillendirme:** Dizilerin satır ve sütun sayılarını değiştirmek için kullanılır. Farklı dizileri birleştirebilmek için şekillerinin uyumlu olması gerekir.
* **`np.stack()` ile İstifleme (Birleştirme):** Şekilleri aynı olan farklı dizileri (örneğin Red, Green ve Blue dizilerini) üst üste koyarak tek bir çok boyutlu dizi oluşturur.

## Veri Görselleştirmeye İlk Bakış: Matplotlib
Matplotlib kütüphanesi (`import matplotlib.pyplot as plt`) kullanılarak temel görselleştirmeler yapılabilir:
* **`plt.scatter(x, y)`:** x ve y eksenlerindeki değerleri kullanarak dağılım (scatter) grafiği oluşturur.
* **`plt.imshow(dizi)`:** İstiflenmiş (stack) çok boyutlu dizi verilerini (RGB gibi) bir resim olarak ekrana basmak için hazırlanır.
* **`plt.show()`:** Arka planda çizilen grafiği veya resmi ekranda göstermek için kullanılır.

---
## 5. Gün: Dizi Matematiği, Görüntü Manipülasyonu ve Pandas'a Giriş (16 Ekim 2026)

Bugün sabah oturumunda NumPy dizileri üzerinde matematiksel özetlemeler, dizi dilimleme ve görüntü (RGB) matrisleri manipülasyonu işlendi; öğleden sonra ise dikdörtgensel (tabular) veri yapıları ve Pandas kütüphanesine giriş yapıldı.

### 1. NumPy: Veri Toplulaştırma (Aggregation) ve Eksen (Axis)
Büyük veri setlerini özetlemek için NumPy fonksiyonları kullanılır:
* **Temel Metotlar:** Verileri özetlemek için `.sum()`, `.min()`, `.max()`, `.mean()` ve `.cumsum()` fonksiyonları kullanılır[span_0](start_span)[span_0](end_span).
* **Genel Toplam:** Bir matrise eksen belirtilmeden `.sum()` uygulandığında matristeki tüm elemanların genel toplamı elde edilir[span_1](start_span)[span_1](end_span).
* **Eksen Belirterek Toplama (`axis=1`):** `security_breaches.sum(axis=1)` kodu, satırlar boyunca toplama yaparak 1 boyutlu (1D) bir dizi döndürür[span_2](start_span)[span_2](end_span).
* **Boyut Koruma (`keepdims=True`):** İşlem sonucunda matrisin orijinal boyut yapısını kaybetmemek (örneğin 2D sütun matrisi olarak kalmasını sağlamak) için `keepdims=True` parametresi kullanılır[span_3](start_span)[span_3](end_span).

### 2. NumPy: Vektörleştirilmiş İşlemler ve Dizi Yığma
* **Vektörleştirilmiş İşlemler (Vectorization):** Python'daki yavaş döngüler yerine tüm dizi üzerinde aynı anda matematiksel işlem yapmayı sağlar[span_4](start_span)[span_4](end_span).
* **Dizileri Yığma (Stacking):** Farklı matrisler birleştirilerek daha büyük yapılar oluşturulabilir. Örneğin iki adet 3x3 matris yan yana birleştirilerek 3x6 boyutunda yeni bir matris elde edilir[span_5](start_span)[span_5](end_span).

### 3. NumPy: Dilimleme (Slicing) ve Görüntü İşleme
Görseller bilgisayarda satır, sütun ve renk kanallarından (RGB) oluşan matrisler olarak tutulur:
* **Renk Kanallarını Dilimleme:** 3 boyutlu bir `rgb` dizisinden belirli renk kanallarını izole etmek için `:` operatörü kullanılır[span_6](start_span)[span_6](end_span). (Örn: Kırmızı kanal için `red_array = rgb[:, :, 0]`)[span_7](start_span)[span_7](end_span).
* **Görüntüyü Çevirme (`np.flip`):** Görseli geometrik olarak tamamen ters çevirir[span_8](start_span)[span_8](end_span). Eğer eksen belirtilirse (`np.flip(logo, axis=2)`) görselin geometrisi bozulmadan yalnızca renk kanallarının sırası tersine çevrilerek renk paleti değiştirilir[span_9](start_span)[span_9](end_span).
* **Koşullu Renk Güncelleme:** `np.where()` koduyla logodaki belirli pikseller tespit edilip renkleri değiştirilebilir[span_10](start_span)[span_10](end_span). (Örn: Beyaz arka planı koyu gri yaparak karanlık tema uygulamak)[span_11](start_span)[span_11](end_span).

---

### 4. Pandas: Veri Bilimi Ekosistemi ve Dikdörtgensel Veri
* **Dikdörtgensel Veri (Tabular Data):** Satır ve sütunlardan oluşan yapılandırılmış veri modelidir[span_12](start_span)[span_12](end_span).
* **Pandas'ın Temeli:** Pandas kütüphanesi (`import pandas as pd`), hesaplama gücünü ve görselleştirme desteğini doğrudan NumPy ve Matplotlib kütüphaneleri üzerinden alır[span_13](start_span)[span_13](end_span).

### 5. Pandas: DataFrame Bileşenleri ve Keşif
Pandas'ın ana veri yapısı olan DataFrame üç temel bileşenden oluşur:
* **`.to_numpy()`:** DataFrame içerisindeki verileri iki boyutlu bir NumPy dizisi (`array`) olarak döndürür[span_14](start_span)[span_14](end_span).
* **`.columns` & `.index`:** Sütun adlarını tutan yapı `.columns` ile, satır indeksleri ise `.index` ile görüntülenir[span_15](start_span)[span_15](end_span).

Veri setini hızlıca tanımak için kullanılan metotlar:
* **`.head()`:** İlk birkaç satırı döndürür.
* **`.info()`:** Sütun isimleri, eksik veri sayıları ve veri tipleri hakkında teknik özet sunar.
* **`.shape`:** DataFrame'in satır ve sütun sayısını verir.
* **`.describe()`:** Sayısal sütunların istatistiksel özetlerini (`count`, `mean`, `std`, `min`, `max` vb.) hesaplar[span_16](start_span)[span_16](end_span).

### 6. Pandas: Sıralama ve Alt Kümeleme (Subsetting)
* **Verileri Sıralama (`.sort_values()`):** DataFrame içerisindeki satırları belirli sütunlara göre sıralar. (Örn: `dogs.sort_values("weight_kg")`)[span_17](start_span)[span_17](end_span).
* **Sütun Seçme:** Sadece belirli bir sütunu ayırmak için `dogs["name"]` kullanılır[span_18](start_span)[span_18](end_span).
* **Koşullu Satır Filtreleme:** Satırları belirli bir şarta göre filtrelemek için kullanılır. (Örn: `dogs[dogs["height_cm"] > 50]`)[span_19](start_span)[span_19](end_span).
* **Birden Çok Koşulla Filtreleme:** Birden fazla koşulu aynı anda uygulamak için `&` (ve) operatörü kullanılır[span_20](start_span)[span_20](end_span). (Örn: `dogs[(dogs["breed"] == "Labrador") & (dogs["color"] == "Brown")]`)[span_21](start_span)[span_21](end_span).

---
**1. Hafta Tamamlandı** Bu hafta algoritmik düşünceye, Python temellerine, NumPy matris işlemlerine ve Pandas ile veri manipülasyonuna sağlam bir giriş yapıldı.

