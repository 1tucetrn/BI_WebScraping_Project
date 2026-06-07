# KDS Raporu - Web Madenciliği ve İş Zekası Final Projesi

# Koşu Ayakkabıları İçin Karar Destek Sistemi (KDS)

## Web Madenciliği, Veri Analizi ve Fiyat Tahmini Çalışması

| Başlık | Açıklama |
|---|---|
| Proje konusu | Zappos koşu ayakkabısı ürünleri üzerinde web scraping, analiz ve fiyat tahmini |
| Veri seti | 100 ürün kaydı; marka, model, fiyat, net fiyat, skor ve ürün bağlantısı |
| Model | Random Forest Regressor |
| Amaç | Fiyat, indirim ve skor bilgilerine göre karar destek önerileri üretmek |

**Kısa sonuç:**  
Fiyat ile net fiyat arasında güçlü bir ilişki bulunmuştur. Skorun fiyatla ilişkisi zayıftır. Model fiyat tahmininde R2=0.89 ile başarılı bir performans göstermiştir.

---

# 1. KDS'nin Amacı ve Kapsamı

Bu rapor, Zappos sitesinden toplanan koşu ayakkabısı verileriyle oluşturulan ürün profilleri üzerinde web madenciliği temelli karar destek sistemi çalışmasını açıklamak amacıyla hazırlanmıştır.

KDS, ürünlerin fiyat, net fiyat, indirim oranı ve kullanıcı skoru açısından değerlendirilmesine yardımcı olur.

Çalışma kapsamında ürünlerin fiyat davranışı incelenmiş, markalar arasında karşılaştırma yapılmış ve yeni bir ürün için fiyat tahmin modeli kurulmuştur.

Bu yapı, kullanıcıların veya yöneticilerin hangi ürünlerin fiyat-performans açısından daha uygun olduğunu değerlendirmesine destek sağlar.

---

# 2. Veri ve Yöntem

Veriler web scraping yöntemiyle Zappos koşu ayakkabıları kategorisinden toplanmıştır.

Requests ve BeautifulSoup kütüphaneleri kullanılarak ürün bağlantıları çıkarılmış, ürünlerden marka, model, fiyat, net fiyat, kullanıcı skoru ve ürün linki bilgileri alınmıştır.

- Eksik net fiyat değerleri ortalama net fiyat ile doldurulmuştur.
- Eksik kullanıcı skorları ortalama skor ile tamamlanmıştır.
- Model adları sadeleştirilmiş ve tekrar eden kayıtlar kontrol edilmiştir.
- İndirim miktarı, indirim oranı ve indirim durumu değişkenleri oluşturulmuştur.

---


# 3. Görsel Analizler ve KDS Yorumları

## 3.1. İndirimli fiyat ve net fiyat karşılaştırması

![Görsel 1 - İndirimli fiyat ve net fiyat karşılaştırması](images/indirimli_fiyat.png)

Grafikte net fiyat ile indirimli fiyat arasında doğrusal ve güçlü bir ilişki görülmektedir.

Net fiyat arttıkça satış fiyatı da genel olarak artmaktadır.

KDS açısından net fiyat bilgisinin fiyat tahmininde önemli bir değişken olduğunu gösterir.

Sistem, yüksek net fiyatlı ürünlerde beklenen satış fiyatını daha güvenilir biçimde tahmin edebilir.

---

## 3.2. Markalara göre ortalama fiyatlar

![Görsel 2 - Markalara göre ortalama fiyatlar](images/markalara_gore_ortalama_fiyat.png)

Markalar arasında ortalama fiyat farklılıkları belirgindir.

Athletic Propulsion Labs, Mizuno, La Sportiva ve TYR gibi markalar daha yüksek ortalama fiyat seviyelerine sahiptir.

KDS, markaları premium, orta segment ve ekonomik segment olarak ayırmak için bu grafikten yararlanabilir.

Kampanya kararlarında yüksek fiyatlı markalar ve ekonomik alternatifler ayrı stratejilerle değerlendirilebilir.

---

## 3.3. Markalara göre ortalama skor

![Görsel 3 - Markalara göre ortalama skor](images/markalara_gore_skor.png)

La Sportiva ve Under Armour gibi markaların ortalama skorları daha yüksek görünmektedir.

Bazı markalarda skorlar birbirine yakın olduğu için yalnızca skora bakarak fiyat kararı vermek yeterli değildir.

KDS açısından marka skoru, ürün memnuniyeti hakkında destekleyici bir göstergedir.

Ancak fiyatla birlikte değerlendirildiğinde daha anlamlı kararlar üretir.

---

## 3.4. Korelasyon ısı haritası

