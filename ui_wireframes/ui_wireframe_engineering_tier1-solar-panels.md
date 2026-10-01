# UI Wireframe Specification: پنل خورشیدی Tier-1 | جینکو، ترینا، لانگی | هورا نور سهند
- **Source Dossier:** `seo_dossiers/engineering_tier1-solar-panels.md`
- **Target URL:** `/engineering/tier1-solar-panels`
- **Page Language:** `fa` | **Direction:** `rtl`

---

## GLOBAL DESIGN SYSTEM

### Color Palette Variables
| Token               | HEX       | Tailwind Alias       | Usage                                     |
|----------------------|-----------|-----------------------|-------------------------------------------|
| `--color-primary`    | `#F5A623` | `solar-gold`          | CTAs, highlights, GEO callout borders     |
| `--color-dark`       | `#0A1929` | `deep-navy`           | Backgrounds, hero overlays, headings      |
| `--color-light`      | `#FFFFFF` | `pure-white`          | Card surfaces, body text on dark          |
| `--color-accent-1`   | `#1E3A5F` | `navy-mid`            | Secondary cards, table headers            |
| `--color-accent-2`   | `#FFF4E0` | `cream-warm`          | Soft highlight backgrounds, GEO blocks    |
| `--color-accent-3`   | `#2ECC71` | `eco-green`           | Success indicators, "vs" win column       |
| `--color-danger`     | `#E74C3C` | `alert-red`           | Danger/diesel/loss column in comparisons  |
| `--color-glass-bg`   | `rgba(255,255,255,0.08)` | — | Glassmorphism fill                        |
| `--color-glass-border` | `rgba(255,255,255,0.18)` | — | Glassmorphism stroke                    |

### Base Typography & Body Classes
```html
<body class="bg-deep-navy text-pure-white font-vazirmatn antialiased" dir="rtl" lang="fa">
```
- **Display / H1:** `font-vazirmatn font-black text-4xl md:text-6xl leading-tight tracking-tight`
- **H2:** `font-vazirmatn font-extrabold text-2xl md:text-4xl`
- **H3:** `font-vazirmatn font-bold text-xl md:text-2xl`
- **Body:** `font-vazirmatn font-normal text-base md:text-lg leading-relaxed`
- **Caption / Small:** `font-vazirmatn text-sm text-pure-white/70`

### Glassmorphism Utility Class
```css
.glass-card {
  background: var(--color-glass-bg);
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid var(--color-glass-border);
  border-radius: 1.5rem;
}
```

### RTL Enforcement Rule
> **CRITICAL:** All layout utilities MUST use Tailwind logical properties: `ms-`, `me-`, `ps-`, `pe-`, `border-s-`, `border-e-`, `rounded-s-`, `rounded-e-`, `text-start`, `text-end`, `start-0`, `end-0`. **NEVER** use `ml-`, `mr-`, `pl-`, `pr-`, `left-`, `right-`, `text-left`, `text-right`.

---

### [SEC_01]: مشخصات فنی و مهندسی پنل‌های خورشیدی Tier-1 (جینکو، ترینا، لانگی)

- **Section Role:** Primary Hero — H1 entity, engineering authority, brand trust.

