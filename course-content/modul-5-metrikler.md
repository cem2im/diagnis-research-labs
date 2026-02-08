# Modül 5: Değerlendirme Metrikleri

## Giriş

Modeliniz eğitildi. Şimdi soru: Ne kadar iyi? Bu basit sorunun cevabı göründüğünden karmaşık. Farklı metrikler farklı şeyler ölçer ve yanlış metrik seçimi sizi yanıltabilir.

Bu modülde doğru metriği nasıl seçeceğinizi öğreneceğiz.

## Accuracy Neden Yanıltıcı?

Accuracy, doğru tahmin sayısının toplam tahmin sayısına oranı. Basit, anlaşılır. Ama büyük bir tuzağı var.

Diyelim ki kanser tarama modeli yapıyorsunuz. 1000 hastadan 50'si hasta, 950'si sağlıklı. Model hiç düşünmeden herkese "sağlıklı" dese accuracy ne olur?

950/1000 = %95 accuracy!

Görünüşte mükemmel, ama tek bir hasta bile tespit edilmemiş. İşte bu yüzden dengesiz veri setlerinde accuracy yanıltıcı.

## Confusion Matrix

Gerçek resmi görmek için confusion matrix'e bakmamız gerekiyor.

Dört hücre var:
- **True Positive (TP):** Gerçekten hasta, model "hasta" dedi
- **True Negative (TN):** Gerçekten sağlıklı, model "sağlıklı" dedi
- **False Positive (FP):** Gerçekten sağlıklı, model "hasta" dedi (yanlış alarm)
- **False Negative (FN):** Gerçekten hasta, model "sağlıklı" dedi (kaçırılmış vaka)

Tıpta genellikle FN en tehlikeli. Hasta olduğunu kaçırmak, yanlış alarm vermekten daha kötü.

## Sensitivity ve Specificity

**Sensitivity (Duyarlılık)** = TP / (TP + FN)

Gerçek hastaların yüzde kaçını yakalıyorsunuz? "Recall" veya "True Positive Rate" olarak da bilinir.

Kanser taramada yüksek sensitivity istiyorsunuz. Hiçbir vakayı kaçırmak istemezsiniz.

**Specificity (Özgüllük)** = TN / (TN + FP)

Gerçek sağlıklıların yüzde kaçını doğru tanımlıyorsunuz? "True Negative Rate."

Yüksek specificity = az yanlış alarm.

**Trade-off:** Genellikle sensitivity artarsa specificity düşer, tam tersi de geçerli. İkisini dengelemeniz gerekir.

## Precision ve F1-Score

**Precision** = TP / (TP + FP)

Model "hasta" dediğinde, gerçekten yüzde kaçı hasta? "Positive Predictive Value" olarak da bilinir.

**F1-Score** = 2 × (Precision × Recall) / (Precision + Recall)

Precision ve recall'un harmonik ortalaması. İkisini tek bir sayıda özetler.

**Ne zaman hangisi?**
- Vaka kaçırmak kritikse: Sensitivity'ye odaklanın
- Yanlış alarm maliyetli ise: Precision'a odaklanın
- Dengeye ihtiyaç varsa: F1-Score kullanın

## ROC Eğrisi ve AUC

**ROC (Receiver Operating Characteristic) Eğrisi:** X ekseninde False Positive Rate (1 - Specificity), Y ekseninde True Positive Rate (Sensitivity).

Eşik değerini değiştirdikçe bu iki değer değişir. ROC eğrisi tüm eşik değerlerindeki performansı gösterir.

**AUC (Area Under Curve):** ROC eğrisinin altında kalan alan.

- AUC = 1.0: Mükemmel ayrım
- AUC = 0.5: Rastgele tahmin (para atma)
- AUC > 0.9: Mükemmel
- AUC 0.8-0.9: İyi
- AUC 0.7-0.8: Orta
- AUC < 0.7: Zayıf

**Neden AUC önemli?**
1. Eşik değerinden bağımsız
2. Sınıf dengesizliğinden nispeten az etkilenir
3. Karşılaştırma için standart metrik

## Precision-Recall Eğrisi ve AUPRC

Çok dengesiz veri setlerinde (mesela %1 pozitif) ROC eğrisi bile iyimser olabilir. Böyle durumlarda Precision-Recall eğrisine bakın.

**AUPRC (Area Under Precision-Recall Curve):** Daha zor bir metrik. Düşük değerler görebilirsiniz ama bu daha gerçekçi.

## Multi-class Metrikleri

İkiden fazla sınıf varsa ne olur?

**Macro Average:** Her sınıf için metriği hesapla, ortalamasını al. Tüm sınıflara eşit ağırlık.

**Weighted Average:** Sınıf büyüklüklerine göre ağırlıklı ortalama.

**Micro Average:** Tüm sınıfları birleştirip tek hesaplama.

**Confusion Matrix:** N×N boyutunda olur. Hangi sınıfların karıştığını görürsünüz.

## Segmentation Metrikleri

Piksel bazında değerlendirme gerekiyor.

**Dice Coefficient (F1 Score for Segmentation):**
2 × |A ∩ B| / (|A| + |B|)

0 ile 1 arası. 1'e yakın = iyi örtüşme.

**IoU (Intersection over Union):**
|A ∩ B| / |A ∪ B|

Benzer Dice'a ama daha sert (genellikle daha düşük değerler).

**Hausdorff Distance:** Segmentasyon sınırlarının ne kadar yakın olduğu. Anatomik yapılarda önemli.

## Metrik Seçimi Rehberi

| Durum | Önerilen Metrik |
|-------|-----------------|
| Dengeli sınıflar | Accuracy, F1 |
| Dengesiz sınıflar | AUC, AUPRC, F1 |
| Vaka kaçırmak kritik | Sensitivity |
| Yanlış alarm kritik | Specificity, Precision |
| Multi-class | Macro/Weighted F1 |
| Segmentation | Dice, IoU |

## Confidence Interval

Tek bir sayı yeterli değil. Güven aralığı raporlayın.

**Bootstrapping:** Veriyi yeniden örnekleyerek metriğin dağılımını tahmin edin. 95% CI (Confidence Interval) verin.

Mesela: "AUC: 0.87 (95% CI: 0.82-0.91)"

Bu, sonucunuzun ne kadar güvenilir olduğunu gösterir.

## Sonuç

Metrik seçimi kritik. Yanlış metrik, yanlış sonuç demek.

Önerilerim:
1. Birden fazla metrik raporlayın
2. Confusion matrix gösterin
3. ROC eğrisi çizin
4. Güven aralığı ekleyin
5. Probleme uygun metriği vurgulayın

Sonraki modülde yayın hazırlığını konuşacağız. TRIPOD guidelines, external validation, methods section...

Quiz zamanı!
