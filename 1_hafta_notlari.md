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

## 3. Gün: Python Ortam Kurulumu ve Veri Yapıları (14 Ekim 2026)

### Geliştirme Ortamı
* Kod yazmak ve hücre (cell) bazlı testler yapabilmek için **Jupyter Notebook** kullanıldı.

### Algoritma Kavramı ve Temel Sözdizimi
* **`=` (Atama Operatörü):** Bir değişkene bir değer atamak için kullanılır.
* **`()` (Parantezler):** Fonksiyonları (örn: `print()`, `type()`) çağırmak için kullanılır.
* **`[]` (Köşeli Parantezler):** Python'da **veri (liste)** tutmak için kullanılır.

### Python Değişken Tipleri (Data Types)
Python'da verinin tipini `type()` fonksiyonu ile öğrenebiliriz:
1. **Integer (Tam Sayılar):** `a = 4`
2. **Float (Ondalıklı Sayılar):** `b = 5.6`
3. **String (Metin/Karakter Dizileri):** `x = 'M'` veya `y = "MHM"`
4. **Boolean (Mantıksal):** `True` veya `False` değerlerini alır.
5. **Complex (Karmaşık Sayılar):** `x = 4+5j`

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
*5. Gün: *
