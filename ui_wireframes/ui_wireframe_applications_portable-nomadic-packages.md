# UI Wireframe Specification: پکیج برق خورشیدی قابل حمل و عشایری
- **Source Dossier:** `seo_dossiers/applications_portable-nomadic-packages.md`
- **Target URL:** `/applications/portable-nomadic-packages`
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
| `--color-danger`     | `#E74C3C` | `alert-red`           | Danger/gasoline/loss column in comparisons|
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

### [SEC_01]: پکیج‌ها و سامانه‌های مولد برق خورشیدی قابل حمل و عشایری

- **Section Role:** Primary Hero — First Contentful Paint anchor, H1 entity definition & niche intent capture.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a cinematic dusk photograph of a nomadic tent at a campsite, illuminated warmly from the inside by a portable solar generator box, with a folded solar panel propped open nearby (see `needed_images.md`). A deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/85 via-deep-navy/50 to-deep-navy`) ensures text contrast. Headline in `pure-white` with the key entity phrase in `solar-gold`. The GEO TL;DR block renders as a Glassmorphism floating card with a `border-s-4 border-solar-gold` accent stripe. A warm, sunset-amber CSS radial glow (`radial-gradient(ellipse at 70% 80%, rgba(245,166,35,0.15), transparent 60%)`) is layered above the image overlay to reinforce the "dusk illumination" mood.

- **Desktop Grid Architecture:**
  12-column CSS Grid. Text block occupies `lg:col-span-7 lg:col-start-1` (right-aligned in RTL), vertically centered. GEO Callout card occupies `lg:col-span-4 lg:col-start-9`, positioned as `lg:sticky lg:top-24` so it stays visible during initial scroll.

- **Mobile Stacking:**
  Single column. Hero image as `object-cover h-[65vh]` with the warm gradient overlay. H1 + body text stacks below. GEO Callout card reflows to full-width below text with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <!-- Background Image -->
    <img src="/images/hero-portable-nomadic.webp"
         alt="چادر عشایری در غروب با پکیج برق خورشیدی قابل حمل روشن"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager"
         fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <!-- Gradient Overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/85 via-deep-navy/50 to-deep-navy"></div>
    <!-- Warm Glow Layer -->
    <div class="absolute inset-0" style="background: radial-gradient(ellipse at 70% 80%, rgba(245,166,35,0.15), transparent 60%);"></div>
    <!-- Content Grid -->
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <!-- Text Block -->
      <div class="lg:col-span-7 text-start">
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          پکیج‌ها و سامانه‌های مولد <span class="text-solar-gold">برق خورشیدی قابل حمل</span> و عشایری
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="سفارش و خرید پکیج خورشیدی قابل حمل">
          سفارش و استعلام قیمت
          <svg><!-- Arrow icon --></svg>
        </a>
      </div>
      <!-- GEO Callout (Sticky) -->
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
  - `<header>` landmark wraps the entire hero.
  - Hero image has descriptive `alt` in Farsi describing the full scene.
  - CTA `<a>` has `role="button"` and explicit `aria-label`.
  - GEO callout `<aside>` is semantically separated as complementary content.
  - `fetchpriority="high"` on hero image for LCP optimization.

---

### [SEC_02]: مکانیزم و مهندسی پکیج‌های پرتابل خورشیدی

- **Section Role:** Deep technical explainer — Semantic Depth & Information Gain with interactive component diagram.

- **UI Aesthetic & Colors:**
  Deep navy background (`bg-deep-navy`). An asymmetrical Bento Grid layout features an "exploded view" interactive diagram on one side (a glass card containing a schematic of the portable box with labeled hotspots) and stacked text + GEO callout on the other. Hotspot labels use `solar-gold` pill badges on `navy-mid` backgrounds. Component connection lines are `stroke-solar-gold` dashed SVG. When a user hovers/taps a hotspot, a tooltip glass card appears with the component description (Alpine.js driven).

- **Desktop Grid Architecture:**
  12-column grid. Interactive diagram block: `lg:col-span-5 lg:sticky lg:top-20`. Text + GEO callout block: `lg:col-span-7`.

- **Mobile Stacking:**
  Diagram block stacks above at full width with `min-h-[350px]`. Hotspot tooltips switch from hover-triggered to tap-triggered on touch devices. Text and GEO callout stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <!-- Exploded Diagram -->
      <div class="lg:col-span-5 lg:sticky lg:top-20" aria-label="نمودار اجزای داخلی پکیج خورشیدی قابل حمل" role="img"
           x-data="{ activeComponent: null }">
        <div class="glass-card p-8 relative min-h-[400px]">
          <!-- Central Box Image -->
          <img src="/images/portable-box-exploded.webp" alt="نمای اکسپلود شده جعبه مرکزی پکیج خورشیدی" class="w-full h-auto rounded-xl" loading="lazy">
          <!-- Hotspot: Inverter -->
          <button class="absolute top-[15%] start-[20%] w-8 h-8 rounded-full bg-solar-gold text-deep-navy font-black text-sm flex items-center justify-center animate-pulse hover:animate-none cursor-pointer"
                  @mouseenter="activeComponent = 'inverter'" @mouseleave="activeComponent = null"
                  @click="activeComponent = activeComponent === 'inverter' ? null : 'inverter'"
                  aria-label="اینورتر داخلی">
            ۱
          </button>
          <div x-show="activeComponent === 'inverter'" x-transition
               class="absolute top-[8%] start-[35%] glass-card p-3 text-sm text-pure-white/90 max-w-[200px] z-20 border border-solar-gold/30">
            <strong class="text-solar-gold">اینورتر</strong><br>تبدیل DC به AC برای خروجی دوشاخه استاندارد
          </div>
          <!-- Hotspot: Battery -->
          <button class="absolute top-[45%] start-[15%] w-8 h-8 rounded-full bg-solar-gold text-deep-navy font-black text-sm flex items-center justify-center animate-pulse hover:animate-none cursor-pointer"
                  @mouseenter="activeComponent = 'battery'" @mouseleave="activeComponent = null"
                  @click="activeComponent = activeComponent === 'battery' ? null : 'battery'"
                  aria-label="باتری ذخیره‌ساز">
            ۲
          </button>
          <div x-show="activeComponent === 'battery'" x-transition
               class="absolute top-[38%] start-[30%] glass-card p-3 text-sm text-pure-white/90 max-w-[200px] z-20 border border-solar-gold/30">
            <strong class="text-solar-gold">باتری سیلد اسید / لیتیومی</strong><br>ذخیره انرژی بدون خطر نشت اسید
          </div>
          <!-- Hotspot: USB Ports -->
          <button class="absolute top-[70%] start-[60%] w-8 h-8 rounded-full bg-solar-gold text-deep-navy font-black text-sm flex items-center justify-center animate-pulse hover:animate-none cursor-pointer"
                  @mouseenter="activeComponent = 'usb'" @mouseleave="activeComponent = null"
                  @click="activeComponent = activeComponent === 'usb' ? null : 'usb'"
                  aria-label="پورت‌های USB و خروجی DC">
            ۳
          </button>
          <div x-show="activeComponent === 'usb'" x-transition
               class="absolute top-[63%] start-[75%] glass-card p-3 text-sm text-pure-white/90 max-w-[200px] z-20 border border-solar-gold/30">
            <strong class="text-solar-gold">خروجی USB & DC 12V</strong><br>شارژ موبایل، لپ‌تاپ و تجهیزات DC
          </div>
          <!-- Hotspot: Charge Controller -->
          <button class="absolute top-[30%] start-[70%] w-8 h-8 rounded-full bg-solar-gold text-deep-navy font-black text-sm flex items-center justify-center animate-pulse hover:animate-none cursor-pointer"
                  @mouseenter="activeComponent = 'controller'" @mouseleave="activeComponent = null"
                  @click="activeComponent = activeComponent === 'controller' ? null : 'controller'"
                  aria-label="شارژ کنترلر">
            ۴
          </button>
          <div x-show="activeComponent === 'controller'" x-transition
               class="absolute top-[23%] start-[85%] glass-card p-3 text-sm text-pure-white/90 max-w-[200px] z-20 border border-solar-gold/30">
            <strong class="text-solar-gold">شارژ کنترلر PWM/MPPT</strong><br>مدیریت هوشمند شارژ از پنل به باتری
          </div>
        </div>
      </div>
      <!-- Text Content -->
      <div class="lg:col-span-7 space-y-8 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مکانیزم و مهندسی <span class="text-solar-gold">پکیج‌های پرتابل خورشیدی</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <!-- GEO Callout Inline -->
        <div class="glass-card p-6 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی برای موتورهای جستجو</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
          </p>
        </div>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article>` semantically wraps the self-contained technical content.
  - Diagram container has `role="img"` with Farsi `aria-label` describing the schematic.
  - Each hotspot is a `<button>` with an explicit Farsi `aria-label`.
  - Tooltip content is in the DOM and accessible when activated; `x-transition` provides smooth reveal.
  - GEO callout is a `<div>` with visual border emphasis (inline within the article flow).

