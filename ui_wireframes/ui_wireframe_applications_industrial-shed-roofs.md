# UI Wireframe Specification: نیروگاه خورشیدی صنعتی | نصب پنل سقف سوله
- **Source Dossier:** `seo_dossiers/applications_industrial-shed-roofs.md`
- **Target URL:** `/applications/industrial-shed-roofs`
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
| `--color-accent-3`   | `#2ECC71` | `eco-green`           | Success indicators, uptime signals        |
| `--color-danger`     | `#E74C3C` | `alert-red`           | Warnings, Article 16 fines, blackout      |
| `--color-steel`      | `#8B9DAF` | `steel-grey`          | Industrial accents, structural visuals    |
| `--color-glass-bg`   | `rgba(255,255,255,0.07)` | — | Glassmorphism fill                        |
| `--color-glass-border` | `rgba(255,255,255,0.15)` | — | Glassmorphism stroke                    |

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

### Page-Level Visual Theme Note
> This page targets **B2B industrial factory managers**. The aesthetic conveys precision engineering, structural authority, and corporate seriousness. Steel-grey accents complement the core solar-gold/navy palette. Typography is confident and assertive. Data visualizations lean towards engineering spec-sheets rather than consumer-friendly charts.

---

### [SEC_01]: احداث نیروگاه خورشیدی صنعتی سه فاز روی سقف سوله و کارخانجات

- **Section Role:** Primary Hero — H1 entity anchor, B2B first impression with EPC authority badge.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a drone-shot photograph of a massive industrial shed covered with perfectly aligned solar panel rows. Dark gradient overlay: `bg-gradient-to-b from-deep-navy/85 via-deep-navy/50 to-deep-navy`. An "EPC Contractor" authority badge floats in the top-start corner as a `bg-solar-gold text-deep-navy font-bold text-xs uppercase rounded-full px-4 py-1.5`. Headline in `pure-white` with `solar-gold` keyword highlights. GEO TL;DR as a sticky glass card.

- **Desktop Grid Architecture:**
  12-column CSS Grid. Text block: `lg:col-span-7`. GEO callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`. EPC badge positioned `absolute top-6 start-6` within the header.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. EPC badge pinned below the hero image. H1 + body text below. GEO card full-width with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <!-- Background Image -->
    <img src="/images/hero-industrial-shed-solar.webp"
         alt="نیروگاه خورشیدی صنعتی روی سقف سوله کارخانه - نمای هوایی"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager"
         fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <!-- Gradient Overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/85 via-deep-navy/50 to-deep-navy"></div>
    <!-- EPC Badge -->
    <div class="absolute top-6 start-6 z-20 bg-solar-gold text-deep-navy font-bold text-xs uppercase rounded-full px-4 py-1.5 shadow-lg">
      ⚡ پیمانکار گریددار EPC — از ۱ کیلووات تا ۱۰ مگاوات
    </div>
    <!-- Content Grid -->
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <!-- Text Block -->
      <div class="lg:col-span-7 text-start">
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          احداث <span class="text-solar-gold">نیروگاه خورشیدی صنعتی</span> سه فاز روی سقف سوله
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <div class="flex flex-wrap gap-4 mt-8">
          <a href="#sec-11" class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
             role="button" aria-label="درخواست بازدید مهندسی از سقف سوله">
            درخواست بازدید مهندسی
            <svg><!-- Arrow icon --></svg>
          </a>
          <a href="#sec-02" class="inline-flex items-center gap-2 px-8 py-4 border-2 border-pure-white/30 text-pure-white font-bold rounded-2xl hover:border-solar-gold hover:text-solar-gold transition-colors"
             role="button" aria-label="اطلاعات بیشتر درباره ماده ۱۶">
            ماده ۱۶ جهش تولید ⚠️
          </a>
        </div>
      </div>
      <!-- GEO Callout (Sticky) -->
      <aside class="lg:col-span-4 lg:col-start-9 lg:sticky lg:top-24 glass-card p-6 border-s-4 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-2">🏭 خلاصه کلیدی</p>
        <p class="text-base text-pure-white/90 leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_01}
        </p>
      </aside>
    </div>
  </header>
  ```

