# Diagnis Research Labs - Design System

## Overview
Linear.app-inspired dark theme with purple accents and smooth animations.

---

## Color Palette

```css
:root {
    --bg: #000000;              /* Pure black background */
    --bg-card: #0a0a0a;         /* Slightly lighter for cards */
    --bg-elevated: #111111;     /* Elevated surfaces */
    --border: rgba(255,255,255,0.08);
    --border-hover: rgba(255,255,255,0.15);
    --text: #ffffff;            /* Primary text */
    --text-secondary: #a1a1aa;  /* Secondary text */
    --text-tertiary: #71717a;   /* Muted text */
    --accent: #6366f1;          /* Primary purple */
    --accent-secondary: #8b5cf6;
    --gradient: linear-gradient(135deg, #6366f1 0%, #8b5cf6 50%, #a855f7 100%);
    --green: #22c55e;           /* Success */
    --red: #ef4444;             /* Error */
}
```

---

## Typography

**Font Family:** Inter (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

**Font Sizes:**
- Hero headline: `clamp(40px, 7vw, 72px)`
- Section title: `clamp(32px, 5vw, 48px)`
- Body: `16px`
- Small: `14px`
- Label: `13px`

**Font Weights:**
- Headlines: 600
- Body: 400
- Labels: 500

**Letter Spacing:**
- Headlines: `-0.03em`
- Labels: `0.15em` (uppercase)

---

## Background Effects

### 1. Grid Background
```css
.grid-bg {
    position: fixed;
    inset: 0;
    background-image: 
        linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
    background-size: 80px 80px;
    mask-image: radial-gradient(ellipse at center, black 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
}
```

### 2. Gradient Mesh
```css
.gradient-mesh {
    position: fixed;
    inset: 0;
    background: 
        radial-gradient(ellipse at 20% 0%, rgba(99, 102, 241, 0.15) 0%, transparent 50%),
        radial-gradient(ellipse at 80% 100%, rgba(139, 92, 246, 0.1) 0%, transparent 50%);
    animation: meshMove1 25s ease-in-out infinite;
}
```

### 3. Aurora Beams
```css
.aurora {
    position: fixed;
    width: 200%;
    height: 200%;
    top: -50%;
    left: -50%;
    background: repeating-linear-gradient(
        100deg,
        transparent 0%,
        rgba(99, 102, 241, 0.03) 10%,
        transparent 20%
    );
    animation: auroraWave 20s linear infinite;
}
```

---

## Interactive Effects

### 1. Cursor Glow
```javascript
// Follows mouse with smooth easing
const cursorGlow = document.createElement('div');
cursorGlow.className = 'cursor-glow';
// 400px radial gradient, purple-indigo
// Use requestAnimationFrame for smooth movement
```

### 2. Magnetic Buttons
```javascript
// Buttons pull slightly toward cursor on hover
// 30% magnetic strength
// Apply to .btn, .nav-cta
```

### 3. 3D Card Tilt
```javascript
// Cards tilt based on mouse position
// Max 8° rotation
// Perspective: 1000px
// Scale up slightly on hover (1.02)
// Add shadow on hover
```

---

## Animations

### Scroll Reveal
```javascript
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
}, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
```

### Stats Counter
```javascript
// Count up from 0 when element enters viewport
// Use easeOutCubic easing
// Duration: 2 seconds
```

### Text Reveal
```javascript
// Hero headline words fade in one by one
// Staggered delay: 0.1s between words
```

### Parallax
```javascript
// Grid: 0.3x scroll speed
// Glow 1: 0.15x scroll speed
// Glow 2: -0.1x (inverse)
```

---

## Components

### Badge
```html
<div class="badge">
    <span class="badge-dot"></span>
    Badge Text
</div>
```
```css
.badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 6px 14px;
    background: rgba(99, 102, 241, 0.1);
    border: 1px solid rgba(99, 102, 241, 0.2);
    border-radius: 100px;
    font-size: 13px;
    color: var(--accent);
}
.badge-dot {
    width: 6px; height: 6px;
    background: #22c55e;
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
}
```

### Button Primary
```html
<a href="#" class="btn btn-primary">
    Button Text
    <svg><!-- Arrow icon --></svg>
</a>
```
```css
.btn-primary {
    background: var(--text);
    color: var(--bg);
    padding: 14px 24px;
    border-radius: 12px;
    font-weight: 500;
}
.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 30px rgba(255,255,255,0.15);
}
```

### Button Secondary
```css
.btn-secondary {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text);
}
.btn-secondary:hover {
    border-color: var(--border-hover);
    background: rgba(255,255,255,0.03);
}
```

### Card
```css
.card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 32px;
    transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
.card:hover {
    border-color: var(--border-hover);
    transform: translateY(-4px);
}
```

### Feature Card with Icon
```css
.feature-icon {
    width: 48px; height: 48px;
    background: rgba(99, 102, 241, 0.1);
    border: 1px solid rgba(99, 102, 241, 0.2);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.feature-icon svg {
    width: 24px; height: 24px;
    color: var(--accent);
}
```

### Section Header
```html
<div class="section-header">
    <div class="section-label">LABEL</div>
    <h2 class="section-title">Title Here</h2>
    <p class="section-subtitle">Subtitle text here.</p>
</div>
```

---

## Header / Navigation

```css
header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
    padding: 0 2rem;
    background: rgba(0,0,0,0.5);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
}
```

**Logo:**
- 32x32px gradient square with rounded corners (8px)
- SVG icon inside (white, 18x18)
- Font-weight 600, font-size 15px

**Nav Links:**
- Font-size 14px
- Color: var(--text-secondary)
- Hover: var(--text)

---

## Footer

```css
footer {
    padding: 32px 2rem;
    border-top: 1px solid var(--border);
    text-align: center;
}
.footer-text {
    font-size: 14px;
    color: var(--text-tertiary);
}
```

---

## Responsive Breakpoints

```css
@media (max-width: 1024px) {
    /* Tablet */
    .features-grid { grid-template-columns: 1fr; }
}

@media (max-width: 768px) {
    /* Mobile */
    nav { display: none; }
    section { padding: 80px 1.5rem; }
}
```

---

## Icons

Use Feather-style SVG icons:
- Stroke-based (not filled)
- stroke-width: 2
- stroke-linecap: round
- stroke-linejoin: round

**No emojis in main UI** - only for quiz results or playful elements.

---

## Animation Timing

- **Fast (UI feedback):** 0.2s ease
- **Normal (transitions):** 0.3s ease
- **Slow (reveals):** 0.8s cubic-bezier(0.16, 1, 0.3, 1)
- **Background animations:** 20-30s linear infinite

---

## Checklist for New Pages

- [ ] Import Inter font
- [ ] Use CSS variables from this guide
- [ ] Add grid-bg, gradient-mesh, aurora
- [ ] Add cursor glow JavaScript
- [ ] Add 3D card tilt for interactive elements
- [ ] Add scroll reveal animations
- [ ] Match header/navigation
- [ ] Match footer
- [ ] Test on mobile
- [ ] Add to navigation on all pages

---

## File Structure

```
website/
├── index.html          # Main landing (EN)
├── tr.html             # Turkish landing
├── team.html           # Team (EN)
├── team-tr.html        # Team (TR)
├── why-ai.html         # Why AI (EN)
├── why-ai-tr.html      # Why AI (TR)
├── ai-quiz.html        # Viral quiz (EN)
├── ai-quiz-tr.html     # Viral quiz (TR)
├── quiz.html           # AI Finder quiz
├── calculator.html     # Sample Size Calculator
├── case-study.html     # Animated workflow
├── guide.html          # AI Research Guide
├── mistakes.html       # Common Mistakes
├── research-finder.html # PubMed Finder
└── DESIGN-README.md    # This file
```