---

### [SEC_03]: جایگزینی قطعی برای موتور برق‌های بنزینی کوچک

- **Section Role:** Pain-point emotional trigger — Comparison table driving conviction.

- **UI Aesthetic & Colors:**
  Warm palette break: background shifts to `bg-cream-warm` with `text-deep-navy` for contrast inversion. The comparison table is rendered as two tall cards side-by-side: the "Gasoline Generator" card uses `bg-alert-red/10 border-2 border-alert-red/30` with a noisy/heavy/toxic visual theme; the "Solar Generator" card uses `bg-eco-green/10 border-2 border-eco-green/30` with a silent/light/clean theme. Each card has stacked rows of icon + attribute pairs. A diagonal SVG wave separator divides this section from the preceding one.

- **Desktop Grid Architecture:**
  12-column grid. Gasoline card: `lg:col-span-5`. Divider (VS badge): `lg:col-span-2 flex items-center justify-center`. Solar card: `lg:col-span-5`. The GEO callout spans full-width below as a `border-t-4 border-solar-gold` banner on `bg-pure-white`.

- **Mobile Stacking:**
  Cards stack vertically. Gasoline card first (red-themed), then a centered "VS" circle badge (`w-16 h-16 rounded-full bg-solar-gold text-deep-navy font-black text-2xl`), then solar card (green-themed). GEO callout below full-width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-cream-warm relative"
           x-data="{ revealed: false }" x-intersect.once="revealed = true">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        جایگزینی قطعی برای <span class="text-solar-gold">موتور برق‌های بنزینی</span>
      </h2>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-stretch mb-12">
        <!-- Gasoline Generator Card -->
        <div class="lg:col-span-5 rounded-2xl p-8 bg-alert-red/10 border-2 border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'">
          <div class="text-center mb-6">
            <span class="text-5xl">⛽</span>
            <h3 class="font-bold text-alert-red text-xl mt-3">موتور برق بنزینی</h3>
          </div>
          <ul class="space-y-4 text-deep-navy/80 text-base" role="list">
            <li class="flex items-start gap-3">
              <span class="text-alert-red text-xl mt-0.5">✗</span>
              <span>وزن سنگین — حمل دشوار در مسیرهای کوهستانی</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-alert-red text-xl mt-0.5">✗</span>
              <span>نیاز مداوم به خرید و حمل گالن‌های بنزین</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-alert-red text-xl mt-0.5">✗</span>
              <span>صدای کرکننده — تخریب آرامش طبیعت و دام‌ها</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-alert-red text-xl mt-0.5">✗</span>
              <span>دود و بوی سمی — آلودگی محیط کمپینگ</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-alert-red text-xl mt-0.5">✗</span>
              <span>هزینه تعمیرات مکرر و قطعات یدکی</span>
            </li>
          </ul>
        </div>
        <!-- VS Badge (Center) -->
        <div class="lg:col-span-2 flex items-center justify-center">
          <div class="w-16 h-16 md:w-20 md:h-20 rounded-full bg-solar-gold text-deep-navy font-black text-2xl md:text-3xl flex items-center justify-center shadow-lg"
               aria-hidden="true">
            VS
          </div>
        </div>
        <!-- Solar Generator Card -->
        <div class="lg:col-span-5 rounded-2xl p-8 bg-eco-green/10 border-2 border-eco-green/30 transition-all duration-700 delay-300"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'">
          <div class="text-center mb-6">
            <span class="text-5xl">☀️</span>
            <h3 class="font-bold text-eco-green text-xl mt-3">ژنراتور خورشیدی هورا نور</h3>
          </div>
          <ul class="space-y-4 text-deep-navy/80 text-base" role="list">
            <li class="flex items-start gap-3">
              <span class="text-eco-green text-xl mt-0.5">✓</span>
              <span>سبک و کامپکت — جای‌گیری در صندوق عقب خودرو</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-eco-green text-xl mt-0.5">✓</span>
              <span>انرژی رایگان خورشید — بدون هزینه سوخت</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-eco-green text-xl mt-0.5">✓</span>
              <span>۱۰۰٪ بی‌صدا (Silent) — حفظ آرامش طبیعت</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-eco-green text-xl mt-0.5">✓</span>
              <span>صفر دود و آلایندگی — دوست‌دار محیط زیست</span>
            </li>
            <li class="flex items-start gap-3">
              <span class="text-eco-green text-xl mt-0.5">✓</span>
              <span>عمر مفید ۲۰+ ساله بدون استهلاک مکانیکی</span>
            </li>
          </ul>
        </div>
      </div>
      <!-- Full Body Text -->
      <div class="max-w-3xl mx-auto text-start mb-8">
        <p class="text-deep-navy/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
      </div>
      <!-- GEO Callout Full-Width -->
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 خلاصه تصمیم‌ساز</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section>` wrapper with `id="sec-03"`.
  - Lists use `role="list"` for explicit list semantics in RTL context.
  - Color is never the sole indicator: textual symbols (✗ / ✓) and labels accompany color coding.
  - VS badge has `aria-hidden="true"` (decorative).
  - `x-intersect` used for scroll-triggered reveal (non-essential, decorative only — content is in DOM from load).

---

### [SEC_04]: باورهای غلط درباره ژنراتورهای سیار خورشیدی (Myth vs. Reality)

- **Section Role:** Myth-busting SGE bait — manages expectations and reduces returns.

- **UI Aesthetic & Colors:**
  Return to `bg-deep-navy`. The callout box uses a distinctive "Myth vs Fact" split design: a single large glass card divided diagonally. The "Myth" half has a subtle `bg-alert-red/5` tint with a ❌ icon and `border-s-4 border-alert-red/40`. The "Fact" half has `bg-eco-green/5` tint with a ✅ icon and `border-e-4 border-eco-green/40`. A prominent warning badge `⚠️` in `bg-solar-gold text-deep-navy` sits atop the card as a floating label.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl mx-auto`. The myth/fact card is a `grid-cols-2` within the glass card. Text body paragraph sits above the card. GEO callout is rendered inline below the card as a `border-t-4 border-solar-gold` banner.

