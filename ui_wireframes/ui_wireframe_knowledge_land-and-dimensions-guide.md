# UI Wireframe Specification: ابعاد پنل خورشیدی و زمین مورد نیاز نیروگاه | ابعاد و وزن | هورا نور سهند
- **Source Dossier:** `seo_dossiers/knowledge_land-and-dimensions-guide.md`
- **Target URL:** `/knowledge/land-and-dimensions-guide`
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

### [SEC_01]: راهنمای ابعاد و فضای مورد نیاز نیروگاه خورشیدی

- **Section Role:** Primary Hero — Space planning H1, visual layout comparison.

- **UI Aesthetic & Colors:**
  Full-viewport hero with split visual: left shows rooftop layout on industrial shed (Eshtehard style), right shows ground-mounted farm layout. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "Space Planning" badge in `solar-gold`. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Left: 3D layout viewer `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. Right: GEO Callout `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-space-planning.webp"
         alt="مقایسه چیدمان نیروگاه خورشیدی روی سقف سوله و روی زمین باز"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          راهنمای محاسبه فضا
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          راهنمای ابعاد و فضای مورد نیاز <span class="text-solar-gold">نیروگاه خورشیدی</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="محاسبه فضای مورد نیاز پروژه شما">
          محاسبه فضای مورد نیاز
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
  - Hero `alt` in Farsi describing rooftop vs ground layout.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: ابعاد دقیق پنل‌های خورشیدی (۵۵۰ و ۶۰۰ وات)

- **Section Role:** Structured data — Interactive specs table with PDF download.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive data table with hover effects. "Download PDF Specs" button in `solar-gold`. Table headers in `solar-gold`.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Table full-width. "Download PDF" button top-right.

- **Mobile Stacking:**
  Table horizontal scroll (`overflow-x-auto`).

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        ابعاد دقیق <span class="text-solar-gold">پنل‌های خورشیدی</span> (۵۵۰ و ۶۰۰ وات)
      </h2>
      <div class="flex justify-end mb-4">
        <button class="inline-flex items-center gap-2 px-6 py-3 bg-solar-gold text-deep-navy font-bold rounded-xl hover:bg-solar-gold/90 transition-colors"
                role="button" aria-label="دانلود فایل PDF مشخصات فنی پنل‌ها">
          <svg class="w-5 h-5"><!-- Download --></svg>
          دانلود PDF Specs
        </button>
      </div>
      <div class="glass-card p-6 overflow-x-auto">
        <table class="w-full min-w-[700px] text-sm" role="table" aria-label="جدول ابعاد و وزن پنل‌های خورشیدی رده‌یک">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">مدل و توان پنل</th>
              <th scope="col" class="p-4 text-start">طول (میلی‌متر)</th>
              <th scope="col" class="p-4 text-start">عرض (میلی‌متر)</th>
              <th scope="col" class="p-4 text-start">ضخامت فریم (میلی‌متر)</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">مساحت کل</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">Trina Solar 550W</td><td class="p-4">2278</td><td class="p-4">1134</td><td class="p-4">35</td><td class="p-4">2.58 m²</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">Jinko 620W</td><td class="p-4">2465</td><td class="p-4">1134</td><td class="p-4">35</td><td class="p-4">2.79 m²</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">LONGi 710W</td><td class="p-4">2382</td><td class="p-4">1303</td><td class="p-4">35</td><td class="p-4">3.10 m²</td></tr>
          </tbody>
        </table>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📋 نکته مهم</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on all headers.
  - Download button `role="button"` + `aria-label`.

---

### [SEC_03]: وزن پنل خورشیدی چقدر است و آیا سقف سوله تحمل آن را دارد؟

- **Section Role:** B2B Pain Point — Structural safety visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Isometric diagram showing weight distribution across roof purlins. Panel weight badge `30kg` in `solar-gold`. Load distribution heat map: green (safe) → yellow (caution) → red (risk).

- **Desktop Grid Architecture:**
  12-col. Left: Isometric diagram `lg:col-span-6 lg:sticky lg:top-20`. Right: Text + GEO `lg:col-span-6`.

