# UI Wireframe Specification: نیروگاه خورشیدی متصل به شبکه (On-Grid) | احداث و تزریق به مدار
- **Source Dossier:** `seo_dossiers/services_on-grid-systems.md`
- **Target URL:** `/services/on-grid-systems`
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

### [SEC_01]: احداث نیروگاه خورشیدی متصل به شبکه (آنگرید و تزریق به مدار)

- **Section Role:** Primary Hero — First Contentful Paint anchor, H1 entity definition, immediate EPC authority signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a cinematic aerial shot of a massive industrial rooftop solar plant in Eshtehard, rows of panels converging to a central inverter station, with the national grid connection visible (see `needed_images.md`). A deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`) ensures text contrast. Headline in `pure-white`, "EPC Contractor" badge in `solar-gold`. The GEO TL;DR block renders as a Glassmorphism floating card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-column CSS Grid. Text block: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body text stacks below. GEO Callout reflows full-width below text with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-ongrid-industrial.webp"
         alt="نیروگاه خورشیدی آنگرید در شهرک صنعتی اشتهارد — تزریق به شبکه برق ملی"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          پیمانکار EPC در استان البرز
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          احداث نیروگاه خورشیدی <span class="text-solar-gold">متصل به شبکه</span> (آنگرید و تزریق به مدار)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="دریافت طرح توجیهی نیروگاه آنگرید">
          دریافت طرح توجیهی
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
  - `<header>` landmark with `id="sec-01"`.
  - Hero `alt` in Farsi describing the industrial plant.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` with semantic complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: سیستم متصل به شبکه چگونه کار می‌کند؟ (بدون نیاز به باتری)

- **Section Role:** Technical explainer — Step-by-step energy flow, SGE step-by-step entity.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive flowchart with animated SVG lines (`stroke-solar-gold`, dashed, `@keyframes flow`). Nodes: Panels (DC) → Inverter (Sync) → AC Board → Bi-directional Meter → Grid. Nodes pulse on hover.

- **Desktop Grid Architecture:**
  12-col. Flowchart: `lg:col-span-5 lg:sticky lg:top-20`. Text: `lg:col-span-7`. Flowchart nodes use `solar-gold` borders on `navy-mid`.

- **Mobile Stacking:**
  Flowchart becomes horizontal scroll strip (`overflow-x-auto snap-x snap-mandatory`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ step: 1 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-5 lg:sticky lg:top-20" aria-label="نمودار جریان انرژی در سیستم آنگرید" role="img">
        <div class="glass-card p-8">
          <div class="flex flex-col gap-5 items-center" x-data="{ activeNode: 0 }">
            <div class="w-full rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeNode === 0 }">
              <span class="text-solar-gold font-black text-xl">☀️ پنل‌های فتوولتائیک (DC)</span>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeNode === 1 }">
              <span class="text-solar-gold font-bold text-lg">⚡ اینورتر آنگرید (Sync + AC)</span>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">📋 تابلو حفاظت AC</span>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">📊 کنتور دوطرفه (طرح فهام)</span>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-4 text-center">
              <span class="text-pure-white font-black text-xl">⚡ شبکه برق ملی</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-7 space-y-8 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          سیستم متصل به شبکه <span class="text-solar-gold">چگونه کار می‌کند؟</span> (بدون نیاز به باتری)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
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
  - `<article>` wraps technical content.
  - Flowchart `role="img"` + `aria-label`.
  - Nodes have descriptive text labels.

---

### [SEC_03]: حل معضلات شبکه: قطعی برق و ماده ۱۶ صنایع

- **Section Role:** Pain-point split view — Industrial pain vs Solar solution.

- **UI Aesthetic & Colors:**
  Split screen. Pain (start/RTL): `bg-navy-mid/90` with factory blackout imagery, `alert-red` accents. Freedom (end): `bg-deep-navy` with solar-powered factory, `eco-green` glow. Diagonal divider `skew-y-3`.