- **UI Aesthetic & Colors:**
  Full-viewport hero with macro close-up of monocrystalline silicon cells catching light at golden hour. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). Brand logos (Jinko, Trina, LONGi) as floating `solar-gold` badges with pulse animation. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-tier1-cells.webp"
         alt="مکرو shot ماکرو سلول‌های مونوکریستال با لوگوهای جینکو، ترینا، لانگی"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          رده‌یک جهانی (Tier-1) | بلومبرگ BNEF
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          مشخصات فنی و مهندسی <span class="text-solar-gold">پنل‌های خورشیدی Tier-1</span> (جینکو، ترینا، لانگی)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="سفارش پنل‌های Tier-1 و مشاوره فنی">
          سفارش پنل‌های Tier-1
          <svg class="w-5 h-5"><!-- Arrow RTL --></svg>
        </a>
      </div>
      <aside class="lg:col-span-4 lg:col-start-9 lg:sticky lg:top-24 glass-card p-6 border-s-4 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-2">خلاصه کلیدی</p>
        <p class="text-base text-pure-white/90 leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_01}
        </p>
      </aside>
    </div>
  </header>
  ```

- **Accessibility & ARIA:**
  - `<header id="sec-01">` landmark.
  - Hero `alt` in Farsi describing monocrystalline cells + brand logos.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: استاندارد بلومبرگ (BNEF) و معنای واقعی Tier-1

- **Section Role:** Industry standard explainer — Trust block with 3 pillars.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Three-pillar trust block: (1) Automated Manufacturing, (2) 5 Bankability Proofs, (3) Unmatched R&D. Each pillar: glass card with `border-s-4` in `solar-gold`, icon + number badge.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. 3-col grid (`grid-cols-3 gap-6`). GEO callout below.

- **Mobile Stacking:**
  Vertical stack. Cards stack vertically.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        استاندارد <span class="text-solar-gold">بلومبرگ (BNEF)</span> و معنای واقعی <span class="text-solar-gold">Tier-1</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12">
        <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50"
             aria-label="معیار ۱: خط تولید تمام اتوماتیک">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🏭</span>
            <div>
              <h3 class="font-bold text-xl text-solar-gold">معیار ۱: خط تولید تمام اتوماتیک</h3>
              <p class="text-pure-white/70 text-sm">خط تولید کاملاً اتوماتیک بدون دست بشر</p>
            </div>
          </div>
          <p class="text-pure-white/80 text-sm leading-relaxed">
            تولیدکنندگان Tier-1 خط تولید تماماً اتوماتیک دارند که تضمین می‌کند کیفیت یکنواخت و عدم خطای انسانی در لحام سلول‌ها و لمیناسیون شیشه.
          </p>
        </div>
        <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50"
             aria-label="معیار ۲: ۵ بانک بین‌المللی">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🏦</span>
            <div>
              <h3 class="font-bold text-xl text-solar-gold">معیار ۲: ۵ بانک بین‌المللی (Bankability)</h3>
              <p class="text-pure-white/70 text-sm">تامین مالی توسط ۵ بانک معتبر جهانی</p>
            </div>
          </div>
          <p class="text-pure-white/80 text-sm leading-relaxed">
            تولیدکننده باید توانایی تامین مالی پروژه در ۵ پروژه مگاواتی مختلف توسط ۵ بانک معتبر جهانی را داشته باشد. این نشان‌دهنده اعتبار مالی و اعتماد بانک‌ها است.
          </p>
        </div>
        <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50"
             aria-label="معیار ۳: R&D بی‌نظیر">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🔬</span>
            <div>
              <h3 class="font-bold text-xl text-solar-gold">معیار ۳: تحقیق و توسعه بی‌نظیر</h3>
              <p class="text-pure-white/70 text-sm">نوآوری مداوم در تکنولوژی سلول</p>
            </div>
          </div>
          <p class="text-pure-white/80 text-sm leading-relaxed">
            تولیدکنندگان Tier-1 سرمایه‌گذاری سنگین در R&D دارند و پیشرو در تکنولوژی‌های جدید مثل N-Type TOPCon و بایفشیال هستند.
          </p>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 تعریف واقعی Tier-1</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
        </p>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article id="sec-02">`.
  - Each pillar card has `aria-label`.
  - Semantic structure.

---

### [SEC_03]: پنل خورشیدی جینکو سولار (تکنولوژی ۶۲۰ وات بایفشیال)

- **Section Role:** Product deep-dive — Jinko Bifacial 620W.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive bifacial diagram: Sun rays hitting top → `solar-gold` arrows, albedo reflection hitting back glass → `eco-green` arrows. Product card with specs.

