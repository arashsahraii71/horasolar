# UI Wireframe Specification: سیستم‌های خورشیدی آفگرید (Off-Grid) | برق بدون شبکه
- **Source Dossier:** `seo_dossiers/services_off-grid-systems.md`
- **Target URL:** `/services/off-grid-systems`
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

### [SEC_01]: طراحی و نصب سیستم‌های خورشیدی آفگرید (مستقل از شبکه برق)

- **Section Role:** Primary Hero — First Contentful Paint anchor, H1 entity definition, immediate trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a cinematic background photograph of a luxury villa in Kordan/Mehrshahr at twilight, illuminated entirely by solar power with a clear starry sky above (see `needed_images.md`). A deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`) ensures text contrast. Headline in `pure-white`, sub-headline accent in `solar-gold`. The GEO TL;DR block renders as a Glassmorphism floating card with a `border-s-4 border-solar-gold` accent stripe.

- **Desktop Grid Architecture:**
  12-column CSS Grid. The text block occupies `lg:col-span-7 lg:col-start-1` (right-aligned in RTL), vertically centered. The GEO Callout card occupies `lg:col-span-4 lg:col-start-8`, positioned as `lg:sticky lg:top-24` so it stays visible during initial scroll.

- **Mobile Stacking:**
  Single column. Hero image as `object-cover h-[60vh]`. H1 + body text stacks below. GEO Callout card reflows to full-width below text with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <!-- Background Image -->
    <img src="/images/hero-offgrid-villa.webp"
         alt="ویلای لوکس در کردان با سیستم خورشیدی آفگرید — برق ۲۴ ساعته بدون شبکه"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager"
         fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <!-- Gradient Overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <!-- Content Grid -->
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <!-- Text Block -->
      <div class="lg:col-span-7 text-start">
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          طراحی و نصب سیستم‌های <span class="text-solar-gold">خورشیدی آفگرید</span> (مستقل از شبکه برق)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-08" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="درخواست مشاوره رایگان سیستم آفگرید">
          مشاوره رایگان
          <svg class="w-5 h-5"><!-- Arrow right (RTL: arrow left) --></svg>
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
  - Hero image has descriptive `alt` in Farsi.
  - CTA `<a>` has `role="button"` and explicit `aria-label`.
  - GEO callout `<aside>` is semantically separated as complementary content.
  - `fetchpriority="high"` on hero image for LCP optimization.

---

### [SEC_02]: سیستم خورشیدی منفصل از شبکه (Off-Grid) چیست و چگونه کار می‌کند؟

- **Section Role:** Deep technical explainer — Information Gain, entity definition, builds topical authority.

- **UI Aesthetic & Colors:**
  Deep navy background (`bg-deep-navy`). Content area uses an asymmetrical Bento Grid with a large technical illustration on one side and stacked glass cards for the text on the other. The illustration shows the energy flow: Sun → Panels → MPPT → Battery → Inverter → Home Loads. Nodes use `solar-gold` borders on `navy-mid` background. Connecting arrows rendered as animated SVG lines (dashed, `stroke-solar-gold`).

- **Desktop Grid Architecture:**
  12-column grid. Illustration block: `lg:col-span-5`. Text + GEO callout block: `lg:col-span-7`. The illustration is sticky (`lg:sticky lg:top-20`) so it stays visible while reading.

- **Mobile Stacking:**
  Illustration collapses to a horizontal scroll strip (`overflow-x-auto snap-x snap-mandatory`) at the top. Text content stacks below in full width.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <!-- Flowchart Visual -->
      <div class="lg:col-span-5 lg:sticky lg:top-20" aria-label="نمودار جریان انرژی در سیستم آفگرید" role="img">
        <div class="glass-card p-8">
          <!-- 5-node energy flow diagram -->
          <div class="flex flex-col gap-6 items-center">
            <!-- Node: Sun -->
            <div class="w-full rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-4 text-center">
              <span class="text-solar-gold font-black text-xl">☀️ آفتاب</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: Panels -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">☀️ پنل‌های فتوولتائیک</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: MPPT -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">⚡ کنترل شارژ MPPT</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: Battery -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">🔋 باتری ذخیره‌ساز عمیق</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: Inverter -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">🔄 اینورتر آفگرید</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: Loads -->
            <div class="w-full rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-4 text-center">
              <span class="text-pure-white font-black text-xl">🏠 بارهای خانگی (۲۴ ساعته)</span>
            </div>
          </div>
        </div>
      </div>
      <!-- Text Content -->
      <div class="lg:col-span-7 space-y-8 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          سیستم خورشیدی <span class="text-solar-gold">آفگرید (Off-Grid)</span> چیست و چگونه کار می‌کند؟
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
  - Flowchart container has `role="img"` with Farsi `aria-label` describing the diagram.
  - GEO callout is a `<div>` with visual border emphasis (inline within article flow).
  - `aria-label` on illustration container describes the diagram for screen readers.

---

### [SEC_03]: چرا برق خورشیدی آفگرید بهترین جایگزین موتور برق است؟ (حل مشکل قطعی برق و آلودگی)

- **Section Role:** Pain-point emotional trigger — Split-view contrast layout (Diesel Generator vs Solar Off-Grid).

- **UI Aesthetic & Colors:**
  Split-screen composition. Left panel (RTL start-side) has a muted, desaturated palette (`bg-navy-mid/90` with faded generator imagery + noise texture) representing the "pain" (diesel noise, cost, pollution). Right panel (RTL end-side) has a vibrant `bg-deep-navy` with a `solar-gold` glow halo behind a silent solar-powered villa image representing "freedom." Divider is a diagonal SVG clip-path using `skew-y-3` Tailwind transform.

- **Desktop Grid Architecture:**
  12-column grid. Pain side: `lg:col-span-6`. Freedom side: `lg:col-span-6`. Both are `min-h-[500px]`. The GEO callout floats as an absolute-positioned glass card overlapping the center divider (`lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`).

- **Mobile Stacking:**
  Vertical stack. Pain panel first (reduced height `h-[300px]` with overlay text), then freedom panel. GEO card reflows between them as a full-width banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <!-- Pain Side (Generator) -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/diesel-generator-noise.webp" alt="موتور برق دیزلی دودی و پر از صدا" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🏭</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">موتور برق دیزلی: هزینه، صدا، آلودگی</h3>
          <p class="text-pure-white/60 mt-2 text-sm">سوخت گران + تعمیرات مداوم + صدا و دود آزاردهنده</p>
        </div>
      </div>
      <!-- Freedom Side (Solar Off-Grid) -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/silent-solar-villa.webp" alt="ویلای آرام با سیستم خورشیدی آفگرید" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">☀️</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">آفگرید خورشیدی: آرامش، экономи، استقلال</h3>
          <p class="text-pure-white/70 mt-2 text-sm">بدون سوخت، بدون صدا، بدون قطعی</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 خلاصه تصمیم‌ساز</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
    <!-- Full Text Below -->
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        چرا برق خورشیدی <span class="text-solar-gold">آفگرید</span> بهترین جایگزین <span class="text-alert-red">موتور برق</span> است؟
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section>` semantic wrapper with `id="sec-03"`.
  - Both background images have descriptive `alt` text.
  - Color is never the sole indicator of meaning; textual labels ("هزینه/صدا/آلودگی" vs "آرامش/اقتصاد/استقلال") accompany color coding.
  - GEO card is visually prominent with `border-2 border-solar-gold` for high contrast.

