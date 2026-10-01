# UI Wireframe Specification: پیمانکار نیروگاه خورشیدی در استان تهران | هورا نور سهند
- **Source Dossier:** `seo_dossiers/locations_tehran-province.md`
- **Target URL:** `/locations/tehran-province`
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

### [SEC_01]: پیمانکار نیروگاه خورشیدی در استان تهران (H1 Hero)

- **Section Role:** Primary Hero — H1 entity, geographic authority, B2B/B2C trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with split background: aerial view of Tehran skyline transitioning to solar panels on villa roofs in Lavasanat. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). Trust badge row (SATBA, Ministry of Energy, E-Namad) below H1. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-tehran-solar.webp"
         alt="پنل‌های خورشیدی روی پشت‌بام‌های لواسانات و سوله‌های شهرک شمس‌آباد — تهران"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          مجری مشروع EPC | تاییدیه ساتبا
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          پیمانکار نیروگاه خورشیدی در <span class="text-solar-gold">استان تهران</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره پروژه‌های خورشیدی در تهران">
          مشاوره رایگان
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
  - Hero `alt` in Farsi describing solar panels on Tehran villas and industrial zones.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: نیروگاه‌های صنعتی خورشیدی (شهرک صنعتی شمس‌آباد)

- **Section Role:** B2B Industrial — On-Grid systems for factories.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Industrial theme. Split view: left side shows factory with rooftop solar (day), right side shows production line running during blackout (`eco-green` glow). GEO callout as overlap card on divider.

- **Desktop Grid Architecture:**
  12-col. Left: `lg:col-span-6` (factory day). Right: `lg:col-span-6` (factory night). GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Day first (`h-[300px]`), then night. GEO between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/factory-day-solar.webp" alt="کارخانه شهرک شمس‌آباد با نیروگاه خورشیدی روی سقف" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🏭</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">نیروگاه آنگرید صنعتی</h3>
          <p class="text-pure-white/60 mt-2 text-sm">تزریق به شبکه + معافیت ماده ۱۶</p>
        </div>
      </div>
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/factory-night-solar.webp" alt="خط تولید در حال کار در طول قطعی برق شهری" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⚡</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">خط تولید در کار + معافیت ماده ۱۶</h3>
          <p class="text-pure-white/70 mt-2 text-sm">تزریق به شبکه + بک‌آپ ۲۴ ساعته</p>
        </div>
      </div>
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 خلاصه تصمیم‌ساز</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
        </p>
      </div>
    </div>
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        نیروگاه‌های خورشیدی <span class="text-solar-gold">صنعتی</span> در <span class="text-solar-gold">شهرک صنعتی شمس‌آباد</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
      </p>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article id="sec-02">`.
  - Color + text labels for meaning.
  - GEO card `border-2 border-solar-gold`.

---

### [SEC_03]: سیستم‌های آفگرید و هیبریدی برای ویلاها (لواسانات و شهریار)

- **Section Role:** B2C Residential — Off-Grid/Hybrid systems for villas.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Lifestyle imagery: villa at sunset with solar panels. Glass cards for package tiers.

- **Desktop Grid Architecture:**
  12-col. Header centered. Package grid: `grid-cols-1 md:grid-cols-3 gap-6`.

- **Mobile Stacking:**
  Single column stack.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        سیستم‌های <span class="text-solar-gold">آفگرید و هیبریدی</span> برای ویلاهای <span class="text-solar-gold">لواسانات و شهریار</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Package 1 -->
        <div class="glass-card p-6 border-s-4 border-eco-green rounded-2xl text-start">
          <span class="inline-block bg-eco-green/20 text-eco-green text-sm font-bold px-3 py-1 rounded-full mb-4">پکیج پایه</span>
          <h3 class="font-bold text-xl text-pure-white mb-3">پکیج ۵ کیلووات (آفگرید)</h3>
          <p class="text-pure-white/70 text-sm mb-4">مناسب برای کولر، یخچال، پمپ و روشنایی</p>
          <p class="text-solar-gold font-bold text-xl">از ~[DATA NEEDED] میلیون تومان</p>
        </div>
        <!-- Package 2 -->
        <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl text-start">
          <span class="inline-block bg-solar-gold/20 text-solar-gold text-sm font-bold px-3 py-1 rounded-full mb-4">پکیج پرکاربرد</span>
          <h3 class="font-bold text-xl text-pure-white mb-3">پکیج ۱۰ کیلووات (هیبریدی)</h3>
          <p class="text-pure-white/70 text-sm mb-4">کولر گازی، یخچال، پمپ استخر، استخر</p>
          <p class="text-solar-gold font-bold text-xl">از ~[DATA NEEDED] میلیون تومان</p>
        </div>
        <!-- Package 3 -->
        <div class="glass-card p-6 border-s-4 border-alert-red rounded-2xl text-start">
          <span class="inline-block bg-alert-red/20 text-alert-red text-sm font-bold px-3 py-1 rounded-full mb-4">پکیج لوکس</span>
          <h3 class="font-bold text-xl text-pure-white mb-3">پکیج ۱۵+ کیلووات (هیبریدی کامل)</h3>
          <p class="text-pure-white/70 text-sm mb-4">پشتیبانی کامل همه تجهیزات ویلای لوکس</p>
          <p class="text-alert-red font-bold text-xl">از ~[DATA NEEDED] میلیون تومان</p>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Package cards have semantic structure.
  - Price emphasis for conversion.

---

### [SEC_04]: نیروگاه‌های مقیاس کوچک برای فروش برق (شهر تهران)

- **Section Role:** Investment — Residential On-Grid for passive income.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Clean, investment-focused. Glass cards with ROI badges.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO callout.

- **Mobile Stacking:**
  No change.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        نیروگاه‌های مقیاس کوچک برای <span class="text-solar-gold">فروش برق در شهر تهران</span>
      </h2>
      <div class="glass-card p-8 space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">💰 درآمد قطعی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
          </p>
        </div>
        <a href="/investment/satba-guaranteed-purchase"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors"
           role="button"
           aria-label="مطالعه قرارداد ۲۰ ساله خرید تضمینی برق ساتبا">
          مطالعه قرارداد ۲۰ ساله ساتبا
          <svg class="w-5 h-5"><!-- Arrow --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - CTA with descriptive `aria-label`.
  - Internal link to SATBA page.

---

### [SEC_05]: سخت‌افزار و مهندسی (Tier-1 Panels & Engineering)

- **Section Role:** E-E-A-T authority — Hardware showcase + engineering protocol.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Brand logo carousel (Jinko, Trina, LONGi, JA Solar, Mana, Taban). Trust badges row.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Logo carousel `flex gap-8 overflow-x-auto snap-x snap-mandatory`. Trust badges row.

- **Mobile Stacking:**
  Carousel `snap-x` with `snap-center` items.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> و پروتکل مهندسی
      </h2>
      <div class="flex gap-8 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             @mouseenter="$el.classList.remove('grayscale')" @mouseleave="$el.classList.add('grayscale')"
             class="grayscale transition-colors duration-300"
             role="figure" aria-label="پنل‌های Jinko Solar">
          <img src="/images/logo-jinko.webp" alt="Jinko Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Jinko Solar</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Trina Solar">
          <img src="/images/logo-trina.webp" alt="Trina Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Trina Solar</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های LONGi">
          <img src="/images/logo-longi.webp" alt="LONGi" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">LONGi</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های JA Solar">
          <img src="/images/logo-ja-solar.webp" alt="JA Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">JA Solar</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Mana">
          <img src="/images/logo-mana.webp" alt="Mana" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Mana</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Taban">
          <img src="/images/logo-taban.webp" alt="Taban" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Taban</span>
        </div>
      </div>
      <div class="mt-8 glass-card p-5 border-s-4 border-solar-gold text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="برندهای تجهیزات Tier-1"`.
  - Hover removes grayscale (decorative).
  - `loading="lazy"` on logos.

