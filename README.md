# 🗺️ Bandırma Deprem Toplanma Noktası Analizi

Bu proje, Balıkesir ili Bandırma ilçesi sınırlarındaki resmi deprem toplanma alanlarının kentsel erişilebilirliğini **Coğrafi Bilgi Sistemleri (CBS)** ve ağ analizi yöntemleriyle test etmek amacıyla geliştirilmiştir.

---

## 🎯 1. Giriş ve Amaç
Bu çalışma kapsamında, Bandırma ilçesi sınırları içerisinde yer alan resmi deprem toplanma alanlarının kentsel erişilebilirliği coğrafi bilgi sistemleri (CBS) tabanlı ağ analizleri kullanılarak test edilmiştir.

Çalışmanın temel amacı, olası bir afet sonrasında kentsel panik, yapısal yıkıntılar ve trafik kilitlenmeleri nedeniyle araç kullanımının imkansız hale geleceği gerçeğinden yola çıkarak, vatandaşların bu alanlara **yaya olarak** ne kadar sürede erişebildiğini sayısal olarak ortaya koymaktır.

---

## 🛠️ 2. Veri Setleri ve Ön İşlem Adımları
Analiz sürecinde kullanılan veriler ve izlenen hazırlık adımları şu şekildedir:

* **Sınır ve Sokak Verileri:** Bandırma ilçesine ait idari mahalle sınırları ve mevcut sokak/yol ağı verileri açık kaynaklı **OpenStreetMap (OSM)** altyapısından `QuickOSM` eklentisi vasıtasıyla çekilmiştir.
* **Deprem Toplanma Alanları:** İlçe genelindeki resmi toplanma noktaları, OSM veritabanından `emergency=assembly_point` sorgusuyla CBS ortamına nokta verisi (point) olarak aktarılmıştır.
* **Projeksiyon Dönüşümü (En Kritik Aşama):** Dünyayı küresel (derece) olarak algılayan varsayılan coğrafi koordinat sistemi, mesafe ve zaman analizlerinin metre cinsinden hatasız hesaplanabilmesi amacıyla, Türkiye'nin resmi metrik izdüşüm sistemi olan **TUREF / TM30 (EPSG:5254)** projeksiyonuna dönüştürülmüştür.
* **Geoprocessing (Çözündürme):** Mahalle bazlı karmaşık kentsel poligonlar `Dissolve` (Çözündür) geometrik aracıyla eritilerek bütüncül bir Bandırma ilçe dış sınırı elde edilmiştir.

---

## 📊 3. Uygulanan Analiz Yöntemi (Isochrone Analizi)
Toplanma alanlarının kapsama güçlerini belirlemek amacıyla **ORS Tools (OpenRouteService)** eklentisi kullanılarak **Eş Zamanlı Eğriler (Isochrone)** analizi yürütülmüştür.

* Yaya sirkülasyonunu kısıtlayan binalar ve sokak geometrisini baz alan **"Yaya Yürüyüş Modeli" (foot-walking)** tercih edilmiştir.
* Afet yönetimindeki kritik *"Altın Saatler"* standardına uygun olarak her bir toplanma odağından dışarıya doğru **5 dakikalık (ideal süre)** ve **10 dakikalık (maksimum kabul edilebilir süre)** yaya erişim halkaları simüle edilmiştir.

---

## 🔍 4. Analiz Bulguları
Üretilen erişilebilirlik haritası incelendiğinde iki temel kentsel bulguya ulaşılmıştır:

### 🟢 A. Merkez Mahallelerde Yüksek Kapsama Gücü
Bandırma'nın sahil şeridinde yer alan ve nüfus yoğunluğunun en yüksek olduğu merkez mahallelerde (Paşakent, Sunullah, Dere vb.) 5 ve 10 dakikalık yürüyüş poligonlarının birbiriyle bütünleştiği ve kentsel dokunun büyük oranda güvenli kapsama alanında kaldığı saptanmıştır.

![Erişilebilirlik Analizi Haritası](https://github.com/yoruware/bandirma-deprem-analizi/blob/main/output/isochrone_map.png?raw=true)

### 🔴 B. Kırsal ve Çeperlerdeki "Kör Noktalar" (Erişim Yetersizliği)
Merkezin güneyinde kalan geniş kırsal mahallelerde (köylerde) ve kentin yeni gelişen çeper alanlarında toplanma alanlarının OpenStreetMap üzerinde veri olarak eksik olduğu veya kurumsal planlama düzeyinde yetersiz kaldığı gözlemlenmiştir[cite: 20]. [cite_start]Haritada renksiz (yeşil/turuncu kapsama alanı dışında) kalan bu "Kör Noktalar", afet anında vatandaşların yaya olarak 10 dakikada ulaşabileceği hiçbir resmi güvenli alanın olmadığını gösteren **en riskli bölgelerdir**.

---

## 🏁 5. Sonuç ve Öneriler
Bu proje, yazılım ve coğrafi bilgi sistemlerinin afet yönetiminde ne kadar efektif kullanılabileceğini kanıtlamaktadır. 

Analiz sonucunda elde edilen veriler ışığında, yerel yönetimlerin ve şehir plancılarının yeni deprem toplanma alanları için bütçe ve yer seçim önceliğini haritada tespit edilen **renksiz (kapsama dışı) çeper ve kırsal mahallelere** vermesi hayati önem arz etmektedir.
