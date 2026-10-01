# UI Wireframe Specification: استراکچر پنل خورشیدی | نصب روی بام و شیروانی | هورا نور سهند
- **Source Dossier:** `seo_dossiers/engineering_mounting-structures-roofs.md`
- **Target URL:** `/engineering/mounting-structures-roofs`
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
| `--color-danger`     | `#E74C4C` | `alert-red`           | Danger/diesel/loss column in comparisons  |
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

### [SEC_01]: استراکچر و سازه‌های مهندسی نصب پنل (پشت‌بام، سقف سوله و زمین)

- **Section Role:** Primary Hero — H1 entity, engineering authority, structural trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with 3D CAD-to-reality morph animation: CAD wireframe of mounting structure transitions into real photo of installed industrial roof. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "Engineering Authority" badge in `solar-gold`. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. 3D viewer: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. 3D model `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-mounting-structure.webp"
         alt="استراکچر پنل خورشیدی روی سقف سوله صنعتی — مهندسی سازه‌های گالوانیزه"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          مهندسی سازه | طراحی EPC | اجرای EPC
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          استراکچر و سازه‌های مهندسی نصب پنل (پشت‌بام، <span class="text-solar-gold">سقف سوله</span> و زمین)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره و طراحی استراکچر فنی">
          مشاوره سازه فنی
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
  - Hero `alt` in Farsi describing mounting structure on industrial roof.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: نصب پنل خورشیدی روی پشت بام (ایزوگام و بام تخت)

- **Section Role:** B2C Residential — Ballast method, zero penetration.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive cross-section diagram: Flat Roof → Rubber Pad → Concrete Ballast → Galvanized Leg → Solar Panel. Layers animate on scroll (staggered). Hover on each layer shows material specs.

- **Desktop Grid Architecture:**
  12-col. Cross-section: `lg:col-span-6 lg:sticky lg:top-20`. Text + Specs: `lg:col-span-6`.

- **Mobile Stacking:**
  Cross-section first (`h-[400px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ activeLayer: 0 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار مقطع عرضی نصب روی پشت بام با بلاست بتنی" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقطع عرضی: پشت بام تخت (Ballast Mount)</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center" x-data="{ activeLayer: -1 }">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار مقطع عرضی لایه‌های نصب روی پشت بام">
              <!-- Roof Membrane -->
              <rect x="40" y="40" width="320" height="10" rx="2" fill="#132F4C" stroke="#F5A623" stroke-width="2"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 0 }"
                    @mouseenter="activeLayer = 0" @mouseleave="activeLayer = -1"/>
              <!-- Insulation / Isofoam -->
              <rect x="40" y="50" width="320" height="15" rx="1" fill="#1E3A5F" opacity="0.5"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 1 }"
                    @mouseenter="activeLayer = 1" @mouseleave="activeLayer = -1"/>
              <!-- EVA / Waterproofing -->
              <rect x="40" y="65" width="320" height="10" rx="1" fill="#2ECC71" opacity="0.4"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 2 }"
                    @mouseenter="activeLayer = 2" @mouseleave="activeLayer = -1"/>
              <!-- Rubber Pad -->
              <rect x="40" y="75" width="320" height="20" rx="2" fill="#E74C3C" opacity="0.3"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 3 }"
                    @mouseenter="activeLayer = 3" @mouseleave="activeLayer = -1"/>
              <!-- Concrete Ballast -->
              <rect x="40" y="95" width="320" height="50" rx="2" fill="#E74C3C" opacity="0.8"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 4 }"
                    @mouseenter="activeLayer = 4" @mouseleave="activeLayer = -1"/>
              <!-- Mounting Leg -->
              <rect x="100" y="145" width="200" height="120" rx="3" fill="#F5A623" opacity="0.8"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 5 }"
                    @mouseenter="activeLayer = 5" @mouseleave="activeLayer = -1"/>
              <!-- Panel -->
              <rect x="50" y="270" width="300" height="15" rx="1" fill="#FFFFFF" opacity="0.9"
                    :class="{ 'ring-2 ring-solar-gold': activeLayer === 6 }"
                    @mouseenter="activeLayer = 6" @mouseleave="activeLayer = -1"/>
            </svg>
            <div class="flex flex-wrap justify-center gap-2 mt-4 text-xs">
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 0 }"><span class="w-4 h-1 rounded bg-deep-navy"></span> ایزوگام / پس‌شیمی</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 1 }"><span class="w-4 h-1 rounded bg-navy-mid"></span> عایق حرارتی</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 1 }"><span class="w-4 h-1 rounded bg-solar-gold/30"></span> EVA</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 2 }"><span class="w-4 h-1 rounded bg-solar-gold/30"></span> EVA</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 3 }"><span class="w-4 h-1 rounded bg-alert-red/30"></span> پد لاستیکی</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 4 }"><span class="w-4 h-1 rounded bg-alert-red"></span> بلاست بتنی (Ballast)</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 5 }"><span class="w-4 h-1 rounded bg-solar-gold"></span> پایه گالوانیزه</span>
              <span class="flex items-center gap-1" :class="{ 'ring-2 ring-solar-gold': activeLayer === 6 }"><span class="w-4 h-1 rounded bg-pure-white"></span> پنل خورشیدی</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          نصب پنل خورشیدی روی <span class="text-solar-gold">پشت بام</span> (ایزوگام و بام تخت)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
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
  - `<article id="sec-02">`.
  - Interactive SVG `role="img"` + `aria-label`.
  - Hover states have text equivalents.

