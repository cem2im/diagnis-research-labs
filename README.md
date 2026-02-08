# Diagnis AI Lab

> Tıbbi araştırmacılar için özel yapay zeka çözümleri

**Live Site:** [cem2im.github.io/diagnis-research-labs](https://cem2im.github.io/diagnis-research-labs/)

**Domain:** [diagnis.ai](https://diagnis.ai)

---

## 📋 İçindekiler

- [Genel Bakış](#-genel-bakış)
- [Sayfa Yapısı](#-sayfa-yapısı)
- [Tasarım Sistemi](#-tasarım-sistemi)
- [Bileşenler](#-bileşenler)
- [İnteraktif Araçlar](#-i̇nteraktif-araçlar)
- [Kurs Sistemi](#-kurs-sistemi)
- [Teknik Detaylar](#-teknik-detaylar)
- [Deployment](#-deployment)
- [Geliştirme](#-geliştirme)

---

## 🎯 Genel Bakış

Diagnis AI Lab, akademik araştırmacılara yapay zeka destekli araştırma hizmetleri sunan bir şirkettir. Bu web sitesi:

- **Hedef Kitle:** Tıp fakültesi araştırmacıları, akademisyenler, doktora öğrencileri
- **Değer Önerisi:** AI model geliştirme, publication-ready çıktılar
- **Dil Desteği:** İngilizce ve Türkçe (tam çeviri)
- **Tasarım:** Linear.app'ten ilham alan dark theme

### Temel Özellikler

- 🌙 Modern dark theme tasarım
- 🌐 Çift dil desteği (EN/TR)
- 🛠️ İnteraktif araçlar (quiz, calculator, research finder)
- 📚 8 modüllük eğitim kursu
- 📱 Tam responsive tasarım
- ✨ Gelişmiş animasyonlar ve efektler

---

## 📄 Sayfa Yapısı

### Ana Sayfalar

| Sayfa | EN | TR | Açıklama |
|-------|----|----|----------|
| Homepage | `index.html` | `tr.html` | Ana landing page |
| Team | `team.html` | `team-tr.html` | Ekip ve yayınlar |
| Why AI | `why-ai.html` | `why-ai-tr.html` | Neden AI kullanmalı |
| Careers | `careers.html` | `careers-tr.html` | Açık pozisyonlar |

### İnteraktif Araçlar

| Araç | EN | TR | Açıklama |
|------|----|----|----------|
| AI Quiz (Viral) | `ai-quiz.html` | `ai-quiz-tr.html` | 20 soruluk viral bilgi testi |
| AI Finder | `quiz.html` | `quiz-tr.html` | Hangi AI modeli uygun |
| Calculator | `calculator.html` | `calculator-tr.html` | Örneklem boyutu hesaplayıcı |
| Research Finder | `research-finder.html` | `research-finder-tr.html` | PubMed AI araştırma bulucu |

### Eğitim İçerikleri

| Sayfa | EN | TR | Açıklama |
|-------|----|----|----------|
| Guide | `guide.html` | `guide-tr.html` | 6 adımlı AI rehberi |
| Mistakes | `mistakes.html` | `mistakes-tr.html` | 10 yaygın hata |
| Case Study | `case-study.html` | `case-study-tr.html` | Animated workflow |
| Course | `course.html` | - | 8 modüllük kurs |

### Toplam: 22 HTML dosyası

---

## 🎨 Tasarım Sistemi

### Renk Paleti

```css
:root {
    /* Arka planlar */
    --bg: #000000;                    /* Ana arka plan */
    --bg-card: #0a0a0a;               /* Kart arka planı */
    --bg-elevated: #111111;           /* Yükseltilmiş yüzeyler */
    
    /* Kenarlıklar */
    --border: rgba(255,255,255,0.08);
    --border-hover: rgba(255,255,255,0.15);
    
    /* Metinler */
    --text: #ffffff;                  /* Birincil metin */
    --text-secondary: #a1a1aa;        /* İkincil metin */
    --text-tertiary: #71717a;         /* Soluk metin */
    
    /* Vurgular */
    --accent: #6366f1;                /* Birincil mor */
    --accent-secondary: #8b5cf6;      /* İkincil mor */
    --gradient: linear-gradient(135deg, #6366f1 0%, #8b5cf6 50%, #a855f7 100%);
    
    /* Durum renkleri */
    --green: #22c55e;                 /* Başarı */
    --red: #ef4444;                   /* Hata */
}
```

### Tipografi

**Font:** Inter (Google Fonts)

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

| Element | Size | Weight | Letter Spacing |
|---------|------|--------|----------------|
| Hero Headline | `clamp(40px, 7vw, 72px)` | 600 | -0.03em |
| Section Title | `clamp(32px, 5vw, 48px)` | 600 | -0.03em |
| Body | 16px | 400 | normal |
| Small | 14px | 400 | normal |
| Label | 13px | 500 | 0.15em |

### Arka Plan Efektleri

#### 1. Grid Background
```css
.grid-bg {
    background-image: 
        linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
    background-size: 80px 80px;
    mask-image: radial-gradient(ellipse at center, black 0%, transparent 70%);
}
```

#### 2. Gradient Mesh
```css
.gradient-mesh {
    background: 
        radial-gradient(ellipse at 20% 0%, rgba(99, 102, 241, 0.15) 0%, transparent 50%),
        radial-gradient(ellipse at 80% 100%, rgba(139, 92, 246, 0.1) 0%, transparent 50%);
    animation: meshMove1 25s ease-in-out infinite;
}
```

#### 3. Aurora Beams
Animasyonlu ışık dalgaları efekti.

### İnteraktif Efektler

#### Cursor Glow
Mouse'u takip eden mor ışık efekti.
```javascript
// 400px çaplı radial gradient
// Purple-indigo renk geçişi
// requestAnimationFrame ile smooth hareket
```

#### Magnetic Buttons
Hover'da mouse'a doğru hafif çekim efekti.
- Çekim gücü: %30
- Uygulanan elementler: `.btn`, `.nav-cta`

#### 3D Card Tilt
Mouse pozisyonuna göre perspektif döndürme.
- Maximum açı: 8°
- Perspective: 1000px
- Hover'da scale: 1.02

### Animasyonlar

| Animasyon | Süre | Easing | Kullanım |
|-----------|------|--------|----------|
| UI Feedback | 0.2s | ease | Buton hover |
| Transitions | 0.3s | ease | Genel geçişler |
| Reveals | 0.8s | cubic-bezier(0.16, 1, 0.3, 1) | Scroll reveal |
| Background | 20-30s | linear infinite | Mesh, aurora |

### Responsive Breakpoints

```css
@media (max-width: 1024px) { /* Tablet */ }
@media (max-width: 768px) { /* Mobile */ }
```

---

## 🧩 Bileşenler

### Badge
```html
<div class="badge">
    <span class="badge-dot"></span>
    Badge Text
</div>
```
Yeşil nokta animasyonlu pulse efekti ile.

### Buttons

**Primary:**
```html
<a href="#" class="btn btn-primary">
    Button Text
    <svg><!-- Arrow --></svg>
</a>
```
Beyaz arka plan, siyah metin, hover'da yukarı kayma.

**Secondary:**
```html
<a href="#" class="btn btn-secondary">Button Text</a>
```
Şeffaf arka plan, kenarlık, hover'da hafif arka plan.

### Cards
```html
<div class="card">
    <div class="feature-icon">
        <svg><!-- Icon --></svg>
    </div>
    <h3>Title</h3>
    <p>Description</p>
</div>
```
Hover'da kenarlık rengi değişir, hafif yukarı kayar.

### Section Header
```html
<div class="section-header">
    <div class="section-label">LABEL</div>
    <h2 class="section-title">Title</h2>
    <p class="section-subtitle">Subtitle</p>
</div>
```

### Navigation
Fixed header, blur backdrop, şeffaf arka plan.
- Logo: 32x32 gradient kare
- Links: 14px, secondary color
- CTA: Primary button style

### Footer
Minimal, border-top, merkez hizalı copyright.

---

## 🛠️ İnteraktif Araçlar

### 1. Viral AI Quiz (`ai-quiz.html`)

20 soruluk AI bilgi testi.

**Özellikler:**
- Rastgele soru sırası
- Zorluk seviyeleri (Kolay, Orta, Zor, Uzman)
- Doğru/yanlış cevap açıklamaları
- "Startup Role" temalı sonuçlar
- Sosyal paylaşım butonları

**Sonuç Temaları:**
| Skor | Rol | Emoji |
|------|-----|-------|
| 0-4 | Zoom'u açamayan yatırımcı | 💼 |
| 5-8 | ChatGPT'ye prompt yazan stajyer | 📝 |
| 9-12 | LinkedIn'de AI paylaşan PM | 📊 |
| 13-16 | Series A alan founder | 🚀 |
| 17-19 | OpenAI'dan teklif alan mühendis | 🔥 |
| 20 | Sam Altman'ı kovup geri alan board member | 👔 |

### 2. AI Model Finder (`quiz.html`)

Araştırma için uygun AI modelini bulan quiz.

**Sorular:**
1. Veri tipi (görüntü, tablo, metin, sinyal)
2. Problem tipi (sınıflandırma, tespit, segmentasyon)
3. Veri miktarı
4. Deneyim seviyesi

**Çıktı:**
- Önerilen model türü
- Neden bu model
- Başlangıç kaynakları

### 3. Sample Size Calculator (`calculator.html`)

Örneklem boyutu hesaplayıcı.

**Girdiler:**
- Task tipi (Image Classification, Object Detection, Segmentation, Tabular, Time Series)
- Complexity (Binary / Multi-class)
- Target accuracy (70% - 95%)

**Çıktılar:**
- Minimum örneklem boyutu
- Train/Val/Test split önerisi
- Görsel grafik
- Benzer çalışma referansları

### 4. PubMed Research Finder (`research-finder.html`)

AI araştırmaları bulan arama motoru.

**Özellikler:**
- Kullanıcı topic girer
- Otomatik AI/ML keyword ekleme
- PubMed E-utilities API (ücretsiz)
- Son 1 yıl original article filtresi
- Max 25 sonuç

**API Kullanımı:**
```javascript
// esearch.fcgi - ID arama
// esummary.fcgi - Detay çekme
// CORS: doğrudan client-side çalışır
```

---

## 📚 Kurs Sistemi

### Kurs: "Sıfırdan AI Paper'a"

8 modüllük kapsamlı AI eğitimi.

**Hedef:** ~2 saat (modül başı ~15 dk)

**Format:** NotebookLM ile audio üretimine uygun markdown içerik

### Modüller

| # | Modül | Dosya | İçerik |
|---|-------|-------|--------|
| 1 | AI Nedir, Neden Şimdi? | `modul-1-ai-nedir.md` | AI/ML/DL farkları, tarihçe |
| 2 | Veri Temelleri | `modul-2-veri-temelleri.md` | Veri tipleri, annotation |
| 3 | Model Seçimi | `modul-3-model-secimi.md` | CNN, Transformer, XGBoost |
| 4 | Model Eğitimi | `modul-4-model-egitimi.md` | Training, overfitting |
| 5 | Metrikler | `modul-5-metrikler.md` | AUC, F1, confusion matrix |
| 6 | Yayın Hazırlığı | `modul-6-yayin-hazirligi.md` | TRIPOD, external validation |
| 7 | Yaygın Hatalar | `modul-7-hatalar.md` | Data leakage, 10 hata |
| 8 | Sonraki Adımlar | `modul-8-sonraki-adimlar.md` | DIY vs outsource |

### İçerik Formatı

Her modül ~1500-2000 kelime:
- Konuşma diliyle yazılmış
- Örnekler ve analojiler
- NotebookLM Audio Overview için optimize

### Web Arayüzü (`course.html`)

**Özellikler:**
- 8 modül kartları (locked/unlocked/completed)
- Modül 1 başta açık
- Quiz geçince sonraki açılır (4/5 gerekli)
- Progress localStorage'da
- Sertifika sistemi (tüm modüller bitince)

### Quiz Sistemi

- Her modül sonunda 5 soru
- Multiple choice (4 seçenek)
- Geçme notu: 4/5 (%80)
- Başarılı: Sonraki modül açılır
- Başarısız: Tekrar deneme

---

## ⚙️ Teknik Detaylar

### Teknoloji Stack

- **Frontend:** Vanilla HTML, CSS, JavaScript
- **Framework:** Yok (statik site)
- **Hosting:** GitHub Pages
- **API:** PubMed E-utilities (ücretsiz)
- **Storage:** localStorage (progress tracking)

### Dosya Yapısı

```
website/
├── index.html              # Ana sayfa (EN)
├── tr.html                 # Ana sayfa (TR)
├── team.html / team-tr.html
├── why-ai.html / why-ai-tr.html
├── careers.html / careers-tr.html
├── ai-quiz.html / ai-quiz-tr.html
├── quiz.html / quiz-tr.html
├── calculator.html / calculator-tr.html
├── research-finder.html / research-finder-tr.html
├── guide.html / guide-tr.html
├── mistakes.html / mistakes-tr.html
├── case-study.html / case-study-tr.html
├── course.html
├── course-content/
│   ├── modul-1-ai-nedir.md
│   ├── modul-2-veri-temelleri.md
│   ├── modul-3-model-secimi.md
│   ├── modul-4-model-egitimi.md
│   ├── modul-5-metrikler.md
│   ├── modul-6-yayin-hazirligi.md
│   ├── modul-7-hatalar.md
│   ├── modul-8-sonraki-adimlar.md
│   └── quizzes.json
├── DESIGN-README.md        # Tasarım sistemi dokümanı
└── README.md               # Bu dosya
```

### Performans

- Tüm CSS inline (HTTP request azaltma)
- Tüm JS inline
- Harici bağımlılık: sadece Google Fonts
- Görsel: Minimal (çoğu CSS/SVG)

### Browser Desteği

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### Erişilebilirlik

- Semantic HTML
- Keyboard navigation (quiz, guide)
- Sufficient color contrast
- Focus states

---

## 🚀 Deployment

### GitHub Pages

```bash
# Repository: cem2im/diagnis-research-labs
# Branch: main
# Folder: /website (root)

git add .
git commit -m "Update"
git push origin main
```

Site otomatik güncellenir: `cem2im.github.io/diagnis-research-labs/`

### Custom Domain

diagnis.ai için:
1. GitHub repo settings → Pages → Custom domain
2. DNS: CNAME record → `cem2im.github.io`
3. HTTPS otomatik aktif

---

## 🔧 Geliştirme

### Yeni Sayfa Ekleme

1. Mevcut sayfayı kopyala (template olarak)
2. İçeriği değiştir
3. Navigation'a link ekle (tüm sayfalarda)
4. TR versiyonunu oluştur
5. Language switcher linklerini güncelle

### Tasarım Checklist

Yeni sayfa için:
- [ ] Inter font import
- [ ] CSS variables kullan
- [ ] grid-bg, gradient-mesh, aurora ekle
- [ ] Cursor glow JavaScript ekle
- [ ] 3D card tilt (interaktif elementler için)
- [ ] Scroll reveal animations
- [ ] Header/navigation (mevcut ile aynı)
- [ ] Footer (mevcut ile aynı)
- [ ] Mobile test
- [ ] Tüm sayfalara navigation linki ekle

### NotebookLM Audio Üretimi

1. `course-content/modul-X-*.md` dosyasını aç
2. NotebookLM'e yükle (Google NotebookLM)
3. "Audio Overview" oluştur
4. Üretilen audio'yu indir
5. Web sayfasına embed et

---

## 📊 Metrikler & Analytics

### Önerilen Tracking

- Google Analytics 4
- Hotjar (heatmaps)
- Form submission tracking

### Hedef KPI'lar

- Sayfa görüntüleme
- Quiz tamamlama oranı
- Form submission (contact, careers)
- Kurs tamamlama oranı
- Ortalama oturum süresi

---

## 🔮 Gelecek Geliştirmeler

### Planlanan

- [ ] WhatsApp chat widget
- [ ] Newsletter signup popup
- [ ] Blog/Updates sayfası
- [ ] Privacy Policy (KVKK)
- [ ] Logo tasarımı
- [ ] Video demo (gerçek)
- [ ] Testimonials carousel
- [ ] Google Analytics entegrasyonu

### Düşünülen

- [ ] Dark/Light mode toggle
- [ ] Çoklu dil (EN, TR, DE, AR)
- [ ] CMS entegrasyonu (blog için)
- [ ] Backend (form submissions)
- [ ] User accounts (kurs için)

---

## 👥 Ekip

**Diagnis AI Lab**
- Cem Şimşek - Founder & Director
- Ataberk Urfalı - AI Engineer
- Ahmet Enes Kılıç - ML Researcher

---

## 📝 Lisans

© 2025 Diagnis AI Lab. Tüm hakları saklıdır.

---

## 📞 İletişim

- **Web:** [diagnis.ai](https://diagnis.ai)
- **Email:** research@diagnis.ai
- **GitHub:** [cem2im/diagnis-research-labs](https://github.com/cem2im/diagnis-research-labs)