- **Accessibility & ARIA:**
  - `<header>` landmark wraps the entire hero.
  - Hero image has descriptive Farsi `alt` text.
  - Both CTAs have `role="button"` and explicit `aria-label`.
  - EPC badge is decorative enhancement; key authority claims are in the body text.
  - `fetchpriority="high"` on hero image for LCP.

---

### [SEC_02]: معافیت قطعی از جرایم سنگین ماده ۱۶ جهش تولید

- **Section Role:** Pain-point urgency trigger — legal/financial warning driving action.

- **UI Aesthetic & Colors:**
  High-urgency alert design. Background: `bg-navy-mid`. The primary element is a large Warning Alert Box with `border-2 border-alert-red bg-alert-red/10 rounded-2xl`. Inside, a ⚠️ icon, bold headline in `text-alert-red`, and body text in `pure-white/90`. A secondary "Resolution" card in `bg-eco-green/10 border-eco-green/30` shows the solar solution. An internal link button to `/investment/article-16-industrial-mandate` uses `bg-solar-gold`. GEO callout as a bottom-attached bar with `border-t-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-column grid. Warning alert: `lg:col-span-7`. Resolution card + GEO: `lg:col-span-5`. Asymmetrical weight emphasizing the "problem" side.

- **Mobile Stacking:**
  Warning alert full-width on top. Resolution card below. GEO callout below both.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <!-- Warning Alert Box -->
      <div class="lg:col-span-7 border-2 border-alert-red rounded-2xl p-8 bg-alert-red/10">
        <div class="flex items-start gap-4">
          <span class="text-4xl mt-1">⚠️</span>
          <div>
            <h2 class="font-vazirmatn font-extrabold text-2xl md:text-3xl text-alert-red mb-4">
              هشدار: جرایم سنگین ماده ۱۶ جهش تولید
            </h2>
            <p class="text-pure-white/90 text-base md:text-lg leading-relaxed">
              {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
            </p>
            <a href="/investment/article-16-industrial-mandate"
               class="inline-flex items-center gap-2 mt-6 px-6 py-3 bg-solar-gold text-deep-navy font-bold rounded-xl hover:bg-solar-gold/90 transition-colors"
               role="button" aria-label="مطالعه کامل قانون ماده ۱۶ جهش تولید">
              جزئیات کامل ماده ۱۶
              <svg><!-- Arrow icon --></svg>
            </a>
          </div>
        </div>
      </div>
      <!-- Resolution + GEO -->
      <div class="lg:col-span-5 space-y-6">
        <!-- Resolution Card -->
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-eco-green text-lg mt-3">راه‌حل: نیروگاه خورشیدی سقف سوله</h3>
          <p class="text-pure-white/80 mt-2 text-base leading-relaxed">
            احداث نیروگاه، جرایم را به طور کامل خنثی کرده و هزینه‌های سربار انرژی را به شدت کاهش می‌دهد.
          </p>
        </div>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📋 خلاصه قانونی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
          </p>
        </div>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article>` semantic wrapper per dossier directive.
  - Warning uses both color (red border) AND icon (⚠️) AND text label ("هشدار") for multi-modal communication.
  - Internal link CTA has `role="button"` and `aria-label`.
  - Sufficient contrast: alert-red text on dark background passes WCAG AA.

---

### [SEC_03]: جلوگیری از توقف خطوط تولید در زمان پیک بار

- **Section Role:** Pain resolution — visual contrast between blackout and solar-powered production.

- **UI Aesthetic & Colors:**
  Split-screen design similar to the crypto page's SEC_03 but with industrial imagery. **Blackout side** (start in RTL): Dark, desaturated image of a halted factory floor with `bg-alert-red/5` tint. Red status indicators, "خط تولید متوقف" label. **Solar side** (end in RTL): Bright, well-lit factory with `bg-eco-green/5` glow. Green status, "تولید بی‌وقفه" label. A diagonal SVG separator between panels.

