# SoftITo Veri Analitiği - 2. Hafta Notları
## 6. Gün: Pandas ile Veri İşleme ve Manipülasyon (19 Ekim 2026)

Bugün, dikdörtgensel verileri (tabular data) işlemek için Veri Bilimi dünyasının en popüler kütüphanesi olan Pandas'ı detaylıca inceledik. Çeşitli veri setleri (`homelessness.csv`, `sales_subset.csv`, `avocados_2016.csv` vb.) üzerinde işlemler yaptık.

### 1. DataFrame'leri Keşfetme (Exploration)
Yeni bir veri seti yüklendiğinde (`pd.read_csv()`) veriyi anlamak için şu metotlar kullanılır:
* **`.head()`:** DataFrame'in ilk 5 satırını getirerek veriye hızlıca göz atmamızı sağlar.
* **`.info()`:** Sütunların veri türlerini ve eksik (null) değer sayısını gösterir.
* **`.shape`:** Veri setinin satır ve sütun sayısını (boyutlarını) verir.
* **`.describe()`:** Nümerik sütunlar için ortalama, standart sapma, minimum ve maksimum değerler gibi özet istatistikleri hesaplar.

### 2. Sıralama ve Alt Küme Oluşturma (Subsetting)
* **Verileri Sıralama (`.sort_values()`):**
  * Tek bir sütuna göre sıralama: `df.sort_values("individuals")`
  * Birden fazla sütuna göre sıralama: `df.sort_values(["region", "family_members"], ascending=[True, False])` (Bölgeye göre artan, aile üyelerine göre azalan).
* **Sütun Seçme:** Sadece ilgilenilen sütunları almak için çift köşeli parantez kullanılır. Örn: `df[["state", "family_members"]]`.
* **Satır Filtreleme:** Mantıksal (Boolean) koşullar kullanılarak belirli veriler çekilebilir:
  * Tek koşul: `df[df["individuals"] > 10000]`
  * Çoklu koşul: `df[(df["family_members"] < 1000) & (df["region"] == "Pacific")]`
* **`.isin()` Metodu:** Birden fazla "veya" (or) koşulu yazmak yerine pratik bir yöntemdir. Örn: `df[df["state"].isin(["California", "Arizona", "Nevada"])]`.

### 3. Yeni Sütunlar Ekleme (Özellik Mühendisliği)
Mevcut sütunlardan matematiksel işlemlerle yeni ve anlamlı veriler üretilebilir:
* Örn: `homelessness["total"] = homelessness["individuals"] + homelessness["family_members"]`
* Örn: `airline_totals["bumps_per_10k"] = airline_totals["nb_bumped"] / airline_totals["total_passengers"] * 10000`

### 4. Özetleme (Aggregation) ve Gruplama (Groupby)
* **Özel Fonksiyonlarla Özetleme (`.agg()`):** DataFrame'in belirli sütunlarına kendi yazdığımız veya yerleşik fonksiyonları aynı anda uygulayabiliriz. Örn: `sales[["temperature_c", "unemployment"]].agg([iqr, "median"])`.
* **Kümülatif İstatistikler:** Zaman serilerinde `.cumsum()` (kümülatif toplam) veya `.cummax()` (kümülatif maksimum) kullanılabilir.
* **Yinelenenleri Silme:** `.drop_duplicates(subset=["store", "type"])` kodu, mağaza ve tür sütunlarındaki mükerrer kayıtları siler.
* **Gruplama (`.groupby()`):** Verileri kategorilere ayırıp hesaplama yapmak için çok güçlü bir yöntemdir:
  * `sales.groupby("type")["weekly_sales"].sum()` kodu, her mağaza türü için haftalık toplam satışı hesaplar.

### 5. Pivot Tablolar
Pandas'ta `.pivot_table()`, `.groupby()` işleminin bir alternatifidir ve özellikle elektronik tablo formatına (Excel gibi) yatkın bir görünüm sunar:
* `sales.pivot_table(values="weekly_sales", index="department", columns="type", fill_value=0, margins=True)`
  * `index` ve `columns`: Gruplanacak kategorileri belirler.
  * `fill_value=0`: Eksik (NaN) değerlerin yerine 0 yazar.
  * `margins=True`: Satır ve sütunların genel toplamlarını ekler.

### 6. İndeksler ve Dilimleme (Slicing - `.loc` & `.iloc`)
* Bir sütunu `.set_index("city")` ile indeks (satır başlığı) yapabilir ve `.sort_index()` ile sıralayabiliriz.
* **`.loc[]`:** İndeks isimleri (etiketler) ile dilimleme yapar. Örn: `df.loc["Pakistan":"Philippines", "date":"avg_temp_c"]` (Hem satır hem sütun dilimleme).
* **`.iloc[]`:** Satır ve sütun numaraları (0'dan başlayan pozisyonlar) ile dilimleme yapar. Örn: `df.iloc[0:5, 2:4]`.

### 7. Veri Görselleştirme ve Eksik Değerler
* `matplotlib.pyplot` kütüphanesi entegrasyonuyla:
  * Bar (Çubuk) grafik: `.plot(kind="bar")`
  * Line (Çizgi) grafik: `.plot(kind="line")`
  * Scatter (Dağılım) grafik: `.plot(kind="scatter", x="nb_sold", y="avg_price")`
  * Histogram: `.hist(alpha=0.5, bins=20)` (Saydamlık ve kutu sayısı ayarlanabilir).
* **Eksik (Missing) Değerler:**
  * Kontrol: `.isna().any()`
  * Silme: `.dropna()`
  * Değiştirme/Doldurma: `.fillna(0)` (Örn: Boş verileri sıfır ile doldurma).
