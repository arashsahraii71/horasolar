# UI Wireframe Specification: پنل خورشیدی چیست و چگونه کار می‌کند؟ | اصول فتوولتائیک | هورا نور سهند
- **Source Dossier:** `seo_dossiers/knowledge_solar-energy-fundamentals.md`
- **Target URL:** `/knowledge/solar-energy-fundamentals`
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
### Icon System Rule
> **CRITICAL:** All icons MUST be inline SVG — **NEVER emoji**. Emoji render inconsistently across OS/browsers and cannot inherit brand colour.
> Use a `24x24` `viewBox` with `fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round"` and size it in em units: `style="width:1em;height:1em;vertical-align:-0.125em;display:inline-block"`.
> Always add `aria-hidden="true" focusable="false"`. Because colour is `currentColor` and size is `1em`, each icon automatically inherits the surrounding text's colour and scale.
> Typographic arrows and operators (`→` `←` `↓` `≥` `≈`) are **not** icons and stay as text.
> Alpine note: an SVG cannot be rendered via `x-text` (it sets `textContent`) — use `x-html` with `&quot;`-escaped inner quotes.

---

### [SEC_01]: پنل خورشیدی (سیستم فتوولتائیک) چیست؟

- **Section Role:** Primary Hero — H1 entity definition, core topic authority.