- **Desktop Grid Architecture:**
  12-column grid. Blackout panel: `lg:col-span-6`. Solar panel: `lg:col-span-6`. Both `min-h-[450px]`. GEO callout overlaps center.

- **Mobile Stacking:**
  Vertical stack. Blackout panel (reduced `h-[260px]`) first. Solar panel second. GEO card between them.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[500px]">
      <!-- Blackout Side -->
      <div class="lg:col-span-6 relative flex flex-col items-center justify-center p-8 bg-deep-navy overflow-hidden min-h-[260px] lg:min-h-0">
        <div class="absolute inset-0 bg-alert-red/5"></div>
        <img src="/images/factory-blackout.webp" alt="توقف خط تولید در زمان قطعی برق" class="absolute inset-0 w-full h-full object-cover opacity-15" loading="lazy">
        <div class="relative z-10 text-center space-y-3">
          <span class="text-5xl">🔴</span>
          <h3 class="text-alert-red font-bold text-xl">خط تولید متوقف</h3>
          <p class="text-pure-white/50 text-sm max-w-xs mx-auto">قطعی برق → ضایعات مواد اولیه → خسارت میلیاردی</p>
        </div>
      </div>
      <!-- Solar Production Side -->
      <div class="lg:col-span-6 relative flex flex-col items-center justify-center p-8 bg-deep-navy overflow-hidden min-h-[260px] lg:min-h-0">
        <div class="absolute inset-0 bg-eco-green/5"></div>
        <img src="/images/factory-solar-running.webp" alt="خط تولید فعال با انرژی خورشیدی" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center space-y-3">
          <span class="text-5xl">🟢</span>
          <h3 class="text-eco-green font-bold text-xl">تولید بی‌وقفه با انرژی خورشیدی</h3>
          <p class="text-pure-white/70 text-sm max-w-xs mx-auto">پایداری شیفت‌های کاری → عبور ایمن از پیک مصرف</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">⚡ پایداری تولید</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
    <!-- Full Text Below -->
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        جلوگیری از <span class="text-alert-red">توقف خطوط تولید</span> در زمان پیک بار
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Background images have descriptive `alt` text.
  - Color indicators supplemented by text labels and icons.
  - GEO card uses high-contrast `border-2 border-solar-gold`.

---

### [SEC_04]: باورهای غلط در احداث نیروگاه سقف سوله (Myth vs. Reality)

- **Section Role:** Myth-busting with engineering evidence — close-up clamp photos.

- **UI Aesthetic & Colors:**
  Background: `bg-cream-warm` (palette break for engagement). Dark text (`text-deep-navy`). Myth card: `bg-alert-red/10 border-alert-red/30`. Reality card: `bg-eco-green/10 border-eco-green/30` featuring a close-up macro photo of non-penetrating clamps on a metal roof inside the card. GEO callout as a `border-t-4 border-solar-gold` banner below.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl mx-auto`. Myth/Reality pair: `grid-cols-2`. Reality card contains an embedded image of clamp installation.

- **Mobile Stacking:**
  Myth card first, Reality card + image second, both full-width stacked vertically.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-cream-warm">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در احداث <span class="text-solar-gold">نیروگاه سقف سوله</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8"
           x-data="{ revealed: false }" x-intersect.once="revealed = true">
        <!-- Myth Card -->
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            نصب پنل خورشیدی باعث سوراخ شدن سقف شیروانی و نفوذ آب باران به داخل سوله می‌شود.
          </p>
        </div>
        <!-- Reality Card -->
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            از کلمپ‌های مخصوص آلومینیومی (Non-Penetrating Clamps) استفاده می‌شود که بدون هیچ سوراخ‌کاری روی درزهای سقف چفت می‌شوند.
          </p>
          <!-- Evidence Photo -->
          <img src="/images/clamp-roof-closeup.webp"
               alt="نمای نزدیک کلمپ بدون نفوذ روی سقف شیروانی سوله"
               class="mt-4 rounded-xl w-full h-40 object-cover"
               loading="lazy">
        </div>
      </div>
      <!-- GEO Callout -->
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔩 حقیقت فنی</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
      <!-- Extended Text -->
      <div class="mt-10 text-start max-w-3xl mx-auto">
        <p class="text-deep-navy/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside>` per SEO Dossier directive.
  - Evidence photo has descriptive `alt` text.
  - Myth/Fact labels use icon + text + color.
  - `x-intersect` animation is decorative; content present in DOM from load.