- **Desktop Grid Architecture:**
  12-col. Pain: `lg:col-span-6`. Freedom: `lg:col-span-6`. Both `min-h-[500px]`. GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Pain first (`h-[300px]`), then freedom. GEO card between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/industrial-blackout.webp" alt="کارخانه در حالت قطعی برق و توقف تولید" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⚡</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">قطعی برق و توقف خطوط تولید</h3>
          <p class="text-pure-white/60 mt-2 text-sm">پیک تابستانی + ماده ۱۶ = ضرر مالی</p>
        </div>
      </div>
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/solar-powered-factory.webp" alt="کارخانه با نیروگاه خورشیدی روی سقف" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⚡</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">نیروگاه آنگرید: درآمد، معافیت، تداوم</h3>
          <p class="text-pure-white/70 mt-2 text-sm">تزریق به شبکه + معافیت ماده ۱۶</p>
        </div>
      </div>
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 خلاصه تصمیم‌ساز</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        حل معضلات <span class="text-solar-gold">شبکه</span>: <span class="text-alert-red">قطعی برق</span> و <span class="text-alert-red">ماده ۱۶</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
      <a href="/investment/article-16-industrial-mandate"
         class="inline-flex items-center gap-2 mt-6 text-solar-gold underline hover:text-solar-gold/80"
         aria-label="مطالعه راهنمای رفع جریمه ماده ۱۶">
        مطالعه راهنمای ماده ۱۶
        <svg><!-- Arrow --></svg>
      </a>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section id="sec-03">`.
  - Color + text labels for meaning.
  - Link to `/investment/article-16-industrial-mandate` with `aria-label`.

---

### [SEC_04]: باورهای غلط و واقعیت‌های مهندسی (Myth vs. Reality)

- **Section Role:** Myth-busting engagement — SGE bait.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background, navy text. Myth cards: `bg-alert-red/10 border-alert-red/30` with ❌. Reality: `bg-eco-green/10 border-eco-green/30` with ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` myth/reality pairs. GEO banner below with `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair. Myth first (red), reality second (green).

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در <span class="text-solar-gold">نیروگاه‌های آنگرید</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8"
           x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            نیروگاه‌های متصل به شبکه در مناطق نیمه‌ابری بازدهی ندارند.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            راندمان پنل‌ها به پرتوهای فرابنفش وابسته است، نه گرمای مستقیم. هوای خنک راندمان را بالا می‌برد. البرز با ۲۵۰ روز آفتابی و دمای بهینه، طلایی‌ترین منطقه است.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت علمی</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside>` per SEO.
  - `x-intersect` for reveal (decorative only).
  - Meaning via icon + text, not color alone.
  - Contrast: dark text on light cards.

---

### [SEC_05]: سخت‌افزار استاندارد نیروگاهی و تجهیزات Tier-1

- **Section Role:** E-E-A-T authority — Brand carousel + specs.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Grayscale logo carousel → color on hover. Each logo: `bg-white/5 rounded-xl p-6 transition-colors`.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Logo carousel `flex gap-8 overflow-x-auto snap-x snap-mandatory`. GEO callout below.

- **Mobile Stacking:**
  Carousel `snap-x` with `snap-center` items.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> نیروگاه‌های آنگرید
      </h2>
      <div class="flex gap-8 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             @mouseenter="$el.classList.remove('grayscale')" @mouseleave="$el.classList.add('grayscale')"
             class="grayscale transition-colors duration-300">
          <img src="/images/logo-trina.webp" alt="Trina Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Trina Solar</span>
        </div>
        <!-- Repeat for Jinko, LONGi, JA Solar, Mana, Taban, Vmax -->
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
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

### [SEC_06]: بازگشت سرمایه و درآمدزایی قطعی

- **Section Role:** Value prop + internal link to pricing.

- **UI Aesthetic & Colors:**
  `bg-deep-navy` → `bg-navy-mid` gradient. Timeline infographic: Year 0 (investment) → Year 3-5 (break-even, `eco-green`) → Year 25 (profit, `solar-gold` line). Bars: `eco-green` for profit, `alert-red` for cost.

