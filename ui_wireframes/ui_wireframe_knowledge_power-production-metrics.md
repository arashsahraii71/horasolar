# UI Wireframe Specification: هر پنل خورشیدی چقدر برق تولید می‌کند؟ | جدول وات و آمپر | هورا نور سهند
- **Source Dossier:** `seo_dossiers/knowledge_power-production-metrics.md`
- **Target URL:** `/knowledge/power-production-metrics`
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

### [SEC_01]: هر پنل خورشیدی چقدر برق تولید می‌کند؟ (مقدمه مهندسی)

- **Section Role:** Primary Hero — SGE Citation Bait, Core Topic Definition.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a clean summary box showing the mathematical formula: `Watts × Peak Sun Hours = Daily Production`. Deep-navy base (`bg-deep-navy`). Formula box with `solar-gold` accent border. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Hero content: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Formula box above fold. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          مرجع محاسبه تولید برق
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          هر پنل خورشیدی <span class="text-solar-gold">چقدر برق تولید می‌کند؟</span> (مقدمه مهندسی)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <div class="glass-card p-6 border-s-4 border-solar-gold mt-6">
          <p class="text-sm font-bold text-solar-gold mb-2">فرمول محاسبه روزانه</p>
          <p class="text-xl font-black text-solar-gold font-mono mb-2">P(kWh/day) = P(W) × PSH × 0.85</p>
          <p class="text-pure-white/80 text-sm mt-2">
            وات پنل × ساعات آفتابی مفید × ضریب راندمن = تولید روزانه (kWh)
          </p>
        </div>
        <a href="#sec-02" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مطالعه تفاوت وات، ولت و آمپر">
          مطالعه پارامترهای الکتریکی
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
  - Formula box has semantic structure.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image (if any).

---

### [SEC_02]: درک تفاوت وات، ولت و آمپر در سیستم‌های خورشیدی

- **Section Role:** Technical basics hub — Water pipe analogy visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Water pipe analogy infographic: Pressure (Voltage) → Pipe diameter (Amperage) → Total water power (Watts). Three animated columns with icons.

- **Desktop Grid Architecture:**
  12-col. Three-column grid (`grid-cols-3 gap-6`) for Voltage, Amperage, Wattage. Each column a glass card with animated icon.

- **Mobile Stacking:**
  Vertical stack. Three cards stack vertically.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        درک تفاوت <span class="text-solar-gold">وات</span>، <span class="text-solar-gold">ولت</span> و <span class="text-solar-gold">آمپر</span> در سیستم‌های خورشیدی
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12">
        <!-- Voltage -->
        <div class="glass-card p-8 rounded-2xl text-center transition-all hover:shadow-xl hover:border-solar-gold/50 border border-solar-gold/20"
             x-data="{ anim: false }" x-intersect.once="anim = true">
          <div class="text-5xl mb-4" :class="anim ? 'animate-bounce' : ''">⚡</div>
          <h3 class="font-bold text-xl text-solar-gold mb-3">ولتاژ (Volt) — فشار</h3>
          <p class="text-pure-white/80 text-base leading-relaxed">
            نیرویی که الکترون‌ها را در مدار به حرکت درمی‌آورد. معادل "فشار آب" در لوله.
          </p>
        </div>
        <!-- Amperage -->
        <div class="glass-card p-8 rounded-2xl text-center transition-all hover:shadow-xl hover:border-solar-gold/50 border border-solar-gold/20"
             x-data="{ anim: false }" x-intersect.once="anim = true" class="delay-100">
          <div class="text-5xl mb-4">💧</div>
          <h3 class="font-bold text-xl text-solar-gold mb-3">آمپر (Ampere) — جریان</h3>
          <p class="text-pure-white/80 text-base leading-relaxed">
            مقدار الکترون‌هایی که در واحد زمان از مدار عبور می‌کنند. معادل "دبی آب" در لوله.
          </p>
        </div>
        <!-- Wattage -->
        <div class="glass-card p-8 rounded-2xl text-center transition-all hover:shadow-xl hover:border-solar-gold/50 border border-solar-gold/20"
             x-data="{ anim: false }" x-intersect.once="anim = true" class="delay-200">
          <div class="text-5xl mb-4">⚡</div>
          <h3 class="font-bold text-xl text-solar-gold mb-3">وات (Watt) — توان</h3>
          <p class="text-pure-white/80 text-base leading-relaxed">
            حاصل‌ضرب ولتاژ در آمپر (W = V × A). توان نهایی برای انجام کار.
          </p>
        </div>
      </div>
      <div class="glass-card p-6 border-s-4 border-solar-gold max-w-3xl mx-auto mt-12">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 اصل کلیدی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_03]: یک پنل خورشیدی چند آمپر برق تولید می‌کند؟

