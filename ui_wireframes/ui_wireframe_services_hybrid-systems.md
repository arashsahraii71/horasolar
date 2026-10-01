# UI Wireframe Specification: سیستم‌های برق خورشیدی هیبریدی | ترکیبی، هوشمند، مطمئن
- **Source Dossier:** `seo_dossiers/services_hybrid-systems.md`
- **Target URL:** `/services/hybrid-systems`
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

### [SEC_01]: اجرای سیستم‌های برق خورشیدی هیبریدی (ترکیب شبکه، باتری و ژنراتور)

- **Section Role:** Primary Hero — H1 entity definition, hybrid architecture visualization, EPC authority.

- **UI Aesthetic & Colors:**
  Full-viewport hero with cinematic split-exposure: left half shows sunrise over panels, right half shows grid connection + battery cabinet. A deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`) with an animated "energy flow" SVG line (dashed `stroke-solar-gold`) animating from Sun → Panels → Hybrid Inverter → Battery/Grid. Headline in `pure-white`, "Hybrid Architecture" badge in `solar-gold`. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-hybrid-architecture.webp"
         alt="معماری سیستم خورشیدی هیبریدی: پنل، شبکه، باتری و اینورتر هوشمند"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <!-- Animated Energy Flow SVG overlay -->
    <svg class="absolute inset-0 pointer-events-none" viewBox="0 0 1200 600" preserveAspectRatio="none">
      <defs>
        <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
          <polygon points="0 0, 10 3.5, 0 7" fill="#F5A623" />
        </defs>
        <path d="M100,300 Q300,150 500,300 T900,300" stroke="#F5A623" stroke-width="2" fill="none" stroke-dasharray="10,10" marker-end="url(#arrowhead)"
              style="animation: flow 4s linear infinite;">
          <animate attributeName="stroke-dashoffset" from="0" to="-20" dur="1s" repeatCount="indefinite"/>
        </path>
      </defs>
    </svg>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          معماری هیبریدی: شبکه + باتری + پنل
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          اجرای سیستم‌های <span class="text-solar-gold">برق خورشیدی هیبریدی</span> (ترکیب شبکه، باتری و ژنراتور)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره رایگان سیستم هیبریدی">
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
  - Hero `alt` in Farsi describing hybrid architecture.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: مکانیزم سوئیچینگ هوشمند و اینورترهای هیبریدی

- **Section Role:** Technical deep-dive — Smart Energy Manager logic, SGE step-by-step.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive priority ladder diagram: Solar → Load → Battery → Grid → Generator. Each rung is a glass card with `border-s-2 border-solar-gold` that highlights on scroll (IntersectionObserver). Active rung glows `ring-2 ring-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Priority ladder: `lg:col-span-5 lg:sticky lg:top-20`. Text: `lg:col-span-7`. Ladder rungs: Solar → Load → Battery → Grid → Generator.

- **Mobile Stacking:**
  Horizontal scroll strip (`overflow-x-auto snap-x`) for ladder. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ activeRung: 0 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-5 lg:sticky lg:top-20" aria-label="نمودار اولویت‌بندی انرژی در سیستم هیبریدی" role="img">
        <div class="glass-card p-8">
          <div class="flex flex-col gap-4 items-center" x-data="{ activeRung: 0 }">
            <div class="w-full rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeRung === 0 }">
              <span class="text-solar-gold font-black text-xl">☀️ اولویت ۱: پنل‌های خورشیدی</span>
              <p class="text-pure-white/70 text-sm mt-1">مصروف مستقیم + شارژ باتری</p>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeRung === 1 }">
              <span class="text-solar-gold font-bold text-lg">🏠 اولویت ۲: بار مصرفی (Load)</span>
              <p class="text-pure-white/70 text-sm mt-1">تلقیم مستقیم از پنل‌ها</p>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeRung === 2 }">
              <span class="text-solar-gold font-bold text-lg">🔋 اولویت ۳: باتری ذخیره‌ساز</span>
              <p class="text-pure-white/70 text-sm mt-1">مازاد تولید / پشتیبان قطعی</p>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeRung === 3 }">
              <span class="text-solar-gold font-bold text-lg">⚡ اولویت ۴: شبکه برق شهری</span>
              <p class="text-pure-white/70 text-sm mt-1">جبران کمبود / فروش مازاد</p>
            </div>
            <svg class="w-1 h-8"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': activeRung === 4 }">
              <span class="text-solar-gold font-bold text-lg">⛽ اولویت ۵: ژنراتور (اختیاری)</span>
              <p class="text-pure-white/70 text-sm mt-1">پشتیبان نهایی در قطعی طولانی</p>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-7 space-y-8 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مکانیزم <span class="text-solar-gold">سوئیچینگ هوشمند</span> و اینورترهای هیبریدی
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
  - `<article id="sec-02">`.
  - Ladder container `role="img"` + `aria-label`.
  - Each rung has text labels, color not sole meaning carrier.

