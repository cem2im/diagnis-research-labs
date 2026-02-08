# Modül 2: Veri - Her Şeyin Temeli

## Giriş

Yapay zeka dünyasında bir söz vardır: "Çöp girerse, çöp çıkar." İngilizce'si "Garbage in, garbage out." Bu söz, veri kalitesinin ne kadar kritik olduğunu anlatıyor.

Dünyanın en iyi algoritmasını kullanabilirsiniz, en pahalı GPU'ları satın alabilirsiniz. Ama veriniz kötüyse, sonuçlarınız da kötü olacak. Bu modülde veriyi konuşacağız - türlerini, ne kadar lazım olduğunu, nasıl hazırlanacağını.

## Veri Tipleri

Tıbbi araştırmada dört ana veri tipi var.

**Görüntü verileri.** Radyoloji, patoloji, dermatoloji, oftalmoloji, endoskopi... Tıbbın büyük bir kısmı görüntüye dayalı. CT, MR, ultrason, X-ray, mikroskop görüntüleri, fundus fotoğrafları, endoskopi kayıtları. Bunların hepsi görüntü verisi.

**Tablo verileri.** Laboratuvar sonuçları, vital bulgular, demografik bilgiler, hasta öyküsü. Excel'de görebileceğiniz her şey. Satırlar hastalar, sütunlar değişkenler.

**Metin verileri.** Doktor notları, epikriz raporları, radyoloji raporları. Serbest metin formatında bilgi. Doğal dil işleme (NLP) teknikleri burada devreye giriyor.

**Sinyal verileri.** EKG, EEG, EMG gibi zaman serisi verileri. Sürekli ölçüm yapılan her şey bu kategoride.

Her veri tipi farklı yaklaşımlar gerektiriyor. Görüntü için CNN, metin için Transformer, sinyal için LSTM veya Temporal CNN kullanılıyor. Ama temel prensipler aynı.

## Ne Kadar Veri Lazım?

Bu en sık sorulan soru. Ve maalesef net bir cevabı yok. "Duruma göre değişir" demek zorundayım, ama bazı rehber ilkeler verebilirim.

**Görüntü sınıflandırma için:** Minimum her sınıf için 100-200 görüntü. İdeal olarak 500-1000. Transfer learning kullanıyorsanız daha az da olabilir.

**Nesne tespiti için:** Her nesne türü için minimum 200-300 örnek. Bounding box annotation gerekiyor.

**Segmentasyon için:** Piksel bazında etiketleme çok zaman alıyor. Minimum 50-100 tam etiketli görüntü, ama 200+ ideal.

**Tablo verileri için:** Değişken sayısının en az 10-20 katı kadar örnek. 50 değişkeniniz varsa, minimum 500-1000 hasta.

Ama şunu unutmayın: Bu sayılar minimum. Daha fazla veri neredeyse her zaman daha iyi sonuç demek. Ve kalite, kantiteden önemli.

## Veri Kalitesi Neden Kritik?

Şimdi kaliteye bakalım. Kötü veri nasıl olur?

**Tutarsız etiketleme.** Aynı lezyona bir doktor "benign" demiş, diğeri "malign." Model ne öğrenecek? Kafası karışacak.

**Eksik veriler.** Bazı hastalarda bazı değişkenler yok. Bu boşlukları nasıl dolduracaksınız?

**Gürültülü görüntüler.** Bulanık, kötü aydınlatılmış, artifaktlı görüntüler. Model gerçek özellikleri mi yoksa gürültüyü mü öğreniyor?

**Dengesiz sınıflar.** 1000 normal, 50 hasta örneği. Model "herkese normal de" stratejisiyle %95 doğruluk elde edebilir ama hiçbir hastayı bulamaz.

**Seçim yanlılığı.** Sadece belirli bir hastaneden, belirli bir popülasyondan veri. Model başka yerlerde çalışmayabilir.

## Annotation: Etiketleme Temelleri

Etiketleme, yapay zeka projesinin en çok zaman alan kısmı. Görüntüdeki her polipe, her tümöre, her lezyona işaret koymanız gerekiyor.

**Kim etiketleyecek?** İdeal olarak uzman. Daha da ideali, birden fazla uzman. İki veya üç doktor bağımsız olarak etiketlesin, sonra fikir birliği sağlansın.

**Inter-rater agreement.** Etiketleyiciler ne kadar uyumlu? Cohen's Kappa veya Fleiss' Kappa ile ölçülür. Düşükse, tanım kriterlerinizi netleştirmeniz gerekiyor.

**Etiketleme araçları.** LabelImg, VGG Image Annotator, Label Studio gibi ücretsiz araçlar var. Ticari seçenekler de mevcut.

**Protokol oluşturun.** Ne etiketlenecek, nasıl etiketlenecek, belirsiz durumlarda ne yapılacak - bunların hepsini önceden belirleyin.

## Data Augmentation

Veri artırma, mevcut verinizi "çoğaltmanın" yollarından biri. Görüntülerinizi döndürür, çevirir, yakınlaştırır, renk değişiklikleri yaparsınız. Böylece model daha robust olur.

Mesela bir endoskopi görüntüsünü 90 derece döndürseniz, polip hâlâ polip. Ama model için bu "yeni" bir örnek.

**Dikkat:** Augmentation sihirli değnek değil. 100 görüntüden augmentation ile 10000 görüntü yaparsanız, hâlâ 100 farklı vakadan öğreniyorsunuz. Gerçek veri çeşitliliğinin yerini tutmaz.

**Tıbbi görüntülerde dikkat:** Bazı augmentasyonlar anlamsız olabilir. Dermatoskopi görüntüsünü ters çevirseniz belki sorun yok, ama EKG sinyalini ters çevirseniz klinik anlam değişir.

## Veri Bölünmesi

Verinizi üçe ayırmalısınız:

**Training set (Eğitim seti):** Model bundan öğrenir. Genellikle verinin %70-80'i.

**Validation set (Doğrulama seti):** Eğitim sırasında modelin performansını izlemek için. %10-15.

**Test set (Test seti):** Final değerlendirme için. Model bunu eğitim sırasında asla görmemeli. %10-15.

**Kritik nokta: Hasta bazlı bölünme.** Aynı hastanın görüntüleri farklı setlere dağılmamalı. Aksi halde data leakage olur. Bu çok yaygın bir hata ve makalenizi reddettirme sebebi.

## Sonuç

Bu modülde veriyi konuştuk. Türleri, miktarı, kalitesi, etiketlemesi, artırılması ve bölünmesi.

Şunu aklınızda tutun: Yapay zeka projenizin %80'i veri hazırlığı. Model seçimi ve eğitimi geri kalan %20. Veri aşamasını aceleye getirirseniz, sonraki her şey sallantılı olur.

Bir sonraki modülde hangi modelin hangi problem için uygun olduğuna bakacağız. Görüntü için ne kullanılır, tablo için ne kullanılır, öğreneceğiz.

Şimdi quiz zamanı!