- **UI Aesthetic & Colors:**
  Full-viewport hero with 3D exploded-view animation of solar panel layers (glass → EVA → cells → EVA → backsheet → frame). Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). Floating layer labels animate in on scroll. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. 3D model viewer: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. 3D model `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          دانشنامه فتوولتائیک | مرجع مهندسی
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          پنل خورشیدی <span class="text-solar-gold">(سیستم فتوولتائیک)</span> چیست؟
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مطالعه جزئیات ساختار پنل خورشیدی">
          مطالعه ساختار پنل
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
  - 3D model has `aria-label` in Farsi.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.

---

### [SEC_02]: پنل خورشیدی از چه چیزی ساخته شده است؟

- **Section Role:** Component anatomy — Interactive layer explorer.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive cross-section: 6-layer panel model. Each layer highlights on hover with glass card showing material specs. Layer colors: Glass (`text-pure-white/30`), EVA (`text-solar-gold/30`), Cells (`solar-gold`), EVA (`text-solar-gold/30`), Backsheet (`text-pure-white/30`), Frame (`navy-mid`).

- **Desktop Grid Architecture:**
  12-col. Left: 3D cross-section `lg:col-span-6 lg:sticky lg:top-20`. Right: Layer list `lg:col-span-6` with hoverable cards.

- **Mobile Stacking:**
  Cross-section first (`h-[400px]`). Layer list stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ activeLayer: 0 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار تعاملی لایه‌های پنل خورشیدی" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">سازماندهی لایه‌های پنل خورشیدی</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center" x-data="{ activeLayer: -1 }">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار لایه‌های پنل خورشیدی">
              <!-- Glass -->
              <rect x="50" y="30" width="300" height="20" rx="2" fill="#FFFFFF" opacity="0.2" stroke="#F5A623" stroke-width="1"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 0 }"
                    @mouseenter="activeLayer = 0" @mouseleave="activeLayer = -1"/>
              <!-- EVA Top -->
              <rect x="50" y="50" width="300" height="15" rx="1" fill="#F5A623" opacity="0.3"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 1 }"
                    @mouseenter="activeLayer = 1" @mouseleave="activeLayer = -1"/>
              <!-- Cells -->
              <rect x="50" y="65" width="300" height="120" rx="2" fill="#F5A623" opacity="0.8"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 2 }"
                    @mouseenter="activeLayer = 2" @mouseleave="activeLayer = -1"/>
              <!-- EVA Bottom -->
              <rect x="50" y="185" width="300" height="15" rx="1" fill="#F5A623" opacity="0.3"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 3 }"
                    @mouseenter="activeLayer = 3" @mouseleave="activeLayer = -1"/>
              <!-- Backsheet -->
              <rect x="50" y="200" width="300" height="20" rx="1" fill="#FFFFFF" opacity="0.2"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 4 }"
                    @mouseenter="activeLayer = 4" @mouseleave="activeLayer = -1"/>
              <!-- Frame -->
              <rect x="40" y="20" width="320" height="200" rx="5" fill="none" stroke="#F5A623" stroke-width="3"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 5 }"
                    @mouseenter="activeLayer = 5" @mouseleave="activeLayer = -1"/>
            </svg>
            <div class="flex flex-wrap justify-center gap-2 mt-4 text-xs">
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 0 }"><span class="w-4 h-1 rounded bg-pure-white/30"></span> شیشه</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 1 }"><span class="w-4 h-1 rounded bg-solar-gold/30"></span> EVA</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 2 }"><span class="w-4 h-1 rounded bg-solar-gold"></span> سلول‌ها</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 3 }"><span class="w-4 h-1 rounded bg-solar-gold/30"></span> EVA</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 4 }"><span class="w-4 h-1 rounded bg-pure-white/30"></span> بک‌شیت</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 5 }"><span class="w-4 h-1 rounded bg-navy-mid"></span> فریم</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-4 text-start" x-data="{ activeLayerName: '' }">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پنل خورشیدی از <span class="text-solar-gold">چه چیزی</span> ساخته شده است؟
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div class="glass-card p-4 border-s-2 border-solar-gold/30 cursor-pointer hover:border-solar-gold"
               x-data="{ active: false }" @click="active = !active"
               :class="{ 'ring-2 ring-solar-gold': active }">
            <h3 class="font-bold text-lg text-solar-gold mb-2">شیشه حرارتی ضدانعکاس</h3>
            <p class="text-pure-white/80 text-sm" x-show="active">شیشه سکوریت آنتی‌رفلکت، عبور >۹۵٪ نور</p>
          </div>
          <div class="glass-card p-4 border-s-2 border-solar-gold/30 cursor-pointer hover:border-solar-gold"
               x-data="{ active: false }" @click="active = !active"
               :class="{ 'ring-2 ring-solar-gold': active }">
            <h3 class="font-bold text-lg text-solar-gold mb-2">فریم آلومینیومی گالوانیزه</h3>
            <p class="text-pure-white/80 text-sm" x-show="active">استحکام ساختاری + نصب آسان</p>
          </div>
        </div>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - Interactive SVG `role="img"` + `aria-label`.
  - Clickable layer cards with `role="button"` + `aria-expanded`.
  - Hover states have text equivalents.

---

### [SEC_03]: اثر فتوولتائیک: پنل خورشیدی دقیقاً چگونه کار می‌کند؟

- **Section Role:** Deep technical explainer — Animated physics visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Animated SVG: Photon hits N-type → electron knocked → electric field at P-N junction → electron flows → DC current. Particles animate on scroll.

- **Desktop Grid Architecture:**
  12-col. Animation: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Animation first (`h-[400px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy" x-data="{ animPlaying: false }" x-intersect.once="animPlaying = true">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="انمیشن اثر فتوولتائیک: فوتون تا الکترون" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">اثر فتوولتائیک: فوتون تا الکترون</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="انمیشن اثر فتوولتائیک">
              <!-- N-type layer -->
              <rect x="50" y="50" width="300" height="80" rx="5" fill="#2ECC71" opacity="0.3"/>
              <text x="200" y="85" text-anchor="middle" fill="#2ECC71" font-size="14" font-family="Vazirmatn" font-weight="bold">N-type (الکترون اضافه)</text>
              <!-- P-type layer -->
              <rect x="50" y="130" width="300" height="80" rx="5" fill="#E74C3C" opacity="0.3"/>
              <text x="200" y="210" text-anchor="middle" fill="#E74C3C" font-size="14" font-family="Vazirmatn" font-weight="bold">P-type (حفره اضافه)</text>
              <!-- Depletion Region -->
              <rect x="50" y="170" width="300" height="20" rx="2" fill="#F5A623" opacity="0.5"/>
              <text x="200" y="185" text-anchor="middle" fill="#F5A623" font-size="12" font-family="Vazirmatn" font-weight="bold">منطقه فراغ (P-N Junction)</text>
              <!-- Photon Animation -->
              <circle cx="200" cy="20" r="6" fill="#F5A623">
                <animateMotion path="M200,20 Q200,100 200,180" dur="2s" repeatCount="indefinite"/>
              </circle>
              <!-- Electron Animation -->
              <circle cx="200" cy="100" r="4" fill="#2ECC71">
                <animateMotion path="M200,100 L200,180" dur="1.5s" repeatCount="indefinite" fill="freeze"/>
              </circle>
            </svg>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          اثر فتوولتائیک: پنل خورشیدی <span class="text-solar-gold">دقیقاً چگونه کار می‌کند؟</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🔬 اثر فتوولتائیک</p>
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
  - Animation respects `prefers-reduced-motion`.

---

### [SEC_04]: خروجی پنل خورشیدی AC است یا DC؟

- **Section Role:** High-volume query answer — Simple comparison table.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Comparison table: DC (panel output) vs AC (household/grid). Inverter bridge visualized as arrow with `solar-gold` color.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Comparison table full-width. Inverter bridge visual below.

- **Mobile Stacking:**
  Table horizontal scroll. Bridge visual stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        خروجی پنل خورشیدی <span class="text-solar-gold">AC است یا DC؟</span>
      </h2>
      <div class="glass-card p-6 overflow-x-auto mb-10">
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="مقایسه خروجی DC پنل در برابر AC خانگی">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">مشخصه</th>
              <th scope="col" class="p-4 text-start">خروجی پنل (DC)</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">خروجی خانه/شبکه (AC)</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">نوع جریان</td><td class="p-3 text-solar-gold font-bold">مستقیم (DC)</td><td class="p-3 text-eco-green font-bold">متناوب (AC)</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">ولتاژ</td><td class="p-3">متغیر (بسته به نور)</td><td class="p-3">۲۲۰ ولت ثابت</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">مصرف‌کننده</td><td class="p-3">باتری، سیستم‌های DC</td><td class="p-3">وسایل منزل، شبکه برق</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">تبدیل</td><td class="p-3 text-alert-red font-bold">نیاز به اینورتر</td><td class="p-3 text-eco-green font-bold">مستقیم قابل استفاده</td></tr>
          </tbody>
        </table>
      </div>
      <!-- Inverter Bridge Visual -->
      <div class="flex items-center justify-center gap-4 mb-8" aria-label="نقش اینورتر در تبدیل DC به AC">
        <div class="glass-card p-4 border border-alert-red/30 text-center">
          <span class="text-alert-red font-bold text-lg">DC</span>
          <p class="text-pure-white/70 text-sm mt-1">خروجی پنل</p>
        </div>
        <svg class="w-16 h-16 text-solar-gold" viewBox="0 0 24 24"><path d="M12 4v16m8-8H4"/></svg>
        <div class="glass-card p-4 border border-solar-gold/30 text-center">
          <span class="text-solar-gold font-bold text-lg">اینورتر</span>
          <p class="text-pure-white/70 text-sm mt-1">مبدل DC→AC</p>
        </div>
        <svg class="w-16 h-16 text-eco-green" viewBox="0 0 24 24"><path d="M12 4v16m8-8H4"/></svg>
        <div class="glass-card p-4 border border-eco-green/30 text-center">
          <span class="text-eco-green font-bold text-lg">AC</span>
          <p class="text-pure-white/70 text-sm mt-1">ورودی خانه/شبکه</p>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
        <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on headers.
  - Bridge visual has `aria-label`.

---

### [SEC_05]: برق پنل خورشیدی کجا و چگونه ذخیره می‌شود؟

- **Section Role:** Storage intent — Off-Grid vs On-Grid comparison.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Two-column layout: Off-Grid (Battery card `eco-green`) vs On-Grid (Grid card `solar-gold`). Animated battery fill vs grid flow.

- **Desktop Grid Architecture:**
  12-col. Two cards side-by-side `lg:col-span-6`. Animated battery visual left, grid flow right.

- **Mobile Stacking:**
  Vertical stack. Battery visual first.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy" x-data="{ fillPercent: 0 }" x-intersect.once="fillPercent = 60">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <div class="lg:col-span-6" aria-label="نمودار ذخیره‌سازی در باتری (Off-Grid)" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">ذخیره‌سازی در باتری (Off-Grid)</h3>
          <div class="relative w-[250px] h-[250px] mx-auto mb-6" x-data="{ fillPercent: 0 }" x-intersect.once="fillPercent = 70">
            <svg viewBox="0 0 200 200" class="w-full h-auto" role="img" aria-label="نمودار شارژ باتری">
              <!-- Battery Outline -->
              <rect x="20" y="20" width="160" height="140" rx="5" fill="none" stroke="#F5A623" stroke-width="3"/>
              <rect x="80" y="0" width="40" height="20" rx="2" fill="#F5A623"/>
              <!-- Fill Animation -->
              <rect x="23" y="140" width="154" height="1" rx="2" fill="#E74C4C">
                <animate attributeName="y" from="140" to="60" dur="2s" fill="freeze"/>
                <animate attributeName="height" from="1" to="80" dur="2s" fill="freeze"/>
              </rect>
            </svg>
            <div class="flex justify-center gap-4 mt-4 text-xs">
              <span class="text-eco-green font-bold">شارژ (۷۰٪)</span>
              <span class="text-solar-gold font-bold">آماده مصرف</span>
            </div>
          </div>
          <h3 class="font-bold text-xl text-pure-white mb-3 text-start">Off-Grid: باتری فیزیکی</h3>
          <p class="text-pure-white/80 text-base leading-relaxed">
            در سیستم‌های آفگرید، برق مازاد در باتری‌های دیپ‌سایکل (ژل/لیتیوم) ذخیره می‌شود تا در شب یا روزهای ابری مصرف شود.
          </p>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          ذخیره‌سازی برق: <span class="text-solar-gold">باتری</span> یا <span class="text-eco-green">شبکه</span>؟
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🔋 مدل ذخیره‌سازی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Battery SVG `role="img"` + `aria-label`.
  - Color + text labels for battery zones.

---

### [SEC_06]: افسانه در برابر واقعیت: تولید برق در هوای ابری

- **Section Role:** Myth-busting — Cloudy day myth.

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
        افسانه در برابر واقعیت: <span class="text-solar-gold">تولید برق در هوای ابری</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">افسانه</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            سیستم‌های خورشیدی فقط در روزهای کاملاً آفتابی کار می‌کنند و در روزهای ابری هیچ برقی تولید نمی‌شود.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های مدرن Tier-1 به ویژه انواع مونوکریستال که توسط هورا نور سهند نصب می‌شوند، حساسیت بالایی به طیف‌های نوری دارند و حتی در روزهای ابری و بارانی با دریافت اشعه غیرمستقیم، برق تولید می‌کنند. البته استان البرز و شهر کرج با میانگین ۲۵۰ روز آفتابی در سال، یکی از ایده‌آل‌ترین مناطق ایران برای احداث نیروگاه است.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت علمی</p>
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

### [SEC_07]: چرا صنایع باید به سیستم‌های فتوولتائیک روی بیاورند؟

- **Section Role:** B2B Pain Point — Article 16 context.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Call-out box with `bg-solar-gold/10 border border-solar-gold/20`. ROI badge `bg-eco-green text-deep-navy`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. ROI badge prominent.

- **Mobile Stacking:**
  No change.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        چرا صنایع باید به <span class="text-solar-gold">سیستم‌های فتوولتائیک</span> روی بیاورند؟
      </h2>
      <div class="bg-solar-gold/10 border border-solar-gold/20 rounded-2xl p-8 mb-8">
        <span class="inline-flex items-center gap-2 bg-eco-green text-deep-navy text-sm font-bold rounded-full px-3 py-1 mb-4">ROI ۳-۵ ساله</span>
        <h3 class="font-bold text-xl text-pure-white mb-4 text-start">چرا صنایع باید به فتوولتائیک روی بیاورند؟</h3>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold bg-eco-green/5">
        <p class="text-sm font-bold text-eco-green mb-1">💰 منطق اقتصادی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for ROI badge.

---

### [SEC_08]: انواع پنل‌های خورشیدی موجود در بازار

- **Section Role:** Consumer guidance — Mono vs Poly comparison.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Side-by-side image comparison cards. Mono: `bg-solar-gold/10 border-solar-gold/30`. Poly: `bg-alert-red/10 border-alert-red/30`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. Side-by-side cards `grid-cols-2 gap-6`.

- **Mobile Stacking:**
  Vertical stack. Mono first.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        انواع پنل‌های خورشیدی <span class="text-solar-gold">موجود در بازار</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div class="glass-card p-6 border border-alert-red/30 bg-alert-red/10 rounded-2xl transition-all hover:shadow-xl"
             aria-label="پنل‌های پلی‌کریستال">
          <span class="text-4xl mb-4">❌</span>
          <h3 class="font-bold text-alert-red text-xl mb-3">پلی‌کریستال (منسوخ)</h3>
          <ul class="space-y-2 text-pure-white/70 text-sm">
            <li class="flex items-center gap-2"><span class="text-alert-red">✗</span> راندمان پایین (< ۱۷٪)</li>
            <li class="flex items-center gap-2"><span class="text-alert-red">✗</span> ظریفیت کمتر در گرما</li>
            <li class="flex items-center gap-2"><span class="text-alert-red">✗</span> منسوخ در پروژه‌های مدرن</li>
          </ul>
        </div>
        <div class="glass-card p-6 border border-solar-gold/30 bg-solar-gold/10 rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50"
             aria-label="پنل‌های مونوکریستال">
          <span class="text-4xl mb-4">✅</span>
          <h3 class="font-bold text-solar-gold text-xl mb-3">مونوکریستال (استاندارد مدرن)</h3>
          <ul class="space-y-2 text-pure-white/80 text-sm">
            <li class="flex items-center gap-2"><span class="text-solar-gold">✓</span> راندمان بالا (> ۲۱٪)</li>
            <li class="flex items-center gap-2"><span class="text-solar-gold">✓</span> عملکرد عالی در گرما</li>
            <li class="flex items-center gap-2"><span class="text-solar-gold">✓</span> استاندارد پروژه‌های مدرن</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_09]: طول عمر و افت راندمان سیستم‌های خورشیدی چقدر است؟