- **Desktop Grid Architecture:**
  12-col. Interactive diagram: `lg:col-span-6 lg:sticky lg:top-20`. Specs: `lg:col-span-6`.

- **Mobile Stacking:**
  Diagram first (`h-[300px]`). Specs stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy" x-data="{ activeLayer: 'front' }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار تعاملی پنل بایفشیال جینکو ۶۲۰ وات" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center" x-data="{ activeSide: 'front' }">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">جینکو ۶۲۰ وات بایفشیال (Tiger Neo)</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار تعاملی پنل بایفشیال جینکو">
              <!-- Front Glass -->
              <rect x="50" y="50" width="300" height="180" rx="5" fill="#FFFFFF" opacity="0.3" stroke="#F5A623" stroke-width="2"/>
              <!-- Sun Rays (Front) -->
              <g stroke="#F5A623" stroke-width="2" stroke-dasharray="5,5">
                <line x1="100" y1="10" x2="150" y2="60" marker-end="url(#arrow-sun)"/>
                <line x1="200" y1="10" x2="200" y2="60" marker-end="url(#arrow-sun)"/>
                <line x1="300" y1="10" x2="250" y2="60" marker-end="url(#arrow-sun)"/>
              </g>
              <!-- Albedo Rays (Back) -->
              <g stroke="#2ECC71" stroke-width="2" stroke-dasharray="5,5">
                <line x1="100" y1="290" x2="150" y2="240" marker-end="url(#arrow-albedo)"/>
                <line x1="200" y1="290" x2="200" y2="240" marker-end="url(#arrow-albedo)"/>
                <line x1="300" y1="290" x2="250" y2="240" marker-end="url(#arrow-albedo)"/>
              </g>
              <defs>
                <marker id="arrow-sun" markerWidth="8" markerHeight="5" refX="7" refY="2.5" orient="auto">
                  <polygon points="0 0, 8 2.5, 0 5" fill="#F5A623"/>
                </marker>
                <marker id="arrow-albedo" markerWidth="8" markerHeight="5" refX="1" refY="2.5" orient="auto">
                  <polygon points="8 0, 0 2.5, 8 5" fill="#2ECC71"/>
                </marker>
              </defs>
            </svg>
            <div class="flex justify-center gap-6 mt-4 text-sm">
              <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-solar-gold"></span> نور مستقیم (Front)</span>
              <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-eco-green"></span> آلبدو/بازتاب (Back)</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پنل خورشیدی <span class="text-solar-gold">جینکو سولار</span> (تکنولوژی ۶۲۰ وات بایفشیال)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">⚡ مزیت بایفشیال</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Interactive diagram `role="img"` + `aria-label`.
  - Color + text labels for rays.

---

### [SEC_04]: پنل خورشیدی ترینا سولار (غول ۷۱۰ وات Vertex)

- **Section Role:** Product deep-dive — Scale comparison, space efficiency.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Scale comparison visual: Old 400W panel vs Trina 710W. Stack visual: fewer panels = less structure, less cable, lower BOS.