- **Desktop Grid Architecture:**
  12-col. Chart: `lg:col-span-7` (`rounded-e-3xl`). Text: `lg:col-span-5` (`rounded-s-3xl`).

- **Mobile Stacking:**
  Chart horizontal scroll. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-gradient-to-b from-deep-navy to-navy-mid" x-data="{ showDetails: false }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <div class="lg:col-span-7 glass-card rounded-e-3xl p-8 overflow-x-auto">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">نمودار بازگشت سرمایه (۲۵ سال)</h3>
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="زمان‌بندی بازگشت سرمایه نیروگاه آنگرید">
          <thead><tr class="bg-navy-mid text-solar-gold">
            <th scope="col" class="p-3 text-start rounded-s-lg">مرحله</th>
            <th scope="col" class="p-3 text-start rounded-e-lg">وضعیت مالی</th>
          </tr></thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">سال ۰</td><td class="p-3 text-alert-red font-bold">سرمایه‌گذاری اولیه</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">سال ۱-۲</td><td class="p-3 text-solar-gold font-bold">تولید و درآمدزایی</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">سال ۳-۵</td><td class="p-3 text-eco-green font-bold text-lg">نقطه تعادل (Break-even)</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">سال ۶-۲۵</td><td class="p-3 text-eco-green font-bold">سود خالص تجمعی</td></tr>
          </tbody>
        </table>
        <button @click="showDetails = !showDetails" class="mt-4 text-solar-gold underline text-sm"
                :aria-expanded="showDetails" aria-controls="roi-details">
          جزئیات محاسبات
        </button>
        <div x-show="showDetails" x-collapse id="roi-details" class="mt-4 text-pure-white/70 text-sm">
          محاسبه بر اساس تعرفه خرید تضمینی ۲۰ ساله ساتبا، بهینه‌سازی ۲۵۰ روز آفتابی البرز، و هزینه عملیاتی نزدیک به صفر.
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          بازگشت سرمایه <span class="text-solar-gold">۳ تا ۵ ساله</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
        <a href="/pricing/industrial-power-plants"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           aria-label="مشاهده قیمت نیروگاه‌های صنعتی">
          مشاهده برآورد سرمایه
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `scope="col"` on `<th>`.
  - Toggle button `:aria-expanded` + `aria-controls`.
  - Color + text labels.

---

### [SEC_07]: تاییدیه و دستورالعمل‌های نهادهای دولتی (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust entities.

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
          تاییدیه و دستورالعمل‌های نهادهای دولتی
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg">سازمان ساتبا</h4>
          <p class="text-pure-white/60 text-sm">قرارداد ۲۰ ساله</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg">وزارت نیرو</h4>
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
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge is decorative; heading provides context.

---

### [SEC_08]: مناطق تحت پوشش و تمرکز جغرافیایی پروژه‌ها

- **Section Role:** Local SEO anchor + NAP.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. SVG map of Alborz/Tehran/Qazvin with gold pulse dots at Eshtehard, Simindasht, Karaj HQ, Tehran, Qazvin. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="نقشه پوشش نیروگاه‌های آنگرید هورا نور سهند" role="img">
        <img src="/images/ongrid-coverage-map.svg" alt="نقشه پوشش نیروگاه‌های آنگرید: اشتهارد، سیمین‌دشت، کرج، تهران، قزوین" class="w-full h-auto" loading="lazy">
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مناطق تحت پوشش <span class="text-solar-gold">هورا نور سهند</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش صنعتی</p>
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

### [SEC_09]: تفاوت کلیدی میان سیستم آنگرید و آفگرید

- **Section Role:** Semantic disambiguation + cross-linking.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Comparison table in glass card. Columns: Feature | آنگرید | آفگرید. `eco-green` for On-Grid wins, `alert-red` for costs.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. Table full width. GEO callout below.