---

### [SEC_03]: پنل خورشیدی روی سقف شیروانی و سوله‌های صنعتی

- **Section Role:** B2B Industrial — Non-penetrating clamps.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Macro photography gallery: clamp close-ups with hover zoom. Each clamp image has tooltip with specs. Split view: Clamp closed vs Clamp open.

- **Desktop Grid Architecture:**
  12-col. Gallery: `lg:col-span-7`. Text: `lg:col-span-5`. GEO callout below.

- **Mobile Stacking:**
  Carousel `snap-x`. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        نصب پنل خورشیدی روی <span class="text-solar-gold">سقف شیروانی و سوله‌های صنعتی</span>
      </h2>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
        <div class="lg:col-span-7">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">کلمپ‌های غیرنفوذه (Non-Penetrating Clamps)</h3>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50 group cursor-pointer"
                 role="figure" aria-label="کلمپ گیره‌ای روی سقف شیروانی">
              <img src="/images/clamp-closed.webp" alt="کلمپ بسته روی درز سقف شیروانی" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
              <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
                <p class="text-pure-white font-bold">کلمپ گیره‌ای (Clamp) - بسته</p>
              </div>
            </div>
            <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50 group cursor-pointer"
                 role="figure" aria-label="کلمپ باز روی سقف شیروانی">
              <img src="/images/clamp-open.webp" alt="کلمپ باز برای نصب پنل" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
              <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
                <p class="text-pure-white font-bold">کلمپ باز - آماده نصب</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          نصب پنل روی <span class="text-solar-gold">سقف شیروانی و سوله‌های صنعتی</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی برای موتورهای جستجو</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `role="figure"` + `aria-label` on clamp images.
  - Hover captions decorative; `alt` provides equivalent info.

---

### [SEC_04]: باورهای غلط در خصوص استراکچرها (Myth vs. Reality)

- **Section Role:** Myth-busting — Weight safety.

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
        باورهای غلط در خصوص <span class="text-solar-gold">استراکچرها</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            استراکچر پنل خورشیدی باعث سنگین شدن و ریزش سقف‌های قدیمی می‌شود.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            وزن اضافه شده به سقف (شامل پنل و استراکچر) کمتر از ۱۵ کیلوگرم در هر متر مربع است که برای تمام سقف‌های استاندارد کاملاً ایمن است. پنل‌های مونوکریستال جدید بسیار سبک شده‌اند و استفاده از استراکچرهای پروفیل آلومینیومی یا فولاد سبک‌سازی شده، وزن کل سیستم را به ۱۲ الی ۱۵ کیلووات در هر متر مربع محدود می‌کند. این عدد در محاسبات نظام مهندسی بسیار ناچیز است.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">⚖️ تحلیل باربردی</p>
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