- **Mobile Stacking:**
  The myth/fact card splits vertically: Myth section first (red accent), then Fact section (green accent). Both full-width with `gap-4`.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-6">
        باورهای غلط درباره <span class="text-solar-gold">ژنراتورهای سیار خورشیدی</span>
      </h2>
      <!-- Body Text -->
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed text-start mb-10 max-w-3xl mx-auto">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
      </p>
      <!-- Myth vs Fact Card -->
      <div class="glass-card overflow-hidden relative"
           x-data="{ revealed: false }" x-intersect.once="revealed = true">
        <!-- Floating Warning Badge -->
        <div class="absolute -top-4 start-1/2 -translate-x-1/2 z-10 bg-solar-gold text-deep-navy font-black text-sm rounded-full px-5 py-2 shadow-lg flex items-center gap-2">
          <span>⚠️</span> هشدار مهم قبل از خرید
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2">
          <!-- Myth Side -->
          <div class="p-8 bg-alert-red/5 border-s-4 border-alert-red/40 transition-all duration-700"
               :class="revealed ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-8'">
            <span class="text-4xl">❌</span>
            <h3 class="font-bold text-alert-red text-xl mt-3 mb-4">باور غلط</h3>
            <p class="text-pure-white/80 text-base leading-relaxed">
              «با پکیج قابل حمل می‌توان المنت حرارتی، هیتر، فرز و دریل صنعتی را روشن کرد.»
            </p>
          </div>
          <!-- Fact Side -->
          <div class="p-8 bg-eco-green/5 border-e-4 border-eco-green/40 transition-all duration-700 delay-200"
               :class="revealed ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-8'">
            <span class="text-4xl">✅</span>
            <h3 class="font-bold text-eco-green text-xl mt-3 mb-4">واقعیت</h3>
            <p class="text-pure-white/80 text-base leading-relaxed">
              این پکیج‌ها صرفاً برای مصارف سبک طراحی شده‌اند: روشنایی LED، شارژ موبایل، لپ‌تاپ، تلویزیون کوچک و یخچال مسافرتی DC.
            </p>
          </div>
        </div>
      </div>
      <!-- GEO Callout -->
      <div class="border-t-4 border-solar-gold glass-card rounded-2xl p-6 mt-8">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت فنی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside>` used per SEO Dossier semantic instruction.
  - Myth/Fact labels use both color AND icon + text so meaning doesn't rely solely on color.
  - `x-intersect` is decorative animation only; content is in DOM from load.
  - Warning badge is decorative reinforcement; heading already communicates "myths."
  - Sufficient contrast: light text on dark backgrounds; red/green labels are accompanied by textual ❌/✅ symbols.

---

### [SEC_05]: توزیع و ارسال از دفتر مرکزی کرج به سراسر کشور

- **Section Role:** Local SEO map anchor & proximity authority signal.

- **UI Aesthetic & Colors:**
  Background: `bg-navy-mid`. A stylized vector graphic/illustration showing dispatch from a Karaj HQ pin to various mountainous and rural terrains across Iran. The HQ pin pulses with a `solar-gold` CSS animation (`animate-pulse`). Dispatch route lines are dashed gold SVG strokes. The `<address>` block uses `bg-solar-gold text-deep-navy` for strong NAP signal contrast. Terrain destination markers use small `eco-green` circle dots.

- **Desktop Grid Architecture:**
  12-column grid. Shipping vector graphic: `lg:col-span-7`. Text + address card + GEO callout: `lg:col-span-5`. The address card is a solid `bg-solar-gold` card for visual prominence.

- **Mobile Stacking:**
  Shipping graphic reduces to `max-h-[280px]` centered above. Text, address card, and GEO callout stack vertically below. Address card is full-width with prominent display.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- Shipping Vector Graphic -->
      <div class="lg:col-span-7" aria-label="نقشه ارسال پکیج از کرج به مناطق کوهستانی و عشایری ایران" role="img">
        <img src="/images/shipping-map-nomadic.svg" alt="نقشه ارسال پکیج خورشیدی از دفتر کرج به طالقان، کردان، جاده چالوس و سراسر ایران" class="w-full h-auto max-h-[400px] object-contain" loading="lazy">
      </div>
      <!-- Text + Address -->
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          توزیع و ارسال از <span class="text-solar-gold">دفتر مرکزی کرج</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <!-- NAP Address Card -->
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد</p>
          <p>📞 <a href="tel:02636506485" class="hover:underline" aria-label="تماس با دفتر: ۰۲۶-۳۶۵۰۶۴۸۵" dir="ltr">026-36506485</a></p>
          <p>📱 <a href="tel:09122641473" class="hover:underline" aria-label="تماس همراه: ۰۹۱۲۲۶۴۱۴۷۳" dir="ltr">09122641473</a></p>
        </address>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش سراسری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<address>` HTML element used per SEO Dossier directive (semantic NAP signal) embedded in `<section>`.
  - Phone numbers use `<a href="tel:...">` with explicit `aria-label` in Farsi.
  - Map image has comprehensive `alt` text listing served regions and routes.
  - Map container has `role="img"` with Farsi `aria-label`.