- **Section Role:** Direct Answer — High-volume query.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Specification table with hover effects. Highlighted `Imp` column in `solar-gold`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Spec table full-width.

- **Mobile Stacking:**
  Table horizontal scroll (`overflow-x-auto`).

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        یک پنل خورشیدی <span class="text-solar-gold">چند آمپر</span> برق تولید می‌کند؟
      </h2>
      <div class="glass-card p-6 overflow-x-auto">
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="جدول آمپر تولیدی پنل‌های پنل‌های رده‌یک">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">پنل</th>
              <th scope="col" class="p-4 text-start">توان (W)</th>
              <th scope="col" class="p-4 text-start">Vmp (V)</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">Imp (A)</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">550W</td><td class="p-3">550W</td><td class="p-3">41.6V</td><td class="p-3 text-solar-gold font-bold">13.2A</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">550W (Trina)</td><td class="p-3">550W</td><td class="p-3">41.6V</td><td class="p-3 text-solar-gold font-bold">13.2A</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">620W (Jinko)</td><td class="p-3">620W</td><td class="p-3">43.2V</td><td class="p-3 text-solar-gold font-bold">14.3A</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">620W (Jinko Bifacial)</td><td class="p-3">620W</td><td class="p-3">43.2V</td><td class="p-3 text-solar-gold font-bold">14.3A</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">710W (LONGi)</td><td class="p-3">710W</td><td class="p-3">44.5V</td><td class="p-3 text-solar-gold font-bold">15.9A</td></tr>
          </tbody>
        </table>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-2xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📊 قاعده کلی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on headers.

---

### [SEC_04]: جدول تخصصی توان، ولت و آمپر مدل‌های پرکاربرد

- **Section Role:** Structured Data Table — SERP snippet target.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Full-width responsive table with `overflow-x-auto` on mobile. Header row `bg-navy-mid text-solar-gold`. Alternating rows `bg-deep-navy/60` / `bg-navy-mid/40`. Efficiency column `text-eco-green font-bold`.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Table full-width. GEO callout below.

- **Mobile Stacking:**
  Table horizontal scroll (`overflow-x-auto`). GEO callout below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        جدول تخصصی <span class="text-solar-gold">توان، ولت و آمپر</span> مدل‌های پرکاربرد
      </h2>
      <div class="glass-card p-6 overflow-x-auto">
        <table class="w-full min-w-[700px] text-sm" role="table" aria-label="جدول تخصصی مشخصات پنل‌های رده‌یک (Jinko, Trina, LONGi)">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">برند و مدل</th>
              <th scope="col" class="p-4 text-start">توان نامی (Pmax)</th>
              <th scope="col" class="p-4 text-start">Vmp (V)</th>
              <th scope="col" class="p-4 text-start">Imp (A)</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">راندمان ماژول</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">Trina Solar</td><td class="p-4">550W</td><td class="p-4">41.6V</td><td class="p-4 text-solar-gold font-bold">13.2A</td><td class="p-4 text-eco-green font-bold">21.0%</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">JinkoSolar</td><td class="p-4">620W</td><td class="p-4">43.2V</td><td class="p-4 text-solar-gold font-bold">14.3A</td><td class="p-4 text-eco-green font-bold">22.1%</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">LONGi</td><td class="p-4">710W</td><td class="p-4">44.5V</td><td class="p-4 text-solar-gold font-bold">15.9A</td><td class="p-4 text-eco-green font-bold">22.8%</td></tr>
          </tbody>
        </table>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📋 نکته مهم</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on all headers.

---

### [SEC_05]: هر متر مربع پنل خورشیدی چقدر برق تولید می‌کند؟

- **Section Role:** Spatial vs Power — Space calculator call-out.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Call-out box: "Space Calculator: 1 kW of power requires approx. 5 sq meters of roof space." `solar-gold` badge on `eco-green` background.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Call-out box centered. Text below.