---

### [SEC_03]: حل بحران‌های کشوری: قطعی برق و استهلاک ژنراتورها

- **Section Role:** Pain-point split view — Generator pain vs Hybrid freedom.

- **UI Aesthetic & Colors:**
  Split screen. Pain (start): `bg-navy-mid/90` with diesel generator noise visualization (audio waveform bars), `alert-red` accents. Freedom (end): `bg-deep-navy` with silent hybrid system glowing `eco-green`. Diagonal divider `skew-y-3`.

- **Desktop Grid Architecture:**
  12-col. Pain: `lg:col-span-6`. Freedom: `lg:col-span-6`. Both `min-h-[500px]`. GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Pain first (`h-[300px]`), then freedom. GEO between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/diesel-generator-crisis.webp" alt="ژنراتور دیزلی دودی، پرصدا و پرهزینه در زمان قطعی" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⛽</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">ژنراتور دیزلی: صدا، سوخت، استهلاک</h3>
          <p class="text-pure-white/60 mt-2 text-sm">هزینه روغن + سوخت + تعمیرات + صدا</p>
        </div>
      </div>
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/silent-hybrid-villa.webp" alt="ویلای آرام با سیستم هیبریدی خورشیدی" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⚡</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">هیبریدی خورشیدی: آرام، هوشمند، اتوماتیک</h3>
          <p class="text-pure-white/70 mt-2 text-sm">سوییچینگ ۲۰ میلی‌ثانیه / بدون صدا / بدون سوخت</p>
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
        حل بحران‌های کشوری: <span class="text-alert-red">قطعی برق</span> و <span class="text-alert-red">استحلاک ژنراتورها</span>
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
  - GEO card `border-2 border-solar-gold` for high contrast.

---

### [SEC_04]: واقعیت‌های مهندسی در برابر باورهای غلط (Myth vs. Reality)