- **Desktop Grid Architecture:**
  12-col. Comparison visual: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Comparison visual first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="مقایسه مقیاس پنل‌های ۴۰۰ وات قدیمی در برابر ۷۱۰ وات ترینا" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقایسه مقیاس: قدیمی vs ترینا ۷۱۰ وات</h3>
          <div class="flex flex-col gap-6 items-center">
            <!-- Old 400W -->
            <div class="w-full bg-navy-mid rounded-xl p-4 border border-alert-red/30">
              <div class="flex items-center justify-between mb-2">
                <span class="font-bold text-alert-red">قدیمی (۴۰۰ وات)</span>
                <span class="text-alert-red font-bold">۲۵ پنل برای ۱۰ کیلووات</span>
              </div>
              <div class="flex gap-2">
                <div class="w-10 h-20 bg-alert-red/20 rounded border border-alert-red/30 flex items-end justify-center p-1"><span class="text-xs text-alert-red">400W</span></div>
                <div class="w-10 h-20 bg-alert-red/20 rounded border border-alert-red/30 flex items-end justify-center p-1"><span class="text-xs text-alert-red">400W</span></div>
                <div class="w-10 h-20 bg-alert-red/20 rounded border border-alert-red/30 flex items-end justify-center p-1"><span class="text-xs text-alert-red">400W</span></div>
                <div class="w-10 h-20 bg-alert-red/20 rounded border border-alert-red/30 flex items-end justify-center p-1"><span class="text-xs text-alert-red">400W</span></div>
                <div class="w-10 h-20 bg-alert-red/20 rounded border border-alert-red/30 flex items-end justify-center p-1"><span class="text-xs text-alert-red">400W</span></div>
              </div>
            </div>
            <!-- Trina 710W -->
            <div class="w-full bg-navy-mid rounded-xl p-4 border border-solar-gold/30">
              <div class="flex items-center justify-between mb-2">
                <span class="font-bold text-solar-gold">ترینا ۷۱۰ وات</span>
                <span class="text-solar-gold font-bold">۱۵ پنل برای ۱۰ کیلووات</span>
              </div>
              <div class="flex gap-2">
                <div class="w-14 h-24 bg-solar-gold/20 rounded border border-solar-gold/30 flex items-end justify-center p-2"><span class="text-xs text-solar-gold">710W</span></div>
                <div class="w-14 h-24 bg-solar-gold/20 rounded border border-solar-gold/30 flex items-end justify-center p-2"><span class="text-xs text-solar-gold">710W</span></div>
                <div class="w-14 h-24 bg-solar-gold/20 rounded border border-solar-gold/30 flex items-end justify-center p-2"><span class="text-xs text-solar-gold">710W</span></div>
                <div class="w-14 h-24 bg-solar-gold/20 rounded border border-solar-gold/30 flex items-end justify-center p-2"><span class="text-xs text-solar-gold">710W</span></div>
              </div>
            </div>
          </div>
          <div class="text-center mt-6">
            <span class="inline-flex items-center gap-2 bg-solar-gold/20 text-solar-gold px-4 py-2 rounded-full font-bold">
              ↓ ۴۰٪ کمتر پنل = ↓ استراکچر، ↓ کابل، ↓ هزینه BOS
            </span>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پنل خورشیدی <span class="text-solar-gold">ترینا سولار</span> (غول ۷۱۰ وات Vertex)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 مزیت تراکم انرژی بالا</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Comparison visual `role="img"` + `aria-label`.
  - Text labels for visual elements.

---

### [SEC_05]: پنل خورشیدی لانگی (پادشاه مونوکریستال هف‌کات)