---

### [SEC_06]: طرح‌های حمایتی عشایری (آپدیت 1403)

- **Section Role:** Temporal freshness signal with authoritative outbound entity link.

- **UI Aesthetic & Colors:**
  Soft informational block on `bg-deep-navy`. The tip box uses a `border-2 border-solar-gold` with a 📰 news icon. Background has a subtle warm tint: `bg-cream-warm/5` inside the info card. The outbound link to `ashayer.ir` is styled as `text-solar-gold underline hover:text-solar-gold/80`. A small "بروزرسانی ۱۴۰۳" freshness badge in `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` sits inline next to the H2.

- **Desktop Grid Architecture:**
  Centered content column: `max-w-3xl mx-auto`. Single column layout — no grid split needed for this informational block.

- **Mobile Stacking:**
  No change needed; already single-column centered. Badge wraps to next line naturally.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          طرح‌های حمایتی عشایری
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">آپدیت ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT — with inline link:}
        ... نهادهای متولی نظیر <a href="https://ashayer.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">سازمان امور عشایر ایران</a> همواره استفاده از سامانه‌های مولد برق خورشیدی قابل حمل را ...
      </p>
      <!-- Informational Tip Box / GEO Block -->
      <div class="border-2 border-solar-gold rounded-2xl p-6 bg-cream-warm/5">
        <div class="flex items-start gap-3">
          <span class="text-2xl mt-1">📰</span>
          <div>
            <p class="text-sm font-bold text-solar-gold mb-1">نکته مهم حمایتی ۱۴۰۳</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link has `rel="external noopener"` and `target="_blank"` per SEO Dossier coder instruction.
  - Freshness badge is decorative and doesn't convey critical info (the heading already contextualizes the year).
  - Tip box uses semantic grouping with icon + text; icon is decorative (emoji).
  - Single-column centered layout ensures comfortable line length for reading.