- **Section Role:** Myth-busting — UPS vs Hybrid distinction.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth cards: `bg-alert-red/10 border-alert-red/30` with ❌. Reality: `bg-eco-green/10 border-eco-green/30` with ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` myth/reality pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair. Myth first (red), reality second (green).

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در <span class="text-solar-gold">سیستم‌های هیبریدی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8"
           x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            سیستم هیبریدی همان UPS است و در قطعی‌های طولانی کارایی ندارد.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            UPS تنها پشتیبان موقت (وابسته به شبکه برای شارژ) است. سیستم هیبریدی یک نیروگاه مستقل است: پنل‌ها باتری‌ها را با انرژی رایگان خورشید شارژ می‌کنند، وابستگی به شبکه صفر می‌شود. البرز با ۲۵۰ روز آفتابی، شارژ روزانه را تضمین می‌کند.
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
  - `<aside id="sec-04">`.
  - `x-intersect` for reveal (decorative).
  - Meaning via icon + text, not color alone.
  - Contrast: dark text on light cards.

---

### [SEC_05]: سخت‌افزار پروژه‌های هیبریدی (تجهیزات Tier-1)

- **Section Role:** E-E-A-T hardware authority — Hybrid Inverter + Gel Battery showcase.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Bento grid: large card (Hybrid Inverter + Battery bank), two small cards (Gel Battery closeup, Smart Monitor). Hover reveal captions. Brand logos on hover.

- **Desktop Grid Architecture:**
  Asymmetrical Bento: large `lg:col-span-8 lg:row-span-2`, two small `lg:col-span-4`. Specs table + GEO: `lg:col-span-8` / `lg:col-span-4`.

- **Mobile Stacking:**
  Carousel `snap-x snap-mandatory`, `w-[85vw]`. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> سیستم‌های هیبریدی
      </h2>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 mb-12" x-data="{ activeImage: null }">
        <div class="lg:col-span-8 lg:row-span-2 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[400px]"
             @mouseenter="activeImage = 1" @mouseleave="activeImage = null"
             role="figure" aria-label="اینورتر هیبریدی و بانک باتری ژل در اتاق فنی">
          <img src="/images/hybrid-inverter-gel-battery.webp" alt="اینورتر هیبریدی و بانک باتری ژل" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-6">
            <p class="text-pure-white font-bold text-lg">اینورتر هیبریدی + بانک باتری ژل Deep-Cycle</p>
          </div>
        </div>
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="باتری‌های ژل Deep-Cycle Vmax">
          <img src="/images/gel-battery-closeup.webp" alt="باتری‌های ژل Deep-Cycle" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">باتری ژل Deep-Cycle (چرخه عمر بالا)</p>
          </div>
        </div>
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="مانیتورینگ هوشمند اینورتر هیبریدی">
          <img src="/images/hybrid-monitor.webp" alt="مانیتورینگ هوشمند انرژی" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">مانیتورینگ هوشمند Real-time</p>
          </div>
        </div>
      </div>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
        <div class="lg:col-span-8 text-start">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقایسه تکنولوژی باتری برای سیستم‌های هیبریدی</h3>
          <table class="w-full min-w-[500px] text-sm" role="table" aria-label="مقایسه باتری ژل در برابر اسیدی در سیستم‌های هیبریدی">
            <thead>
              <tr class="bg-navy-mid text-solar-gold">
                <th scope="col" class="p-3 text-start rounded-s-lg">مشخصه</th>
                <th scope="col" class="p-3 text-start">Lead-Acid (اسیدی)</th>
                <th scope="col" class="p-3 text-start rounded-e-lg">Gel Deep-Cycle (ژل عمیق)</th>
              </tr>
            </thead>
            <tbody>
              <tr class="bg-deep-navy/60"><td class="p-3">چرخه عمر (DoD 50%)</td><td class="p-3 text-alert-red font-bold">۳۰۰–۵۰۰</td><td class="p-3 text-eco-green font-bold">۱۰۰۰–۱۵۰۰</td></tr>
              <tr class="bg-navy-mid/40"><td class="p-3">نیاز به نگهداری</td><td class="p-3 text-alert-red font-bold">بله (آب蒸馏/روغن)</td><td class="p-3 text-eco-green font-bold">بدون نگهداری</td></tr>
              <tr class="bg-deep-navy/60"><td class="p-3">عملکرد در دمای پایین</td><td class="p-3 text-alert-red font-bold">ضعیف</td><td class="p-3 text-eco-green font-bold">عالی</td></tr>
              <tr class="bg-navy-mid/40"><td class="p-3">خطر نشت/گاز</td><td class="p-3 text-alert-red font-bold">بله (هیدروژن)</td><td class="p-3 text-eco-green font-bold">خیر (مُهر شده)</td></tr>
              <tr class="bg-deep-navy/60"><td class="p-3">عمر مفید در هیبریدی</td><td class="p-3 text-alert-red font-bold">۱–۲ سال</td><td class="p-3 text-eco-green font-bold">۵–۷ سال</td></tr>
            </tbody>
          </table>
        </div>
        <div class="lg:col-span-4 glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `role="figure"` + `aria-label` on image cards.
  - `loading="lazy"` on gallery images.
  - `<table role="table">` + `aria-label` + `scope="col"` on `<th>`.

---

### [SEC_06]: انطباق با استانداردها و لینک‌های مرجع (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust entities.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Trust badges grid. External link to `moe.gov.ir` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badges grid `grid-cols-3 gap-4`.

- **Mobile Stacking:**
  Badges `grid-cols-2`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          انطباق با استانداردها و دستورالعمل‌های نهادهای دولتی
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg">سازمان ساتبا</h4>
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
        {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
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

### [SEC_07]: تمرکز جغرافیایی پشتیبانی ما در استان البرز

- **Section Role:** Local SEO map anchor + proximity authority.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. SVG map of Alborz with gold pulse dots at Karaj HQ, Kordan, Mehrshahr, Hashtgerd, Eshtehard. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="نقشه پوشش سیستم‌های هیبریدی هورا نور سهند" role="img">
        <img src="/images/hybrid-coverage-map.svg" alt="نقشه پوشش سیستم‌های هیبریدی: کرج، کردان، مهرشهر، هشتگرد، اشتهارد" class="w-full h-auto" loading="lazy">
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مناطق تحت پوشش <span class="text-solar-gold">هورا نور سهند</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش محلی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
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

### [SEC_08]: سرمایه‌گذاری و توجیه اقتصادی

- **Section Role:** Value prop + internal link to calculator.

- **UI Aesthetic & Colors:**
  `bg-deep-navy` → `bg-navy-mid` gradient. Timeline: Year 0 → Year 3-5 break-even (`eco-green`) → Year 25 profit (`solar-gold`). Bars: `eco-green` for savings.

- **Desktop Grid Architecture:**
  12-col. Chart: `lg:col-span-7` (`rounded-e-3xl`). Text: `lg:col-span-5` (`rounded-s-3xl`).

- **Mobile Stacking:**
  Chart horizontal scroll. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-gradient-to-b from-deep-navy to-navy-mid" x-data="{ showDetails: false }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <div class="lg:col-span-7 glass-card rounded-e-3xl p-8 overflow-x-auto">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">زمان‌بندی بازگشت سرمایه (۲۵ سال)</h3>
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="زمان‌بندی بازگشت سرمایه سیستم هیبریدی">
          <thead><tr class="bg-navy-mid text-solar-gold">
            <th scope="col" class="p-3 text-start rounded-s-lg">مرحله</th>
            <th scope="col" class="p-3 text-start rounded-e-lg">وضعیت مالی</th>
          </tr></thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">سال ۰</td><td class="p-3 text-alert-red font-bold">سرمایه‌گذاری اولیه</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">سال ۱-۲</td><td class="p-3 text-solar-gold font-bold">تولید و درآمدزایی / حذف هزینه ژنراتور</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">سال ۳-۵</td><td class="p-3 text-eco-green font-bold text-lg">نقطه تعادل (Break-even)</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">سال ۶-۲۵</td><td class="p-3 text-eco-green font-bold">سود خالص تجمعی</td></tr>
          </tbody>
        </table>
        <button @click="showDetails = !showDetails" class="mt-4 text-solar-gold underline text-sm"
                :aria-expanded="showDetails" aria-controls="roi-details">
          جزئیات محاسبات
        </button>
        <div x-show="showDetails" x-collapse id="roi-details" class="mt-4 text-pure-white/70 text-sm">
          محاسبه بر اساس حذف هزینه سوخت ژنراتور (میانگین ۱۵۰ میلیون تومان/سال)، بازگشت سرمایه ۳ تا ۵ ساله.
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          سرمایه‌گذاری <span class="text-solar-gold">مطمئن</span> با بازگشت <span class="text-eco-green">۳ تا ۵ ساله</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <a href="/pricing/solar-calculator"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           aria-label="محاسبه‌گر آنلاین سرمایه‌گذاری هیبریدی">
          محاسبه سرمایه‌گذاری
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `scope="col"` on `<th>`.
  - Toggle button `:aria-expanded` + `aria-controls`.

---

### [SEC_09]: بخش پاسخ به سوالات متداول (FAQ)

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
        سوالات متداول <span class="text-solar-gold">سیستم‌های هیبریدی</span>
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
              آیا سیستم هیبریدی هنگام قطع برق چشمک می‌زند یا وقفه دارد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر، اینورترهای هیبریدی دارای زمان سوئیچینگ (Transfer Time) کمتر از ۱۰ الی ۲۰ میلی‌ثانیه هستند. تجهیزات حساس مانند کامپیوترها و سرورها بدون وقفه کار می‌کنند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              تفاوت اصلی سیستم هیبریدی با سیستم‌های آفگرید چیست؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            سیستم آفگرید هیچ اتصالی به شبکه شهر ندارد. سیستم هیبریدی هوشمندانه از برق شهر نیز کمک می‌گیرد؛ در کمبود نور آفتاب، باتری‌ها را با برق شهر در ساعت‌های ارزان‌شب شارژ می‌کند تا همیشه فول باشد.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا سیستم هیبریدی می‌تواند جایگزین کامل ژنراتور شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. با سوئیچینگ کمتر از ۲۰ میلی‌ثانیه، باتری‌های ژل عمیق و اینورترهای هوشمند، سیستم هیبریدی بهترین جایگزین بی‌صدا، بدون سوخت و اتوماتیک برای دیزل ژنراتورها است.
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

### [SEC_10]: شروع طراحی و برآورد فنی سیستم شما (Call to Action)

- **Section Role:** CRO conversion — NAP + high-contrast.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. Messenger icons `w-16 h-16`. Grain overlay.

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
          همین امروز، انرژی ویلا یا کارخانه خود را با سیستم هیبریدی تضمین کنید
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_10}
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
        <p class="text-deep-navy font-bold text-lg">ارتباط از طریق پیام‌رسان‌های محلی:</p>
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