- **Mobile Stacking:**
  No change.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        هر متر مربع پنل خورشیدی <span class="text-solar-gold">چقدر برق</span> تولید می‌کند؟
      </h2>
      <div class="glass-card p-8 border-s-4 border-solar-gold mb-10">
        <span class="inline-flex items-center gap-2 bg-eco-green text-deep-navy text-sm font-bold rounded-full px-3 py-1 mb-4">
          Space Calculator
        </span>
        <p class="text-pure-white/90 text-lg font-bold mb-2">۱ kW توان = حدود ۵ متر مربع سقف</p>
        <p class="text-pure-white/80 text-base leading-relaxed max-w-xl mx-auto">
          پنل‌های مدرن با ابعادی در حدود ۲.۵ متر مربع، توانایی تولید بالغ بر ۵۵۰ تا ۶۰۰ وات را دارند.
        </p>
      </div>
      <div class="text-start max-w-2xl mx-auto mt-8">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
          هر متر مربع پنل خورشیدی <span class="text-solar-gold">چقدر برق</span> تولید می‌کند؟
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 محاسبه فضا</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_06]: تاثیر اقلیم و تابش بر تولید واقعی (داده‌های اختصاصی البرز)

- **Section Role:** Proprietary data integration — Regional production map.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Infographic: Sun arc over Alborz map with `solar-gold` arc line showing "5.5 kWh/kW/day" badge. Map uses `solar-gold` pulse dots for Karaj, Mehrshahr, Kordan.

- **Desktop Grid Architecture:**
  12-col. Map/Illustration: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Map first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار تولید روزانه بر حسب کیلووات در البرز" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">تولید روزانه در استان البرز (هر کیلووات ظرفیت)</h3>
          <div class="relative h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار تولید روزانه بر حسب کیلووات در البرز">
              <!-- Sun Arc -->
              <path d="M50,250 Q200,50 350,250" stroke="#F5A623" stroke-width="3" fill="none" stroke-linecap="round">
                <animate attributeName="stroke-dashoffset" from="1000" to="0" dur="2s" fill="freeze"/>
              </path>
              <!-- Stats Badge -->
              <text x="200" y="150" text-anchor="middle" fill="#2ECC71" font-size="24" font-family="Vazirmatn" font-weight="bold">۵.۵ kWh/kW/روز</text>
              <!-- Pulse Dots -->
              <circle cx="150" cy="200" r="8" fill="#F5A623">
                <animate attributeName="r" from="8" to="20" dur="2s" repeatCount="indefinite"/>
                <animate attributeName="opacity" from="0.8" to="0" dur="2s" repeatCount="indefinite"/>
              </circle>
            </svg>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تاثیر اقلیم و تابش بر <span class="text-solar-gold">تولید واقعی</span> (داده‌های اختصاصی البرز)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="glass-card p-5 border-s-4 border-eco-green bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">☀️ مزیت اقلیمی البرز</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Map `role="img"` + `aria-label`.
  - Color + text labels for stats.

---

### [SEC_07]: یک پنل خورشیدی چند لامپ را روشن می‌کند؟

- **Section Role:** Real-world B2C contextualization — Icon grid.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Icon grid: 1 Panel = 40 Bulbs = 1 TV + 1 Fridge + 1 Pump. Icons with `solar-gold` glow.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Icon grid `grid-cols-3 gap-6` below text.

- **Mobile Stacking:**
  Stack vertically.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        یک پنل خورشیدی <span class="text-solar-gold">چند لامپ</span> را روشن می‌کند؟
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-10 max-w-2xl mx-auto">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div class="glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-5xl mb-3">💡</span>
          <h3 class="font-bold text-xl text-pure-white mb-2">۴۰ لامپ LED (۱۰ وات)</h3>
          <p class="text-pure-white/70 text-sm">۸ ساعت روشنایی شبانه</p>
        </div>
        <div class="glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-5xl mb-3">📺</span>
          <h3 class="font-bold text-xl text-pure-white mb-2">۱ تلویزیون + ۱ یخچال</h3>
          <p class="text-pure-white/70 text-sm">چند ساعت استفاده</p>
        </div>
        <div class="glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-5xl mb-3">⚡</span>
          <h3 class="font-bold text-xl text-pure-white mb-2">شارژ لپ‌تاپ + موبایل</h3>
          <p class="text-pure-white/70 text-sm">استفاده روزانه</p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_08]: محاسبه تولید برق برای راه‌اندازی کولر گازی

- **Section Role:** High-value B2C pain point — Warning/Alert block.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Warning/Alert block: `bg-alert-red/10 border-2 border-alert-red`. Warning icon ⚠️. "Heavy-Duty Inverter Required" badge `bg-alert-red text-deep-navy`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Warning box prominent. Text below.

