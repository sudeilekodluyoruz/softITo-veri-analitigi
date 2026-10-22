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
 
##  7.Gün:  İleri Seviye Pandas (Veri Birleştirme ve Şekillendirme) (20 Ekim 2026)

### 1. Temel Birleştirme İşlemleri (Merges & Joins)
Farklı DataFrame'leri ortak sütunlar (key) üzerinden ilişkilendirmek için `.merge()` metodu kullanılır:
* **İç Birleşim (Inner Join):** Sadece her iki tabloda da eşleşen değere sahip satırları döndürür. (Örn: `df1.merge(df2, on='vid')`).
* **Sonekler (Suffixes):** Birleştirilen tablolarda aynı isimde sütunlar varsa (örneğin iki tabloda da `name` varsa), çakışmayı önlemek için kullanılır. (Örn: `suffixes=('_own', '_veh')`).
* **Bire-Çoka (One-to-Many) İlişkiler:** Sol tablodaki tek bir kayıt, sağ tabloda birden fazla kayıtla eşleşiyorsa, sol tablodaki veri çoğaltılarak listelenir (Örn: Bir müşterinin birden fazla siparişinin olması).
* **Çoklu Birleştirme:** İkiden fazla tablo metod zincirleme ile tek satırda birleştirilebilir: `df1.merge(df2, on='col').merge(df3, on='col')`.
* **Farklı Sütun İsimleriyle Birleştirme:** Ortak veriyi tutan sütunların isimleri tablolarda farklıysa `left_on` ve `right_on` argümanları kullanılır. (Örn: `left_on='id', right_on='movie_id'`).

### 2. Farklı Birleştirme Türleri (`how` Argümanı)
Birleştirme mantığı `.merge(how='...')` argümanı ile değiştirilebilir:
* **`how='left'` (Left Join):** Sol tablodaki tüm satırları tutar, sağ tabloda eşleşme bulunamayan satırların karşılığını `NaN` (boş değer) ile doldurur. Bir ana veriyi diğer tablolardaki ek bilgilerle zenginleştirmek için idealdir.
* **`how='right'` (Right Join):** Sağ tablodaki tüm satırları tutar, solda karşılığı olmayanları `NaN` yapar.
* **`how='outer'` (Outer Join):** Her iki tablodaki tüm satırları getirir. Eksik eşleşmeler `NaN` olur. Tablolar arasındaki farklılıkları ve veri eksikliklerini bulmak için çok kullanışlıdır.
* **Self Join (Kendi Kendine Birleştirme):** Bir tablonun yine kendisiyle birleştirilmesidir (`df.merge(df, on='id')`). Hiyerarşik verilerde (örn: çalışan-yönetici ilişkisi) aynı sütundaki değerleri birbiriyle kıyaslamak için kullanılır.

### 3. Filtreleyen Birleştirmeler (Filtering Joins)
* **Semi Join (Yarı Birleştirme):** Sol tabloyu, yalnızca sağ tabloda eşleşmesi olan satırları tutacak şekilde filtreler. 
  * *Uygulanışı:* İç birleşim yapılır, sağ tablodan dönen ortak ID'ler bir değişkene atanır ve sol tabloda `.isin()` metoduyla filtrelenir.
* **Anti Join:** Sol tabloda olup sağ tabloda *hiçbir karşılığı olmayan* kayıtları bulur. 
  * *Uygulanışı:* `how='left', indicator=True` argümanlarıyla birleştirilir, ardından `_merge == 'left_only'` olan satırlar filtrelenir.

### 4. Dikey Birleştirme (Concatenation)
Ortak sütun yapılarına sahip farklı veri setlerini (örneğin 3 farklı ayın faturasını) alt alta eklemek için `pd.concat()` kullanılır:
* `pd.concat([df1, df2, df3])` şeklinde DataFrame listesi alır.
* `ignore_index=True`: Alt alta eklenen tabloların eski indeks numaralarını silip `0`'dan `n-1`'e kadar yeniden ve sıralı bir indeks oluşturur.
* `keys=['A', 'B']`: Verilerin hangi orijinal tablodan geldiğini ayırmak için hiyerarşik (multi-level) bir indeks ekler.

