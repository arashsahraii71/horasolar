# UI Wireframe Specification: پنل خورشیدی برای ماینر | برق استخراج رمزارز
- **Source Dossier:** `seo_dossiers/applications_crypto-mining-solar.md`
- **Target URL:** `/applications/crypto-mining-solar`
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
| `--color-accent-3`   | `#2ECC71` | `eco-green`           | Success indicators, active hash rate      |
| `--color-danger`     | `#E74C3C` | `alert-red`           | Danger states, offline miners, diesel     |
| `--color-cyber`      | `#00E5FF` | `cyber-cyan`          | Crypto/tech accent, data overlays         |
| `--color-glass-bg`   | `rgba(255,255,255,0.06)` | — | Glassmorphism fill (darker variant for crypto page) |
| `--color-glass-border` | `rgba(255,255,255,0.12)` | — | Glassmorphism stroke                    |

### Base Typography & Body Classes
```html
<body class="bg-deep-navy text-pure-white font-vazirmatn antialiased" dir="rtl" lang="fa">
```
- **Display / H1:** `font-vazirmatn font-black text-4xl md:text-6xl leading-tight tracking-tight`
- **H2:** `font-vazirmatn font-extrabold text-2xl md:text-4xl`
- **H3:** `font-vazirmatn font-bold text-xl md:text-2xl`
- **Body:** `font-vazirmatn font-normal text-base md:text-lg leading-relaxed`
- **Caption / Small:** `font-vazirmatn text-sm text-pure-white/70`
- **Mono/Tech:** `font-mono text-sm text-cyber-cyan` (for hash rates, kW values, tech specs)

### Glassmorphism Utility Class (Crypto Dark Variant)
```css
.glass-card {
  background: var(--color-glass-bg);
  backdrop-filter: blur(20px) saturate(160%);
  -webkit-backdrop-filter: blur(20px) saturate(160%);
  border: 1px solid var(--color-glass-border);
  border-radius: 1.5rem;
}
```

### RTL Enforcement Rule
> **CRITICAL:** All layout utilities MUST use Tailwind logical properties: `ms-`, `me-`, `ps-`, `pe-`, `border-s-`, `border-e-`, `rounded-s-`, `rounded-e-`, `text-start`, `text-end`, `start-0`, `end-0`. **NEVER** use `ml-`, `mr-`, `pl-`, `pr-`, `left-`, `right-`, `text-left`, `text-right`.

### Page-Level Visual Theme Note
> This page targets crypto/blockchain investors. The aesthetic leans **darker, more futuristic** than the agricultural pages — think cyber-noir with subtle scan-line overlays, matrix-green data accents (`cyber-cyan`), and a more aggressive glassmorphism. Still anchored by brand `solar-gold` for CTAs and GEO blocks.

---

### [SEC_01]: احداث نیروگاه خورشیدی اختصاصی برای استخراج رمزارز (ماینر)

- **Section Role:** Primary Hero — H1 entity anchor, first-impression for crypto investors.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a dual-exposure background: a high-tech mining farm interior (rows of ASIC miners with green LED blinking) cross-fading into an expansive solar array on a rooftop. Background uses a cinematic overlay: `bg-gradient-to-b from-deep-navy/90 via-deep-navy/60 to-deep-navy`. Subtle animated CSS scan-lines effect (`background-image: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,229,255,0.03) 2px, rgba(0,229,255,0.03) 4px)`) for a cyber aesthetic. Headline in `pure-white` with a `text-solar-gold` keyword highlight. The GEO TL;DR floats as a Glassmorphism card with `border-s-4 border-cyber-cyan`.