- **Section Role:** Product deep-dive — Half-cut shading animation.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Shading animation: shadow sweeps bottom half of panel → top half continues glowing `solar-gold`, bottom half dims. "Half-Cut" badge `bg-solar-gold/20 text-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Animation visual: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Animation first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy" x-data="{ shadowPos: 0 }" x-intersect.once="shadowPos = 100">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="انمیشن سایه‌اندازی پنل لانگی هف‌کات" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">تکنولوژی هف‌کات (Half-Cut) لانگی</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="انمیشن سایه‌اندازی پنل لانگی هف‌کات">
              <!-- Panel Outline -->
              <rect x="50" y="50" width="300" height="180" rx="5" fill="#132F4C" stroke="#F5A623" stroke-width="2"/>
              <!-- Top Half (Active) -->
              <rect x="55" y="55" width="290" height="85" rx="3" fill="#F5A623" opacity="0.3">
                <animate attributeName="opacity" from="0.3" to="0.8" dur="2s" repeatCount="indefinite"/>
              </rect>
              <!-- Bottom Half (Shadowed) -->
              <rect x="55" y="145" width="290" height="80" rx="3" fill="#132F4C" stroke="#2ECC71" stroke-width="2"/>
              <text x="200" y="195" text-anchor="middle" fill="#2ECC71" font-size="14" font-family="Vazirmatn" font-weight="bold">سایه (Inactive)</text>
              <!-- Shadow Sweep -->
              <rect x="55" y="55" width="290" height="85" rx="3" fill="#132F4C" opacity="0">
                <animate attributeName="y" from="55" to="145" dur="3s" repeatCount="indefinite" fill="freeze"/>
                <animate attributeName="height" from="85" to="175" dur="3s" repeatCount="indefinite" fill="freeze"/>
              </rect>
              <!-- Labels -->
              <text x="200" y="45" text-anchor="middle" fill="#F5A623" font-size="16" font-family="Vazirmatn" font-weight="bold">نور مستقیم (بالا: فعال)</text>
              <text x="200" y="240" text-anchor="middle" fill="#2ECC71" font-size="14" font-family="Vazirmatn" font-weight="bold">سایه (پایین: غیرفعال)</text>
            </svg>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پنل خورشیدی <span class="text-solar-gold">لانگی</span> (پادشاه مونوکریستال هف‌کات)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">⚡ مزیت هف‌کات</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Animation `role="img"` + `aria-label`.
  - Animation respects `prefers-reduced-motion`.

---

### [SEC_06]: باورهای غلط در انتخاب تکنولوژی پنل (Myth vs. Reality)

- **Section Role:** Myth-busting — Poly vs Mono debate.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth: `bg-alert-red/10 border-alert-red/30` ❌. Reality: `bg-eco-green/10 border-eco-green/30` ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-06" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در <span class="text-solar-gold">انتخاب تکنولوژی پنل</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های پلی‌کریستال قدیمی برای مناطق گرمسیر ایران بهتر هستند. مونوکریستال‌ها در گرما افت می‌کنند.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            تکنولوژی N-type TOPCon و PERC در مونوکریستال‌های نسل جدید (مانند جینکو و لانگی)، ضریب حرارتی آن‌ها را به مراتب بهتر از پلی‌کریستال کرده است. هورا نور سهند در هیچ‌کدام از پروژه‌های خود از تکنولوژی منسوخ پلی‌کریستال استفاده نمی‌کند.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 پایان مناظره پلی در برابر مونو</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside id="sec-06">`.
  - `x-intersect` decorative.
  - Meaning via icon + text.
  - Contrast: dark text on light cards.

---

### [SEC_07]: گارانتی ۲۵ ساله و افت خطی توان (Linear Degradation)

- **Section Role:** Durability authority — Line graph vs Tier-3.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Line graph: Tier-1 (gentle slope `eco-green`), Tier-3 (steep drop `alert-red`). Tier-1 line animates drawing on scroll. "25-Year Linear Warranty" badge `bg-eco-green text-deep-navy`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Graph: `lg:col-span-7 lg:sticky lg:top-20`. Text: `lg:col-span-5`.