---

### [SEC_07]: انتخاب بین سیستم ثابت ویلایی و پکیج سیار

- **Section Role:** Internal linking bridge — anti-cannibalization, redirecting users to the correct product.

- **UI Aesthetic & Colors:**
  Background: gradient `bg-gradient-to-b from-deep-navy to-navy-mid`. A decision-tree style card layout: two glass cards side-by-side, one representing "Portable/Nomadic" (current page, `border-2 border-solar-gold` highlighted, with a ✅ "شما اینجا هستید" badge) and one representing "Fixed Villa System" (with a `border-2 border-pure-white/20` muted style and a prominent internal link CTA). An arrow SVG connects them with a dashed gold line.

- **Desktop Grid Architecture:**
  12-column grid. Current page card: `lg:col-span-5`. Arrow connector: `lg:col-span-2 flex items-center justify-center`. Villa card: `lg:col-span-5`. Text body below spans `max-w-3xl mx-auto`. GEO callout inline below text.

- **Mobile Stacking:**
  Cards stack vertically. Current page card first (highlighted). A downward arrow icon between them. Villa card second with the internal link CTA button. Text and GEO callout below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-gradient-to-b from-deep-navy to-navy-mid">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-12">
        انتخاب بین <span class="text-solar-gold">سیستم ثابت</span> و پکیج سیار
      </h2>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-stretch max-w-5xl mx-auto mb-12">
        <!-- Current Page Card (Portable) -->
        <div class="lg:col-span-5 glass-card p-8 border-2 border-solar-gold relative">
          <span class="absolute -top-3 start-4 bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">✅ شما اینجا هستید</span>
          <div class="text-center mb-4">
            <span class="text-5xl">🎒</span>
            <h3 class="font-bold text-solar-gold text-xl mt-3">پکیج قابل حمل / عشایری</h3>
          </div>
          <ul class="space-y-2 text-pure-white/80 text-sm" role="list">
            <li>✓ برای کمپینگ و کوچ عشایر</li>
            <li>✓ ظرفیت محدود (مصارف سبک)</li>
            <li>✓ Plug & Play بدون نصاب</li>
            <li>✓ قابل جابجایی مداوم</li>
          </ul>
        </div>
        <!-- Arrow Connector -->
        <div class="lg:col-span-2 flex items-center justify-center">
          <div class="text-solar-gold text-4xl" aria-hidden="true">
            <span class="hidden lg:inline">⟷</span>
            <span class="lg:hidden">⟵ یا ⟶</span>
          </div>
        </div>
        <!-- Villa Card (Link Target) -->
        <div class="lg:col-span-5 glass-card p-8 border-2 border-pure-white/20 hover:border-solar-gold/50 transition-colors">
          <div class="text-center mb-4">
            <span class="text-5xl">🏡</span>
            <h3 class="font-bold text-pure-white text-xl mt-3">سیستم ثابت ویلایی / آفگرید</h3>
          </div>
          <ul class="space-y-2 text-pure-white/80 text-sm" role="list">
            <li>✓ برای خانه باغ و کانکس دائمی</li>
            <li>✓ ظرفیت بالا (یخچال، تلویزیون بزرگ)</li>
            <li>✓ نصب تخصصی توسط مهندسین</li>
            <li>✓ باتری‌های بزرگ‌تر و اینورتر قوی‌تر</li>
          </ul>
          <a href="/applications/residential-villa-appliances"
             class="mt-6 inline-flex items-center gap-2 px-6 py-3 bg-solar-gold text-deep-navy font-bold rounded-xl hover:bg-solar-gold/90 transition-colors w-full justify-center"
             role="button"
             aria-label="مشاهده پکیج‌های خورشیدی ویلایی - سیستم ثابت نصبی">
            مشاهده پکیج‌های خورشیدی ویلایی
            <svg><!-- Arrow icon --></svg>
          </a>
        </div>
      </div>
      <!-- Body Text -->
      <div class="max-w-3xl mx-auto text-start mb-8">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07 — internal link anchor "پکیج‌های خورشیدی ویلایی" must link to /applications/residential-villa-appliances}
        </p>
      </div>
      <!-- GEO Callout -->
      <div class="glass-card p-6 border-s-4 border-solar-gold max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته انتخابی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Internal link CTA has `role="button"` with full descriptive `aria-label` per SEO Dossier.
  - Link anchor text strictly matches the dossier's requirement: "پکیج‌های خورشیدی ویلایی" links to `/applications/residential-villa-appliances`.
  - Arrow connector has `aria-hidden="true"` (decorative).
  - Both cards use `role="list"` on their feature lists.
  - Current-page badge visually and textually identifies which card represents this page.

