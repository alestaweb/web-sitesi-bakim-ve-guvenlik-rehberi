# Web Sitesi Bakım ve Güvenlik Rehberi — Site Sahipleri İçin

Bir web sitesi yayına girdiği gün bitmez. Yazılımın güvenlik güncellemeleri çıkar, sertifikanın
süresi dolar, bir çalışan ayrılır ama yönetici hesabı açık kalır, yedekler alınır ama hiç
denenmez. Bunların hiçbiri ilk gün görünmez; çoğu, bir sabah site açılmadığında ya da bir
müşteri "sitenizden garip bir e-posta geldi" dediğinde fark edilir.

Bu depo, **bir web sitesinin yayına girdikten sonra nasıl yaşatılacağını** sade bir dille
anlatıyor: kim sorumlu, neyin envanteri tutulmalı, güncellemeler hangi sırayla yapılmalı,
acil bir güvenlik açığı duyurulduğunda ilk saatlerde ne yapılmalı, yedek nasıl denenmeli,
şüpheli bir durumda ilk 24 saat nasıl geçirilmeli.

Hedef kitle teknik ekip değil; site sahibi, işletme yöneticisi ve onlara hizmet veren web
geliştiricisi. **Ürün, firma ya da fiyat önerisi yok.** Hangi yazılımı, hangi barındırma
hizmetini kullanırsanız kullanın sorulması gereken sorular burada.