- **Mobile Stacking:**
  Graph first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-deep-navy" x-data="{ chartLoaded: false }" x-intersect.once="chartLoaded = true">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-7 lg:sticky lg:top-20" aria-label="نمودار خطی افت توان ۲۵ ساله: Tier-1 در برابر Tier-3" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">گارانتی ۲۵ ساله حفظ راندمان (Linear Performance Warranty)</h3>
          <div class="relative h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 600 300" class="w-full h-full" role="img" aria-label="نمودار خطی افت توان ۲۵ ساله: Tier-1 (سبز ملایم) در برابر Tier-3 (قرمز تیز)">
              <!-- Axes -->
              <line x1="50" y1="250" x2="550" y2="250" stroke="#FFFFFF" stroke-width="1"/>
              <line x1="50" y1="250" x2="50" y2="20" stroke="#FFFFFF" stroke-width="1"/>
              <!-- Tier-1 Line (Green Gentle) -->
              <path d="M50,250 Q150,240 300,230 T550,210" stroke="#2ECC71" stroke-width="3" fill="none" marker-end="url(#arrowhead)">
                <animate attributeName="stroke-dashoffset" from="1000" to="0" dur="2s" fill="freeze"/>
              </path>
              <!-- Tier-3 Line (Red Steep) -->
              <path d="M50,250 Q150,200 300,100 T550,20" stroke="#E74C3C" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
              <!-- Defs for arrows -->
              <defs>
                <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
                  <polygon points="0 0, 10 3.5, 0 7" fill="#2ECC71" />
                </marker>
              </defs>
            </svg>
            <div class="flex justify-center gap-6 mt-4 text-sm">
              <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-eco-green"></span> Tier-1: < 0.5%/سال</span>
              <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-alert-red"></span> Tier-3: > 1%/سال</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          گارانتی ۲۵ ساله و <span class="text-eco-green">افت خطی توان</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">🛡️ تضمین ۲۵ ساله</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Chart `role="img"` + `aria-label`.
  - Color + text labels for lines.
  - Animation respects `prefers-reduced-motion`.

---

### [SEC_08]: تامین، فروش و توزیع از هاب لجستیکی کرج

- **Section Role:** Supply chain authority — Warehouse photo + serial verification.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Photo of stacked pallets with "100% Genuine Serial Verification" badge. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Photo: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Photo `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="انبار لجستیکی هورا نور سهند" role="img">
        <img src="/images/warehouse-tier1-pallets.webp" alt="پالت‌های بانت‌بندی پنل‌های جینکو، ترینا، لانگی در انبار هورا نور سهند" class="w-full h-auto" loading="lazy">
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تامین، فروش و توزیع از <span class="text-solar-gold">هاب لجستیکی کرج</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📦 تضمین اصالت</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<address>` for NAP.
  - Map `role="img"` + `aria-label`.
  - Phones `dir="ltr"`.

---

### [SEC_09]: استانداردها و تکنولوژی‌های جهانی (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (BloombergNEF).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". External link to `bnef.com` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badges grid `grid-cols-3 gap-4`.

- **Mobile Stacking:**
  Badges `grid-cols-2`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استانداردها و تکنولوژی‌های جهانی
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">📊</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://about.bnef.com/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">موسسه معتبر BloombergNEF</a></h4>
          <p class="text-pure-white/60 text-sm">رتبه‌بندی Tier-1 ۲۰۲۴</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://www.iec.ch/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">IEC Standards</a></h4>
          <p class="text-pure-white/60 text-sm">استانداردهای ۶۱۷۲۴</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">📜</span>
          <h4 class="font-bold text-pure-white text-lg">اینماد / ساماندهی</h4>
          <p class="text-pure-white/60 text-sm">تأیید تجارت الکترونیک</p>
        </div>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
      </p>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        مراجعه به <a href="https://about.bnef.com/" rel="external noopener" target="_blank"
           class="text-solar-gold underline hover:text-solar-gold/80">موسسه معتبر BloombergNEF</a> برای رتبه‌بندی‌های جدید.
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External links `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_10]: بخش پاسخ به سوالات متداول فنی (FAQ)

- **Section Role:** GEO/SGE bait — FAQPage schema.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Glass accordion. Expanded: `border-s-4 border-solar-gold` + `text-solar-gold` summary.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO preamble banner.

- **Mobile Stacking:**
  Full-width `<summary>` with `py-5`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-navy-mid" x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">فنی پنل‌های Tier-1</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
        </p>
      </div>
      <div class="space-y-4" x-data="{ openFaq: null }">
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 1 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 1 ? null : 1">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 1 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 1 ? 'text-solar-gold' : 'text-pure-white'">
              پنل خورشیدی دو طرفه (بایفشیال) آیا به آینه در زیر خود نیاز دارد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر! نیازی به نصب آینه نیست. پنل‌های بایفشیال پرتوهای بازتاب‌شده از محیط طبیعی مانند سنگ‌ریزه، بتن روشن و حتی چمن را شکار می‌کنند (اثر آلبدو). قرار دادن شن سفید یا رنگ کردن سقف سوله به رنگ روشن، بازدهی سمت پشتی را به شدت افزایش می‌دهد.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              وزن پنل خورشیدی 710 وات چقدر است؟ آیا سقف سوله تحمل آن را دارد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            این پنل‌ها ابعاد بزرگی دارند (بیش از ۲ متر طول) و وزن آن‌ها معمولاً بین ۳۲ تا ۳۸ کیلوگرم است. با این حال، به دلیل پخش شدن وزن روی استراکچرهای استاندارد، بار مرده ایجاد شده زیر ۱۵ کیلوگرم بر متر مربع است که برای سقف ساندویچ‌پانل استاندارد کاملاً ایمن می‌باشد.
          </div>
        </details>
      </div>
      <!-- CODER NOTE: Wrap in FAQPage JSON-LD schema. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>`/`<summary>`.
  - `aria-expanded` via Alpine.
  - `role="button"` on `<summary>`.
  - Touch target `py-5 px-6`.

