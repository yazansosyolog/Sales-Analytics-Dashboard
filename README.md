## 📊 Global Satış & Lojistik Operasyonları Performans Analizi (Power BI)

Bu projeye başlarken amacım sadece ham verileri alıp renkli grafiklere dönüştürmek değil; bir şirketin tepe yönetiminin (CEO/COO) stratejik karar alırken yaşadığı **"veri körlüğünü"** ortadan kaldırmaktır. Proje sürecinde ham veriden aksiyon edilebilir içgörüye (actionable insights) giden süreç şu metodoloji ile kurgulanmıştır:

![Panel Görüntüsü](https://github.com/yazansosyolog/sales-analytics-dashboard-/blob/master/Panel-g%C3%B6r%C3%BCnt%C3%BCs%C3%BC)

### 1. Excel'in Sınırlarını Aşmak ve Veri İlişkilerini Doğru Kurgulamak
* **Ne Yapmak İstedim?:** Excel üzerinde büyük tablolarda pivot tablolarla boğuşmak, veri büyüdükçe performans kayıplarına ve statik raporlara yol açıyordu. Amacım, veriyi Excel'in kısıtlı hücre mantığından çıkarıp, kurumsal bir veri ambarı mantığıyla birbiriyle konuşan dinamik bir mimariye taşımaktı.
* **Ne Yaptım?:** Power BI'a aktarılan ham veriler arasında karmaşık formüller (VLOOKUP/XLOOKUP) kullanmak yerine; satışlar, ürünler, coğrafya ve müşteriler arasında **Yıldız Şeması (Star Schema)** ilişkileri kurdum. Böylece raporun saniyeler içinde, binlerce satırda bile performans kaybı yaşamadan filtrelenmesini sağladım.

### 2. Sadece Ciroyu Değil, "Kârlılık Sızıntılarını" Yakalamak
* **Ne Yapmak İstedim?:** Şirketler genellikle sadece "Satışlarımız (Sales) artıyor mu?" sorusuna odaklanır ve bu durum büyük bir yanılsama (vanity metric) yaratır. Ciro artarken arkada dönen gizli zararları ve operasyonel maliyet sızıntılarını görünür kılmak istedim.
* **Ne Yaptım?:** Dashboard'un merkezine sadece Satış değil, yan yana **Toplam Kâr (Total Profit)** ve **Benzersiz Sipariş Sayısı** metriklerini koydum. Böylece hacimsel büyümenin gerçek bir kâr getirip getirmediğini yöneticinin tek bakışta test etmesini sağladım.

### 3. Zaman Zekası (Time Intelligence) ile "Büyüme Ritmini" Ölçmek
* **Ne Yapmak İstedim?:** Mevcut yılın satış rakamları tek başına bir anlam ifade etmez. Şirketin doğru bir rotada olup olmadığını anlamak için geçmiş yılların aynı dönemleriyle (Year-over-Year) kıyaslama yapmak, dönemsel (Kasım-Aralık gibi) anomalileri yakalamak gerekiyordu.
* **Ne Yaptım?:** Sadece ham sipariş tarihlerine bağımlı kalmamak adına sıfırdan kesintisiz bir `Dim_Date` takvim tablosu inşa ettim. DAX dilinde `SAMEPERIODLASTYEAR` ve `DIVIDE` fonksiyonlarını kullanarak "Geçen yılın aynı ayında ne kadar satmıştık, bu yıl yüzde kaç büyüdük?" sorusunu dinamik bir analiz çizgisine dönüştürdüm.

### 4. Lojistik ve Operasyonel Darboğazları Teşhis Etmek
* **Ne Yapmak İstedim?:** Satış ekiplerinin agresif hedefleri ile lojistik/tedarik zinciri ekiplerinin operasyonel gerçekleri arasındaki uçurumu göstermek istedim. Hızlı teslimat sözü verilen eyaletlerde işlerin gerçekten yürüyüp yürümediğini, hangi bölgelerin teslimat süresi yüzünden müşteri memnuniyeti riski taşıdığını ifşa etmeyi amaçladım.
* **Ne Yaptım?:** Teslimat türlerinin pasta grafikteki ağırlığını çıkarttıktan sonra, en alta eyalet bazlı **Ortalama Teslimat Süresi (Shipping Time Days)** matrisini yerleştirdim. Buraya uyguladığım soft kırmızı gradyan renk koşullandırması sayesinde, operasyonun yavaşladığı ve kargo sürelerinin 5-6 günü aşarak tehlike sinyali verdiği eyaletleri (Örn: Arizona, Alabama, California) birer "operasyonel alarm hücresine" dönüştürdüm.