Hazırlayan: [Alesta WEB](https://alestaweb.com) — haber yazılımı, adisyon ve web yazılımı geliştiricisi.

---

## İçindekiler

1. Bakım neden ayrı bir iştir
2. Sorumluluk: kim, neyi, ne zaman yapacak
3. Envanter: önce neyiniz olduğunu bilin
4. Güncelleme döngüsü
5. Destek süresi biten yazılım
6. Acil güvenlik duyurusu geldiğinde: ilk 48 saat
7. Yedek: almak yetmez, geri yüklemeyi deneyin
8. Hesaplar ve erişim
9. HTTPS, sertifika ve sertifika deposu
10. Formlar, yorumlar ve bot trafiği
11. Dosya yükleme alanları
12. Siteden dışarıya giden bağlantılar
13. İzleme: sorunu müşteriden önce görmek
14. Performans bakımı
15. Şüpheli bir durumda ilk 24 saat
16. KVKK açısından bakım
17. Sessizce yanlış giden 12 şey
18. 20 maddelik kontrol listesi
19. İlgili rehberler ve resmî kaynaklar

---

## 1. Bakım neden ayrı bir iştir

Site yapımı bir projedir: başlangıcı ve teslimi vardır. Bakım ise süreklidir ve teslim günü
başlar. İkisini aynı iş saymak en sık yapılan hatadır; "siteyi yaptırdık, bitti" düşüncesi
yüzünden yıllarca güncellenmemiş, yöneticisi bilinmeyen, yedeği olmayan siteler ortaya çıkar.

Bakımın üç amacı var:

- **Sitenin açık kalması:** sertifika, alan adı, barındırma, disk alanı gibi süreli ya da
  dolabilen şeylerin takibi.
- **Sitenin güvende kalması:** yazılım güncellemeleri, hesap temizliği, yedek, izleme.
- **Sitenin işe yarar kalması:** kırık bağlantılar, yavaşlayan sayfalar, çalışmayan formlar,
  eskiyen içerik.

Bir sitenin bakımsız kaldığını gösteren tipik işaretler: telif yılı birkaç yıl geride, iletişim
formu cevapsız kalıyor, yönetim paneline kimin girebildiği bilinmiyor, "en son ne zaman
güncellendi" sorusuna kimse cevap veremiyor.

## 2. Sorumluluk: kim, neyi, ne zaman yapacak

Bakım sözleşmesi ya da en azından yazılı bir iş bölümü olmadan sorumluluk boşlukta kalır.
Site sahibiyle hizmet veren arasında şu soruların cevabı yazılı olmalı:

| Konu | Sorulacak soru |
|---|---|
| Güncellemeler | Yazılım ve eklenti güncellemelerini kim, hangi sıklıkla yapıyor? |
| Acil yamalar | Kritik bir açık duyurulduğunda ne kadar sürede müdahale ediliyor? |
| Yedek | Yedeği kim alıyor, nerede saklanıyor, geri yükleme ne kadar sürer? |
| İzleme | Site kapandığında ilk kim haberdar oluyor? |
| Hesaplar | Yönetici hesaplarını kim açıyor ve kapatıyor? |
| Alan adı ve sertifika | Yenilemeleri kim takip ediyor, hangi hesaptan ödeniyor? |
| İçerik | Metin, görsel ve ürün güncellemeleri bakıma dahil mi? |
| Çıkış | Hizmet sona ererse dosyalar, veritabanı ve erişimler nasıl teslim ediliyor? |

Son satır özellikle önemli. Hizmet ilişkisi bittiğinde alan adının, barındırma hesabının ve
yedeklerin kimde kaldığı belli değilse site fiilen rehin kalır. Alan adının sahipliği için
ayrıca [tr-alan-adi-ve-dns-rehberi](https://github.com/alestaweb/tr-alan-adi-ve-dns-rehberi)
deposuna bakın.

## 3. Envanter: önce neyiniz olduğunu bilin

Bakım, neyin bakılacağını bilmekle başlar. Bir sayfalık bir envanter yeter:

- **Alan adı:** uzantı, kayıt kuruluşu, bitiş tarihi, kimin adına kayıtlı.
- **Barındırma:** hizmet türü (paylaşımlı, sanal sunucu, bulut), sözleşme bitişi, yönetim paneli.
- **Yazılım:** kullanılan içerik yönetim sistemi ya da özel yazılım, sürümü, eklentileri ve temaları.
- **Çalışma ortamı:** sitenin çalıştığı programlama dili ve veritabanının sürümü. (Bu bilgiyi
  barındırma panelinden ya da geliştiricinizden alabilirsiniz.)
- **Entegrasyonlar:** ödeme kuruluşu, kargo, e-fatura, SMS, e-posta gönderim hizmeti, harita,
  analiz araçları. Her birinin anahtarı nerede tanımlı, kimin hesabına bağlı.
- **E-posta:** kurumsal e-posta nerede barındırılıyor, alan adının DNS kayıtları kimde.
- **Hesaplar:** yönetim paneli, barındırma paneli, alan adı hesabı, ödeme kuruluşu paneli,
  arama motoru konsolu, sosyal medya — her birinde kimlerin hesabı var.
- **Yedek:** nerede, ne sıklıkla, kaç gün geriye.

Envanteri yılda iki kez güncelleyin. Bir entegrasyonun kimin hesabına bağlı olduğunu
bilmemek, o kişi ayrıldığında hizmetin kesilmesi demektir.

## 4. Güncelleme döngüsü

Bir sitenin güncellenmesi gereken dört katmanı vardır. Her katmanın riski ve sıklığı farklı:

| Katman | Örnek | Önerilen sıklık |
|---|---|---|
| İşletim sistemi ve sunucu paketleri | Sertifika deposu, web sunucusu, veritabanı sunucusu | Güvenlik güncellemeleri haftalık |
| Çalışma ortamı | Programlama dilinin kendisi (PHP, Node.js vb.) | Güvenlik sürümleri çıktıkça; ana sürüm yılda bir planlı |
| Uygulama | İçerik yönetim sistemi, özel yazılım | Güvenlik güncellemesi hemen, özellik güncellemesi planlı |
| Eklenti ve tema | Form, galeri, SEO, ödeme eklentileri | Aylık; kullanılmayanları kaldırın |

Güncelleme için basit bir sıra:

1. **Önce yedek.** Dosya ve veritabanı, aynı anda.
2. **Sürüm notunu okuyun.** "Kırıcı değişiklik" (breaking change) ibaresi varsa test ortamında deneyin.
3. **Test ortamı varsa önce orada.** Yoksa en azından trafiğin düşük olduğu saatte.
4. **Güncelleyin, sonra kritik akışları deneyin:** ana sayfa, bir iç sayfa, iletişim formu,
   giriş, varsa sepet ve ödeme.
5. **Hata günlüğüne bakın.** Sayfa açılıyor olsa bile arka planda hata yazılıyor olabilir.
6. **Ne yaptığınızı not edin:** tarih, neyi hangi sürüme güncellediniz.

Eklenti sayısını az tutmak bakımın en ucuz yoludur. Kullanılmayan ama yüklü duran her eklenti,
güncellenmesi gereken bir kod parçası daha demektir.

## 5. Destek süresi biten yazılım

Her yazılımın ve her programlama dili sürümünün bir destek takvimi vardır. Destek bittikten
sonra o sürüme güvenlik yaması çıkmaz; yeni bir açık duyurulduğunda kapatılmaz.

- Kullandığınız dil sürümünün ve yazılımın **destek bitiş tarihini** envantere yazın.
  Örneğin PHP'nin resmî sitesi her sürüm için aktif destek ve güvenlik desteği bitiş tarihlerini yayımlar.
- Destek bitişinden **en az üç ay önce** geçiş planlayın. Eski sürümde çalışan özel kodun yeni
  sürüme uyarlanması zaman alabilir.
- Barındırma hizmetinizin eski sürümleri ne zaman kaldıracağını sorun. Bazı hizmetler destek
  biten sürümü bir gün haber vermeden kaldırır; site o gün hata verir.
- "Çalışıyor, dokunmayalım" yaklaşımı kısa vadede doğru görünür, ama geçişi zorunlu hale
  getiren bir güvenlik açığı geldiğinde iş acil ve pahalı hale gelir.

## 6. Acil güvenlik duyurusu geldiğinde: ilk 48 saat

Ekim 2026'da PHP'de çok sayıda siteyi etkileyen kritik açıklar duyuruldu; aynı hafta bir
sertifika otoritesinin ara sertifika anahtarlarının hesaplanabilir olduğu ortaya çıktı ve
sunuculardaki sertifika depolarının güncellenmesi gerekti. Bu tür haftalar her yıl birkaç kez
yaşanır. Hazırlıklı olmak için:

**İlk saatler**

1. **Etkileniyor muyum?** Envanterdeki sürümlere bakın. Duyurudaki etkilenen sürüm aralığıyla karşılaştırın.
2. **Saldırıda kullanılıyor mu?** Üretici duyurusunda ya da resmî kurumların bilinen istismar
   edilen açıklar listelerinde yer alıyorsa öncelik en üste çıkar.
3. **Geçici önlem var mı?** Üretici bir ayar, bir erişim kısıtlaması ya da bir özelliği
   kapatmayı öneriyorsa yama gelene kadar uygulayın.

**İlk gün**

4. Yedek alın, yamayı uygulayın, kritik akışları deneyin.
5. Yönetim panelinin erişimini mümkünse tanımlı adreslerle sınırlayın.

**İkinci gün**

6. Günlüklere geriye dönük bakın: açığın duyurulmasından önceki günlerde şüpheli istek, yeni
   yönetici hesabı, beklenmedik dosya değişikliği var mı?
7. Site sahibine kısa ve açık bir not yazın: ne oldu, etkilendik mi, ne yapıldı.

Güvenlik duyurularını takip etmek için kullandığınız yazılımın güvenlik bülteni ya da e-posta
listesine abone olun. Ulusal düzeyde USOM duyuruları da takip edilebilir.

## 7. Yedek: almak yetmez, geri yüklemeyi deneyin

Yedek, geri yüklenebildiği kadar değerlidir. Sık görülen durum: yedek her gece alınıyor, ama
hiç denenmediği için gerektiği gün eksik ya da bozuk çıkıyor.

- **Dosya ve veritabanı birlikte.** Yalnız dosya ya da yalnız veritabanı yedeği yarım yedektir.
- **3-2-1 yaklaşımı:** en az üç kopya, iki farklı ortamda, biri sunucunun dışında.
  Sunucuyla aynı yerde duran yedek, sunucuyla birlikte kaybolabilir.
- **Saklama süresi.** Bir saldırı ya da hatalı işlem günler sonra fark edilebilir. Yalnız son
  gecenin yedeği varsa o yedek de bozuk olabilir. Birkaç gün ve birkaç hafta geriye giden
  kopyalar tutun.
- **Yılda en az iki kez geri yükleme denemesi.** Yedeği ayrı bir ortama açın, sitenin açıldığını,
  görsellerin geldiğini, yönetim paneline girilebildiğini görün.
- **Yedeğe kim erişebiliyor?** Yedek, veritabanının tamamını, yani müşteri bilgilerini içerir.
  Herkese açık bir klasörde ya da herkese açık bağlantıyla paylaşılan bir bulut klasöründe durmamalı.

Ayrıntılı anlatım için [turkce-web-yazilim-rehberi](https://github.com/alestaweb/turkce-web-yazilim-rehberi)
deposundaki "Web sitesi yedeği" makalesine bakın.

## 8. Hesaplar ve erişim

Ele geçirilen sitelerin önemli bir kısmında giriş yolu bir yazılım açığı değil, bir hesaptır.

- **Herkesin kendi hesabı olsun.** Ortak kullanılan "admin" hesabı, kimin ne yaptığını
  bilinemez hale getirir ve ayrılan kişinin erişimini kapatmayı imkânsızlaştırır.
- **En az yetki.** İçerik giren kişiye yönetici yetkisi verilmez. Muhasebeye yalnız raporları
  gören bir hesap yeter.
- **İki adımlı doğrulama.** Yönetim paneli, barındırma paneli, alan adı hesabı ve e-posta
  yönetimi için mutlaka.
- **Ayrılan çalışan ve biten hizmet.** Aynı gün hesabını kapatın; ortak parola kullanılıyorsa
  aynı gün değiştirin.
- **Üç ayda bir hesap listesi.** Kim var, en son ne zaman girmiş, hâlâ gerekli mi?
- **Parolalar e-postayla ya da mesajla gönderilmez.** Bir parola yöneticisi ya da tek kullanımlık
  paylaşım yolu kullanın.

Parola ve iki adımlı doğrulama için [kvkk-icin-web-gelistirici-rehberi](https://github.com/alestaweb/kvkk-icin-web-gelistirici-rehberi)
deposundaki makaleye bakabilirsiniz.

## 9. HTTPS, sertifika ve sertifika deposu

- **Sertifikanın kendiliğinden yenilendiğinden emin olun.** Sertifika ömürleri kısalıyor;
  ücretsiz sertifika sağlayıcılarından biri 2027'de 64 günlük sertifikaya geçeceğini duyurdu.
  Elle yenilenen sertifika, kısa ömürle birlikte daha sık unutulur.
- **Yenilemenin başarısız olduğunu kim görür?** Sertifika bitmeden en az iki hafta önce uyarı
  verecek bir izleme kurun.
- **Tüm adresler HTTPS'e yönlensin:** www'lu ve www'suz, http ve https; tek bir adrese.
- **Sertifika deposu da bir yazılımdır.** Sunucunun dışarıya bağlanırken güvendiği sertifika
  otoritelerinin listesi işletim sistemi ve çalışma ortamı güncellemeleriyle gelir. Bir sertifika
  otoritesinin güvenilirliği kaldırıldığında bu liste güncellenmezse sunucu sahte sertifikaya
  güvenmeye devam edebilir.

## 10. Formlar, yorumlar ve bot trafiği

- İletişim formuna gelen spam, formun çalıştığını gösterir ama asıl mesajları gömebilir. Bot
  doğrulaması ve basit hız sınırı ekleyin.
- Formdan giden e-postaların ulaştığını ayda bir deneyin. E-posta ayarları (gönderim hizmeti,
  DNS kayıtları) değiştiğinde formlar sessizce çalışmayı bırakabilir.
- Yorum ve üyelik açık sitelerde onay mekanizması olsun; otomatik açılan sahte hesapları düzenli temizleyin.
- Anormal trafik (bir saatte binlerce istek, aynı adrese tekrar tekrar giriş denemesi) için
  barındırma hizmetinizin sunduğu sınırlamaları açın.

## 11. Dosya yükleme alanları

Siteye dosya yüklenebilen her alan (iletişim formu eki, profil fotoğrafı, iş başvurusu CV'si,
yönetim panelindeki görsel yükleme) dikkat ister:

- Yalnız gerekli dosya türlerine izin verilsin; uzantı ve içerik birlikte kontrol edilsin.
- Yüklenen dosyalar çalıştırılabilir kod olarak yorumlanamayacak bir yerde dursun.
- Dosya boyutu sınırlansın.
- Kişisel veri içeren yüklemeler (kimlik, CV) herkese açık bir adresten erişilebilir olmasın ve
  saklama süresi belirlensin.

Yükleme klasöründe beklenmedik bir dosya türü görmek, şüpheli durumun en net işaretlerinden biridir.

## 12. Siteden dışarıya giden bağlantılar

Sitenizin arka planda başka hizmetlere bağlandığı noktalar da bakımın parçası:

- **Ödeme kuruluşu, kargo, e-fatura, SMS:** anahtarlarının süresi doluyor mu, hangi hesaba bağlı,
  kim yeniliyor? Bir anahtarın süresinin dolması, siparişlerin sessizce düşmesi demek olabilir.
- **Bu bağlantılar düzenli denensin.** Haftalık küçük bir test siparişi ya da test gönderimi,
  sorunu müşteriden önce gösterir.
- **Anahtarlar kodun içinde değil, ayar dosyasında ya da yönetim panelinde tutulsun** ve bu
  dosya herkese açık adresten erişilemesin.
- **Hizmet değiştiğinde eski anahtarlar iptal edilsin.**

## 13. İzleme: sorunu müşteriden önce görmek

Asgari izleme seti:

| Ne izlenir | Neden |
|---|---|
| Sitenin açık olması (birkaç dakikada bir) | Kesintiyi ilk siz görürsünüz |
| Sertifika bitiş tarihi | Yenileme hatasını erken yakalar |
| Alan adı bitiş tarihi | En pahalı kaybı önler |
| Disk doluluğu | Dolan disk veritabanını ve e-postayı durdurur |
| Hata günlüğü | Sayfa açılsa bile arka planda biriken hatayı gösterir |
| Arama motoru konsolu | Dizin, güvenlik ve elle işlem uyarıları buraya düşer |
| Form ve ödeme testi | En çok para kaybettiren sessiz arızalar |

İzleme uyarısının kime gittiği de önemli. Kimsenin okumadığı bir adrese giden uyarı, uyarı yokmuş gibidir.

## 14. Performans bakımı

Site zamanla yavaşlar: içerik büyür, görseller sıkıştırılmadan yüklenir, veritabanı şişer,
eklentiler birikir. Üç ayda bir kısa bir kontrol yeterli:

- Ana sayfa ve en çok ziyaret edilen sayfaların mobilde açılma süresi.
- Büyük görseller: telefonla çekilmiş birkaç megabaytlık fotoğraflar doğrudan yüklenmiş mi?
- Veritabanında biriken gereksiz kayıtlar: eski oturumlar, spam yorumlar, geçici kayıtlar.
- Kullanılmayan eklenti ve temalar.
- Kırık iç bağlantılar ve 404 veren sayfalar.

## 15. Şüpheli bir durumda ilk 24 saat

Sitede tanımadığınız bir sayfa, arama sonuçlarında alakasız başlıklar, müşterilerden "sitenize
girince başka yere yönlendirildim" şikâyeti ya da barındırma hizmetinden bir uyarı geldiyse:

1. **Paniğe kapılıp her şeyi silmeyin.** Delil de silinir, giriş yolu bulunamaz.
2. **Mevcut durumun kopyasını alın:** dosyalar, veritabanı, günlükler. Bu kopya temiz yedek değildir,
   inceleme içindir.
3. **Tüm parolaları değiştirin:** yönetim paneli, barındırma, veritabanı, e-posta, entegrasyon anahtarları.
4. **Yönetici hesaplarını kontrol edin:** tanımadığınız hesap var mı?
5. **Son değişen dosyalara bakın** ve yükleme klasörlerinde beklenmedik dosya arayın.
6. **Giriş yolunu bulun.** Güncellenmemiş bir eklenti mi, çalınmış bir parola mı? Bulunmadan yapılan
   temizlik birkaç gün sonra tekrar eder.
7. **Temiz yedekten dönmek gerekiyorsa** olaydan önceki bir tarihi seçin ve yamayı uygulamadan siteyi açmayın.
8. **Kişisel veri etkilendiyse** bir sonraki bölüme bakın.

## 16. KVKK açısından bakım

Bakım yalnız teknik bir iş değil; kişisel veri işleyen her site için hukuki bir yükümlülüğün de parçası.

- Kişisel Verileri Koruma Kurulu, veri ihlalinin ilgili kişilere ve Kurula **en kısa sürede ve
  en geç 72 saat içinde** bildirilmesine karar vermiştir. Bu süre, bir ihlali fark etmenizi
  sağlayacak izleme ve günlük kaydının önemini artırır.
- Güncel olmayan yazılım, ortak parolalar ve denenmemiş yedekler, "gerekli teknik tedbirler
  alındı mı" sorusuna verilecek cevabı zayıflatır.
- Yedeklerin ve günlüklerin ne kadar süre saklandığı, kişisel veri saklama politikanızla uyumlu olmalı.

Ayrıntılar için [kvkk-icin-web-gelistirici-rehberi](https://github.com/alestaweb/kvkk-icin-web-gelistirici-rehberi)
deposuna bakın. Bu bölüm hukuki görüş değildir.

## 17. Sessizce yanlış giden 12 şey

| Durum | Sonucu |
|---|---|
| Yedek alınıyor ama hiç denenmemiş | Gerektiği gün eksik ya da bozuk çıkar |
| Yedek sunucuyla aynı yerde | Sunucuyla birlikte kaybolur |
| Ayrılan çalışanın hesabı açık | Yetkisiz erişim, kimin ne yaptığı belirsiz |
| Ortak "admin" hesabı | Parola değiştirilemez, iz sürülemez |
| Kullanılmayan eklentiler yüklü | Güncellenmeyen kod, açık kapı |
| Destek süresi bitmiş dil sürümü | Yeni açıklar kapanmaz |
| Sertifika elle yenileniyor | Kısa ömürlerle birlikte unutulur |
| Formdan giden e-postalar ulaşmıyor | Müşteri talepleri sessizce kaybolur |
| Entegrasyon anahtarının süresi doldu | Sipariş, kargo ya da fatura sessizce düşer |
| Hata günlüğüne kimse bakmıyor | Sorun büyüyene kadar görünmez |
| İzleme uyarısı okunmayan adrese gidiyor | Kesinti saatlerce fark edilmez |
| Alan adı yenileme e-postası eski adrese gidiyor | Site ve e-posta birlikte kapanır |

## 18. 20 maddelik kontrol listesi

**Her hafta**

- [ ] Sunucu ve çalışma ortamının güvenlik güncellemeleri uygulandı.
- [ ] Sitenin açık olduğu ve formun çalıştığı denendi.
- [ ] Hata günlüğünde yeni ve tekrarlayan hata yok.
- [ ] Yedeklerin son gece alındığı görüldü.

**Her ay**

- [ ] Uygulama, eklenti ve tema güncellemeleri yedekten sonra uygulandı.
- [ ] Kullanılmayan eklenti ve temalar kaldırıldı.
- [ ] Ödeme, kargo, e-fatura gibi entegrasyonlar birer kez denendi.
- [ ] Disk doluluğu ve sertifika bitiş tarihi kontrol edildi.
- [ ] Arama motoru konsolundaki uyarılar okundu.

**Üç ayda bir**

- [ ] Yönetici ve kullanıcı hesap listesi gözden geçirildi, gereksizler kapatıldı.
- [ ] İki adımlı doğrulamanın tüm kritik hesaplarda açık olduğu doğrulandı.
- [ ] Mobil açılış süresi ve büyük görseller kontrol edildi.
- [ ] Kırık iç bağlantılar tarandı.

**Altı ayda bir**

- [ ] Yedekten ayrı bir ortama geri yükleme denendi.
- [ ] Envanter (alan adı, barındırma, yazılım, entegrasyon, hesap) güncellendi.
- [ ] Kullanılan dil sürümünün ve yazılımın destek bitiş tarihi kontrol edildi.

**Her zaman**

- [ ] Kritik güvenlik duyurularında 48 saatlik planın kimde olduğu belli.
- [ ] Alan adı ve sertifika yenileme uyarıları okunan bir adrese gidiyor.
- [ ] Parolalar e-postayla ya da mesajla paylaşılmıyor.
- [ ] Hizmet sona ererse dosya, veritabanı ve erişim tesliminin nasıl olacağı yazılı.

## 19. İlgili rehberler ve resmî kaynaklar

**Bu hesaptaki diğer rehberler**

- [tr-alan-adi-ve-dns-rehberi](https://github.com/alestaweb/tr-alan-adi-ve-dns-rehberi) — alan adı sahipliği, yenileme, DNS ve e-posta kayıtları
- [kvkk-icin-web-gelistirici-rehberi](https://github.com/alestaweb/kvkk-icin-web-gelistirici-rehberi) — web formları, aydınlatma metni, parola ve iki adımlı doğrulama
- [turkce-web-yazilim-rehberi](https://github.com/alestaweb/turkce-web-yazilim-rehberi) — web sitesi yaptırma, yedek ve teklif karşılaştırma makaleleri
- [eticaret-hukuki-uyum-rehberi](https://github.com/alestaweb/eticaret-hukuki-uyum-rehberi) — e-ticaret sitelerinde hukuki uyum

**Resmî kaynaklar**

- **PHP — Desteklenen sürümler ve destek bitiş tarihleri** — https://www.php.net/supported-versions.php
- **Kişisel Verileri Koruma Kurumu** — https://www.kvkk.gov.tr
- **USOM — Ulusal Siber Olaylara Müdahale Merkezi duyuruları** — https://www.usom.gov.tr
- **CISA — Bilinen istismar edilen açıklar kataloğu** — https://www.cisa.gov/known-exploited-vulnerabilities-catalog
- **OWASP Top 10** — https://owasp.org/www-project-top-ten/
- **Let's Encrypt — 64 günlük sertifika takvimi** — https://letsencrypt.org/2026/10/07/64-day-certs.html

---

## Katkı

Eksik gördüğünüz, güncelliğini yitirmiş veya yanlış bulduğunuz bir madde varsa issue açın.
Ürün ve firma önerisi bilinçli olarak yazılmadı.

## Lisans

MIT — serbestçe kullanın, çoğaltın, alıntılayın.

---

*Hazırlayan: [Alesta WEB](https://alestaweb.com) · haber yazılımı, adisyon ve web yazılımı geliştiricisi*
