# Modül 4: Model Eğitimi Temelleri

## Giriş

Modelinizi seçtiniz, veriniz hazır. Şimdi eğitim zamanı. Bu modülde eğitim sürecinin temellerini, nelere dikkat etmeniz gerektiğini ve en yaygın hataları konuşacağız.

## Train/Validation/Test Split

Bu konuya bir önceki modülde değindik ama çok önemli olduğu için tekrar edelim.

**Training set:** Model bundan öğrenir. Parametre güncellemeleri bu set üzerinden yapılır.

**Validation set:** Eğitim sırasında modelin "görülmemiş" veri üzerindeki performansını izlersiniz. Hyperparameter seçimi burada yapılır.

**Test set:** Final değerlendirme. Makaleye yazacağınız sonuçlar buradan gelir. Eğitim sürecinde asla kullanılmamalı.

**Tipik oranlar:** 70/15/15 veya 80/10/10.

## Hasta Bazlı Bölünme - Kritik Nokta

Bu çok yaygın bir hata ve makalenizi reddettirmek için yeterli.

Diyelim bir hastadan 50 endoskopi görüntüsü aldınız. Bu görüntüler farklı açılardan ama aynı hastanın aynı lezyonları. Eğer bu görüntüleri rastgele train/test'e dağıtırsanız ne olur?

Model, test setindeki görüntüyle neredeyse aynı olan bir görüntüyü training'de görmüş olur. Bu **data leakage**. Model gerçekten lezyonu öğrenmemiş, sadece "bu hastayı daha önce gördüm" demiş.

**Çözüm:** Bölünmeyi hasta bazında yapın. Bir hastanın tüm görüntüleri ya training'de ya da test'te olmalı, asla karışmamalı.

## Overfitting Nedir?

Overfitting, modelin eğitim verisini "ezberlemesi." Training'de %99 doğruluk, test'te %60. Bu felaket.

**Belirtileri:**
- Training loss düşüyor, validation loss bir noktadan sonra artıyor
- Training accuracy çok yüksek, validation accuracy düşük
- Model eğitim setindeki gürültüyü bile öğrenmiş

**Neden olur?**
- Model çok karmaşık (çok fazla parametre)
- Veri çok az
- Çok uzun eğitim

## Overfitting'i Önleme

Birden fazla strateji var.

**1. Regularization:**
- L1/L2 regularization: Ağırlıkları küçük tutmaya zorlar
- Dropout: Eğitim sırasında rastgele nöronları kapatır
- Batch normalization: Katmanlar arası normalizasyon

**2. Early Stopping:**
Validation loss artmaya başlayınca eğitimi durdurun. Genellikle "patience" parametresi kullanılır - 5-10 epoch boyunca iyileşme yoksa dur.

**3. Data Augmentation:**
Eğitim verisini yapay olarak çoğaltma. Model daha çeşitli örnekler görür.

**4. Daha az karmaşık model:**
ResNet-152 yerine ResNet-18, EfficientNet-B7 yerine EfficientNet-B0.

**5. Cross-validation:**
Veriyi k parçaya bölün, k kez farklı kombinasyonlarla eğitin. Daha güvenilir performans tahmini.

## Learning Rate

Learning rate, modelin ne kadar büyük adımlarla öğrendiğini belirler.

**Çok yüksek:** Model diverge eder, öğrenemez.
**Çok düşük:** Eğitim çok yavaş, local minima'da takılabilir.

**Tipik başlangıç değerleri:**
- Adam optimizer ile: 1e-3 veya 1e-4
- Transfer learning yaparken: 1e-4 veya 1e-5 (daha düşük)

**Learning rate scheduling:**
Eğitim ilerledikçe learning rate'i düşürmek genellikle iyi sonuç verir. StepLR, CosineAnnealingLR gibi scheduler'lar var.

## Batch Size

Bir seferde kaç örnek üzerinden gradient hesaplanacağı.

**Büyük batch:**
- Eğitim daha stabil
- GPU belleği daha çok kullanır
- Genellikle daha yüksek learning rate gerektirir

**Küçük batch:**
- Eğitim daha gürültülü
- Bazı araştırmalara göre generalization daha iyi
- Düşük bellek kullanımı

**Tipik değerler:** 16, 32, 64. GPU belleğinize göre ayarlayın.

## Epoch Sayısı

Tüm eğitim verisi üzerinden bir geçiş = bir epoch.

Ne kadar epoch? "Yeterli kadar." Early stopping kullanıyorsanız, yüksek bir değer verin (mesela 100) ve validation performansı düşmeye başlayınca otomatik dursun.

**Dikkat:** Çok az epoch = underfitting (model yeteri kadar öğrenememiş). Çok fazla epoch = overfitting riski.

## Loss Function

Model neyi optimize etmeye çalışıyor? Loss function bunu belirler.

**Binary classification:** Binary Cross-Entropy Loss
**Multi-class classification:** Categorical Cross-Entropy Loss
**Regression:** Mean Squared Error (MSE) veya Mean Absolute Error (MAE)
**Segmentation:** Dice Loss veya Combination Loss (BCE + Dice)

**Imbalanced data için:**
- Weighted Cross-Entropy: Az olan sınıfa daha fazla ağırlık
- Focal Loss: Kolay örnekleri az, zor örnekleri çok cezalandırır

## Optimizer

Ağırlıkları nasıl güncelleyeceğinizi belirler.

**Adam:** Varsayılan seçim. Çoğu durumda iyi çalışır.
**SGD with Momentum:** Bazen Adam'dan daha iyi generalize eder.
**AdamW:** Weight decay düzeltmeli Adam. Fine-tuning için popüler.

Başlangıç için Adam kullanın, gerekirse diğerlerini deneyin.

## Eğitim Süreci Özet

1. Veriyi train/val/test olarak ayırın (hasta bazlı!)
2. Model seçin, pre-trained weights yükleyin
3. Loss function ve optimizer belirleyin
4. Hyperparameters: learning rate, batch size, epoch sayısı
5. Eğitimi başlatın, validation loss'u izleyin
6. Early stopping ile durdurun
7. En iyi validation performansı veren modeli kaydedin
8. Final değerlendirmeyi test seti üzerinde yapın

## Sonuç

Model eğitimi sabır işi. İlk denemeniz muhtemelen mükemmel olmayacak. Hyperparameter tuning yapın, farklı stratejiler deneyin.

Ama en önemli şey: Test setinizi kirletmeyin. O set final sınav. Daha önce görmemelisi.

Sonraki modülde metrikleri konuşacağız. Modeliniz %90 doğruluk verdi. Bu iyi mi? Accuracy gerçekten doğru metrik mi? Öğreneceğiz.

Quiz zamanı!