- **Desktop Grid Architecture:**
  12-column CSS Grid. Text block: `lg:col-span-7 lg:col-start-1`. GEO callout card: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`. A faint animated hashrate counter (`font-mono text-cyber-cyan/40 text-8xl`) in the background as a decorative element.

- **Mobile Stacking:**
  Single column. Hero image as `object-cover h-[65vh]` with overlay. H1 + body text below. GEO card full-width with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <!-- Background Image -->
    <img src="/images/hero-crypto-mining-solar.webp"
         alt="نیروگاه خورشیدی اختصاصی فارم استخراج رمزارز"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager"
         fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <!-- Gradient + Scan-line Overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/90 via-deep-navy/60 to-deep-navy"></div>
    <div class="absolute inset-0 pointer-events-none" style="background-image: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,229,255,0.03) 2px, rgba(0,229,255,0.03) 4px);"></div>
    <!-- Content Grid -->
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <!-- Text Block -->
      <div class="lg:col-span-7 text-start">
        <div class="inline-block bg-cyber-cyan/10 border border-cyber-cyan/30 rounded-full px-4 py-1 mb-6">
          <span class="font-mono text-cyber-cyan text-sm">CRYPTO MINING × SOLAR ENERGY</span>
        </div>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          احداث نیروگاه خورشیدی اختصاصی برای <span class="text-solar-gold">استخراج رمزارز</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="دریافت پروپوزال مهندسی نیروگاه ماینینگ">
          دریافت پروپوزال مهندسی
          <svg><!-- Arrow icon --></svg>
        </a>
      </div>
      <!-- GEO Callout (Sticky) -->
      <aside class="lg:col-span-4 lg:col-start-9 lg:sticky lg:top-24 glass-card p-6 border-s-4 border-cyber-cyan">
        <p class="text-sm font-bold text-cyber-cyan mb-2">⛏️ خلاصه کلیدی</p>
        <p class="text-base text-pure-white/90 leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_01}
        </p>
      </aside>
    </div>
  </header>
  ```

- **Accessibility & ARIA:**
  - `<header>` landmark wraps the entire hero section.
  - Hero image has descriptive Farsi `alt` text.
  - CTA `<a>` has `role="button"` and explicit `aria-label`.
  - Scan-line overlay is `pointer-events-none` and purely decorative.
  - `fetchpriority="high"` on hero image for LCP optimization.
  - Tech badge text is decorative enhancement; key information is in the H1.

---

### [SEC_02]: چالش توان پیوسته و مدیریت حرارتی در مزارع ماینینگ

- **Section Role:** Technical depth — specification chart mapping miners to required solar capacity.

- **UI Aesthetic & Colors:**
  Dark background (`bg-deep-navy`) with a data-visualization-forward design. The spec chart uses a Data-Viz table with `cyber-cyan` header row accents and `solar-gold` highlight on key values. Row hover state uses `bg-cyber-cyan/5`. Column headers use `font-mono` for a terminal/dashboard feel. GEO callout rendered as a sidebar glass card.

- **Desktop Grid Architecture:**
  12-column grid. Spec chart/table: `lg:col-span-8`. Text + GEO callout: `lg:col-span-4`. The table has an asymmetrical Bento appearance with `rounded-s-3xl` (start-side rounded in RTL).

