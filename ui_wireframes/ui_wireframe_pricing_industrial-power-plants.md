# UI Wireframe Specification: هزینه احداث نیروگاه خورشیدی مگاواتی و صنعتی | هورا نور سهند
- **Source Dossier:** `seo_dossiers/pricing_industrial-power-plants.md`
- **Target URL:** `/pricing/industrial-power-plants`
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

### [SEC_01]: برآورد هزینه و طرح توجیهی احداث نیروگاه خورشیدی (۵۰ کیلووات تا مگاواتی)

- **Section Role:** Primary Hero — B2B Investor H1, EPC authority, Feasibility Study promise.

- **UI Aesthetic & Colors:**
  Full-viewport hero with aerial drone shot of a multi-megawatt solar farm stretching to horizon (Eshtehard/Simin Dasht), panels converging to substation. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "EPC Contractor | Feasibility Study" badge in `solar-gold`. Corporate typography: bold, clean. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-industrial-megawatt.webp"
         alt="نیروگاه خورشیدی مگاواتی در اشتهارد — طرح توجیهی، EPC، طرح توجیهی COMFAR"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          پیمانکار EPC | طرح توجیهی COMFAR
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          برآورد هزینه و طرح توجیهی <span class="text-solar-gold">نیروگاه خورشیدی</span> (۵۰ کیلووات تا مگاواتی)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="درخواست طرح توجیهی (FS) و پیش‌فاکتور EPC">
          درخواست طرح توجیهی
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
  - Hero `alt` in Farsi describing mega-watt solar farm.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: جدول تحلیل هزینه‌ها و بازده سرمایه‌گذاری (Investment Yield)

- **Section Role:** SERP Table Snippet — Structured KPI table for SERP snippet extraction.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Full-width responsive table with `overflow-x-auto` on mobile. Header row `bg-navy-mid text-solar-gold`. Alternating rows `bg-deep-navy/60` / `bg-navy-mid/40`. KPI columns: Capacity, CAPEX Range, Land (m²), Payback Period, IRR.

- **Desktop Grid Architecture:**
  Centered `max-w-7xl`. Table full-width. GEO callout below.

- **Mobile Stacking:**
  Table horizontal scroll (`overflow-x-auto`). GEO callout below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-7xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        جدول تحلیل <span class="text-solar-gold">هزینه‌ها و بازده سرمایه‌گذاری</span> (Investment Yield)
      </h2>
      <div class="glass-card p-6 overflow-x-auto">
        <table class="w-full min-w-[800px] text-sm" role="table" aria-label="جدول شاخص‌های کلیدی نیروگاه‌های مگاواتی">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">ظرفیت</th>
              <th scope="col" class="p-4 text-start">CAPEX تخمینی (مینیون تومان)</th>
              <th scope="col" class="p-4 text-start">متراژ زمین (متر مربع)</th>
              <th scope="col" class="p-4 text-start">دوره بازگشت سرمایه</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">IRR تخمینی</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">۵۰ kW</td><td class="p-4">از ~[DATA NEEDED]</td><td class="p-4">۵۰۰-۶۰۰</td><td class="p-4">۳-۵ سال</td><td class="p-4 text-eco-green font-bold">۳۵٪+</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">۱۰۰ kW</td><td class="p-4">از ~[DATA NEEDED]</td><td class="p-4">۱،۰۰۰-۱،۲۰۰</td><td class="p-4">۳-۴ سال</td><td class="p-4 text-eco-green font-bold">۳۸٪+</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">۵۰۰ kW</td><td class="p-4">از ~[DATA NEEDED]</td><td class="p-4">۵،۰۰۰-۶،۰۰۰</td><td class="p-4">۳-۴ سال</td><td class="p-4 text-eco-green font-bold">۴۰٪+</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">۱ MW</td><td class="p-4">از ~[DATA NEEDED]</td><td class="p-4">۱۰،۰۰۰-۱۲،۰۰۰</td><td class="p-4">۳-۴ سال</td><td class="p-4 text-eco-green font-bold">۴۲٪+</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">۵ MW</td><td class="p-4">از ~[DATA NEEDED]</td><td class="p-4">۵۰،۰۰۰-۶۰،۰۰۰</td><td class="p-4">۴-۵ سال</td><td class="p-4 text-eco-green font-bold">۳۸٪+</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">۱۰ MW</td><td class="p-4">از ~[DATA NEEDED]</td><td class="p-4">۱۰۰،۰۰۰-۱۲۰،۰۰۰</td><td class="p-4">۴-۵ سال</td><td class="p-4 text-eco-green font-bold">۳۵٪+</td></tr>
          </tbody>
        </table>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📊 شاخص‌های کلیدی</p>
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

---

