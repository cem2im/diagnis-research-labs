# Modül 3: Doğru Model Seçimi

## Giriş

Veriniz hazır, etiketleriniz tamam. Şimdi soru şu: Hangi modeli kullanacaksınız? Bu modülde farklı model ailelerini ve hangi durumda hangisinin uygun olduğunu konuşacağız.

## Görüntü Verileri için Modeller

Görüntü işlemede altın standart **Convolutional Neural Network (CNN)**, yani evrişimli sinir ağları.

CNN neden bu kadar başarılı? Çünkü görüntülerdeki uzamsal ilişkileri yakalıyor. Bir pikselin yanındaki piksellerle ilişkisi önemli. CNN bunu anlıyor.

**Popüler mimariler:**

**ResNet (Residual Network):** Skip connection denen bir teknikle çok derin ağlar eğitmeyi mümkün kıldı. ResNet-50, ResNet-101 gibi varyasyonları var. Tıbbi görüntülemede çok yaygın.

**EfficientNet:** Daha az parametre ile daha iyi sonuç. Kaynak kısıtlamanız varsa iyi bir seçim.

**VGG:** Eski ama hâlâ kullanılıyor. Basit yapısı anlamayı kolaylaştırıyor.

**DenseNet:** Her katman önceki tüm katmanlara bağlı. Özellik yeniden kullanımı iyi.

**Vision Transformer (ViT):** Son dönemin yıldızı. Transformer mimarisini görüntüye uyguluyor. Büyük veri setlerinde çok başarılı.

**Hangisini seçmeli?** Başlangıç için ResNet-50 veya EfficientNet-B0 iyi tercihler. Çok veri varsa ViT deneyebilirsiniz.

## Tablo Verileri için Modeller

Tablo verisi farklı bir dünya. Burada derin öğrenme her zaman en iyisi değil.

**Klasik makine öğrenmesi:**

**Random Forest:** Birden fazla karar ağacının ortalaması. Yorumlaması kolay, overfitting'e dayanıklı.

**Gradient Boosting (XGBoost, LightGBM, CatBoost):** Yarışmalarda şampiyon. Tablo veride genellikle en iyi performans.

**Lojistik Regresyon:** Basit ama güçlü. Yorumlanabilirlik önemliyse ilk tercih.

**Derin öğrenme:**

**Multi-Layer Perceptron (MLP):** Basit yapay sinir ağı. Tablo veri için de kullanılabilir ama genellikle XGBoost'tan iyi değil.

**TabNet:** Tablo veri için özel tasarlanmış derin öğrenme. Attention mekanizması var.

**Tavsiye:** Tablo veride önce XGBoost veya Random Forest deneyin. Sonra karşılaştırma için derin öğrenme ekleyin.

## Metin Verileri için Modeller

Metin işleme, doğal dil işleme (NLP) alanına giriyor.

**Transformer mimarisi:** 2017'de "Attention Is All You Need" makalesiyle devrim oldu. Şimdi NLP'nin standardı.

**BERT (Bidirectional Encoder Representations from Transformers):** Google'dan. Metni iki yönlü okuyor. Tıbbi metinler için BioBERT, ClinicalBERT gibi özelleştirilmiş versiyonlar var.

**GPT serisi:** OpenAI'dan. Metin üretmede çok başarılı. Ama sınıflandırma için BERT genellikle daha iyi.

**Tıbbi NLP için öneriler:**
- Tıbbi raporlardan bilgi çıkarma: BioBERT veya ClinicalBERT
- Metin sınıflandırma: BERT fine-tuning
- Duygu/sentiment analizi: BERT

## Zaman Serisi için Modeller

EKG, EEG gibi sinyaller için özel yaklaşımlar var.

**LSTM (Long Short-Term Memory):** Uzun süreli bağımlılıkları öğrenebilen RNN türü. Zaman serisinde klasik.

**GRU (Gated Recurrent Unit):** LSTM'in basitleştirilmiş hali. Daha az parametre, bazen daha iyi.

**Temporal CNN (1D CNN):** Zaman serisi üzerinde evrişim. LSTM'den daha hızlı eğitilir.

**Transformer:** Zaman serisine de uygulanabiliyor. Özellikle çok uzun dizilerde avantajlı.

## Transfer Learning

Şimdi çok önemli bir konsept: Transfer learning, yani aktarım öğrenmesi.

Fikir şu: Büyük veri setlerinde eğitilmiş bir modeli alıyorsunuz, kendi küçük veri setinize adapte ediyorsunuz. Sıfırdan eğitmek yerine, öğrenilmiş özellikleri kullanıyorsunuz.

**ImageNet üzerinde eğitilmiş modeller** görüntü işlemede standart başlangıç noktası. 14 milyon görüntüden öğrenilmiş özellikler, sizin 1000 görüntünüze aktarılıyor.

**Transfer learning nasıl yapılır?**
1. Pre-trained model yükleyin (ResNet-50 ImageNet ağırlıklarıyla)
2. Son katmanları değiştirin (sizin sınıf sayınıza göre)
3. Ya sadece son katmanları eğitin, ya da tüm modeli düşük learning rate ile fine-tune edin

**Ne kadar veri varsa:**
- Çok az veri (<500): Sadece son katmanları eğitin
- Orta miktarda (500-5000): Son birkaç katmanı unfreeze edin
- Çok veri (>5000): Tüm modeli fine-tune edin

## Model Karşılaştırma

Tek bir model değil, birden fazla model deneyin. Karşılaştırmalı sonuçlar makalenizi güçlendirir.

Mesela:
- ResNet-50 vs EfficientNet-B0 vs ViT
- XGBoost vs Random Forest vs Lojistik Regresyon
- BERT vs BioBERT

**Ensemble:** Birden fazla modelin tahminlerini birleştirmek genellikle tek modelden iyi sonuç verir. Basit oylama veya ağırlıklı ortalama.

## Sonuç

Model seçimi deneye dayalı bir süreç. Ama bazı kurallar var:
- Görüntü = CNN (ResNet, EfficientNet) veya ViT
- Tablo = XGBoost veya Random Forest
- Metin = BERT veya varyasyonları
- Zaman serisi = LSTM veya Temporal CNN

Transfer learning kullanmayı unutmayın - özellikle az veriniz varsa hayat kurtarır.

Sonraki modülde model eğitiminin detaylarına ineceğiz. Train/test split, overfitting, regularization...

Quiz zamanı!