---

### [SEC_05]: استقرار تیم‌های مهندسی در هاب‌های صنعتی البرز و تهران

- **Section Role:** Local SEO anchor — service area proximity for industrial parks.

- **UI Aesthetic & Colors:**
  Background: `bg-deep-navy`. Map highlighting industrial parks in Alborz and Tehran with distance lines to Karaj HQ. Map uses `steel-grey` tones with `solar-gold` markers. The `<address>` card uses `bg-solar-gold text-deep-navy` for NAP prominence. Distance badges (e.g., "۱۵ دقیقه تا اشتهارد") in `bg-steel-grey/20 text-pure-white text-xs rounded-full`.

- **Desktop Grid Architecture:**
  12-column grid. Map: `lg:col-span-7`. Text + address + GEO: `lg:col-span-5`.

- **Mobile Stacking:**
  Map at `max-h-[280px]`. Address and text stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- Map Visual -->
      <div class="lg:col-span-7 rounded-2xl overflow-hidden" aria-label="نقشه شهرک‌های صنعتی تحت پوشش هورا نور سهند" role="img">
        <img src="/images/industrial-parks-coverage-map.webp"
             alt="نقشه دسترسی از کرج به شهرک‌های صنعتی اشتهارد، سیمین‌دشت و بهارستان"
             class="w-full h-auto max-h-[400px] object-cover"
             loading="lazy">
      </div>
      <!-- Text + Address -->
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استقرار در <span class="text-solar-gold">هاب‌های صنعتی</span> البرز و تهران
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <!-- Distance Badges -->
        <div class="flex flex-wrap gap-2">
          <span class="bg-steel-grey/20 text-pure-white text-xs rounded-full px-3 py-1">🏭 اشتهارد — ۱۵ دقیقه</span>
          <span class="bg-steel-grey/20 text-pure-white text-xs rounded-full px-3 py-1">🏭 سیمین‌دشت — ۲۰ دقیقه</span>
          <span class="bg-steel-grey/20 text-pure-white text-xs rounded-full px-3 py-1">🏭 بهارستان — ۳۰ دقیقه</span>
        </div>
        <!-- NAP Address Card -->
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد</p>
          <p>📞 026-36506485</p>
          <p>📱 09125728170</p>
        </address>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 دسترسی سریع</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<address>` HTML element for structured NAP data per dossier directive.
  - Map has `role="img"` and Farsi `aria-label`.
  - Distance badges are supplementary; distances also mentioned in body text.

---

### [SEC_06]: سخت‌افزار استاندارد نیروگاهی و طول عمر تجهیزات (Tier-1)

- **Section Role:** E-E-A-T hardware authority — technical spec grid for industrial components.

- **UI Aesthetic & Colors:**
  Background: `bg-navy-mid`. An asymmetrical Bento Grid of three spec cards: (1) Inverter IP ratings card, (2) Panel degradation curve card with a mini line chart, (3) Galvanized steel thickness card. Each card is a glass card with `border-b-2 border-solar-gold`. Data values in `font-mono text-solar-gold`. Text block + GEO below the grid.

- **Desktop Grid Architecture:**
  3-card Bento layout across 12 columns: Card 1 `lg:col-span-4`, Card 2 `lg:col-span-5`, Card 3 `lg:col-span-3`. Text + GEO below in a centered `max-w-3xl` block.

- **Mobile Stacking:**
  Horizontal scroll carousel with `snap-x snap-mandatory` for the 3 cards. Each card `w-[80vw] snap-center`. Text below at full width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> و طول عمر تجهیزات
      </h2>
      <!-- Bento Spec Grid -->
      <div class="flex lg:grid lg:grid-cols-12 gap-4 mb-12 overflow-x-auto lg:overflow-visible snap-x snap-mandatory lg:snap-none pb-4 lg:pb-0">
        <!-- Card 1: Inverter IP Rating -->
        <div class="glass-card p-6 border-b-2 border-solar-gold min-w-[80vw] lg:min-w-0 snap-center lg:col-span-4">
          <span class="text-3xl">🔌</span>
          <h3 class="font-bold text-pure-white text-lg mt-3">اینورتر سه فاز صنعتی</h3>
          <div class="mt-4 space-y-2">
            <div class="flex justify-between text-sm">
              <span class="text-pure-white/60">درجه حفاظت</span>
              <span class="font-mono text-solar-gold font-bold">IP65</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-pure-white/60">THD هارمونیک</span>
              <span class="font-mono text-solar-gold font-bold">&lt; 3%</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-pure-white/60">ظرفیت</span>
              <span class="font-mono text-solar-gold font-bold">تا ۱۱۰ kW</span>
            </div>
          </div>
        </div>
        <!-- Card 2: Panel Degradation -->
        <div class="glass-card p-6 border-b-2 border-solar-gold min-w-[80vw] lg:min-w-0 snap-center lg:col-span-5">
          <span class="text-3xl">📉</span>
          <h3 class="font-bold text-pure-white text-lg mt-3">منحنی افت عملکرد پنل ۲۵ ساله</h3>
          <div class="mt-4 bg-deep-navy/40 rounded-xl p-4 h-32 flex items-end gap-1">
            <!-- Simplified bar chart visualization -->
            <div class="flex-1 bg-solar-gold/80 rounded-t" style="height: 100%;" title="سال ۱: ۱۰۰٪"></div>
            <div class="flex-1 bg-solar-gold/70 rounded-t" style="height: 97%;" title="سال ۵: ۹۷٪"></div>
            <div class="flex-1 bg-solar-gold/60 rounded-t" style="height: 94%;" title="سال ۱۰: ۹۴٪"></div>
            <div class="flex-1 bg-solar-gold/50 rounded-t" style="height: 90%;" title="سال ۱۵: ۹۰٪"></div>
            <div class="flex-1 bg-solar-gold/40 rounded-t" style="height: 87%;" title="سال ۲۰: ۸۷٪"></div>
            <div class="flex-1 bg-solar-gold/30 rounded-t" style="height: 84%;" title="سال ۲۵: ۸۴٪"></div>
          </div>
          <p class="text-xs text-pure-white/50 mt-2">گارانتی خروجی ≥ ۸۴٪ در سال ۲۵ — پنل‌های Tier-1</p>
        </div>
        <!-- Card 3: Steel Structure -->
        <div class="glass-card p-6 border-b-2 border-solar-gold min-w-[80vw] lg:min-w-0 snap-center lg:col-span-3">
          <span class="text-3xl">🔧</span>
          <h3 class="font-bold text-pure-white text-lg mt-3">سازه نگهدارنده</h3>
          <div class="mt-4 space-y-2">
            <div class="flex justify-between text-sm">
              <span class="text-pure-white/60">متریال</span>
              <span class="font-mono text-solar-gold font-bold">آلومینیوم آلیاژی</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-pure-white/60">پوشش</span>
              <span class="font-mono text-solar-gold font-bold">گالوانیزه گرم</span>
            </div>
            <div class="flex justify-between text-sm">
              <span class="text-pure-white/60">مقاوم در برابر</span>
              <span class="font-mono text-solar-gold font-bold">گازهای اسیدی</span>
            </div>
          </div>
        </div>
      </div>
      <!-- Text + GEO -->
      <div class="max-w-3xl mx-auto text-start space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ استاندارد صنعتی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Spec data presented as key-value pairs with semantic text (not relying on visual layout alone).
  - Bar chart is a decorative visualization; textual caption below provides the same data.
  - Mobile scroll carousel uses `snap-x` for smooth snapping; content accessible via scroll.
  - `title` attributes on bars provide tooltip data on hover.

---

### [SEC_07]: استانداردهای وزارت نیرو و سازمان ساتبا (آپدیت 1403)

- **Section Role:** Temporal freshness + trust authority with outbound link.

- **UI Aesthetic & Colors:**
  Background: `bg-deep-navy`. Trust badge area with institutional feel. The section features a bordered trust card (`border-2 border-steel-grey/40 bg-navy-mid rounded-2xl`) with organizational logos placeholder area and the external link to Tavanir. A `bg-solar-gold text-deep-navy text-xs rounded-full` freshness badge ("آپدیت ۱۴۰۳"). GEO callout below with `border-t-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single column informational layout.