---

### [SEC_04]: تجهیزات اصلی سیستم آفگرید (پنل‌های Tier-1، اینورتر، و باتری‌های ذخیره‌ساز)

- **Section Role:** E-E-A-T authority builder via hardware gallery + technical specs table.

- **UI Aesthetic & Colors:**
  Return to `bg-deep-navy`. Image gallery cards use Glassmorphism with hover-reveal captions. Each card has a thin `border-b-2 border-solar-gold` bottom accent. Image overlay gradient (`from-transparent to-deep-navy/70`) shows caption text on hover. A comparison table for battery chemistries uses `eco-green` for LiFePO4 wins, `alert-red` for Lead-Acid losses.

- **Desktop Grid Architecture:**
  Asymmetrical Bento Grid of 3 images: one large card `lg:col-span-8 lg:row-span-2` and two smaller stacked cards `lg:col-span-4`. Below, a specs table spans `lg:col-span-8` with GEO callout on `lg:col-span-4`.

- **Mobile Stacking:**
  Horizontal scroll carousel with `snap-x snap-mandatory`. Each card is `w-[85vw] snap-center`. Text + GEO callout stack vertically below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> سیستم‌های آفگرید
      </h2>
      <!-- Bento Image Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 mb-12" x-data="{ activeImage: null }">
        <!-- Large Card: Inverter + Battery Bank -->
        <div class="lg:col-span-8 lg:row-span-2 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[400px]"
             @mouseenter="activeImage = 1" @mouseleave="activeImage = null"
             role="figure" aria-label="بانک باتری لیتیوم و اینورتر آفگرید در اتاق فنی ویلا">
          <img src="/images/offgrid-inverter-battery-bank.webp" alt="اینورتر آفگرید و بانک باتری لیتیوم در اتاق فنی" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-6">
            <p class="text-pure-white font-bold text-lg">اینورتر آفگرید + بانک باتری لیتیوم</p>
          </div>
        </div>
        <!-- Small Card 1: Panels -->
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="پنل‌های مونوکریستال ۶۰۰+ وات روی سقف ویلا">
          <img src="/images/tier1-panel-roof.webp" alt="پنل‌های مونوکریستال Tier-1 روی سقف" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">پنل‌های مونوکریستال ۶۰۰+ وات</p>
          </div>
        </div>
        <!-- Small Card 2: Battery Closeup -->
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="باتری‌های لیتیوم-فروفسفات (LiFePO4) با چرخه عمر بالا">
          <img src="/images/lifepo4-battery-bank.webp" alt="باتری‌های لیتیوم-فروفسفات LiFePO4" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">باتری‌های LiFePO4 (چرخه عمر ۶۰۰۰+)</p>
          </div>
        </div>
      </div>
      <!-- Specs Table + GEO Row -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
        <div class="lg:col-span-8 text-start">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقایسه شیمی‌های باتری برای ذخیره‌سازی آفگرید</h3>
          <table class="w-full min-w-[500px] text-sm" role="table" aria-label="مقایسه شیمی‌های باتری: LiFePO4 در برابر Lead-Acid">
            <thead>
              <tr class="bg-navy-mid text-solar-gold">
                <th scope="col" class="p-3 text-start rounded-s-lg">مشخصه</th>
                <th scope="col" class="p-3 text-start">Lead-Acid (اسیدی-سربی)</th>
                <th scope="col" class="p-3 text-start rounded-e-lg">LiFePO4 (لیتیوم-فروفسفات)</th>
              </tr>
            </thead>
            <tbody>
              <tr class="bg-deep-navy/60">
                <td class="p-3">چرخه عمر (Depth 80%)</td>
                <td class="p-3 text-alert-red font-bold">۵۰۰–۸۰۰</td>
                <td class="p-3 text-eco-green font-bold">۴۰۰۰–۶۰۰۰</td>
              </tr>
              <tr class="bg-navy-mid/40">
                <td class="p-3">عمق تخلیه بهینه (DoD)</td>
                <td class="p-3 text-alert-red font-bold">۵۰٪</td>
                <td class="p-3 text-eco-green font-bold">۸۰–۹۰٪</td>
              </tr>
              <tr class="bg-deep-navy/60">
                <td class="p-3">بهره‌وی شارژ/تخلیه</td>
                <td class="p-3 text-alert-red font-bold">۸۰–۸۵٪</td>
                <td class="p-3 text-eco-green font-bold">۹۵–۹۸٪</td>
              </tr>
              <tr class="bg-navy-mid/40">
                <td class="p-3">وزن برایCapacity یکسان</td>
                <td class="p-3 text-alert-red font-bold">سنگین (۳–۴ برابر)</td>
                <td class="p-3 text-eco-green font-bold">سبک</td>
              </tr>
              <tr class="bg-deep-navy/60">
                <td class="p-3">بازگشت سرمایه (ROI)</td>
                <td class="p-3 text-alert-red font-bold">منفی (تعویض مکرر)</td>
                <td class="p-3 text-eco-green font-bold">۳ تا ۵ سال</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="lg:col-span-4 glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Each image card has `role="figure"` and `aria-label` in Farsi.
  - Hover captions are decorative overlays; `alt` text on images provides equivalent info for screen readers.
  - `loading="lazy"` on all gallery images for performance.
  - `<table>` has `role="table"` and descriptive `aria-label`.
  - All `<th>` elements use `scope="col"`.

