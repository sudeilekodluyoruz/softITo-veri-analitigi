# İstanbul İBB Wi-Fi Kullanıcı Verisi Analizi

Bu proje, İstanbul Büyükşehir Belediyesi (İBB) Açık Veri Portalı'ndan alınan "Günlük İBB Wi-Fi Yeni Kullanıcı Verisi" üzerinde Keşifçi Veri Analizi (EDA) yapılarak belirli bir hipotezin test edilmesini içermektedir.

##  Projenin Amacı ve Hipotez

Bu analizde aşağıdaki önerme (hipotez) test edilmiştir:

> **Önerme:** *"Yabancı abonelerin oranı yaz aylarında (Haziran–Ağustos) kış aylarından (Aralık–Şubat) yüksektir."*

##  Kullanılan Teknolojiler ve Kısıtlamalar

Bu proje, belirli ödev/görev koşulları çerçevesinde sadece temel veri bilimi kütüphaneleri kullanılarak geliştirilmiştir:
* **Dil:** Python 3
* **Kütüphaneler:** `pandas`, `numpy`
* **Ortam:** Jupyter Notebook (`.ipynb`)

##  Veri Seti

* **Kaynak:** İBB Açık Veri Portalı
* **Veri:** Günlük İBB Wi-Fi Yeni Kullanıcı Verisi
* **Dosya:** `Veri_Seti.csv` (Proje dizininde bulunmalıdır)
* **İçerik:** 2015-2021 yılları arasındaki abonelik tarihleri, lokasyon (ilçe, enlem, boylam) ve yerli/yabancı abone sayıları.

##  Analiz Adımları

1. **Veri Temizleme:** Eksik verilerin kontrolü, tarih formatlarının düzenlenmesi ve "Bilinmiyor" olarak işaretlenen uyruk verilerinin setten çıkarılması.
2. **Özellik Mühendisliği (Feature Engineering):** Tarih verisinden ay bilgisi çekilerek ayların "Yaz" ve "Kış" olarak kategorize edilmesi.
3. **Gruplama ve Hesaplama:** Mevsimlere göre yerli ve yabancı abone sayılarının toplanıp pivot tablo haline getirilmesi ve yabancı abone yüzdelerinin hesaplanması.

##  Sonuçlar ve Bulgular

Analiz sonucunda elde edilen veriler şöyledir:
* **Kış Sezonu Yabancı Oranı:** %22.0
* **Yaz Sezonu Yabancı Oranı:** %17.0

Yaz aylarında toplam abone sayısı (hem yerli hem yabancı) büyük bir artış gösterse de, yerli kullanıcıların sisteme katılımındaki devasa artış, yabancı abonelerin oransal payını düşürmüştür.
Sonuç olarak, başlangıçtaki önerme **ÇÜRÜTÜLMÜŞTÜR**.