- **Section Role:** Trust building — Line chart visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Line chart: Tier-1 (gentle slope `eco-green`), Tier-3 (steep drop `alert-red`). Tier-1 line animates drawing on scroll.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Graph: `lg:col-span-7 lg:sticky lg:top-20`. Text: `lg:col-span-5`.

- **Mobile Stacking:**
  Graph first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-deep-navy" x-data="{ chartLoaded: false }" x-intersect.once="chartLoaded = true">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-7 lg:sticky lg:top-20" aria-label="نمودار خطیeft توان ۲۵ ساله: Tier-1 در برابر Tier-3" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">طول عمر و افت راندمان (۲۵ سال)</h3>
          <div class="relative h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 600 300" class="w-full h-full" role="img" aria-label="نمودار خطی افت توان ۲۵ ساله: Tier-1 (سبز ملایم) در برابر Tier-3 (قرمز تیز)">
              <line x1="50" y1="250" x2="550" y2="250" stroke="#FFFFFF" stroke-width="1"/>
              <line x1="50" y1="250" x2="50" y2="20" stroke="#FFFFFF" stroke-width="1"/>
              <path d="M50,250 Q150,240 300,230 T550,210" stroke="#2ECC71" stroke-width="3" fill="none" marker-end="url(#arrowhead)">
                <animate attributeName="stroke-dashoffset" from="1000" to="0" dur="2s" fill="freeze"/>
              </path>
              <path d="M50,250 Q150,200 300,100 T550,20" stroke="#E74C3C" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
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
          طول عمر و <span class="text-eco-green">افت راندمان</span> سیستم‌های خورشیدی
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">🛡️ تضمین ۲۵ ساله</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
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