- **Mobile Stacking:**
  No change; already single-column.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استانداردهای <span class="text-solar-gold">وزارت نیرو</span> و سازمان ساتبا
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">آپدیت ۱۴۰۳</span>
      </div>
      <!-- Trust Card -->
      <div class="border-2 border-steel-grey/40 bg-navy-mid rounded-2xl p-8 mb-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT — with inline link:}
          ... آیین‌نامه‌های <a href="https://www.tavanir.org.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">شرکت توانیر</a> و سازمان انرژی‌های تجدیدپذیر ...
        </p>
        <!-- Trust Badges Row -->
        <div class="flex flex-wrap gap-4 mt-6">
          <div class="bg-steel-grey/10 rounded-xl px-4 py-2 text-sm text-pure-white/70 border border-steel-grey/20">🏛️ مورد تایید ساتبا</div>
          <div class="bg-steel-grey/10 rounded-xl px-4 py-2 text-sm text-pure-white/70 border border-steel-grey/20">⚡ منطبق با Grid Codes</div>
          <div class="bg-steel-grey/10 rounded-xl px-4 py-2 text-sm text-pure-white/70 border border-steel-grey/20">📋 پیمانکار EPC گریددار</div>
        </div>
      </div>
      <!-- GEO Callout -->
      <div class="border-t-4 border-solar-gold bg-cream-warm/5 rounded-b-2xl p-6">
        <p class="text-sm font-bold text-solar-gold mb-1">📜 انطباق ۱۴۰۳</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link has `rel="external noopener"` and `target="_blank"`.
  - Trust badges use both icon and text.
  - Freshness badge is supplementary; year is contextual in body text.