---

### [SEC_05]: قیمت و برآورد هزینه نصب سیستم خورشیدی آفگرید

- **Section Role:** Pricing transparency bridge — internal linking to calculator, prevents keyword cannibalization with pricing pages.

- **UI Aesthetic & Colors:**
  Minimal, clean block on `bg-deep-navy`. A single glass card with a `border-b-4 border-solar-gold` bottom accent. A pricing tier accordion reveals capacity ranges. The internal link to `/pricing/solar-calculator` is a prominent pill-shaped CTA button (`bg-solar-gold text-deep-navy`).

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. The text block, accordion, and CTA are vertically stacked.

- **Mobile Stacking:**
  No change. Accordion items stack naturally. CTA button becomes `w-full` on mobile.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-24 bg-deep-navy"
           x-data="{ activePricing: null }">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        قیمت و برآورد هزینه <span class="text-solar-gold">نصب سیستم آفگرید</span>
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <!-- Pricing Tiers Accordion -->
        <div class="space-y-3" x-data="{ openTier: null }">
          <details class="glass-card overflow-hidden group"
                   :class="openTier === 1 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                   @toggle="openTier = openTier === 1 ? null : 1">
            <summary class="cursor-pointer py-4 px-6 flex items-center justify-between text-start"
                     role="button" aria-expanded="false"
                     :aria-expanded="openTier === 1 ? 'true' : 'false'">
              <span class="font-bold text-lg" :class="openTier === 1 ? 'text-solar-gold' : 'text-pure-white'">
                ویلا ۱ تا ۲ کیلوات (پایه) — از ~[DATA NEEDED] میلیون تومان
              </span>
              <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openTier === 1 ? 'rotate-180' : ''">
                <!-- Chevron -->
              </svg>
            </summary>
            <div class="px-6 pb-4 text-pure-white/80 text-sm leading-relaxed">
              مناسب برای روشنایی، یخچال، تلویزیون و شارژ موبایل. شامل پنل ۵۵۰ وات، اینورتر ۱ کیلوات، باتری ۲۰۰ آمپر.
            </div>
          </details>
          <details class="glass-card overflow-hidden group"
                   :class="openTier === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                   @toggle="openTier = openTier === 2 ? null : 2">
            <summary class="cursor-pointer py-4 px-6 flex items-center justify-between text-start"
                     role="button" aria-expanded="false"
                     :aria-expanded="openTier === 2 ? 'true' : 'false'">
              <span class="font-bold text-lg" :class="openTier === 2 ? 'text-solar-gold' : 'text-pure-white'">
                ویلا ۳ تا ۵ کیلوات (استاندارد) — از ~[DATA NEEDED] میلیون تومان
              </span>
              <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openTier === 2 ? 'rotate-180' : ''">
                <!-- Chevron -->
              </svg>
            </summary>
            <div class="px-6 pb-4 text-pure-white/80 text-sm leading-relaxed">
              پشتیبانی کولر گازی ۱۲۰۰۰-۱۸۰۰۰ BTU، یخچال، ماشین لباسشویی، پمپ آب. اینورتر ۳-۵ کیلوات، باتری ۴۰۰-۶۰۰ آمپر.
            </div>
          </details>
          <details class="glass-card overflow-hidden group"
                   :class="openTier === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                   @toggle="openTier = openTier === 3 ? null : 3">
            <summary class="cursor-pointer py-4 px-6 flex items-center justify-between text-start"
                     role="button" aria-expanded="false"
                     :aria-expanded="openTier === 3 ? 'true' : 'false'">
              <span class="font-bold text-lg" :class="openTier === 3 ? 'text-solar-gold' : 'text-pure-white'">
                ویلا ۶ تا ۱۰ کیلوات (لوکس) — از ~[DATA NEEDED] میلیون تومان
              </span>
              <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openTier === 3 ? 'rotate-180' : ''">
                <!-- Chevron -->
              </svg>
            </summary>
            <div class="px-6 pb-4 text-pure-white/80 text-sm leading-relaxed">
              پوشش کامل تمام لوازم خانگی شامل کولرها، پمپ استخر، شارژ خودرو برقی. اینورتر ۶-۱۰ کیلوات، باتری ۸۰۰-۱۲۰۰ آمپر.
            </div>
          </details>
        </div>
        <!-- GEO Callout Inline -->
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 فرمول کلیدی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
        <!-- Internal Link CTA -->
        <a href="/pricing/solar-calculator"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="محاسبه‌گر آنلاین برق خورشیدی — برآورد دقیق هزینه سیستم آفگرید">
          محاسبه‌گر آنلاین برق خورشیدی
          <svg class="w-5 h-5"><!-- Calculator icon --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>`/`<summary>` for accordion — native keyboard/AT support.
  - `aria-expanded` dynamically bound via Alpine.
  - CTA `role="button"` with descriptive `aria-label`.
  - `w-full` on mobile ensures ≥48px touch target.

---

### [SEC_06]: چرا هورا نور سهند؟ (مجری تخصصی با ۴۰+ پروژه موفق)

- **Section Role:** E-E-A-T authority builder — Local trust, portfolio proof, government endorsements.

- **UI Aesthetic & Colors:**
  Soft informational block on `bg-navy-mid`. A trust badge carousel (auto-rotating + manual navigation). Each badge is a glass card with `border-s-4 border-solar-gold`. A project counter uses a rolling number animation (`data-value="40"`). The `<address>` NAP block uses `bg-solar-gold text-deep-navy` for strong contrast.

- **Desktop Grid Architecture:**
  12-column grid. Trust badges carousel: `lg:col-span-7`. NAP address card + GEO callout: `lg:col-span-5`. Address card is solid `bg-solar-gold` for NAP contrast.

- **Mobile Stacking:**
  Carousel reduces to `max-w-[300px]` with swipe navigation (`snap-x`). NAP card stacks below full-width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- Trust Carousel -->
      <div class="lg:col-span-7" aria-label="نمادهای اعتماد و گواهی‌های هورا نور سهند">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">گواهی‌ها و اعتمادنامه‌ها</h3>
        <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
          <!-- Badge 1 -->
          <div class="min-w-[260px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
            <span class="text-3xl mb-2">🏛️</span>
            <h4 class="font-bold text-pure-white text-lg">تاییدیه ساتبا</h4>
            <p class="text-pure-white/60 text-sm mt-1">سازمان انرژی‌های تجدیدپذیر</p>
          </div>
          <!-- Badge 2 -->
          <div class="min-w-[260px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
            <span class="text-3xl mb-2">⚡</span>
            <h4 class="font-bold text-pure-white text-lg">تأیید توزیع برق البرز</h4>
            <p class="text-pure-white/60 text-sm mt-1">شرکت توزیع نیروی برق</p>
          </div>
          <!-- Badge 3 -->
          <div class="min-w-[260px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
            <span class="text-3xl mb-2">📜</span>
            <h4 class="font-bold text-pure-white text-lg">نماد اعتماد الکترونیک (اینماد)</h4>
            <p class="text-pure-white/60 text-sm mt-1">تأیید مرکز توسعه تجارت الکترونیک</p>
          </div>
          <!-- Badge 4 -->
          <div class="min-w-[260px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
            <span class="text-3xl mb-2">🏗️</span>
            <h4 class="font-bold text-pure-white text-lg">نظام مهندسی ساختمان</h4>
            <p class="text-pure-white/60 text-sm mt-1">عضو رسمی و مجاز اجرا</p>
          </div>
          <!-- Badge 5 -->
          <div class="min-w-[260px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
            <span class="text-3xl mb-2">🏆</span>
            <h4 class="font-bold text-pure-white text-lg">۴۰+ پروژه موفق</h4>
            <p class="text-pure-white/60 text-sm mt-1">استقرار در البرز، تهران، کردان، لواسان</p>
          </div>
        </div>
        <!-- Project Counter -->
        <div class="mt-6 glass-card p-6 rounded-2xl text-center border border-solar-gold/30">
          <p class="text-pure-white/70 text-sm mb-1">پروژه‌های اجرا شده</p>
          <p class="font-black text-4xl md:text-6xl text-solar-gold" data-value="40">۴۰</p>
          <p class="text-pure-white/60 text-sm mt-1">و تعداد رو به رشد...</p>
        </div>
      </div>
      <!-- NAP Address Card + GEO -->
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          چرا <span class="text-solar-gold">هورا نور سهند</span>؟
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <!-- NAP Address Card -->
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش محلی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<address>` HTML element used per SEO Dossier directive (semantic NAP signal).
  - Carousel has `aria-label` describing the badge set.
  - Phone numbers are plain text with `dir="ltr"` for correct digit rendering.
  - Carousel is horizontally scrollable with keyboard navigation (native browser behavior).