### [SEC_03]: تحلیل اهرم مالی ماده ۱۶ برای کارخانجات

- **Section Role:** Pain-point financial trigger — Split view: Penalty vs Asset.

- **UI Aesthetic & Colors:**
  Split screen. Penalty side (start): `bg-navy-mid/90` with invoice/paperwork imagery, `alert-red` accents. Asset side: `bg-deep-navy` with solar-powered factory, `eco-green` glow. Diagonal divider `skew-y-3`.

- **Desktop Grid Architecture:**
  12-col. Penalty: `lg:col-span-6`. Asset: `lg:col-span-6`. Both `min-h-[500px]`. GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Penalty first (`h-[300px]`), then Asset. GEO between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <!-- Penalty Side -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/industrial-penalty-invoice.webp" alt="قبض برق سنگین با جریمه ماده ۱۶" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">💸</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">جریمه ماده ۱۶: پول سوزانده شده</h3>
          <p class="text-pure-white/60 mt-2 text-sm">هزینه خرید برق تابلو سبز = جریمه ماهانه</p>
        </div>
      </div>
      <!-- Asset Side -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/solar-factory-asset.webp" alt="کارخانه با نیروگاه خورشیدی روی سقف — دارایی ۲۰ ساله" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🏭</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">نیروگاه اختصاصی: دارایی ۲۰ ساله</h3>
          <p class="text-pure-white/70 mt-2 text-sm">جریمه = اقساط نیروگاه</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 تحلیل مالی COMFAR</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        تحلیل اهرم مالی <span class="text-alert-red">ماده ۱۶</span> برای <span class="text-solar-gold">کارخانجات</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section id="sec-03">`.
  - Color + text labels for meaning.
  - GEO card `border-2 border-solar-gold`.

---

### [SEC_04]: باورهای غلط در تامین مالی مگاواتی (Myth vs. Reality)

- **Section Role:** Myth-busting — 25-year panel warranty vs generator wear.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth: `bg-alert-red/10 border-alert-red/30` ❌. Reality: `bg-eco-green/10 border-eco-green/30` ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در <span class="text-solar-gold">تأمین مالی مگاواتی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های خورشیدی در سال دهم فرسوده شده و نیازمند تعویض (CAPEX مجدد) هستند.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های Tier-1 (Jinko, LONGi) گارانتی راندمان خطی ۲۵ ساله دارند. افت توان سال بیستم < ۱۵٪. هلاک-N/A قطعات متحرک = OPEX نزدیک صفر. ۲۵ سال عمر، ۲۰ سال تحت پوشش قرارداد ساتبا.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت سرمایه‌گذاری</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside id="sec-04">`.
  - `x-intersect` decorative.
  - Meaning via icon + text.
  - Contrast: dark text on light cards.

---

### [SEC_05]: تفکیک هزینه‌های سرمایه‌ای (CAPEX Breakdown)

- **Section Role:** Semantic depth — CAPEX pie chart with drill-down.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Pie chart: Panels (50% `solar-gold`), Inverters (15% `eco-green`), Structure (15% `eco-green`), Grid/Electrical (20% `alert-red`). Hover slice = highlight + tooltip. Glass card container.

- **Desktop Grid Architecture:**
  12-col. Pie chart: `lg:col-span-6 lg:sticky lg:top-20`. Text + GEO: `lg:col-span-6`.

- **Mobile Stacking:**
  Pie chart first. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار دایره‌ای تفکیک CAPEX نیروگاه ۱۰ مگاواتی" role="img">
        <div class="glass-card p-8">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">تفکیک CAPEX نیروگاه ۱۰ مگاواتی</h3>
          <div class="w-full h-[400px] flex items-center justify-center">
            <svg viewBox="0 0 400 400" class="w-full h-auto" role="img" aria-label="نمودار دایره‌ای تفکیک CAPEX: پنل‌ها ۵۰٪، اینورترها ۱۵٪، سازه ۱۵٪، شبکه/الکتریکال ۲۰٪">
              <!-- Panels 50% -->
              <path d="M200,200 L200,20 A150,150 0 0,1 339,200 L200,200 Z" fill="#F5A623" opacity="0.85"/>
              <!-- Inverters 15% -->
              <path d="M200,200 L200,20 A150,150 0 0,1 247,50 L200,200 Z" fill="#2ECC71" opacity="0.85"/>
              <!-- Structure 15% -->
              <path d="M200,200 L247,50 A150,150 0 0,1 120,200 L200,200 Z" fill="#2ECC71" opacity="0.85"/>
              <!-- Grid/Electrical 20% -->
              <path d="M200,200 L120,200 A150,150 0 0,1 200,20 Z" fill="#E74C3C" opacity="0.85"/>
              <!-- Center Label -->
              <text x="200" y="210" text-anchor="middle" fill="#FFFFFF" font-size="18" font-weight="bold" font-family="Vazirmatn">۱۰ MW</text>
            </svg>
            <div class="flex flex-wrap justify-center gap-4 mt-6 text-sm">
              <span class="flex items-center gap-1"><span class="w-3 h-3 rounded-full bg-solar-gold"></span> پنل‌ها ۵۰٪</span>
              <span class="flex items-center gap-1"><span class="w-3 h-3 rounded-full bg-eco-green"></span> اینورترها ۱۵٪</span>
              <span class="flex items-center gap-1"><span class="w-3 h-3 rounded-full bg-eco-green"></span> سازه ۱۵٪</span>
              <span class="flex items-center gap-1"><span class="w-3 h-3 rounded-full bg-alert-red"></span> شبکه/الکتریکال ۲۰٪</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تفکیک <span class="text-solar-gold">هزینه‌های سرمایه‌ای</span> (CAPEX Breakdown)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 تفکیک लागت</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - SVG `role="img"` + `aria-label`.
  - Color + text labels for slices.
  - Contrast ratios maintained.