### [SEC_05]: تنظیم دقیق جهت پنل خورشیدی و زاویه تابش

- **Section Role:** Technical precision — Compass + Tilt visualizer.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive compass + tilt slider. Compass: animated sun arc (E→W) with `solar-gold` arc. Tilt slider: 0°–45°, live updates panel angle.

- **Desktop Grid Architecture:**
  12-col. Compass: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Compass first (`h-[400px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy" x-data="{ tilt: 30, azimuth: 0 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار تعاملی جهت و زاویه تابش پنل خورشیدی" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">جهت و زاویه بهینه (ایران / نیمکره شمالی)</h3>
          <div class="relative w-full h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار جهت و زاویه پنل خورشیدی">
              <!-- Compass Rose -->
              <circle cx="200" cy="150" r="120" fill="none" stroke="#F5A623" stroke-width="2"/>
              <!-- North Arrow -->
              <path d="M200,30 L200,120" stroke="#F5A623" stroke-width="3" stroke-linecap="round" marker-end="url(#arrow-north)"/>
              <!-- South Direction -->
              <path d="M200,150 L200,270" stroke="#2ECC71" stroke-width="4" stroke-linecap="round" marker-end="url(#arrow-south)"/>
              <text x="200" y="290" text-anchor="middle" fill="#2ECC71" font-size="14" font-family="Vazirmatn" font-weight="bold">جنوب (آزیموت ۰°)</text>
              <!-- Panel Tilt Indicator -->
              <line x1="200" y1="150" x2="200" y2="280" stroke="#F5A623" stroke-width="4" stroke-linecap="round" marker-end="url(#arrow-panel)">
              <defs>
                <marker id="arrow-panel" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
                  <polygon points="0 0, 10 3.5, 0 7" fill="#F5A623"/>
                </marker>
              </defs>
            </svg>
            <div class="flex justify-center gap-6 mt-6 text-sm">
              <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-solar-gold"></span> آزیموت: ۰° (جنوب)</span>
              <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-eco-green"></span> شیب: ۳۰-۳۵°</span>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تنظیم دقیق <span class="text-solar-gold">جهت و زاویه</span> پنل خورشیدی
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🧭 اصل مهندسی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Interactive SVG `role="img"` + `aria-label`.
  - Color + text labels for direction/tilt.

---

### [SEC_06]: متریال ضدزنگ: گالوانیزه گرم و آلومینیوم آنودایز شده

- **Section Role:** E-E-A-T Material authority — Material showcase.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Material quality cards: Hot-Dip Galvanized (steel) vs Anodized Aluminum. Each with magnification zoom on hover.

- **Desktop Grid Architecture:**
  12-col. Two cards side-by-side `grid-cols-2 gap-6`. GEO callout below.

- **Mobile Stacking:**
  Vertical stack.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        متریال ضدزنگ: <span class="text-solar-gold">گالوانیزه گرم</span> و <span class="text-eco-green">آلومینیوم آنودایز</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
        <!-- Hot-Dip Galvanized Steel -->
        <div class="glass-card p-8 rounded-2xl border border-solar-gold/30 hover:shadow-xl hover:border-solar-gold/50 transition-all"
             role="figure" aria-label="فولاد گالوانیزه گرم (Hot-Dip Galvanized)">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🔩</span>
            <div>
              <h3 class="font-bold text-xl text-solar-gold">فولاد گالوانیزه گرم (HDG)</h3>
              <p class="text-pure-white/70 text-sm">پوشش گالوانیزه گرم با ضخامت ۸۰ میکرون+</p>
            </div>
          </div>
          <ul class="space-y-3 text-pure-white/80 text-sm">
            <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> پوشش گالوانیزه گرم (Hot-Dip) با ضخامت ≥ ۸۰ میکرون</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> مقاومت برابر ۵۰ سال در برابر خورده‌ی محیطی</li>
            <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> اتصالات مشتک فولادی ضد زنگ (Stainless Steel)</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> تست نمک (Salt Spray Test) ۱۰۰۰ ساعت</li>
          </ul>
        </div>
        <!-- Anodized Aluminum -->
        <div class="glass-card p-8 rounded-2xl border border-eco-green/30 bg-eco-green/10 transition-all hover:shadow-xl hover:border-eco-green/50"
             role="figure" aria-label="آلومینیوم آنودایز">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🔩</span>
            <div>
              <h3 class="font-bold text-xl text-eco-green">آلومینیوم آنودایز (Anodized)</h3>
              <p class="text-pure-white/70 text-sm">پروفیل‌های آلومینیومی آنودایز سخت</p>
            </div>
          </div>
          <ul class="space-y-3 text-pure-white/80 text-sm">
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> آنودایز سخت (Hard Anodize) ۲۵ میکرون+</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> مقاومت عالی در برابر اسیدها و بیس‌ها</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> سبک و استحکام بالا</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> عدم نیاز به نگهداری</li>
          </ul>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_07]: الزامات مبحث ششم مقررات ملی ساختمان (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + Legal compliance.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". External link to `inbr.ir` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badge inline with H2.

- **Mobile Stacking:**
  Badge wraps naturally.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          الزامات مبحث ششم مقررات ملی ساختمان
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="glass-card p-5 border-s-4 border-solar-gold">
        <div class="flex items-start gap-3">
          <span class="text-2xl mt-1">📰</span>
          <div>
            <p class="text-sm font-bold text-solar-gold mb-1">نکته مهم قانونی ۱۴۰۳</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
            </p>
          </div>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mt-8">
          مراجعه به <a href="https://inbr.ir/" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">مقررات ملی ساختمان ایران (مبحث ششم)</a> برای اطلاع از استانداردهای بار برف و باد.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: پشتیبانی کارگاهی از دفتر مرکزی هورا نور در البرز

- **Section Role:** Local SEO + Supply chain authority.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Photo of Karaj workshop + HQ. Map pinpoints to villa zones (Kordan, Hashtgerd) and industrial zones (Eshtehard, Simindasht). `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="موقعیت کارگاه و دفتر مرکزی هورا نور سهند" role="img">
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d50000!2d50.9!3d35.8!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3f8d1e0000000000%3A0x0!2z2YbYsdin2KfZhdi4INin2YTYp9mE!5e0!3m2!1sfa!2sir!4v1"
                width="100%" height="400" style="border:0;" allowfullscreen="" loading="lazy"
                aria-label="موقعیت کارگاه و دفتر مرکزی هورا نور سهند در کرج و البرز"></iframe>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پشتیبانی کارگاهی از <span class="text-solar-gold">دفتر مرکزی البرز</span>
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
          <p class="text-sm font-bold text-solar-gold mb-1">🏭 پوشش کارگاهی</p>
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

### [SEC_09]: انتخاب سیستم ثابت یا متحرک (ترکر)?

- **Section Role:** Internal linking — Anti-cannibalization to industrial pricing.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Comparison card: Fixed vs Tracker. Tracker card has animated sun-tracking icon.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. Side-by-side comparison cards.

- **Mobile Stacking:**
  Vertical stack. Tracker card below Fixed.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        انتخاب <span class="text-solar-gold">سیستم ثابت یا متحرک</span> (ترکر)
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-10">
        <!-- Fixed Tilt -->
        <div class="glass-card p-8 rounded-2xl border border-solar-gold/30 transition-all hover:shadow-xl"
             aria-label="سازه ثابت (Fixed Tilt)">
          <span class="text-4xl mb-4">📐</span>
          <h3 class="font-bold text-xl text-pure-white mb-3">سازه ثابت (Fixed Tilt)</h3>
          <ul class="space-y-2 text-pure-white/80 text-sm">
            <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> هزینه پایین‌تر (CAPEX)</li>
            <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> بدون قطعه متحرک (OPEX صفر)</li>
            <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> مناسب پشت‌بام، سقف سوله، زمین</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> خردروترین برای پوشش ۱ تا ۱۰۰ کیلوات</li>
          </ul>
        </div>
        <!-- Solar Tracker -->
        <div class="glass-card p-8 rounded-2xl border border-eco-green/30 bg-eco-green/10 transition-all hover:shadow-xl hover:border-eco-green/50"
             aria-label="سازه ردیاب خورشیدی (Solar Tracker)">
          <span class="text-4xl mb-4">🌞</span>
          <h3 class="font-bold text-xl text-eco-green mb-3">سازه ردیاب (Solar Tracker)</h3>
          <ul class="space-y-2 text-pure-white/80 text-sm">
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> افزایش ۱۵-۲۵٪ تولید انرژی</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> ردیابی تک‌محوره / دو‌محوره</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> مناسب نیروگاه‌های مگاواتی روی زمین</li>
            <li class="flex items-center gap-2"><span class="text-alert-red">⚠️</span> نیاز به نگهداری مکانیکی / OPEX بالاتر</li>
          </ul>
        </div>
      </div>
      <div class="text-start max-w-3xl mx-auto mt-10">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">چه زمانی ترکر انتخاب می‌شود؟</h3>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
        </p>
        <a href="/pricing/industrial-power-plants"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors"
           role="button"
           aria-label="مطالعه طرح توجیهی نیروگاه‌های مگاواتی برای ترکر">
          مشاهده طرح توجیهی نیروگاه‌های مگاواتی
          <svg class="w-5 h-5"><!-- Arrow --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_10]: بخش پاسخ به سوالات متداول سازه‌ای (FAQ - SGE Bait)