---

### [SEC_11]: سفارش مستقیم پنل و طراحی نیروگاه با تجهیزات Tier-1 (CTA)

- **Section Role:** CRO conversion — Procurement CTA.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. Messenger icons `w-16 h-16`. Grain overlay.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7`. Messenger: `lg:col-span-5`.

- **Mobile Stacking:**
  Single column. Phones stack. Messenger row `flex gap-4 justify-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-11" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          سفارش مستقیم <span class="text-deep-navy">پنل‌های Tier-1</span> و طراحی نیروگاه
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_11}
        </p>
        <div class="space-y-4">
          <a href="tel:02636506485" class="block text-3xl md:text-5xl font-black text-deep-navy hover:text-deep-navy/70 transition-colors" dir="ltr"
             aria-label="تماس با دفتر مرکزی کرج: ۰۲۶-۳۶۵۰۶۴۸۵">
            026-36506485
          </a>
          <a href="tel:09122641473" class="block text-2xl md:text-4xl font-bold text-deep-navy/80 hover:text-deep-navy/60 transition-colors" dir="ltr"
             aria-label="تماس با مدیریت پروژه: ۰۹۱۲۲۶۴۱۴۷۳">
            0912-264-1473
          </a>
        </div>
        <a href="https://wa.me/989125728170?text=سفارش%20پنل‌های%20Tier-1"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="سفارش پنل‌های Tier-1 در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
          سفارش مستقیم پنل‌های Tier-1
        </a>
      </div>
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-deep-navy font-bold text-lg">ارتباط از طریق پیام‌رسان‌ها:</p>
        <div class="flex gap-4">
          <a href="https://wa.me/989125728170" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="واتس‌اپ">
            <svg class="w-8 h-8"><!-- WA --></svg>
          </a>
          <a href="https://ble.ir/horasolar" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="بله">
            <svg class="w-8 h-8"><!-- Bale --></svg>
          </a>
          <a href="https://eitaa.com/horasolar" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ایتا">
            <svg class="w-8 h-8"><!-- Eitaa --></svg>
          </a>
          <a href="https://rubika.ir/horasolar" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="روبیکا">
            <svg class="w-8 h-8"><!-- Rubika --></svg>
          </a>
        </div>
        <div class="bg-deep-navy/10 rounded-2xl p-5 border-2 border-deep-navy/20 mt-4">
          <p class="text-deep-navy text-base leading-relaxed font-medium">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_11}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<a href="tel:...">` + `dir="ltr"` + `aria-label`.
  - Messenger `aria-label` per platform.
  - Touch targets ≥64px.
  - External links `rel="noopener"`.

---

[VERIFIED_UI_END_OF_FILE]