- **Mobile Stacking:**
  Table scrolls horizontally inside `overflow-x-auto`. Text and GEO callout stack below at full width.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-4">
        چالش <span class="text-solar-gold">توان پیوسته</span> و مدیریت حرارتی در مزارع ماینینگ
      </h2>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start mt-10">
        <!-- Data-Viz Table -->
        <div class="lg:col-span-8 glass-card rounded-s-3xl p-8 overflow-x-auto">
          <h3 class="font-bold text-lg text-cyber-cyan mb-4 font-mono">CAPACITY PLANNING MATRIX</h3>
          <table class="w-full min-w-[600px] text-sm" role="table" aria-label="جدول برآورد ظرفیت نیروگاه خورشیدی بر اساس تعداد ماینر">
            <thead>
              <tr class="bg-cyber-cyan/10 text-cyber-cyan font-mono">
                <th scope="col" class="p-3 text-start rounded-s-lg">تعداد ماینر ASIC</th>
                <th scope="col" class="p-3 text-start">مصرف کل (kW)</th>
                <th scope="col" class="p-3 text-start">سربار خنک‌کننده (kW)</th>
                <th scope="col" class="p-3 text-start">ظرفیت نیروگاه خورشیدی (kWp)</th>
                <th scope="col" class="p-3 text-start rounded-e-lg">تعداد پنل ۶۰۰W</th>
              </tr>
            </thead>
            <tbody>
              <tr class="bg-deep-navy/60 hover:bg-cyber-cyan/5 transition-colors">
                <td class="p-3 font-mono text-pure-white">۱۰</td>
                <td class="p-3 font-mono">۳۰</td>
                <td class="p-3 font-mono">۸</td>
                <td class="p-3 font-mono text-solar-gold font-bold">~۵۰</td>
                <td class="p-3 font-mono">~۸۴</td>
              </tr>
              <tr class="bg-navy-mid/40 hover:bg-cyber-cyan/5 transition-colors">
                <td class="p-3 font-mono text-pure-white">۵۰</td>
                <td class="p-3 font-mono">۱۵۰</td>
                <td class="p-3 font-mono">۴۰</td>
                <td class="p-3 font-mono text-solar-gold font-bold">~۲۵۰</td>
                <td class="p-3 font-mono">~۴۱۷</td>
              </tr>
              <tr class="bg-deep-navy/60 hover:bg-cyber-cyan/5 transition-colors">
                <td class="p-3 font-mono text-pure-white">۱۰۰</td>
                <td class="p-3 font-mono">۳۰۰</td>
                <td class="p-3 font-mono">۸۰</td>
                <td class="p-3 font-mono text-solar-gold font-bold">~۵۰۰</td>
                <td class="p-3 font-mono">~۸۳۴</td>
              </tr>
              <tr class="bg-navy-mid/40 hover:bg-cyber-cyan/5 transition-colors">
                <td class="p-3 font-mono text-pure-white">۵۰۰</td>
                <td class="p-3 font-mono">۱,۵۰۰</td>
                <td class="p-3 font-mono">۴۰۰</td>
                <td class="p-3 font-mono text-solar-gold font-bold">~۲,۵۰۰</td>
                <td class="p-3 font-mono">~۴,۱۶۷</td>
              </tr>
            </tbody>
          </table>
          <p class="text-xs text-pure-white/40 mt-3 font-mono">* Estimates based on 3kW/unit ASIC + 25% cooling overhead. Actual values vary by model and climate.</p>
        </div>
        <!-- Text + GEO Sidebar -->
        <div class="lg:col-span-4 space-y-6 text-start">
          <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
            {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
          </p>
          <div class="glass-card p-5 border-s-4 border-solar-gold">
            <p class="text-sm font-bold text-solar-gold mb-1">⚡ نکته فنی حیاتی</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
            </p>
          </div>
        </div>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article>` semantically wraps the self-contained technical content.
  - `<table>` has `role="table"` and descriptive Farsi `aria-label`.
  - All `<th>` elements use `scope="col"`.
  - Monospace font is used for data values but doesn't replace semantic meaning; column headers explain each metric.
  - Hover states use subtle color, not the sole differentiator.

---

### [SEC_03]: حل معضل قطعی برق و افت فاجعه‌بار هش‌ریت

- **Section Role:** Pain-point emotional trigger — split-screen offline vs. online contrast.

- **UI Aesthetic & Colors:**
  Split-screen composition. **Offline/Pain side** (start in RTL): Deep red-tinted dark background (`bg-deep-navy` with `alert-red/10` overlay). Disconnected miner icons, a flatlined hash rate graph, static noise texture. **Online/Solar side** (end in RTL): Deep navy with `eco-green/10` glow. Active miner LEDs, a climbing hash rate chart, solar-gold energy pulse animation. Central divider is a vertical lightning bolt SVG separator.

- **Desktop Grid Architecture:**
  12-column grid. Offline panel: `lg:col-span-6`. Online panel: `lg:col-span-6`. Both `min-h-[500px]` with centered content. GEO callout as an overlapping glass card at the horizontal center.

- **Mobile Stacking:**
  Vertical stack. Offline panel (reduced `h-[280px]`) first, then online panel. GEO card between them as full-width banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[550px]">
      <!-- Offline Pain Side -->
      <div class="lg:col-span-6 relative flex flex-col items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <div class="absolute inset-0 bg-alert-red/5"></div>
        <div class="relative z-10 text-center space-y-4">
          <span class="text-6xl">🔴</span>
          <h3 class="text-alert-red font-bold text-xl">OFFLINE — قطعی برق شبکه</h3>
          <div class="font-mono text-alert-red/60 text-4xl font-black line-through">0.00 TH/s</div>
          <p class="text-pure-white/50 text-sm max-w-xs mx-auto">افت هش‌ریت، از دست رفتن درآمد دلاری، ری‌استارت زمان‌بر استخرها</p>
        </div>
      </div>
      <!-- Online Solar Side -->
      <div class="lg:col-span-6 relative flex flex-col items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <div class="absolute inset-0 bg-eco-green/5"></div>
        <div class="relative z-10 text-center space-y-4">
          <span class="text-6xl">🟢</span>
          <h3 class="text-eco-green font-bold text-xl">ONLINE — برق خورشیدی پایدار</h3>
          <div class="font-mono text-eco-green text-4xl font-black">99.9% Uptime</div>
          <p class="text-pure-white/70 text-sm max-w-xs mx-auto">هش‌ریت ۱۰۰٪ فعال، درآمد بی‌وقفه، ریسک صفر خاموشی</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">⚠️ ریسک خاموشی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
    <!-- Full Text Below -->
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        حل معضل <span class="text-alert-red">قطعی برق</span> و افت فاجعه‌بار <span class="text-solar-gold">هش‌ریت</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section>` semantic wrapper with `id="sec-03"`.
  - Color is supplemented by text labels and icons (`🔴 OFFLINE` vs `🟢 ONLINE`) so meaning isn't color-dependent.
  - Monospace hash rate values have surrounding context (headings, descriptions) for screen readers.
  - GEO card is visually prominent with `border-2 border-solar-gold`.

---

### [SEC_04]: باورهای غلط درباره ماینر و پنل خورشیدی (Myth vs. Reality)

- **Section Role:** Myth-busting block — debunks amateur DIY mining assumptions, targets serious B2B investors.

- **UI Aesthetic & Colors:**
  Dark background with a slight warm shift: `bg-navy-mid`. The myth/fact block is a single large glass card with an internal two-column layout. Myth column has `bg-alert-red/8 border-e border-alert-red/20` (border on the end side in RTL). Fact column has `bg-eco-green/8`. A bold `⚠️ هشدار برای سرمایه‌گذاران` label at the top in `text-solar-gold`. GEO callout as a bottom-attached bar with `border-t-4 border-cyber-cyan`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl mx-auto`. Inside the glass card: `grid-cols-2` with myth on `col-span-1` and fact on `col-span-1`.

- **Mobile Stacking:**
  Myth and Fact stack vertically inside the card. Myth card first (red accent), Fact second (green accent).

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        باورهای غلط درباره <span class="text-solar-gold">ماینر و پنل خورشیدی</span>
      </h2>
      <p class="text-center text-pure-white/60 text-sm mb-10">⚠️ هشدار: این بخش مخصوص سرمایه‌گذاران جدی است</p>

      <div class="glass-card overflow-hidden"
           x-data="{ revealed: false }" x-intersect.once="revealed = true">
        <div class="grid grid-cols-1 md:grid-cols-2">
          <!-- Myth Column -->
          <div class="p-8 bg-alert-red/8 border-e border-alert-red/20 transition-all duration-700"
               :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
            <span class="text-3xl">❌</span>
            <h3 class="font-bold text-alert-red text-lg mt-3">باور غلط</h3>
            <p class="text-pure-white/80 mt-3 text-base leading-relaxed">
              با دو عدد پنل خورشیدی کوچک می‌توان یک ماینر قدرتمند را در خانه روشن کرد.
            </p>
          </div>
          <!-- Fact Column -->
          <div class="p-8 bg-eco-green/8 transition-all duration-700 delay-200"
               :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
            <span class="text-3xl">✅</span>
            <h3 class="font-bold text-eco-green text-lg mt-3">واقعیت مهندسی</h3>
            <p class="text-pure-white/80 mt-3 text-base leading-relaxed">
              روشن کردن ۲۴ ساعته تنها یک ماینر ۳۰۰۰ واتی، به یک نیروگاه خورشیدی کوچک با ده‌ها پنل و بانک باتری عظیم (یا اتصال شبکه) نیاز دارد.
            </p>
          </div>
        </div>
        <!-- GEO Callout Bar -->
        <div class="border-t-4 border-cyber-cyan p-6 bg-deep-navy/30">
          <p class="text-sm font-bold text-cyber-cyan mb-1">🔬 حقیقت صنعتی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
          </p>
        </div>
      </div>

      <!-- Extended Text -->
      <div class="mt-10 text-start max-w-3xl mx-auto">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside>` used per SEO Dossier semantic directive.
  - `x-intersect` is decorative animation; content is in the DOM from page load.
  - Myth/Fact labels use both color AND icon + text labels.
  - `border-e` (logical property) separates myth from fact in RTL direction.

---

### [SEC_05]: استفاده از پنل‌های نسل جدید برای کاهش فضای مورد نیاز

- **Section Role:** E-E-A-T hardware authority — Bifacial panel showcase.

- **UI Aesthetic & Colors:**
  Return to `bg-deep-navy`. A large high-resolution hero image of a Bifacial solar panel capturing light from both sides, placed inside an asymmetrical Bento card with one side rounded (`rounded-e-3xl`). The image has a subtle `cyber-cyan` glow border effect. Text block alongside with E-E-A-T hardware branding mentions (Jinko, Trina, LONGi) styled as small inline badges (`bg-cyber-cyan/10 text-cyber-cyan text-xs rounded-full px-2 py-0.5`).

- **Desktop Grid Architecture:**
  12-column grid. Image card: `lg:col-span-6`. Text + GEO block: `lg:col-span-6`. Both vertically centered with `items-center`.

- **Mobile Stacking:**
  Image card on top at full width with `max-h-[350px] object-cover`. Text below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- Bifacial Panel Image -->
      <div class="lg:col-span-6 relative rounded-e-3xl overflow-hidden shadow-2xl shadow-cyber-cyan/10">
        <img src="/images/bifacial-panel-detail.webp"
             alt="پنل خورشیدی دوطرفه Bifacial در حال جذب نور از هر دو سمت"
             class="w-full h-auto object-cover max-h-[450px]"
             loading="lazy">
        <!-- Glow Border Effect -->
        <div class="absolute inset-0 rounded-e-3xl border-2 border-cyber-cyan/20 pointer-events-none"></div>
      </div>
      <!-- Text + GEO -->
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پنل‌های <span class="text-solar-gold">نسل جدید Bifacial</span> برای کاهش فضا
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <!-- Brand Badges -->
        <div class="flex flex-wrap gap-2">
          <span class="bg-cyber-cyan/10 text-cyber-cyan text-xs font-mono rounded-full px-3 py-1">Jinko Solar</span>
          <span class="bg-cyber-cyan/10 text-cyber-cyan text-xs font-mono rounded-full px-3 py-1">Trina Solar</span>
          <span class="bg-cyber-cyan/10 text-cyber-cyan text-xs font-mono rounded-full px-3 py-1">LONGi Green</span>
        </div>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 بهینه‌سازی فضا</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Image has descriptive Farsi `alt` text explaining bifacial light capture.
  - Glow border overlay is `pointer-events-none` and decorative.
  - Brand badges are supplementary; brand names also appear in the body text.
  - `rounded-e-3xl` uses logical property for RTL correctness.

---

### [SEC_06]: زیرساخت قانونی و آیین‌نامه‌های وزارت نیرو (آپدیت 1403)

- **Section Role:** Temporal freshness + legal authority signal with outbound trust link.

- **UI Aesthetic & Colors:**
  A highlighted legal/informational block on `bg-navy-mid`. Uses a prominent bordered box (`border-2 border-eco-green`) on a `bg-eco-green/5` surface to signal "legal safety." The outbound link to `tavanir.org.ir` is `text-solar-gold underline`. A "بروزرسانی ۱۴۰۳" badge in `bg-solar-gold text-deep-navy text-xs rounded-full`. A ⚖️ law icon anchors the visual.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single column informational layout.

- **Mobile Stacking:**
  No change; already single-column centered.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-16 md:py-24 bg-navy-mid">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          زیرساخت قانونی و آیین‌نامه‌های <span class="text-solar-gold">وزارت نیرو</span>
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">آپدیت ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT — with inline link:}
        ... آخرین آیین‌نامه‌های اجرایی <a href="https://www.tavanir.org.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">شرکت توانیر</a> در سال ۱۴۰۳ ...
      </p>
      <!-- Legal Safety Box / GEO Block -->
      <div class="border-2 border-eco-green rounded-2xl p-6 bg-eco-green/5">
        <div class="flex items-start gap-3">
          <span class="text-3xl mt-1">⚖️</span>
          <div>
            <p class="text-sm font-bold text-eco-green mb-1">✅ وضعیت قانونی — کاملاً مجاز</p>
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
  - External link has `rel="external noopener"` and `target="_blank"`.
  - Legal safety box uses both color (green border) AND text ("✅ وضعیت قانونی — کاملاً مجاز") for accessibility.
  - Icon is decorative; critical information is in text.

---

### [SEC_07]: پوشش جغرافیایی هورا نور سهند در مناطق مستعد ماینینگ

- **Section Role:** Local SEO anchor — NAP signals with industrial zones for crypto farms.

- **UI Aesthetic & Colors:**
  Dark background (`bg-deep-navy`). An embedded map snippet (static WebP or interactive iframe) showing Karaj HQ and industrial outskirts (Eshtehard, Simindasht, Savojbolagh). Map has a `cyber-cyan` tint filter. The `<address>` block uses `bg-solar-gold text-deep-navy` for high-contrast NAP. Industrial zone markers glow with `cyber-cyan` pulse dots.

- **Desktop Grid Architecture:**
  12-column grid. Map: `lg:col-span-7`. Text + address: `lg:col-span-5`.

- **Mobile Stacking:**
  Map reduces to `max-h-[280px]`. Address and text stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- Map Visual -->
      <div class="lg:col-span-7 rounded-2xl overflow-hidden" aria-label="نقشه مناطق صنعتی مستعد فارم ماینینگ" role="img">
        <img src="/images/crypto-farm-coverage-map.webp"
             alt="نقشه پوشش خدمات نیروگاه خورشیدی ماینینگ - کرج، اشتهارد، ساوجبلاغ، قزوین"
             class="w-full h-auto max-h-[400px] object-cover"
             loading="lazy"
             style="filter: hue-rotate(180deg) saturate(0.3) brightness(0.8);">
      </div>
      <!-- Text + Address -->
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پوشش جغرافیایی <span class="text-solar-gold">مناطق مستعد ماینینگ</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <!-- NAP Address Card -->
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد</p>
          <p>📞 026-36506485</p>
          <p>📱 09125728170</p>
        </address>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-cyber-cyan">
          <p class="text-sm font-bold text-cyber-cyan mb-1">📍 مناطق صنعتی تحت پوشش</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<address>` HTML element for structured NAP data.
  - Map image has comprehensive `alt` text listing served industrial zones.
  - Map container has `role="img"` with Farsi `aria-label`.
  - CSS filter on map image is purely aesthetic; `alt` text carries all semantic meaning.

---

### [SEC_08]: بررسی اقتصادی و نرخ بازگشت سرمایه (ROI)

- **Section Role:** Internal linking bridge to pricing page — prevents keyword cannibalization.

- **UI Aesthetic & Colors:**
  Dark gradient from `navy-mid` to `deep-navy`. A single prominent glass card with a large 📈 chart icon and financial metrics displayed in `font-mono text-solar-gold`. The internal link to `/pricing/industrial-power-plants` is a glowing pill-shaped CTA. GEO callout integrated inline within the card.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single-column vertical stack inside the glass card.

- **Mobile Stacking:**
  No change; CTA becomes `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-gradient-to-b from-navy-mid to-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        بررسی اقتصادی و <span class="text-solar-gold">نرخ بازگشت سرمایه (ROI)</span>
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <!-- ROI Visual Teaser -->
        <div class="flex items-center gap-4 mb-4">
          <span class="text-5xl">📈</span>
          <div>
            <p class="font-mono text-solar-gold text-2xl font-black">ROI &lt; 3 YEARS</p>
            <p class="text-pure-white/60 text-sm">بازگشت سرمایه سریع‌تر از استاندارد صنعت</p>
          </div>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <!-- GEO Callout Inline -->
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">💰 تحلیل مالی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <!-- Internal Link CTA -->
        <a href="/pricing/industrial-power-plants"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="مشاهده جدول برآورد هزینه‌های احداث نیروگاه صنعتی">
          جدول برآورد هزینه‌ها
          <svg><!-- Arrow icon --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Internal link CTA has `role="button"` with descriptive `aria-label`.
  - ROI metric is shown in both English shorthand and Farsi description for dual-audience readability.
  - `w-full` on mobile for large touch target.

---

### [SEC_09]: بخش پاسخ به سوالات متداول (FAQ)

- **Section Role:** GEO/SGE bait — FAQ accordion with FAQPage JSON-LD backing.

- **UI Aesthetic & Colors:**
  Background: `bg-deep-navy`. FAQ items are glass cards with `border-s-4 border-cyber-cyan` when expanded, `border-s-4 border-pure-white/10` when collapsed. Summary text highlights in `text-cyber-cyan` when open. Smooth Alpine `x-collapse` transitions.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single-column accordion stack.

- **Mobile Stacking:**
  No change; full-width accordion. Touch targets at `py-5 px-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-deep-navy"
           x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">ماینینگ خورشیدی</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
        </p>
      </div>
      <!-- FAQ Accordion -->
      <div class="space-y-4">
        <!-- FAQ Item 1 -->
        <details class="glass-card overflow-hidden"
                 :class="openFaq === 1 ? 'border-s-4 border-cyber-cyan' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 1 ? null : 1">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   :aria-expanded="openFaq === 1 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 1 ? 'text-cyber-cyan' : 'text-pure-white'">
              برای یک ماینر M30s چند عدد پنل خورشیدی لازم است؟
            </span>
            <svg class="w-5 h-5 text-cyber-cyan transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron icon -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            یک دستگاه واتسین ماینر M30s حدود ۳۴۰۰ وات مصرف دارد. برای روشن نگه‌داشتن ۲۴ ساعته آن با پنل، به دلیل نیاز به شارژ باتری‌های غول‌پیکر برای مصرف در شب، شما به حداقل ۱۵ الی ۲۰ پنل ۵۵۰ واتی به همراه تجهیزات صنعتی نیاز دارید.
          </div>
        </details>
        <!-- FAQ Item 2 -->
        <details class="glass-card overflow-hidden"
                 :class="openFaq === 2 ? 'border-s-4 border-cyber-cyan' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-cyber-cyan' : 'text-pure-white'">
              فارم ماینینگ در شب چگونه از خورشید برق می‌گیرد؟
            </span>
            <svg class="w-5 h-5 text-cyber-cyan transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron icon -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            دو راهکار صنعتی وجود دارد: اول سیستم‌های هیبریدی... دوم، سرمایه‌گذاری سنگین روی بانک‌های باتری لیتیومی یا دیپ‌سایکل ژل...
          </div>
        </details>
      </div>
      <!-- CODER NOTE: Wrap above FAQ content in FAQPage JSON-LD schema as per dossier directive. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>` / `<summary>` elements for keyboard and screen reader support.
  - `:aria-expanded` dynamically bound via Alpine.
  - `role="button"` on `<summary>`.
  - Generous touch targets (`py-5 px-6`).
  - `cyber-cyan` accent differentiates this crypto-themed FAQ from the agricultural page's `solar-gold` FAQ.

---

### [SEC_10]: رزرو وقت مشاوره برای احداث فارم خورشیدی

- **Section Role:** Final CRO conversion block — dark-mode high-tech CTA targeting crypto investors.

- **UI Aesthetic & Colors:**
  Full-width section with a deep, rich background: `bg-gradient-to-br from-deep-navy via-navy-mid to-deep-navy`. A subtle animated grid pattern background (CSS `background-image` with thin `cyber-cyan/5` grid lines) for a futuristic data-center feel. CTA button in `bg-solar-gold text-deep-navy`. Phone numbers are oversized `font-mono` for a terminal aesthetic. Messenger icons in glowing `cyber-cyan` circles.

- **Desktop Grid Architecture:**
  12-column grid. Text + CTA: `lg:col-span-7`. Messenger icons + GEO callout: `lg:col-span-5`.

- **Mobile Stacking:**
  Single column centered. Phone numbers stack vertically. Messenger icons in a centered row. Full-width tap targets.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-gradient-to-br from-deep-navy via-navy-mid to-deep-navy relative overflow-hidden">
    <!-- Grid Pattern Background -->
    <div class="absolute inset-0 pointer-events-none opacity-20"
         style="background-image: linear-gradient(rgba(0,229,255,0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(0,229,255,0.05) 1px, transparent 1px); background-size: 40px 40px;"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- CTA Text Block -->
      <div class="lg:col-span-7 text-start">
        <div class="inline-block bg-cyber-cyan/10 border border-cyber-cyan/30 rounded-full px-4 py-1 mb-6">
          <span class="font-mono text-cyber-cyan text-sm">BOOK YOUR ENGINEERING PROPOSAL</span>
        </div>
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
          رزرو وقت مشاوره برای <span class="text-solar-gold">احداث فارم خورشیدی</span>
        </h2>
        <p class="text-pure-white/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_10}
        </p>
        <!-- Phone Numbers -->
        <div class="space-y-4">
          <a href="tel:02636506485" class="block font-mono text-3xl md:text-5xl font-black text-solar-gold hover:text-solar-gold/80 transition-colors" dir="ltr"
             aria-label="تماس با دفتر مرکزی کرج: ۰۲۶-۳۶۵۰۶۴۸۵">
            026-36506485
          </a>
          <a href="tel:09125728170" class="block font-mono text-2xl md:text-4xl font-bold text-solar-gold/70 hover:text-solar-gold/60 transition-colors" dir="ltr"
             aria-label="تماس با مدیریت پروژه: ۰۹۱۲۵۷۲۸۱۷۰">
            0912-572-8170
          </a>
        </div>
      </div>
      <!-- Messenger Icons + GEO -->
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-pure-white font-bold text-lg">ارتباط از طریق پیام‌رسان‌ها:</p>
        <div class="flex gap-4">
          <a href="https://wa.me/989125728170" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-cyber-cyan/10 border border-cyber-cyan/30 text-cyber-cyan flex items-center justify-center text-2xl hover:bg-cyber-cyan/20 hover:scale-110 transition-all"
             aria-label="ارسال پیام در واتس‌اپ">
            <svg><!-- WA --></svg>
          </a>
          <a href="#"
             class="w-16 h-16 rounded-full bg-cyber-cyan/10 border border-cyber-cyan/30 text-cyber-cyan flex items-center justify-center text-2xl hover:bg-cyber-cyan/20 hover:scale-110 transition-all"
             aria-label="ارسال پیام در بله">
            <svg><!-- Bale --></svg>
          </a>
          <a href="#"
             class="w-16 h-16 rounded-full bg-cyber-cyan/10 border border-cyber-cyan/30 text-cyber-cyan flex items-center justify-center text-2xl hover:bg-cyber-cyan/20 hover:scale-110 transition-all"
             aria-label="ارسال پیام در ایتا">
            <svg><!-- Eitaa --></svg>
          </a>
        </div>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold mt-4 w-full">
          <p class="text-sm font-bold text-solar-gold mb-1">🏗️ شروع پروژه</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Phone links use `<a href="tel:...">` with explicit Farsi `aria-label`.
  - Phone number elements have `dir="ltr"` for correct digit rendering in RTL.
  - Messenger icon buttons: `w-16 h-16` (64px) exceeds WCAG 2.5.8 minimum of 44px.
  - Each messenger link has unique `aria-label`.
  - External links have `rel="noopener"`.
  - Grid pattern background is `pointer-events-none` and purely decorative.
  - English tech badge is decorative enhancement; key CTA information is in the Farsi H2 and body text.

---

[VERIFIED_UI_END_OF_FILE]