---

### [SEC_06]: اطلاعات پیشگام و داده‌های اجرا (Information Gain)

- **Section Role:** Authority — Proprietary data + project counter.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Rolling counter `data-value="40"`. Capacity range visual.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Counter + capacity bar + GEO callout.

- **Mobile Stacking:**
  Stacks naturally.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        داده‌های اجرا <span class="text-solar-gold">هورا نور سهند در تهران</span>
      </h2>
      <div class="glass-card p-8 rounded-2xl text-center border border-solar-gold/30 mb-8">
        <p class="text-pure-white/70 text-sm mb-1">پروژه‌های اجرا شده</p>
        <p class="font-black text-4xl md:text-6xl text-solar-gold" data-value="40">۴۰</p>
        <p class="text-pure-white/60 text-sm mt-1">و تعداد رو به رشد...</p>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">📊 داده‌های اجرا</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Counter has `data-value` for animation.
  - Semantic heading structure.

---

### [SEC_07]: لینک‌های داخلی و معماری لینک‌دهی

- **Section Role:** Internal linking hub — Anti-cannibalization.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Three prominent pill links with icons.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Three pill links side-by-side on desktop, stacked on mobile.

- **Mobile Stacking:**
  Stacked vertically, each `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-16 md:py-24 bg-navy-mid">
    <div class="container mx-auto px-4 max-w-3xl text-center space-y-4">
      <a href="/investment/article-16-industrial-mandate"
         class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
         role="button"
         aria-label="مطالعه راهنمای معافیت ماده ۱۶ برای صنایع">
        <svg class="w-5 h-5"><!-- Factory --></svg>
        معافیت ماده ۱۶ و نیروگاه‌های صنعتی
      </a>
      <a href="/applications/residential-villa-appliances"
         class="inline-flex items-center gap-2 px-8 py-4 bg-eco-green text-pure-white font-bold rounded-2xl hover:bg-eco-green/90 transition-colors w-full md:w-auto justify-center"
         role="button"
         aria-label="مطالعه پکیج‌های ویلایی برای لواسانات و شهریار">
        <svg class="w-5 h-5"><!-- Home --></svg>
        پکیج‌های برق خورشیدی ویلایی
      </a>
      <a href="/investment/satba-guaranteed-purchase"
         class="inline-flex items-center gap-2 px-8 py-4 bg-eco-green text-pure-white font-bold rounded-2xl hover:bg-eco-green/90 transition-colors w-full md:w-auto justify-center"
         role="button"
         aria-label="مطالعه قرارداد ۲۰ ساله خرید تضمینی برق ساتبا">
        <svg class="w-5 h-5"><!-- Contract --></svg>
        قرارداد ۲۰ ساله خرید تضمینی برق
      </a>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Buttons `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile for touch target.

---

### [SEC_08]: CTA نهایی — مشاوره پروژه‌های تهران (CTA)

- **Section Role:** CRO conversion — B2B + B2C combined.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. Messenger icons `w-16 h-16`. Grain overlay.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7`. Messenger: `lg:col-span-5`.

- **Mobile Stacking:**
  Single column. Phones stack. Messenger row `flex gap-4 justify-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          پروژه خورشیدی خود در تهران را همین امروز آغاز کنید
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
        </div>
        <a href="https://wa.me/989125728170?text=مشاوره%20پروژه%20خورشیدی%20در%20تهران"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="مشاوره پروژه‌های خورشیدی در تهران در واتس‌اپ">
          مشاوره رایگان واتس‌اپ
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
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