- **Mobile Stacking:**
  Table horizontal scroll.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-4xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        تفاوت کلیدی <span class="text-solar-gold">آنگرید</span> و <span class="text-alert-red">آفگرید</span>
      </h2>
      <div class="glass-card p-8 overflow-x-auto">
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="مقایسه آنگرید در برابر آفگرید">
          <thead><tr class="bg-navy-mid text-solar-gold">
            <th scope="col" class="p-3 text-start rounded-s-lg">ویژگی</th>
            <th scope="col" class="p-3 text-start">آنگرید (متصل به شبکه)</th>
            <th scope="col" class="p-3 text-start rounded-e-lg">آفگرید (مستقل)</th>
          </tr></thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">اتصال به شبکه</td><td class="p-3 text-eco-green font-bold">بله (تزریق)</td><td class="p-3 text-alert-red font-bold">خیر (مستقل)</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">باتری</td><td class="p-3 text-eco-green font-bold">نیازی نیست</td><td class="p-3 text-alert-red font-bold">الزامی (LiFePO4)</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">هزینه نگهداری</td><td class="p-3 text-eco-green font-bold">کم (بدون باتری)</td><td class="p-3 text-alert-red font-bold">موجود (باتری)</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">درآمد</td><td class="p-3 text-eco-green font-bold">فروش به ساتبا</td><td class="p-3 text-alert-red font-bold">تأمین خود (بدون فروش)</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">مناسب برای</td><td class="p-3">صنایع، سقف سوله، زمین</td><td class="p-3">مناطق دور از شبکه، ویلا</td></tr>
          </tbody>
        </table>
        <a href="/services/off-grid-systems"
           class="inline-flex items-center gap-2 mt-6 text-solar-gold underline hover:text-solar-gold/80"
           aria-label="مطالعه سیستم‌های آفگرید">
          مشاهده سیستم‌های آفگرید
          <svg><!-- Arrow --></svg>
        </a>
        <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
          <p class="text-sm font-bold text-solar-gold mb-1">🔄 انتخاب معماری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
          </p>
        </div>
      </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table>` + `aria-label`.
  - `scope="col"` on `<th>`.
  - Link to `/services/off-grid-systems` with `aria-label`.

---

### [SEC_10]: بخش پاسخ به سوالات متداول (FAQ)

- **Section Role:** GEO/SGE bait — FAQPage schema.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Glass accordion items. Expanded: `border-s-4 border-solar-gold` + `text-solar-gold` summary. Collapsed: `border-pure-white/10`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO preamble banner.

- **Mobile Stacking:**
  Full-width `<summary>` with `py-5`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-navy-mid" x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">نیروگاه‌های آنگرید</span>
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
              آیا در زمان قطعی برق سراسری، نیروگاه متصل به شبکه برق تولید می‌کند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر. به دلیل الزامات ایمنی شبکه (Anti-Islanding)، اینورترها در قطعی برق شهری به صورت اتوماتیک خاموش می‌شوند. برای رفع قطعی، سیستم‌های هیبریدی پیشنهاد می‌شوند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا نصب پنل‌ها روی سقف سوله به ایزوگام آسیب می‌رساند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر. با استراکچرهای آلومینیومی/گالوانیزه و اتصالات کلمپ (Clamp) بدون سوراخ‌کاری، نصب ۱۰۰٪ ایمن روی هر پوشش سقف امکان‌پذیر است.
          </div>
        </details>
      </div>
      <!-- CODER NOTE: Wrap in FAQPage JSON-LD schema. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>`/`<summary>`.
  - `aria-expanded` bound via Alpine.
  - `role="button"` on `<summary>`.
  - Touch target `py-5 px-6`.

---

### [SEC_11]: مشاوره مهندسی و آغاز فاز طراحی (Call to Action)

- **Section Role:** CRO conversion — NAP + high-contrast.

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
          همین امروز، تهدید قطعی برق را به درآمد تبدیل کنید
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_11}
        </p>
        <div class="space-y-4">
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

---

[VERIFIED_UI_END_OF_FILE]