---

### [SEC_08]: بررسی ابعاد فیزیکی و توان قابل استخراج از سقف

- **Section Role:** Internal linking bridge — redirects to dimensions guide, prevents cannibalization.

- **UI Aesthetic & Colors:**
  Minimal informational card on `bg-navy-mid`. A glass card with a roof-area calculation teaser: a visual showing roof dimensions with `solar-gold` dashed outlines. Internal link CTA as a pill-shaped `bg-solar-gold` button. GEO callout inline.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single column.

- **Mobile Stacking:**
  No change; CTA becomes `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-navy-mid">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        ابعاد فیزیکی و <span class="text-solar-gold">توان قابل استخراج</span> از سقف
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <!-- Quick Stat -->
        <div class="bg-deep-navy/40 rounded-xl p-4 flex items-center gap-4">
          <span class="text-4xl">📐</span>
          <div>
            <p class="font-mono text-solar-gold text-xl font-bold">~۶۰–۷۰ m² = ۱۰ kWp</p>
            <p class="text-pure-white/60 text-sm">هر ۱۰ کیلووات ظرفیت ≈ ۶۰ تا ۷۰ متر مربع سقف مفید</p>
          </div>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <!-- GEO Callout Inline -->
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📏 قاعده ابعادی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <!-- Internal Link CTA -->
        <a href="/knowledge/land-and-dimensions-guide"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="مشاهده راهنمای کامل ابعاد فیزیکی و فونداسیون">
          ابعاد فیزیکی و فونداسیون
          <svg><!-- Arrow icon --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Internal link has `role="button"` and descriptive `aria-label`.
  - Quick stat uses both monospace visual and plain-text description.
  - `w-full` on mobile for large touch target.

---

### [SEC_09]: بازگشت سرمایه (ROI) برای پروژه‌های صنعتی

- **Section Role:** Financial value proposition with internal link to detailed pricing.

- **UI Aesthetic & Colors:**
  Background: `bg-deep-navy`. A visually prominent ROI teaser card with a large "۳–۵ سال" in `font-mono text-solar-gold text-5xl`. A timeline strip showing investment → breakeven → profit phases using colored segments (gold → green). Internal link to `/pricing/industrial-power-plants`. GEO callout inline.

- **Desktop Grid Architecture:**
  12-column grid. ROI visual + timeline: `lg:col-span-5`. Text + GEO + CTA: `lg:col-span-7`.

- **Mobile Stacking:**
  ROI visual on top. Text + CTA below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- ROI Visual -->
      <div class="lg:col-span-5 glass-card p-8 text-center">
        <p class="text-pure-white/60 text-sm mb-2">نرخ بازگشت سرمایه</p>
        <p class="font-mono text-solar-gold text-5xl md:text-7xl font-black">۳–۵</p>
        <p class="text-pure-white font-bold text-xl mt-2">سال</p>
        <!-- Timeline Strip -->
        <div class="flex mt-6 rounded-full overflow-hidden h-3">
          <div class="bg-solar-gold w-1/3" title="سال ۱–۳: بازگشت سرمایه"></div>
          <div class="bg-eco-green w-2/3" title="سال ۴–۲۵: سود خالص"></div>
        </div>
        <div class="flex justify-between text-xs text-pure-white/50 mt-2">
          <span>سرمایه‌گذاری</span>
          <span>نقطه سربه‌سر</span>
          <span>سود خالص ۲۰+ سال</span>
        </div>
      </div>
      <!-- Text + GEO + CTA -->
      <div class="lg:col-span-7 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          بازگشت سرمایه <span class="text-solar-gold">(ROI)</span> پروژه‌های صنعتی
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">💰 تحلیل اقتصادی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
          </p>
        </div>
        <a href="/pricing/industrial-power-plants"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button"
           aria-label="مشاهده جدول برآورد هزینه‌ها و طرح توجیهی صنعتی">
          برآورد هزینه‌ها
          <svg><!-- Arrow icon --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Timeline strip has `title` attributes on segments.
  - Text labels below timeline provide the same info non-visually.
  - CTA has `role="button"` and `aria-label`.

---

### [SEC_10]: سوالات متداول مدیران صنایع (FAQ)

- **Section Role:** GEO/SGE bait — FAQ accordion with FAQPage JSON-LD.

- **UI Aesthetic & Colors:**
  Background: `bg-navy-mid`. Glass card accordions with `border-s-4 border-solar-gold` when expanded, `border-s-4 border-pure-white/10` when collapsed. Summary text `text-solar-gold` when open.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single-column accordion stack.

- **Mobile Stacking:**
  No change; full-width accordion.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-navy-mid"
           x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">مدیران صنایع</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
        </p>
      </div>
      <div class="space-y-4">
        <!-- FAQ Item 1 -->
        <details class="glass-card overflow-hidden"
                 :class="openFaq === 1 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 1 ? null : 1">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" :aria-expanded="openFaq === 1 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 1 ? 'text-solar-gold' : 'text-pure-white'">
              آیا سقف سوله‌های قدیمی تحمل وزن پنل‌های خورشیدی را دارند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''"><!-- Chevron --></svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، وزن اضافه‌شده (Dead Load) معمولاً کمتر از ۱۵ کیلوگرم بر متر مربع است... تیم نظام مهندسی ما قبل از اجرا تحلیل سازه‌ای دقیقی انجام می‌دهد.
          </div>
        </details>
        <!-- FAQ Item 2 -->
        <details class="glass-card overflow-hidden"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا گرد و غبار شهرک‌های صنعتی راندمان پنل‌ها را کاهش می‌دهد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''"><!-- Chevron --></svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، تا ۱۵ درصد. ما مسیرهای ایمن دسترسی، سیستم‌های نازل آب یا ربات‌های تمیزکننده را در طراحی لحاظ می‌کنیم.
          </div>
        </details>
      </div>
      <!-- CODER NOTE: Wrap FAQ in FAQPage JSON-LD schema per dossier directive. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>` / `<summary>` for keyboard + screen reader support.
  - `:aria-expanded` dynamically bound via Alpine.
  - Generous touch targets.