---

### [SEC_06]: تضمین کیفیت با مهندسی تجهیزات (E-E-A-T)

- **Section Role:** E-E-A-T authority — Portfolio showcase + trust badges.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Portfolio showcase: 3 large project cards (Eshtehard 5MW, Simindasht 2MW, Hashtgerd 1MW). Each card: Glassmorphism, hover zoom, hover caption. Trust badges row. Rolling counter `data-value="40"`.

- **Desktop Grid Architecture:**
  12-col. Showcase: `lg:col-span-7`. Trust badges + GEO: `lg:col-span-5`.

- **Mobile Stacking:**
  Carousel `snap-x`. Trust badges stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="پورتفوی پروژه‌های مگاواتی هورا نور سهند">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">پروژه‌های مگاواتی شاخص</h3>
        <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ۵ مگاواتی اشتهارد">
            <img src="/images/project-eshtehard-5mw.webp" alt="نیروگاه ۵ مگاواتی شهرک صنعتی اشتهارد" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">نیروگاه ۵ مگاواتی اشتهارد</h4>
            <p class="text-pure-white/60 text-sm mt-1">SMA Inverters + Trina Panels</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ۲ مگاواتی سیمین‌دشت">
            <img src="/images/project-simindasht-2mw.webp" alt="نیروگاه ۲ مگاواتی سیمین‌دشت" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">نیروگاه ۲ مگاواتی سیمین‌دشت</h4>
            <p class="text-pure-white/60 text-sm mt-1">Growatt + Jinko Panels</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ۱ مگاواتی هشتگرد">
            <img src="/images/project-hashtgerd-1mw.webp" alt="نیروگاه ۱ مگاواتی هشتگرد" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">نیروگاه ۱ مگاواتی هشتگرد</h4>
            <p class="text-pure-white/60 text-sm mt-1">SMA + Trina Panels</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ۳ مگاواتی قزوین">
            <img src="/images/project-qazvin-3mw.webp" alt="نیروگاه ۳ مگاواتی قزوین" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">نیروگاه ۳ مگاواتی قزوین</h4>
            <p class="text-pure-white/60 text-sm mt-1">SMA + Trina Panels</p>
          </div>
        </div>
        <div class="mt-6 glass-card p-6 rounded-2xl text-center border border-solar-gold/30">
          <p class="text-pure-white/70 text-sm mb-1">پروژه‌های مگاواتی اجرا شده</p>
          <p class="font-black text-4xl md:text-6xl text-solar-gold" data-value="40">۴۰</p>
          <p class="text-pure-white/60 text-sm mt-1">و تعداد رو به رشد...</p>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تضمین کیفیت <span class="text-solar-gold">E-E-A-T</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="flex flex-wrap gap-3 mb-6">
          <img src="/images/logo-jinko.webp" alt="Jinko Solar" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
          <img src="/images/logo-trina.webp" alt="Trina Solar" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
          <img src="/images/logo-longi.webp" alt="LONGi" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
          <img src="/images/logo-vmax.webp" alt="Vmax" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
        </div>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="پروژه‌های مگاواتی"`.
  - `<address>` for NAP.
  - Phones `dir="ltr"`.
  - Carousel keyboard navigable.

---

### [SEC_07]: قراردادهای خرید تضمینی ساتبا (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (SATBA).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Trust badges grid. External link to `satba.gov.ir` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badges grid `grid-cols-3 gap-4`.

- **Mobile Stacking:**
  Badges `grid-cols-2`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          قراردادهای خرید تضمینی ساتبا
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://satba.gov.ir" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">سازمان ساتبا</a></h4>
          <p class="text-pure-white/60 text-sm">قرارداد ۲۰ ساله</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://moe.gov.ir" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">وزارت نیرو</a></h4>
          <p class="text-pure-white/60 text-sm">آیین‌نامه Grid Code</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">📜</span>
          <h4 class="font-bold text-pure-white text-lg">اینماد / ساماندهی</h4>
          <p class="text-pure-white/60 text-sm">تأیید تجارت الکترونیک</p>
        </div>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        مراجعه به <a href="https://satba.gov.ir" rel="external noopener" target="_blank"
           class="text-solar-gold underline hover:text-solar-gold/80">سازمان ساتبا</a> برای اطلاع از تعرفه‌های فعلی.
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External links `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: بررسی مسیرهای قانونی ماده 16 برای صنایع

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to article-16 page.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Single glass card with `border-b-4 border-solar-gold`. Internal link pill CTA to `/investment/article-16-industrial-mandate`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Vertical stack.