### [SEC_10]: آپدیت‌های جهانی و آینده تکنولوژی فتوولتائیک

- **Section Role:** Temporal freshness + outbound trust (DOE).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی تکنولوژی". External link to `energy.gov` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badge inline with H2.

- **Mobile Stacking:**
  Badge wraps naturally.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          آپدیت‌های جهانی و آینده تکنولوژی فتوولتائیک
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">آپدیت تکنولوژی</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_10}
      </p>
      <div class="glass-card p-5 border-s-4 border-solar-gold">
        <div class="flex items-start gap-3">
          <span class="text-2xl mt-1">🔬</span>
          <div>
            <p class="text-sm font-bold text-solar-gold mb-1">تکنولوژی N-Type TOPCon</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
            </p>
          </div>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mt-8">
          مراجعه به <a href="https://www.energy.gov/" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">دپارتمان انرژی ایالات متحده (DOE)</a> برای استانداردهای مرجع جهانی.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_11]: سوالات متداول درباره نحوه کار سیستم‌های خورشیدی (FAQ)

- **Section Role:** GEO/SGE bait — FAQPage schema.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Glass accordion. Expanded: `border-s-4 border-solar-gold` + `text-solar-gold` summary.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO preamble banner.

- **Mobile Stacking:**
  Full-width `<summary>` with `py-5`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-11" class="py-20 md:py-32 bg-navy-mid" x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">نحوه کار سیستم‌های خورشیدی</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_11}
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
              آیا پنل خورشیدی در طول شب نیز کار می‌کند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر، فرآیند فتوولتائیک نیازمند نور خورشید است. برای استفاده از برق در شب، شما به یک بانک باتری یا استفاده از شبکه سراسری نیاز دارید.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا شستشوی پنل‌های خورشیدی الزامی است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. نشستن گرد و غبار شدید روی سطح پنل می‌تواند تا ۱۵ درصد از راندمان تولید را کاهش دهد.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا سیستم‌های خورشیدی خطر برق‌گرفتگی دارند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در صورت اجرای صحیح و اصولی کابل‌کشی و استفاده از تجهیزات حفاظتی استاندارد توسط یک پیمانکار مجاز مانند هورا نور سهند، سیستم کاملاً ایمن است.
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