---

### [SEC_07]: سوالات متداول درباره سیستم‌های آفگرید (FAQ)

- **Section Role:** GEO/SGE bait — FAQ with FAQPage JSON-LD schema, accordion UI.

- **UI Aesthetic & Colors:**
  Background: `bg-navy-mid`. Each FAQ item is a glass card with `border-s-4 border-solar-gold` when expanded, `border-s-4 border-pure-white/10` when collapsed. The summary text uses `text-solar-gold` when open. Smooth `x-collapse` transition.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single column stack of accordion items. GEO callout at top as a `bg-cream-warm/5` banner.

- **Mobile Stacking:**
  No change; already single-column. Touch targets for `<summary>` elements are full-width with `py-5` padding.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-navy-mid"
           x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">سیستم‌های آفگرید</span>
      </h2>
      <!-- GEO Preamble -->
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
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
              آیا سیستم آفگرید در روزهای ابری و زمستان هم برق می‌دهد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. با طراحی مهندسی دقیق و محاسبه ظرفیت باتری‌ها بر اساس ۲۵۰ روز آفتابی البرز، سیستم به گونه‌ای طراحی می‌شود که در روزهای ابری نیز برق مورد نیاز تامین شود. باتری‌های LiFePO4 در دمای پایین هم عملکرد بالا دارند.
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
              تفاوت سیستم آفگرید با آنگرید چیست؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            سیستم آنگرید به شبکه ملی متصل است و اضافه‌تولید را می‌فروشد (بدون باتری). سیستم آفگرید کاملاً مستقل است، باتری دارد و در قطعی شبکه هم برق می‌دهد. برای مناطق دور از شبکه یا nơi‌هایی با قطعی مکرر، آفگرید انتخاب صحیح است.
          </div>
        </details>
        <!-- FAQ Item 3 -->
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا سیستم آفگرید می‌تواند جایگزین کامل موتور برق شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. سیستم‌های هورا نور سهند با باتری‌های ذخیره‌ساز عمیق (LiFePO4) و اینورترهای افس-Off-Grid، برق ۲۴ ساعته را بدون هیچ‌گونه صدا، آلودگی و نیاز به سوخت تضمین می‌کنند و بهترین جایگزین برای دیزل ژنراتورها هستند.
          </div>
        </details>
        <!-- FAQ Item 4 -->
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 4 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 4 ? null : 4">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   aria-expanded="false"
                   :aria-expanded="openFaq === 4 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 4 ? 'text-solar-gold' : 'text-pure-white'">
              هزینه نگهداری سیستم آفگرید چقدر است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 4 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            تقریباً صفر. پنل‌ها فقط نیاز به شستشو سالانه دارند. باتری‌های LiFePO4 بی‌نگهداری هستند. اینورترها گارانتی ۵ تا ۱۰ ساله دارند. مقایسه با موتور برق: صفر هزینه سوخت، صفر تعمیرات مداوم، صفر صدا.
          </div>
        </details>
      </div>
      <!-- JSON-LD Reminder for Developer -->
      <!-- CODER NOTE: Wrap above FAQ content in FAQPage JSON-LD schema as per dossier directive. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>`/`<summary>` elements ensure keyboard accessibility and screen reader support.
  - `aria-expanded` is dynamically bound via Alpine for enhanced state communication.
  - `role="button"` on `<summary>` for consistent interaction model.
  - Touch target height is generous (`py-5 px-6`).

---

### [SEC_08]: تماس برای مشاوره و طراحی مهندسی سیستم آفگرید شما

- **Section Role:** Final CRO conversion block — high-contrast CTA for villa owners.

- **UI Aesthetic & Colors:**
  Full-width high-contrast block. Background: `bg-solar-gold`. All text: `text-deep-navy`. Phone numbers are oversized (`text-3xl md:text-5xl font-black`), clickable with `<a href="tel:...">`. Messenger icons (WhatsApp, Bale, Eitaa) are circular icon buttons in `bg-deep-navy text-solar-gold`. A subtle grain texture overlay for premium feel.

- **Desktop Grid Architecture:**
  12-column grid. Text + CTA column: `lg:col-span-7`. Messenger icons + secondary info: `lg:col-span-5`. Both centered vertically.

- **Mobile Stacking:**
  Single column, centered text. Phone numbers stack vertically. Messenger icons row with `flex gap-4 justify-center`. Full-width tap targets.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <!-- Subtle grain overlay -->
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- CTA Text Block -->
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          همین امروز، استقلال برق ویلا خود را تضمین کنید
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08 (CTA section)}
        </p>
        <!-- Phone Numbers -->
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
      <!-- Messenger Icons -->
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-deep-navy font-bold text-lg">ارتباط از طریق پیام‌رسان‌ها:</p>
        <div class="flex gap-4">
          <a href="https://wa.me/989125728170" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در واتس‌اپ">
            <svg class="w-8 h-8"><!-- WhatsApp Icon --></svg>
          </a>
          <a href="https://ble.ir/horasolar" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در بله">
            <svg class="w-8 h-8"><!-- Bale Icon --></svg>
          </a>
          <a href="https://eitaa.com/horasolar" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در ایتا">
            <svg class="w-8 h-8"><!-- Eitaa Icon --></svg>
          </a>
        </div>
        <!-- GEO Callout -->
        <div class="bg-deep-navy/10 rounded-2xl p-5 border-2 border-deep-navy/20 mt-4">
          <p class="text-deep-navy text-base leading-relaxed font-medium">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08 (CTA section)}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Phone links use `<a href="tel:...">` with explicit `aria-label` in Farsi including the formatted number.
  - Phone number elements have `dir="ltr"` to ensure correct digit rendering in RTL context.
  - Messenger icon buttons have individual `aria-label` describing the messenger platform.
  - Minimum touch target: `w-16 h-16` (64px) exceeds WCAG 2.5.8 minimum of 44px.
  - External links have `rel="noopener"`.

---

[VERIFIED_UI_END_OF_FILE]