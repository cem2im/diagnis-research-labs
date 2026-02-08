# Modül 6: Yayına Hazırlık

## Giriş

Modeliniz harika çalışıyor. AUC 0.92, sensitivity %89, specificity %85. Şimdi bunu dünyaya duyurma zamanı. Ama bekleyin - yayına gönderilmeye hazır mısınız?

Bu modülde bir AI makalesini yayına hazır hale getirmek için yapmanız gerekenleri konuşacağız.

## TRIPOD ve CLAIM Guidelines

Tıbbi yapay zeka makaleleri için iki önemli kılavuz var.

**TRIPOD (Transparent Reporting of a Multivariable Prediction Model for Individual Prognosis or Diagnosis):**

Tahmin modelleri için raporlama standardı. 22 maddeden oluşan bir checklist. Birçok dergi TRIPOD uyumluluğu istiyor.

Önemli noktalar:
- Çalışma tasarımını açıkça belirtin
- Veri kaynağını detaylı tanımlayın
- Eksik verileri nasıl ele aldığınızı söyleyin
- Model geliştirme adımlarını şeffaf anlatın
- Performans ölçümlerini uygun şekilde raporlayın

**CLAIM (Checklist for Artificial Intelligence in Medical Imaging):**

Tıbbi görüntüleme AI çalışmaları için özel. Radiology dergisi yayınladı. 42 maddelik detaylı bir liste.

Kapsadığı konular:
- Veri seti tanımı
- Ground truth nasıl belirlendi
- Model mimarisi detayları
- Eğitim prosedürü
- Değerlendirme metodolojisi
- Sonuçların sunumu

**Tavsiye:** Makale yazmaya başlamadan önce bu checklisti indirin ve her maddeyi kontrol edin.

## External Validation - Neden Şart?

Internal validation: Kendi veri setinizi train/test'e böldünüz, test performansı güzel. Bu yeterli mi?

Hayır.

**External validation:** Tamamen farklı bir kaynaktan veri ile test. Farklı hastane, farklı cihaz, farklı popülasyon.

Neden bu kadar önemli?
1. **Generalizability:** Modeliniz sadece sizin hastanenizde mi çalışıyor?
2. **Hidden biases:** Belki modeliniz cihaz markasını öğrenmiş, hastalığı değil
3. **Reviewer beklentisi:** İyi dergiler artık external validation istiyor

**Nasıl yapılır?**
- Başka bir merkezle işbirliği
- Açık veri setleri (PhysioNet, Grand Challenges, TCIA)
- Prospektif veri toplama

**Performans düşecek:** External validation'da genellikle performans düşer. Bu normal. %5-10 düşüş beklenen. Daha fazlaysa model robust değil demektir.

## Methods Section Nasıl Yazılır?

Methods section, makalenizin reproducibility'sini belirler. Birisi sizin yaptığınızı tekrar edebilmeli.

**Veri:**
- Kaç hasta, kaç görüntü
- Dahil etme/dışlama kriterleri
- Veri toplama periyodu
- Etik kurul onay numarası

**Annotation:**
- Kim etiketledi? Kaç kişi?
- Inter-rater agreement (Cohen's Kappa)
- Etiketleme kriterleri, belirsiz durumlar

**Model:**
- Mimari (ResNet-50, EfficientNet-B0, vs.)
- Pre-training (ImageNet, RadImageNet, vs.)
- Input boyutu, normalizasyon

**Eğitim:**
- Train/val/test split oranları
- Hasta bazlı mı, görüntü bazlı mı?
- Optimizer, learning rate, batch size
- Augmentation teknikleri
- Early stopping kriterleri
- Epoch sayısı

**Değerlendirme:**
- Hangi metrikler?
- Confidence interval nasıl hesaplandı?
- İstatistiksel testler

## Reproducibility Checklist

Kendinize sorun:
- [ ] Kod paylaşılabilir mi? (GitHub)
- [ ] Veri paylaşılabilir mi? (En azından kısmen)
- [ ] Random seed sabitlendi mi?
- [ ] Yazılım versiyonları belirtildi mi? (Python, PyTorch, vs.)
- [ ] Hyperparameter'lar tam olarak belirtildi mi?

**Model Weights:** İdeal olarak eğitilmiş model ağırlıklarını paylaşın. Başkaları doğrudan kullanabilsin.

**Docker Container:** En iyi reproducibility için. Tüm ortamı paketleyip paylaşın.

## Supplementary Materials

Ana metinde her şeyi anlatmak zor. Supplementary materials kullanın.

Neler koyabilirsiniz?
- Detaylı mimari şeması
- Hyperparameter tuning sonuçları
- Ek ROC eğrileri ve confusion matrix'ler
- Ablation studies
- Failure case örnekleri
- Kod linkleri

## Reviewer'lar Ne Bekler?

Peer review sürecinde karşılaşacağınız tipik sorular:

1. **"External validation nerede?"** - Yoksa zayıf nokta
2. **"Data leakage var mı?"** - Hasta bazlı split yaptığınızı açıkça söyleyin
3. **"Baseline karşılaştırma?"** - İnsan performansı, basit modeller
4. **"Class imbalance nasıl ele alındı?"** - Weighted loss, resampling, vs.
5. **"Explainability?"** - GradCAM, SHAP, attention maps
6. **"Clinical utility?"** - Bu model pratikte nasıl kullanılır?
7. **"Limitations?"** - Dürüst olun, zayıf noktalarınızı belirtin

## Etik Konular

Birkaç önemli nokta:

**Etik kurul onayı:** Retrospektif bile olsa çoğu dergi istiyor.

**Hasta gizliliği:** HIPAA, GDPR, KVKK uyumluluğu. Görüntülerde hasta bilgisi olmamalı.

**Bias ve fairness:** Modeliniz belirli grupları dezavantajlı kılıyor mu? Yaş, cinsiyet, etnisite bazında performans farkları?

**AI limitations disclaimer:** Yapay zekanın karar verici değil, yardımcı olduğunu belirtin.

## Dergi Seçimi

Hedeflerinize göre dergi seçin:

**Yüksek impakt:** Nature Medicine, Lancet Digital Health, JAMA Network Open, Radiology, Nature Communications

**Orta impakt ama hızlı:** PLOS ONE, Scientific Reports, Diagnostics, Journal of Medical Internet Research

**Specialty dergiler:** Her alanda AI kabul eden specialty dergiler var. Kendi alanınızın dergilerini araştırın.

**Preprint:** Hızlı duyurmak istiyorsanız medRxiv'e yükleyin, sonra dergi'ye gönderin.

## Sonuç

Yayın hazırlığı zaman alır. TRIPOD/CLAIM checklist'leri takip edin, external validation yapın, methods'u detaylı yazın, reproducibility'yi sağlayın.

Bu aşamayı aceleye getirmeyin. İyi hazırlanmış bir makale, ret oranını düşürür ve daha iyi dergilere kabul şansını artırır.

Sonraki modülde yaygın hatalara bakacağız. Başkalarının düştüğü tuzaklardan ders alalım.

Quiz zamanı!
