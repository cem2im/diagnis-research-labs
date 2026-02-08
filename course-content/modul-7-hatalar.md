# Modül 7: Yaygın Hatalar ve Çözümleri

## Giriş

Bu modül belki de en önemli modül. Çünkü başkalarının yaptığı hatalardan öğrenmek, kendiniz yapıp öğrenmekten çok daha az acı verici.

Tıbbi yapay zeka alanında sıkça karşılaşılan hataları ve bunlardan nasıl kaçınacağınızı konuşalım.

## Hata 1: Data Leakage

Bu en yaygın ve en tehlikeli hata.

**Ne oluyor?**
Test verisinden bilgi, eğitim sürecine sızıyor. Model aslında ezberliyor ama siz bunu fark etmiyorsunuz.

**Örnek 1:** Aynı hastanın farklı görüntüleri train ve test'e dağılmış.

**Örnek 2:** Görüntülerin metadata'sında tanı bilgisi var. Mesela dosya adında "malign_001.jpg" yazıyor.

**Örnek 3:** Veri normalizasyonu tüm veri seti üzerinde yapılmış, sonra split yapılmış. Test setinin istatistikleri training'e sızmış.

**Çözüm:**
- Hasta bazlı split yapın
- Preprocessing pipeline'ını sadece training verisi üzerinde fit edin
- Metadata'yı temizleyin
- Kör test seti oluşturun (etiketler ayrı tutulsun)

## Hata 2: Imbalanced Data'yı Görmezden Gelmek

**Ne oluyor?**
%95 normal, %5 hasta. Model herkese "normal" diyor, accuracy %95 ama sensitivity %0.

**Çözüm:**
- Weighted loss function kullanın
- Oversampling (az olan sınıfı çoğaltın) veya undersampling (çok olan sınıfı azaltın)
- SMOTE gibi sentetik veri üretme teknikleri
- Doğru metrik seçin (accuracy değil, AUC/F1/AUPRC)

## Hata 3: Yanlış Metrik Seçimi

**Ne oluyor?**
Accuracy raporluyorsunuz ama veri dengesiz. Ya da F1 raporluyorsunuz ama tarama testi için sensitivity önemli.

**Çözüm:**
- Probleme uygun metrik seçin
- Birden fazla metrik raporlayın
- Confusion matrix gösterin
- Clinical context'i düşünün (vaka kaçırmak mı kötü, yanlış alarm mı kötü?)

## Hata 4: Overfitting'i Görmezden Gelmek

**Ne oluyor?**
Training accuracy %99, validation accuracy %70. Fark büyük ama siz "training iyi gidiyor" diye devam ediyorsunuz.

**Çözüm:**
- Validation loss'u izleyin
- Early stopping kullanın
- Regularization ekleyin (dropout, weight decay)
- Model karmaşıklığını azaltın
- Data augmentation yapın

## Hata 5: External Validation Atlama

**Ne oluyor?**
Sadece kendi veri setinizde test ettiniz. Sonuçlar harika. Ama model başka bir hastanede çalışmıyor.

**Çözüm:**
- Mutlaka external validation yapın
- Farklı cihaz, farklı hastane, farklı popülasyon
- Açık veri setleri kullanın
- Performans düşüşü beklenen, panik yapmayın

## Hata 6: Kara Kutu Bırakmak

**Ne oluyor?**
Model karar veriyor ama neden o kararı verdiği belli değil. Reviewer'lar ve klinisyenler güvenmiyor.

**Çözüm:**
- Explainability teknikleri kullanın
  - GradCAM, ScoreCAM (görüntüler için)
  - SHAP, LIME (tablo verileri için)
  - Attention visualization (Transformer için)
- Önemli özellikleri (feature importance) raporlayın
- Failure case'leri analiz edin ve gösterin

## Hata 7: Baseline Karşılaştırma Yapmamak

**Ne oluyor?**
"Modelimiz %90 accuracy elde etti" diyorsunuz. Ama basit bir logistic regression %88 yapıyorsa, derin öğrenmenin getirisi ne?

**Çözüm:**
- Her zaman baseline modeller ekleyin
  - Random classifier
  - Basit modeller (logistic regression, random forest)
  - Insan performansı (varsa)
- İstatistiksel anlamlılık testi yapın (McNemar, DeLong)

## Hata 8: Annotation Kalitesini Önemsememek

**Ne oluyor?**
Tek bir kişi, aceleyle etiketlemiş. Tutarsızlıklar, hatalar var. Model bu gürültüyü öğreniyor.

**Çözüm:**
- Birden fazla annotator kullanın
- Inter-rater agreement hesaplayın (Cohen's Kappa > 0.7 ideal)
- Belirsiz vakalar için konsensüs mekanizması kurun
- Annotation guideline yazın

## Hata 9: Reproducibility Düşünmemek

**Ne oluyor?**
Makale kabul edildi. Birileri replike etmek istiyor ama seed değerleri yok, kod yok, versiyon bilgisi yok.

**Çözüm:**
- Random seed'leri sabitleyin ve raporlayın
- Kod paylaşın (GitHub)
- Yazılım versiyonlarını belirtin
- requirements.txt veya environment.yml hazırlayın
- İdeal olarak Docker container paylaşın

## Hata 10: Deployment Planı Yapmamak

**Ne oluyor?**
Model mükemmel ama sadece Jupyter notebook'ta çalışıyor. Gerçek dünyada nasıl kullanılacağı düşünülmemiş.

**Çözüm:**
- Inference pipeline tasarlayın
- Model serving düşünün (API, web service)
- Latency/throughput gereksinimlerini belirleyin
- Monitoring ve model drift takibi planlayın
- Regulatory gereksinimler (FDA, CE marking)?

## Gerçek Dünyadan Örnekler

**Epic fail 1:** Bir model, COVID tanısını görüntü yerine yazı fontundan öğrenmişti. Farklı hastaneler farklı yazı tipi kullanıyordu.

**Epic fail 2:** Bir dermatoloji modeli, lezyonun kendisi yerine cetvelin (ölçek için konulan) varlığından tanı koyuyordu. Malign lezyonların yanına daha sık cetvel konuluyormuş.

**Epic fail 3:** Bir göğüs X-ray modeli, taşınabilir cihazdan çekilen görüntüleri "hasta" olarak işaretliyordu. Çünkü taşınabilir cihaz genellikle yatak başında, yani daha hasta kişilerde kullanılıyor.

## Sonuç

Bu hatalardan ders alın. Her birini akılda tutun ve kendi çalışmanızda kontrol edin.

İyi haber: Bu hataları bilerek başlarsanız, çoğundan kaçınabilirsiniz. Kötü haber: Hâlâ yeni ve beklenmedik hatalar yapabilirsiniz. O yüzden mütevazı olun ve peer review sürecine açık olun.

Son modülde bir sonraki adımlarınızı konuşacağız. Kendiniz mi yapacaksınız, destek mi alacaksınız?

Quiz zamanı!