- **Mobile Stacking:**
  Warning box first. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl">
      <div class="bg-alert-red/10 border-2 border-alert-red rounded-2xl p-8 mb-10" role="alert" aria-live="polite">
        <div class="flex items-start gap-4">
          <span class="text-4xl">⚠️</span>
          <div>
            <h3 class="text-alert-red font-bold text-xl mb-2">هشدار فنی: کولر گازی نیاز به پکیج ۵+ کیلووات دارد</h3>
            <p class="text-pure-white/80 text-base md:text-lg leading-relaxed">
              {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
            </p>
          </div>
        </div>
      </div>
      <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
          محاسبه تولید برق برای راه‌اندازی <span class="text-solar-gold">کولر گازی</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="glass-card p-5 border-s-4 border-alert-red mt-8 bg-alert-red/5">
          <p class="text-sm font-bold text-alert-red mb-1">⚠️ هشدار فنی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `role="alert"` on alert box.
  - `aria-live="polite"` for dynamic content.
  - Color + text labels.

---

### [SEC_09]: افت توان حرارتی: افسانه در برابر واقعیت

- **Section Role:** Myth-busting — Temperature coefficient.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth: `bg-alert-red/10 border-alert-red/30` ❌. Reality: `bg-eco-green/10 border-eco-green/30` ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-09" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        افت توان حرارتی: <span class="text-solar-gold">افسانه در برابر واقعیت</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">افسانه</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            هرچه هوا گرم‌تر باشد و آفتاب سوزان‌تر بتابد، پنل خورشیدی برق بیشتری تولید می‌کند.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های خورشیدی فتوولتائیک با "نور" کار می‌کنند، نه با "حرارت". در واقع، با افزایش دمای سلول‌های سیلیکونی به بالای ۲۵ درجه سانتی‌گراد، ولتاژ پنل دچار افت می‌شود (ضریب افت دمایی). به همین دلیل، یک ظهر خنک زمستانی در صورت تابش مستقیم آفتاب، راندمان بالاتری نسبت به ظهر داغ تابستان دارد. ما در هورا نور سهند با ایجاد فاصله استاندارد استراکچر از سطح بام، تهویه طبیعی زیر پنل‌ها را فراهم کرده و این افت توان را مهار می‌کنیم.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت علمی</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside id="sec-09">`.
  - `x-intersect` decorative.
  - Meaning via icon + text.
  - Contrast: dark text on light cards.

---

### [SEC_10]: ارتباط توان تولیدی با قرارداد ساتبا (درآمدزایی)

- **Section Role:** Financial intent — Income banner + external link.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Info banner `border-2 border-solar-gold`. External link to `satba.gov.ir` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badge inline with H2.

- **Mobile Stacking:**
  Badge wraps naturally.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          ارتباط توان تولیدی با <span class="text-solar-gold">قرارداد ساتبا</span>
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">درآمدزایی</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_10}
      </p>
      <div class="glass-card p-5 border-s-4 border-solar-gold">
        <div class="flex items-start gap-3">
          <span class="text-2xl mt-1">💰</span>
          <div>
            <p class="text-sm font-bold text-solar-gold mb-1">💰 فرمول درآمد</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
            </p>
          </div>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mt-8">
          مراجعه به <a href="https://satba.gov.ir/" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">سازمان انرژی‌های تجدیدپذیر و بهره‌وری انرژی برق (ساتبا)</a> برای اطلاع از تعرفه‌های فعلی.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_11]: سوالات متداول درباره تولید برق پنل‌ها (FAQ)

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
        سوالات متداول <span class="text-solar-gold">تولید برق پنل‌ها</span>
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
              پنل خورشیدی ۱۲ ولت است یا ۲۴ ولت؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            پنل‌های کوچک (زیر ۲۰۰ وات) معمولاً ولتاژ ۱۲ یا ۱۸ ولت دارند، اما پنل‌های نیروگاهی مدرن (مانند برندهای Jinko و Trina) ولتاژی بین ۴۰ تا ۵۰ ولت (DC) تولید می‌کنند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا می‌توان برق تولید شده توسط پنل را مستقیماً استفاده کرد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر، برای استفاده در وسایل خانگی، ولتاژ متغیر DC پنل باید توسط دستگاهی به نام اینورتر (Inverter) به ولتاژ ثابت ۲۲۰ ولت متناوب (AC) تبدیل شود.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              چگونه بفهمیم چند عدد پنل نیاز داریم؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            ابتدا باید مجموع مصرف لوازم برقی خود را به وات‌ساعت محاسبه کنید و سپس با استفاده از میزان تابش منطقه، تعداد پنل و سایز باتری توسط دپارتمان مهندسی هورا نور سهند برآورد می‌گردد.
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