---

### [SEC_08]: ویژگی‌های پنل خورشیدی تاشو و کیفی

- **Section Role:** Entity depth builder — camping hardware product gallery.

- **UI Aesthetic & Colors:**
  Background: `bg-deep-navy`. A horizontal photo gallery of foldable/briefcase solar panels with a "scale comparison" visual style (panel next to a backpack or hand for size reference). Gallery cards use Glassmorphism with hover-reveal captions. Each card has a thin `border-b-2 border-solar-gold` bottom accent. Image overlay gradient (`from-transparent to-deep-navy/70`) shows caption text on hover. Key specs (weight, wattage, USB ports) are displayed as pill badges on each card.

- **Desktop Grid Architecture:**
  Asymmetrical Bento Grid: one large card `lg:col-span-8 lg:row-span-2` (the "folded vs unfolded" comparison shot) and two smaller stacked cards `lg:col-span-4` (close-ups of ETFE coating and USB ports). Text block below spans `lg:col-span-8` with GEO callout on `lg:col-span-4`.

- **Mobile Stacking:**
  Horizontal scroll carousel with `snap-x snap-mandatory`. Each card is `w-[85vw] snap-center`. Text and GEO callout stack vertically below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-10">
        ویژگی‌های <span class="text-solar-gold">پنل خورشیدی تاشو</span> و کیفی
      </h2>
      <!-- Bento Image Grid (Desktop) / Carousel (Mobile) -->
      <div class="hidden lg:grid grid-cols-12 gap-4 mb-12">
        <!-- Large Card -->
        <div class="lg:col-span-8 lg:row-span-2 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[400px]"
             role="figure" aria-label="پنل خورشیدی تاشو در حالت باز و بسته کنار کوله‌پشتی">
          <img src="/images/foldable-panel-scale.webp" alt="پنل خورشیدی تاشو باز و بسته در مقایسه با کوله‌پشتی" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-6">
            <div>
              <p class="text-pure-white font-bold text-lg">مقایسه اندازه: باز و بسته</p>
              <div class="flex gap-2 mt-2">
                <span class="bg-solar-gold/20 text-solar-gold text-xs font-bold rounded-full px-3 py-1">زیر ۳ کیلوگرم</span>
                <span class="bg-solar-gold/20 text-solar-gold text-xs font-bold rounded-full px-3 py-1">ETFE Coating</span>
              </div>
            </div>
          </div>
        </div>
        <!-- Small Card 1 -->
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="نمای نزدیک پوشش ETFE پنل تاشو">
          <img src="/images/etfe-coating-closeup.webp" alt="پوشش پلیمری ETFE مقاوم در برابر خط و خش" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">پوشش ETFE ضدخش</p>
          </div>
        </div>
        <!-- Small Card 2 -->
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="پورت‌های USB داخلی پنل کیفی">
          <img src="/images/panel-usb-ports.webp" alt="پورت‌های USB داخلی پنل خورشیدی کیفی برای شارژ مستقیم" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">پورت USB داخلی — شارژ مستقیم</p>
          </div>
        </div>
      </div>
      <!-- Mobile Carousel -->
      <div class="lg:hidden flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 mb-12 -mx-4 px-4" role="region" aria-label="گالری پنل‌های خورشیدی تاشو">
        <div class="w-[85vw] flex-shrink-0 snap-center rounded-2xl overflow-hidden relative min-h-[280px]">
          <img src="/images/foldable-panel-scale.webp" alt="پنل خورشیدی تاشو باز و بسته" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute bottom-0 inset-x-0 bg-gradient-to-t from-deep-navy/80 to-transparent p-4">
            <p class="text-pure-white font-bold">مقایسه اندازه: باز و بسته</p>
          </div>
        </div>
        <div class="w-[85vw] flex-shrink-0 snap-center rounded-2xl overflow-hidden relative min-h-[280px]">
          <img src="/images/etfe-coating-closeup.webp" alt="پوشش ETFE" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute bottom-0 inset-x-0 bg-gradient-to-t from-deep-navy/80 to-transparent p-4">
            <p class="text-pure-white font-bold">پوشش ETFE ضدخش</p>
          </div>
        </div>
        <div class="w-[85vw] flex-shrink-0 snap-center rounded-2xl overflow-hidden relative min-h-[280px]">
          <img src="/images/panel-usb-ports.webp" alt="پورت‌های USB پنل کیفی" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute bottom-0 inset-x-0 bg-gradient-to-t from-deep-navy/80 to-transparent p-4">
            <p class="text-pure-white font-bold">پورت USB — شارژ مستقیم</p>
          </div>
        </div>
      </div>
      <!-- Text + GEO Row -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
        <div class="lg:col-span-8 text-start">
          <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
            {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
          </p>
        </div>
        <div class="lg:col-span-4 glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📦 مشخصات کلیدی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Each image card has `role="figure"` and descriptive `aria-label` in Farsi.
  - Hover captions are decorative overlays; `alt` text on images provides equivalent information for screen readers.
  - Mobile carousel has `role="region"` with descriptive `aria-label`.
  - `loading="lazy"` on all gallery images for performance.
  - Spec pill badges are supplementary; their content is reiterated in the text body below.

---

### [SEC_09]: بخش پاسخ به سوالات متداول (FAQ)

- **Section Role:** GEO/SGE bait — FAQ with FAQPage JSON-LD schema, accordion UI.

- **UI Aesthetic & Colors:**
  Background: `bg-navy-mid`. Each FAQ item is a glass card with `border-s-4 border-solar-gold` when expanded, `border-s-4 border-pure-white/10` when collapsed. The summary text uses `text-solar-gold` when open, `text-pure-white` when closed. Smooth `x-collapse` transition. GEO preamble at top as a `bg-cream-warm/5` banner.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single column stack of accordion items.

- **Mobile Stacking:**
  No change; already single-column. Touch targets for `<summary>` elements are full-width with `py-5` padding.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-navy-mid"
           x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">پکیج خورشیدی قابل حمل</span>
      </h2>
      <!-- GEO Preamble -->
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
        </p>
      </div>
      <!-- FAQ Accordion -->
      <div class="space-y-4">
        <!-- FAQ Item 1 -->
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 1 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 1 ? null : 1">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   aria-expanded="false"
                   :aria-expanded="openFaq === 1 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 1 ? 'text-solar-gold' : 'text-pure-white'">
              آیا پکیج برق خورشیدی قابل حمل ضدآب است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform flex-shrink-0 ms-4" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron icon -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            پنل‌های خورشیدی کاملاً ضدآب هستند و در زیر باران مشکلی پیدا نمی‌کنند. اما جعبه کنترل مرکزی (که شامل باتری و اینورتر است) باید در محیطی خشک مانند داخل چادر یا ماشین نگهداری شود و در برابر باران مستقیم محافظت گردد.
          </div>
        </details>
        <!-- FAQ Item 2 -->
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              یک پکیج عشایری چند ساعت روشنایی در شب می‌دهد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform flex-shrink-0 ms-4" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron icon -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            این کاملاً به مدل پکیج و آمپر باتری آن بستگی دارد. اما به طور میانگین، پکیج‌های استاندارد هورا نور سهند می‌توانند ۴ تا ۶ لامپ LED را به مدت ۸ تا ۱۲ ساعت در شبانه‌روز (از غروب تا طلوع آفتاب) روشن نگه دارند.
          </div>
        </details>
      </div>
      <!-- JSON-LD Reminder for Developer -->
      <!-- CODER NOTE: Wrap above FAQ content strictly in FAQPage JSON-LD schema as per dossier directive. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>` / `<summary>` elements ensure keyboard accessibility and screen reader support out of the box.
  - `aria-expanded` is dynamically bound via Alpine for enhanced state communication.
  - `role="button"` on `<summary>` for consistent interaction model.
  - Touch target height is generous (`py-5 px-6`).
  - Chevron icon has `ms-4` (logical margin) for RTL spacing.

---

### [SEC_10]: سفارش و خرید پکیج‌های قابل حمل

- **Section Role:** Final CRO conversion block — high-contrast CTA for nomadic/camping customers.

- **UI Aesthetic & Colors:**
  Full-width high-contrast block. Background: `bg-solar-gold`. All text: `text-deep-navy`. Phone numbers are oversized (`text-3xl md:text-5xl font-black`), clickable with `<a href="tel:...">`. Messenger icons (WhatsApp, Bale, Eitaa, Rubika) are circular icon buttons in `bg-deep-navy text-solar-gold`. A subtle grain texture overlay for premium feel. The GEO callout renders as a `bg-deep-navy/10 rounded-2xl border-2 border-deep-navy/20` card to stay readable on the golden background.

- **Desktop Grid Architecture:**
  12-column grid. Text + CTA column: `lg:col-span-7`. Messenger icons + GEO callout: `lg:col-span-5`. Both centered vertically.

- **Mobile Stacking:**
  Single column, centered text. Phone numbers stack vertically. Messenger icons row with `flex gap-4 justify-center`. Full-width tap targets.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <!-- Subtle grain overlay -->
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- CTA Text Block -->
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          سفارش و خرید پکیج‌های قابل حمل
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_10}
        </p>
        <!-- Phone Numbers -->
        <div class="space-y-4">
          <a href="tel:02636506485" class="block text-3xl md:text-5xl font-black text-deep-navy hover:text-deep-navy/70 transition-colors" dir="ltr"
             aria-label="تماس با دفتر مرکزی کرج: ۰۲۶-۳۶۵۰۶۴۸۵">
            026-36506485
          </a>
          <a href="tel:09122641473" class="block text-2xl md:text-4xl font-bold text-deep-navy/80 hover:text-deep-navy/60 transition-colors" dir="ltr"
             aria-label="تماس با بخش فروش: ۰۹۱۲۲۶۴۱۴۷۳">
            0912-264-1473
          </a>
        </div>
      </div>
      <!-- Messenger Icons + GEO -->
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-deep-navy font-bold text-lg">دریافت کاتالوگ از طریق پیام‌رسان‌ها:</p>
        <div class="flex gap-4 flex-wrap">
          <a href="https://wa.me/989122641473" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در واتس‌اپ">
            <svg><!-- WhatsApp Icon --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در بله">
            <svg><!-- Bale Icon --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در ایتا">
            <svg><!-- Eitaa Icon --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در روبیکا">
            <svg><!-- Rubika Icon --></svg>
          </a>
        </div>
        <!-- GEO Callout -->
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
  - Phone links use `<a href="tel:...">` with explicit `aria-label` in Farsi including the formatted number.
  - `dir="ltr"` on phone numbers for correct digit rendering in RTL context.
  - Each messenger icon has a unique `aria-label` identifying the platform.
  - Touch targets are `w-16 h-16` (64px) — exceeding 48px minimum.
  - `<footer>` or `<section>` used per dossier directive; `<section>` chosen here for CTA semantics while the page-level `<footer>` remains available for site-wide footer.
  - Rubika messenger icon added per dossier text mentioning it alongside Bale, Eitaa, and WhatsApp.

---

[VERIFIED_UI_END_OF_FILE]