![Görsel 4 - Korelasyon ısı haritası](images/korelasyon_isi_haritasi.png)

Fiyat ile net fiyat arasında yaklaşık 0.93 düzeyinde güçlü pozitif korelasyon vardır.

Skor ile fiyat arasındaki ilişki ise oldukça zayıftır.

Bu sonuç, fiyat tahmininde net fiyatın güçlü bir değişken olduğunu; skorun ise tek başına fiyatı açıklamada yetersiz kaldığını gösterir.

KDS, modelinde skor destekleyici değişken olarak kullanılmalıdır.

---

## 3.5. Markalara göre ortalama indirim oranı

![Görsel 5 - Markalara göre ortalama indirim oranı](images/markalara_gore_indirim_orani.png)

Under Armour, INOV8, Saucony, Ryka ve SKECHERS gibi markalarda ortalama indirim oranı daha yüksektir.

Bazı markalarda indirim oranı sıfıra yakındır.

KDS, yüksek indirim oranına sahip markaları kampanya fırsatı olarak işaretleyebilir.

Düşük indirimli fakat yüksek fiyatlı markalar ise premium segment olarak değerlendirilebilir.

---

## 3.6. İndirimli ve indirimsiz ürünlerin ortalama skorları

![Görsel 6 - İndirimli ve indirimsiz ürünlerin ortalama skorları](images/indirimli_indirimsiz_skor.png)

İndirimli ve indirimsiz ürünlerin ortalama skorları birbirine oldukça yakındır.

Bu durum, indirimli ürünlerin kullanıcı memnuniyetinin düşük olduğu anlamına gelmediğini gösterir.

KDS açısından indirimli ürünler doğrudan riskli kabul edilmemelidir.

Skoru yüksek ve indirim oranı yüksek ürünler fiyat-performans açısından öncelikli önerilebilir.

---

## 3.7. Yeni ürün için fiyat tahmini

![Görsel 7 - Yeni ürün için fiyat tahmini](images/yeni_urun_fiyat_tahmini.png)

Random Forest modeli, örnek bir Nike ürünü için 150 dolar net fiyat ve 4.5 skor bilgisine göre yaklaşık 141.10 dolar satış fiyatı tahmin etmiştir.

KDS'nin yeni ürün fiyatlandırma sürecinde tahmini fiyat aralığı sunabileceğini gösterir.

Tahmin edilen fiyat, ürünün kampanya veya satış fiyatı belirlenirken referans olarak kullanılabilir.
# 4. Makine Öğrenmesi Modeli

Fiyat tahmini için Random Forest Regressor modeli kullanılmıştır.

Bağımlı değişken ürün fiyatıdır.

Bağımsız değişkenler:

- marka
- net fiyat
- kullanıcı skoru

Marka değişkeni OneHotEncoder ile sayısal hale getirilmiş, veri seti %80 eğitim ve %20 test olacak şekilde ayrılmıştır.

| Başlık | Açıklama |
|---|---|
| MAE | 10.21 |
| RMSE | 14.33 |
| R2 skoru | 0.89 |
| Örnek tahmin | Nike, net fiyat 150 $, skor 4.5 için tahmini fiyat 141.10 $ |

R2 skorunun 0.89 olması, modelin fiyat değişkenini büyük ölçüde açıklayabildiğini göstermektedir.

MAE ve RMSE değerleri, tahminlerde belirli bir hata payı olduğunu ancak modelin genel karar destek amacı için kullanılabilir düzeyde olduğunu göstermektedir.

---

# 5. KDS Karar Önerileri

- Net fiyat, satış fiyatını tahmin etmek için en güçlü göstergelerden biridir.
- Skor tek başına fiyatı açıklamadığı için fiyat, indirim ve marka bilgileriyle birlikte değerlendirilmelidir.
- Yüksek skor ve yüksek indirim oranına sahip ürünler fiyat-performans açısından öncelikli önerilebilir.
- Premium fiyat seviyesindeki markalarda kampanya yapılacaksa indirim oranı dikkatli belirlenmelidir.
- Model çıktısı, yeni ürün fiyatlandırmasında karar vericiye referans fiyat sağlayabilir.

---

# 6. Sonuç

Bu çalışma, web scraping ile toplanan koşu ayakkabısı verilerinin karar destek sistemi yaklaşımıyla analiz edilebileceğini göstermektedir.

Görseller, ürün fiyatları, indirimler ve kullanıcı skorları arasındaki ilişkileri anlaşılır şekilde ortaya koymuştur.

Makine öğrenmesi modeli ise yeni ürünler için fiyat tahmini yaparak KDS'nin karar verme sürecine katkı sağlayabileceğini göstermiştir.