### 5. Sıralı ve Zaman Serisi Verilerini Birleştirme
Özellikle tarih/zaman ve finansal analizlerde hizalama yapmak için geliştirilmiş özel fonksiyonlardır:
* **`pd.merge_ordered()`:** Sıralı verileri birleştirmek için kullanılır (varsayılanı outer join'dir). `fill_method='ffill'` (ileri doldurma) argümanı sayesinde eksik veya farklı frekanstaki zaman verilerini (örn: aylık vs üç aylık veri) mantıklı değerlerle enterpole edebilir.
* **`pd.merge_asof()`:** Zaman damgaları saniyesi saniyesine eşleşmediğinde, "en yakın ve en son" zamandaki veriyi eşleştirir. Borsa verilerindeki milisaniyelik gecikmeleri veya tam eşleşmeyen tarihleri hizalamak için kritik bir araçtır.

### 6. Gelişmiş Sorgulama ve Şekillendirme
* **`.query()`:** Mantıksal koşullar kullanarak DataFrame satırlarını SQL benzeri temiz bir metin (string) sözdizimi ile filtreler.
  * *Örnek:* `df.query('gdp_per_capita > 50000')` veya `df.query('date >= "1991-01-01"')`.
* **`.melt()`:** Geniş formattaki (wide) verileri uzun formata (long) çevirmek (unpivot işlemi) için kullanılır. Dağınık verileri görselleştirmeye (plot) uygun hale getirir.
  * `id_vars`: Satırlarda sabit kalacak tanımlayıcı sütunlar.
  * `var_name`: Eski başlıkların toplanacağı yeni kategori sütununun adı.
  * `value_name`: Eski sayısal değerlerin toplanacağı yeni değer sütununun adı.
 
##  8.Gün: İlişkisel Veritabanları (PostgreSQL) ve Python ETL Süreçleri (21 Ekim 2026)

Bugün yapılandırılmış verilerin depolandığı İlişkisel Veritabanı Yönetim Sistemlerine (RDBMS) geçiş yaparak **PostgreSQL** ve **pgAdmin** kurulumlarını tamamladık. Özellikle Python kullanarak veritabanına otomatik veri aktarımı (ETL) yapmayı öğrendik.

### 1. PostgreSQL Tablolarını Toplu Silme (`drop_all_tables.sql`)
Geliştirme aşamasında veritabanını sıfırlamak için kullandığımız SQL bloğu ve komutların detayları[cite: 41]:

*   **`DO $$ ... END $$;`**: PostgreSQL'de isimsiz (anonim) bir PL/pgSQL kod bloğu başlatır[cite: 41].
*   **`FOR r IN (SELECT tablename FROM pg_tables WHERE schemaname = current_schema())`**: Veritabanının mevcut şemasındaki (genellikle `public` şeması) tüm tablo isimlerini bulur ve işlemi bir döngüye sokar[cite: 41].
*   **`EXECUTE 'DROP TABLE IF EXISTS ... CASCADE';`**: Döngüde bulunan her bir tabloyu siler. Buradaki kritik nokta olan `CASCADE` komutu, silinen tabloya bağlı olan diğer yapıların (örneğin yabancı anahtarlar - foreign keys veya görünümler - views) da otomatik olarak düşürülmesini sağlar ve hata alınmasını engeller[cite: 41].

### 2. Python ile Otomatik Veri Aktarımı (ETL Süreci)
Farklı CSV dosyalarını tek tek pgAdmin üzerinden içeri aktarmak (import) yerine, `postgre_import_csv.py` dosyası ile tam otomatik bir veri mühendisliği (Data Engineering) boru hattı (pipeline) geliştirdik[cite: 42]. 

Betik (script) temelde 4 aşamadan oluşur:

**Adım 1: Kütüphaneler ve Veritabanı Bağlantısı**
*   Veritabanı ile iletişim kurmak için `sqlalchemy` kütüphanesinin `create_engine` fonksiyonu kullanıldı[cite: 42].
*   `postgresql+psycopg2://kullanici:sifre@localhost:5432/eu_soccer` formatında oluşturulan bağlantı dizesi (connection string) ile PostgreSQL'e güvenli bir köprü kuruldu[cite: 42].

**Adım 2: Dosyaların Bulunması ve Tablo İsimlendirme**
*   **`glob.glob()`**: Belirlenen klasördeki (Örn: `1_manupilate`) tüm `.csv` uzantılı dosyaları otomatik olarak tarayıp bulur[cite: 42].
*   **Regex (`re.sub`)**: CSV dosya isimlerindeki boşlukları veya geçersiz karakterleri alt çizgiye (`_`) çevirip küçük harfe dönüştürerek, PostgreSQL standartlarına %100 uygun, temiz tablo isimleri üretir[cite: 42].

**Adım 3: Veri Temizleme ve Hizalama (Data Cleaning & Padding)**
Python'ın yerleşik `csv.reader` modülü kullanılarak veriler satır satır okundu ve oluşabilecek veri bozulmalarının önüne geçildi[cite: 42]:
*   **Eksik Sütun Tamamlama (Padding):** Eğer bir satırdaki veri sayısı, başlık (header) sayısından azsa, aradaki fark `None` değerleri ile doldurulur (Bu değerler PostgreSQL'e aktarılırken `NULL` olarak yansır). Böylece aktarımın yapısal bir hata verip çökmesi engellenir[cite: 42].
*   **Fazla Sütun Kırpma (Truncating):** Eğer bir satırda başlıktan daha fazla veri varsa, fazla olan veriler kesilerek (truncate) tablo yapısı korunur[cite: 42].

**Adım 4: SQL'e Yazma İşlemi**
*   Temizlenen satırlar bir Pandas DataFrame'ine (`pd.DataFrame`) dönüştürülür[cite: 42].
*   **`df.to_sql()`**: DataFrame'i doğrudan PostgreSQL'e bir tablo olarak yazar. `if_exists="fail"` parametresi ile tablonun zaten var olması durumunda yanlışlıkla üzerine yazılması engellenir. `index=False` parametresi ile Pandas'ın varsayılan indeks numaralarının gereksiz yere veritabanına kaydedilmesi önlenir[cite: 42].

### 3. Kullanılan Örnek Veri Setleri
Bu otomasyon scripti ile aşağıdaki çeşitli veri setleri PostgreSQL içerisine başarıyla aktarıldı:
*   **Avrupa Futbol Verileri:** Ülkeler (`country`), Ligler (`league`), Takımlar (`team`), Maçlar (`match`).
 