- **Mobile Stacking:**
  Diagram first (`h-[400px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار توزیع بار وزنی پنل‌ها روی پرلین‌های سقف سوله" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">توزیع بار وزنی روی پرلین‌های سقف</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار توزیع بار وزنی پنل‌ها روی پرلین‌ها">
              <!-- Purlins -->
              <line x1="50" y1="80" x2="350" y2="80" stroke="#F5A623" stroke-width="4" stroke-dasharray="8,4"/>
              <line x1="50" y1="150" x2="350" y2="150" stroke="#F5A623" stroke-width="4" stroke-dasharray="8,4"/>
              <line x1="50" y1="220" x2="350" y2="220" stroke="#F5A623" stroke-width="4" stroke-dasharray="8,4"/>
              <!-- Panel Array -->
              <rect x="70" y="90" width="260" height="100" rx="5" fill="#F5A623" opacity="0.3" stroke="#F5A623" stroke-width="2"/>
              <!-- Load Arrows -->
              <path d="M200,170 L200,220" stroke="#F5A623" stroke-width="3" marker-end="url(#arrow-down)"/>
              <text x="200" y="240" text-anchor="middle" fill="#F5A623" font-size="14" font-family="Vazirmatn" font-weight="bold">~۱۵–۱۸ kg/m²</text>
              <!-- Safe Zone -->
              <rect x="70" y="80" width="260" height="10" rx="2" fill="#2ECC71" opacity="0.5"/>
              <text x="200" y="95" text-anchor="middle" fill="#FFFFFF" font-size="10" font-family="Vazirmatn" font-weight="bold">منطقه امن (Safe Zone)</text>
            </svg>
            <div class="flex justify-center gap-6 mt-4 text-xs">
              <span class="flex items-center gap-2"><span class="w-4 h-1 rounded bg-eco-green"></span> امن (۰-۱۵ kg/m²)</span>
              <span class="flex items-center gap-2"><span class="w-4 h-1 rounded bg-solar-gold"></span> مراقبتی (۱۵-۱۸ kg/m²)</span>
              <span class="flex items-center gap-2"><span class="w-4 h-1 rounded bg-alert-red"></span> خطرناک (>۱۸ kg/m²)</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          وزن پنل خورشیدی و <span class="text-solar-gold">تحمل سقف سوله</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
          <p class="text-sm font-bold text-solar-gold mb-1">⚖️ تحلیل سازه</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - SVG `role="img"` + `aria-label`.
  - Color + text labels for zones.

---

### [SEC_04]: حداقل زمین برای احداث نیروگاه خورشیدی (مقیاس خانگی)

- **Section Role:** B2C Context — 3D isometric villa roof layout.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. 3D isometric view of villa roof with 10-panel array. South-facing badge `bg-solar-gold text-deep-navy`. Shade analysis overlay.

- **Desktop Grid Architecture:**
  12-col. 3D view: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  3D view first (`h-[400px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار سه‌بعدی چیدمان پنل‌ها روی بام ویلا" role="img">
        <div class="relative h-[400px] bg-navy-mid/50 rounded-2xl overflow-hidden flex items-center justify-center">
          <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار سه‌بعدی چیدمان ۱۰ پنل روی بام ویلای ۵ کیلواتی">
            <!-- Roof Outline -->
            <path d="M50,50 L350,50 L350,250 L50,250 Z" stroke="#F5A623" stroke-width="3" fill="none" stroke-dasharray="10,5"/>
            <!-- Panels (10 units) -->
            <g fill="#F5A623" opacity="0.7" stroke="#FFFFFF" stroke-width="1">
              <rect x="60" y="70" width="80" height="40" rx="3"/>
              <rect x="160" y="70" width="80" height="40" rx="3"/>
              <rect x="260" y="70" width="80" height="40" rx="3"/>
              <rect x="60" y="130" width="80" height="40" rx="3"/>
              <rect x="160" y="130" width="80" height="40" rx="3"/>
              <rect x="260" y="130" width="80" height="40" rx="3"/>
              <rect x="60" y="190" width="80" height="40" rx="3"/>
              <rect x="160" y="190" width="80" height="40" rx="3"/>
              <rect x="260" y="190" width="80" height="40" rx="3"/>
              <rect x="60" y="250" width="80" height="40" rx="3"/>
              <rect x="160" y="250" width="80" height="40" rx="3"/>
            </svg>
            <div class="absolute bottom-6 left-1/2 -translate-x-1/2 flex gap-4 text-xs">
              <span class="flex items-center gap-1"><span class="w-3 h-3 rounded bg-solar-gold"></span> پنل ۵۵۰ وات</span>
              <span class="flex items-center gap-1"><span class="w-4 h-4 rounded-full bg-solar-gold"></span> رو به جنوب</span>
              <span class="flex items-center gap-1"><span class="w-4 h-4 rounded-full bg-eco-green"></span> ۲۵-۳۰ متر مربع</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          حداقل زمین برای نیروگاه <span class="text-solar-gold">۵ کیلواتی خانگی</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
        </p>
        <div class="glass-card p-5 border-s-4 border-eco-green mt-8">
          <p class="text-sm font-bold text-eco-green mb-1">🏠 پکیج ویلایی پایه</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - SVG `role="img"` + `aria-label`.
  - South-facing badge with text.

---

### [SEC_05]: یک هکتار پنل خورشیدی چقدر برق تولید می‌کند؟

- **Section Role:** Investment scale — Info-graphic with row spacing logic.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Top-down view of 1 Hectare with correctly spaced rows. Shading zones highlighted. `eco-green` for productive area, `alert-red` for spacing gaps.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. Info-graphic centered. Text below.

- **Mobile Stacking:**
  Info-graphic first (`h-[400px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-4xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        یک هکتار پنل خورشیدی <span class="text-solar-gold">چقدر برق</span> تولید می‌کند؟
      </h2>
      <!-- Top-down Hectare View -->
      <div class="relative w-full max-w-3xl mx-auto mb-10" aria-label="نمودار از بالای یک هکتار نیروگاه خورشیدی" role="img">
        <div class="relative w-full h-[400px] bg-navy-mid/50 rounded-2xl overflow-hidden flex items-center justify-center">
          <svg viewBox="0 0 400 400" class="w-full h-auto" role="img" aria-label="نمودار بالا روی یک هکتار نیروگاه خورشیدی با ردیف‌های فاصله‌دار">
            <!-- Field Boundary -->
            <rect x="20" y="20" width="360" height="360" rx="5" stroke="#F5A623" stroke-width="2" fill="none"/>
            <!-- Rows (6 rows) -->
            <g fill="#F5A623" opacity="0.7" stroke="#F5A623" stroke-width="1">
              <rect x="40" y="50" width="320" height="20" rx="2"/>
              <rect x="40" y="110" width="320" height="20" rx="2"/>
              <rect x="40" y="170" width="320" height="20" rx="2"/>
              <rect x="40" y="230" width="320" height="20" rx="2"/>
              <rect x="40" y="290" width="320" height="20" rx="2"/>
              <rect x="40" y="350" width="320" height="20" rx="2"/>
            </g>
            <!-- Spacing Arrows -->
            <g stroke="#F5A623" stroke-width="2" stroke-dasharray="5,5">
              <line x1="200" y1="70" x2="200" y2="110" marker-end="url(#arrow-up-down)"/>
              <line x1="200" y1="130" x2="200" y2="170" marker-end="url(#arrow-up-down)"/>
              <line x1="200" y1="190" x2="200" y2="230" marker-end="url(#arrow-up-down)"/>
              <line x1="200" y1="250" y2="290" marker-end="url(#arrow-up-down)"/>
              <line x1="200" y1="270" y2="310" marker-end="url(#arrow-up-down)"/>
            </g>
            <defs>
              <marker id="arrow-up-down" markerWidth="10" markerHeight="7" refX="5" refY="3.5" orient="auto">
                <polygon points="0 0, 10 3.5, 0 7" fill="#F5A623"/>
              </defs>
            </defs>
          </svg>
          <div class="flex justify-center gap-4 mt-6 text-xs">
            <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-eco-green"></span> نوار پنل (Productive)</span>
            <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-solar-gold"></span> فاصله سایه (۳-۴ متر)</span>
          </div>
        </div>
      </div>
      <h3 class="font-bold text-xl text-pure-white mb-6 text-center">قدرت نصب در ۱ هکتار</h3>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-6">
        <div class="glass-card p-4 border-s-4 border-eco-green text-center">
          <p class="text-3xl font-black text-eco-green">۶۰۰–۷۵۰</p>
          <p class="text-pure-white/70 text-sm">کیلوات ظرفیت</p>
        </div>
        <div class="glass-card p-4 border-s-4 border-solar-gold text-center">
          <p class="text-3xl font-black text-solar-gold">۱۰,۰۰۰</p>
          <p class="text-pure-white/70 text-sm">متر مربع مفید</p>
        </div>
        <div class="glass-card p-4 border-s-4 border-alert-red text-center">
          <p class="text-3xl font-black text-alert-red">۳–۴</p>
          <p class="text-pure-white/70 text-sm">متر فاصله ردیف‌ها</p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - SVG `role="img"` + `aria-label`.
  - Color + text labels for stats.

---

### [SEC_06]: تاثیر ماده ۱۶ بر استفاده حداکثری از فضای سقف صنایع

- **Section Role:** B2B Pain Point + Regulatory integration — Split view.

- **UI Aesthetic & Colors:**
  Split screen. Left: "Wasted Roof Space" (`bg-navy-mid/90` with empty roof, `alert-red` accents). Right: "Profitable Solar Roof" (`bg-deep-navy` with panels, `eco-green` glow). Diagonal divider `skew-y-3`.

- **Desktop Grid Architecture:**
  12-col. Left: `lg:col-span-6`. Right: `lg:col-span-6`. Both `min-h-[500px]`. GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Wasted first (`h-[300px]`), then Solar. GEO between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <!-- Wasted Space -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/empty-industrial-roof.webp" alt="سقف سوله خالی و بی‌استفاده" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🏭</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">سقف سوله خالی: فرصت ضایع شده</h3>
          <p class="text-pure-white/60 mt-2 text-sm">جریمه ماده ۱۶ + هزینه برق بالا</p>
        </div>
      </div>
      <!-- Solar Roof -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/solar-roof-factory.webp" alt="سقف سوله پوشیده با پنل‌های خورشیدی" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🏭</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">سقف سوله قدرتمند: درآمد + معافیت ماده ۱۶</h3>
          <p class="text-pure-white/70 mt-2 text-sm">تزریق به شبکه + سایه‌بانی خنک‌کننده</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 تحلیل اقتصادی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        تاثیر <span class="text-alert-red">ماده ۱۶</span> بر استفاده حداکثری از <span class="text-solar-gold">فضای سقف صنایع</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section id="sec-06">`.
  - Color + text labels for meaning.
  - GEO card `border-2 border-solar-gold`.

---

### [SEC_07]: افسانه در برابر واقعیت: جهت نصب پنل‌ها

- **Section Role:** Myth-busting — Orientation myth.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth: `bg-alert-red/10 border-alert-red/30` ❌. Reality: `bg-eco-green/10 border-eco-green/30` ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-07" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط بومی درباره <span class="text-solar-gold">جهت نصب پنل‌ها</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            اگر پنل‌ها را کاملاً صاف و افقی روی زمین بخوابانیم، نور خورشید را در تمام طول روز از هر جهتی دریافت می‌کنند و نیازی به سازه‌های زاویه‌دار گران‌قیمت نیست.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            نصب افقی پنل‌ها بزرگترین اشتباه محاسباتی است! اولا زاویه تابش خورشید عمود نیست، ثانیا نصب افقی باعث تجمع آب باران، گل و لای و گرد و غبار روی سطح پنل شده و راندمان را تا ۵۰ درصد کاهش می‌دهد. تیم هورا نور سهند از استراکچرهای استاندارد گالوانیزه گرم استفاده می‌کند تا شیب دقیق ۳۵ درجه (بهینه‌ترین شیب برای استان البرز و تهران) را برای تخلیه خودکار آلودگی‌ها و دریافت حداکثر زاویه تابش تامین کند.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 واقعیت نصب صحیح</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside id="sec-07">`.
  - `x-intersect` decorative.
  - Meaning via icon + text.
  - Contrast: dark text on light cards.

---

### [SEC_08]: راهنمای ابعاد استراکچر برای چاه‌های کشاورزی

- **Section Role:** Vertical niche — High-mounted agricultural structures.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Photo gallery of high-mounted agricultural structures. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Gallery: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Gallery `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="گالری استراکچرهای بلند کشاورزی هورا نور سهند" role="img">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <img src="/images/agri-high-structure-1.webp" alt="استراکچر بلند پمپ آب خورشیدی در مزارع" class="w-full h-64 object-cover rounded-xl mb-3" loading="lazy">
          <img src="/images/agri-high-structure-2.webp" alt="استراکچر ارتفاع بالا برای امنیت فیزیکی" class="w-full h-64 object-cover rounded-xl mb-3" loading="lazy">
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          راهنمای ابعاد استراکچر برای <span class="text-solar-gold">چاه‌های کشاورزی</span>
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
          <p class="text-sm font-bold text-solar-gold mb-1">🚜 پوشش کشاورزی</p>
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
  - Gallery `role="img"` + `aria-label`.
  - Phones `dir="ltr"`.

---

### [SEC_09]: آپدیت‌های تکنولوژی: پنل‌های دوطرفه (Bifacial) و کاهش فضای مورد نیاز

- **Section Role:** Temporal freshness + Outbound trust (NREL).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی تکنولوژی". External link to `nrel.gov` with `rel="external noopener"`.

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
          آپدیت تکنولوژی: <span class="text-solar-gold">پنل‌های دوطرفه (Bifacial)</span>
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">آپدیت تکنولوژی</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
      </p>
      <div class="bg-eco-green/10 border border-eco-green/30 rounded-2xl p-6 bg-solar-gold/5 flex items-start gap-3">
        <span class="text-2xl mt-1">🚀</span>
        <div>
          <p class="text-sm font-bold text-solar-gold mb-1">نکته مهم فنی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
          </p>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mt-8">
          مراجعه به <a href="https://www.nrel.gov/" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">آزمایشگاه ملی انرژی‌های تجدیدپذیر آمریکا (NREL)</a> برای گزارشات رسمی اثربخشی این تکنولوژی.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_10]: سوالات متداول درباره ابعاد و زمین نیروگاه خورشیدی

- **Section Role:** GEO/SGE bait — Local FAQ schema.

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
        سوالات متداول <span class="text-solar-gold">ابعاد و زمین نیروگاه خورشیدی</span>
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
              آیا برای فروش برق به ساتبا حتماً باید زمین به نام شخص باشد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، برای احداث نیروگاه‌های متصل به شبکه تجاری و عقد قرارداد ۲۰ ساله با وزارت نیرو، داشتن سند مالکیت (یا اجاره‌نامه رسمی طولانی‌مدت) زمین الزامی است.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا پنل‌ها روی سقف‌های شیروانی و سفالی نصب می‌شوند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، هورا نور سهند با استفاده از استراکچرها و یراق‌آلات مخصوص آلومینیومی (Roof Hooks)، پنل‌ها را بدون آسیب به عایق‌بندی، روی سقف‌های شیروانی نصب می‌کند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا زمین شیب‌دار برای نیروگاه مناسب است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            زمین‌هایی که دارای شیب طبیعی به سمت جنوب (South-facing slope) هستند، ایده‌آل‌ترین زمین‌ها محسوب می‌شوند زیرا هزینه‌های استراکچر و خاک‌برداری را به شدت کاهش می‌دهند.
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

[VERIFIED_UI_END_OF_FILE]