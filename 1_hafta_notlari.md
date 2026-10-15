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

## 4. Gün: Veri Bilimi Ekosistemi ve NumPy (15 Ekim 2026)

### Veri Bilimi İçin Python Kütüphaneleri (Ecosystem)
* **ETL (Çıkarma, Dönüştürme, Yükleme):** pandas, BeautifulSoup, Intake.
* **Data Exploration (Veri Keşfi):** Seaborn, matplotlib.
* **Data Evaluation (Veri Değerlendirme):** NumPy, TensorFlow.
* **Data Modeling (Veri Modelleme):** scikit-learn, SciPy, statsmodels.
* **Data Presentation (Veri Sunumu):** matplotlib, HoloViews, VisPy.

### NumPy Veri Türleri ve `.dtype`
NumPy, belleği verimli kullanmak için standart Python türlerinden daha detaylı tipler sunar (`np.int64`, `np.float32` vb.).
* Elemanların tipini öğrenmek için `.dtype` kullanılır. *(Örn: `np.array([1.32, 5.78]).dtype`)*

### 2B Dizilerde Boyut (Axis) Kavramı
* **Birinci Boyut (Axis 0):** Satırları temsil eder (Yukarıdan aşağıya).
* **İkinci Boyut (Axis 1):** Sütunları temsil eder (Soldan sağa).

### NumPy Veri Manipülasyonu Fonksiyonları
* **`np.delete()`:** Veri silmek için kullanılır. Eksen belirtilmezse diziyi tek boyuta indirgeyip siler. `axis=1` verilirse o indeksteki sütunu tamamen siler.
* **`np.where()`:** Belirli bir koşulu sağlayan verilerin indekslerini bulur. *(Örn: `np.where(tree_census[:, 1] == 313879)`)*
* **`np.arange()`:** Belirli aralıklarda ve adımlarla dizi oluşturur.

### Matplotlib ile Görselleştirmeye Giriş
* **`plt.scatter(x, y)`:** Dağılım (scatter) grafiği oluşturur.
* **`plt.show()`:** Arka planda çizilen grafiği ekranda gösterir.

---
*5. Gün: *