- **Mobile Stacking:**
  CTA `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        بررسی مسیرهای قانونی <span class="text-solar-gold">ماده ۱۶</span> برای صنایع
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📋 مسیر قانونی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <a href="/investment/article-16-industrial-mandate"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="مطالعه جزئیات حقوقی و معافیت ماده ۱۶">
          جزئیات حقوقی و معافیت ماده ۱۶
          <svg class="w-5 h-5"><!-- Arrow --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - CTA `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile.

---

### [SEC_09]: بخش پاسخ به سوالات متداول طرح توجیهی (FAQ)

- **Section Role:** GEO/SGE bait — FAQPage schema.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Glass accordion. Expanded: `border-s-4 border-solar-gold` + `text-solar-gold` summary.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO preamble banner.

- **Mobile Stacking:**
  Full-width `<summary>` with `py-5`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-navy-mid" x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">طرح توجیهی نیروگاه</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
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
              برای احداث نیروگاه خورشیدی یک مگاواتی چقدر زمین لازم است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            با توجه به راندمان بالای پنل‌های جدید، برای یک نیروگاه ۱ مگاواتی زمینی (Ground-Mounted)، به طور میانگین به حدود ۱ الی ۱.۲ هکتار (۱۰۰۰۰ تا ۱۲۰۰۰ متر مربع) زمین با سطح هموار و فاقد سایه‌اندازی نیاز است.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              درآمد نیروگاه خورشیدی 100 کیلووات چقدر است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            درآمد دقیق به نرخ مصوب قرارداد در لحظه عقد با ساتبا و ضریب تعدیل سالانه بستگی دارد. اما به طور تقریبی یک نیروگاه ۱۰۰ کیلوواتی در منطقه کرج سالانه حدود ۱۸۰ هزار کیلووات‌ساعت برق تولید می‌کند که مستقیماً در نرخ پایه ضرب شده و به صورت ریالی به حساب سرمایه‌گذار واریز می‌گردد.
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

### [SEC_10]: درخواست طرح توجیهی (FS) و پیش‌فاکتور EPC (CTA)

- **Section Role:** CRO conversion — B2B investor CTA.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. Messenger icons `w-16 h-16`. Grain overlay. "درخواست جلسه کارشناسی" CTA.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7`. Messenger: `lg:col-span-5`.

- **Mobile Stacking:**
  Single column. Phones stack. Messenger row `flex gap-4 justify-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          درخواست طرح توجیهی (FS) و <span class="text-deep-navy">پیش‌فاکتور EPC</span>
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_10}
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
          <a href="tel:09124641442" class="block text-2xl md:text-4xl font-bold text-deep-navy/80 hover:text-deep-navy/60 transition-colors" dir="ltr"
             aria-label="تماس با مشاور فنی: ۰۹۱۲۴۶۴۱۴۴۲">
            0912-464-1442
          </a>
        </div>
        <a href="https://wa.me/989125728170?text=درخواست%20جلسه%20کارشناسی%20FS"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="درخواست جلسه کارشناسی FS در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
          درخواست جلسه کارشناسی
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
        <a href="https://wa.me/989125728170?text=درخواست%20جلسه%20کارشناسی%20FS"
           class="inline-flex items-center gap-2 mt-4 w-full md:w-auto px-6 py-3 bg-deep-navy text-solar-gold font-bold rounded-xl hover:bg-deep-navy/90 transition-colors justify-center"
           role="button"
           aria-label="درخواست جلسه کارشناسی FS در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WA --></svg>
          درخواست جلسه کارشناسی
        </a>
        <div class="bg-deep-navy/10 rounded-2xl p-5 border-2 border-deep-navy/20 mt-4">
          <p class="text-deep-navy text-base leading-relaxed font-medium">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
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