- **Section Role:** GEO/SGE bait — FAQPage schema.

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
        سوالات متداول <span class="text-solar-gold">سازه‌های نصب پنل خورشیدی</span>
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
              آیا می‌توان پنل خورشیدی را روی سقف شیروانی که شیب آن رو به شمال است نصب کرد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، نصب پنل مستقیماً روی ضلع شمالی سقف شیب‌دار به شدت باعث افت راندمان می‌شود (چون نور جنوب را از دست می‌دهد). در این موارد، مهندسین ما با ساخت استراکچرهای معکوس (Reverse Tilt)، زاویه پنل‌ها را برخلاف شیب سقف اصلاح کرده و رو به جنوب تنظیم می‌کنند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              فاصله ردیف‌های پنل چقدر باید باشد تا روی هم سایه نیندازند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در سقف‌های تخت و زمین‌ها، باید بین هر ردیف از استراکچرها فاصله مشخصی (Pitch) لحاظ شود تا سایه ردیف جلو در روزهای کوتاه زمستان (که خورشید در پایین‌ترین زاویه است) روی ردیف عقب نیفتد. این فاصله توسط نرم‌افزار PVSYST به دقت محاسبه می‌شود تا از اتلاف فضای زمین جلوگیری گردد.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا می‌توان پنل‌ها را روی سقف‌های شیروانی و سفالی نصب کرد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، هورا نور سهند با استفاده از استراکچرها و یراق‌آلات مخصوص آلومینیومی (Roof Hooks)، پنل‌ها را بدون آسیب به عایق‌بندی، روی سقف‌های شیروانی نصب می‌کند.
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

### [SEC_11]: درخواست بازدید حضوری و کارشناسی سقف (CTA)

- **Section Role:** CRO conversion — Structural safety CTA.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. "Engineering Inspection" badge.

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
          طراحی ایمن، کلید دوام <span class="text-deep-navy">نیروگاه خورشیدی شماست</span>
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_11}
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
        <a href="https://wa.me/989125728170?text=درخواست%20کارشناسی%20سازه%20فنی"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="درخواست کارشناسی استراکچر فنی در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
          درخواست کارشناسی استراکچر
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
  - External links `rel="noopener"`.

---

[VERIFIED_UI_END_OF_FILE]