---

### [SEC_11]: درخواست بازدید مهندسی از سقف سوله کارخانه شما

- **Section Role:** Final CRO conversion block — B2B focused with "Request Site Visit" CTA.

- **UI Aesthetic & Colors:**
  Full-width high-contrast block. Background: `bg-solar-gold`. Text: `text-deep-navy`. A prominent "درخواست بازدید مهندسی" button in `bg-deep-navy text-solar-gold` (inverted from usual CTA). Phone numbers are oversized. A secondary "Request Site Visit" action card with a clipboard icon. Messenger icons in `bg-deep-navy text-solar-gold` circles.

- **Desktop Grid Architecture:**
  12-column grid. Text + CTA + phones: `lg:col-span-7`. Messenger + GEO: `lg:col-span-5`.

- **Mobile Stacking:**
  Single column centered. Full-width CTA buttons and phone numbers.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-11" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- CTA Text Block -->
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          درخواست بازدید مهندسی از <span class="text-deep-navy/70">سقف سوله کارخانه شما</span>
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_11}
        </p>
        <!-- Primary CTA -->
        <a href="#contact-form"
           class="inline-flex items-center gap-3 px-10 py-5 bg-deep-navy text-solar-gold font-black text-lg rounded-2xl hover:bg-deep-navy/90 transition-colors shadow-xl mb-6"
           role="button" aria-label="درخواست بازدید مهندسی رایگان از سقف سوله">
          📋 درخواست بازدید مهندسی رایگان
        </a>
        <!-- Phone Numbers -->
        <div class="space-y-3 mt-4">
          <a href="tel:02636506485" class="block text-3xl md:text-5xl font-black text-deep-navy hover:text-deep-navy/70 transition-colors" dir="ltr"
             aria-label="تماس با دفتر مرکزی کرج: ۰۲۶-۳۶۵۰۶۴۸۵">
            026-36506485
          </a>
          <a href="tel:09125728170" class="block text-2xl md:text-4xl font-bold text-deep-navy/80 hover:text-deep-navy/60 transition-colors" dir="ltr"
             aria-label="تماس با مدیریت پروژه: ۰۹۱۲۵۷۲۸۱۷۰">
            0912-572-8170
          </a>
        </div>
      </div>
      <!-- Messenger Icons + GEO -->
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-deep-navy font-bold text-lg">ارسال لوکیشن کارخانه و دریافت رزومه مگاواتی:</p>
        <div class="flex gap-4">
          <a href="https://wa.me/989125728170" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در واتس‌اپ">
            <svg><!-- WA --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در بله">
            <svg><!-- Bale --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در ایتا">
            <svg><!-- Eitaa --></svg>
          </a>
        </div>
        <!-- GEO Callout -->
        <div class="bg-deep-navy/10 rounded-2xl p-5 border-2 border-deep-navy/20 mt-4 w-full">
          <p class="text-deep-navy text-base leading-relaxed font-medium">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_11}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Phone links use `<a href="tel:...">` with Farsi `aria-label`.
  - Phone numbers `dir="ltr"` for correct digit rendering.
  - Primary CTA has `role="button"` with descriptive `aria-label`.
  - Messenger buttons: `w-16 h-16` (64px) exceeds WCAG minimum.
  - External links `rel="noopener"`.

---

[VERIFIED_UI_END_OF_FILE]
