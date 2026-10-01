# UI Wireframe Specification: فروش تضمینی برق به ساتبا | قرارداد ۲۰ ساله | هورا نور سهند
- **Source Dossier:** `seo_dossiers/investment_satba-guaranteed-purchase.md`
- **Target URL:** `/investment/satba-guaranteed-purchase`
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

### [SEC_01]: راهنمای قرارداد خرید تضمینی ۲۰ ساله برق ساتبا و نرخ تعرفه‌ها

- **Section Role:** Primary Hero — H1 entity, investment promise, government guarantee trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a cinematic handshake overlay: a solar panel graphic merging with a government building silhouette, handshake glowing `solar-gold`. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). Trust badges row (Ministry of Energy, SATBA, E-Namad) prominently below H1. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-satba-handshake.webp"
         alt="دست‌دهی متقابل: پنل خورشیدی و ساختمان وزارت نیرو — قرارداد ۲۰ ساله ساتبا"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          قرارداد ۲۰ ساله | تضمین دولتی | معاف از تورم
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          راهنمای قرارداد خرید تضمینی <span class="text-solar-gold">۲۰ ساله برق ساتبا</span> و نرخ تعرفه‌ها
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره سرمایه‌گذاری و قرارداد ساتبا">
          مشاوره سرمایه‌گذاری
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
  - Hero `alt` in Farsi describing handshake + solar panel + government building.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: نحوه دسته‌بندی نیروگاه‌ها و جدول نرخ خرید برق خورشیدی

- **Section Role:** Pricing structure explainer — Tiered rate table, Information Gain.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Tiered table: three brackets (<20kW, 20-200kW, >1MW). Each bracket a glass card with `border-s-4` in bracket color (small: `eco-green`, medium: `solar-gold`, large: `alert-red`). "Smaller = Higher Rate" highlighted with `solar-gold` badge.

- **Desktop Grid Architecture:**
  12-col. Tier cards: `lg:grid-cols-3 gap-6`. Text block below: `lg:col-span-12`.

- **Mobile Stacking:**
  Tier cards stack vertically. Table scrolls horizontally.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        نحوه دسته‌بندی نیروگاه‌ها و <span class="text-solar-gold">جدول نرخ خرید برق خورشیدی</span>
      </h2>
      <!-- Tier Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12">
        <!-- Tier 1: Residential -->
        <div class="glass-card p-6 border-s-4 border-eco-green rounded-2xl transition-all hover:shadow-xl hover:border-eco-green/50"
             aria-label="دسته انشعابی خرد: زیر ۲۰ کیلووات">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🏠</span>
            <div>
              <h3 class="font-bold text-xl text-eco-green">انشعابی خرد (زیر ۲۰ kW)</h3>
              <p class="text-pure-white/70 text-sm">خانگی / ویلا / مسکونی</p>
            </div>
          </div>
          <span class="inline-block bg-eco-green/20 text-eco-green text-sm font-bold px-3 py-1 rounded-full mb-4">بالاترین نرخ خرید</span>
          <p class="text-pure-white/80 text-sm leading-relaxed">
            مناسب برای ویلاها، خانه‌های باغ، واحدهای مسکونی. دولت خریداری برق با بالاترین نرخ پایه برای تشویق شهروندان.
          </p>
        </div>
        <!-- Tier 2: Commercial/Industrial -->
        <div class="glass-card p-6 border-s-4 border-solar-gold rounded-2xl transition-all hover:shadow-xl hover:border-solar-gold/50"
             aria-label="دسته انشعابی متوسط: ۲۰ تا ۲۰۰ کیلووات">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🏢</span>
            <div>
              <h3 class="font-bold text-xl text-solar-gold">انشعابی متوسط (۲۰ تا ۲۰۰ kW)</h3>
              <p class="text-pure-white/70 text-sm">تجاری / سوله / کارگاه</p>
            </div>
          </div>
          <span class="inline-block bg-solar-gold/20 text-solar-gold text-sm font-bold px-3 py-1 rounded-full mb-4">نرخ پایه متوسط</span>
          <p class="text-pure-white/80 text-sm leading-relaxed">
            مناسب برای سوله‌های صنعتی، مراکز تجاری، کارگاه‌ها. نرخ پایه متناسب با سرمایه‌گذاری‌های متوسط.
          </p>
        </div>
        <!-- Tier 3: Industrial/Mega -->
        <div class="glass-card p-6 border-s-4 border-alert-red rounded-2xl transition-all hover:shadow-xl hover:border-alert-red/50"
             aria-label="دسته نیروگاه‌های مگاواتی: بالای ۱ مگاوات">
          <div class="flex items-center gap-3 mb-4">
            <span class="text-4xl">🏭</span>
            <div>
              <h3 class="font-bold text-xl text-alert-red">نیروگاه‌های مگاواتی (بالای ۱ MW)</h3>
              <p class="text-pure-white/70 text-sm">صنعتی / بایر / مگاواتی</p>
            </div>
          </div>
          <span class="inline-block bg-alert-red/20 text-alert-red text-sm font-bold px-3 py-1 rounded-full mb-4">نرخ پایه پایین‌تر</span>
          <p class="text-pure-white/80 text-sm leading-relaxed">
            مناسب برای سرمایه‌گذاری‌های کلان صنعتی، زمین‌های بایر، نیروگاه‌های مگاواتی. نرخ پایه پایین‌تر اما حجم درآمد بالا.
          </p>
        </div>
      </div>
      <!-- Explanatory Text -->
      <div class="text-start max-w-3xl mx-auto">
        <h3 class="font-bold text-xl text-pure-white mb-4 text-start">چرا پکیج‌های کوچک‌تر نرخ بالاتر دارند؟</h3>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
          <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی</p>
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
  - Tier cards have `aria-label` describing bracket.
  - Color + text for meaning.

---

### [SEC_03]: مصونیت در برابر تورم با مکانیسم "ضریب تعدیل"

- **Section Role:** Economic trust builder — Inflation hedge visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Dual-line animated chart: X-axis = Years (1-20), Y-axis = Value. Inflation line: `alert-red` dashed, trending up. Revenue line: `eco-green` solid, moving in parallel, always above. "Anti-Inflation Guarantee" badge `bg-eco-green text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Chart: `lg:col-span-7 lg:sticky lg:top-20`. Text: `lg:col-span-5`.

- **Mobile Stacking:**
  Chart first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy" x-data="{ chartLoaded: false }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-7 lg:sticky lg:top-20" aria-label="نمودار موازی تورم و درآمد ساتبا" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">ضریب تعدیل (Adjustment Factor) — تضمین ضد تورم</h3>
          <div class="relative h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 600 300" class="w-full h-full" role="img" aria-label="نمودار موازی تورم (قرمز) و درآمد ساتبا (سبز) در ۲۰ سال">
              <!-- Axes -->
              <line x1="50" y1="250" x2="550" y2="250" stroke="#FFFFFF" stroke-width="1"/>
              <line x1="50" y1="250" x2="50" y2="20" stroke="#FFFFFF" stroke-width="1"/>
              <!-- Inflation Line (Red Dashed) -->
              <path d="M50,250 Q150,200 300,100 T550,20" stroke="#E74C3C" stroke-width="3" fill="none" stroke-dasharray="8,8" marker-end="url(#arrowhead)"/>
              <!-- Revenue Line (Green Solid) -->
              <path d="M50,250 Q150,220 300,80 T550,40" stroke="#2ECC71" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
              <!-- Defs for arrows -->
              <defs>
                <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
                  <polygon points="0 0, 10 3.5, 0 7" fill="#2ECC71" />
                </marker>
              </defs>
            </svg>
            <!-- Legend -->
            <div class="flex justify-center gap-6 mt-4 text-sm">
              <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-alert-red"></span> تورم (CPI + ارز)</span>
              <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-eco-green"></span> درآمد ساتبا (منحنی صعودی موازی)</span>
            </div>
          </div>
          <div class="mt-4 text-center">
            <span class="inline-flex items-center gap-2 bg-eco-green text-deep-navy text-sm font-bold rounded-full px-3 py-1">
              تضمین ضد تورم (Anti-Inflation Guarantee)
            </span>
          </div>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مصونیت در برابر <span class="text-alert-red">تورم</span> با مکانیسم <span class="text-solar-gold">ضریب تعدیل</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-eco-green/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین ضد تورم</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Chart `role="img"` + `aria-label`.
  - Color + text labels for lines.
  - Animation respects `prefers-reduced-motion`.

---

### [SEC_04]: باورهای غلط درباره قراردادهای دولتی (Myth vs. Reality)

- **Section Role:** Myth-busting — Government default risk vs Budget guarantee.

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
        باورهای غلط درباره <span class="text-solar-gold">قراردادهای دولتی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            دولت پس از چند سال قرارداد خرید برق را یک‌طرفه لغو می‌کند یا پول برق را نمی‌دهد.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت حقوقی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            قراردادهای ساتبا تضمین حاکمیتی دارند. منبع مالی: "عوارض برق" روی ۸۰ میلیون قبض برق کل کشور. این مبلغ مستقیماً به حساب ساتبا واریز شده و شرعاً و قانوناً فقط برای پرداخت نیروگاه‌های تجدیدپذیر تخصیص می‌یابد. سابقه پرداخت‌ها: مستمر و بدون لغو قراردادی.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ اطمینان حقوقی</p>
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

### [SEC_05]: مراحل ثبت نام برق خورشیدی (سامانه مهرسان)

- **Section Role:** Procedural guide — 5-step timeline.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Horizontal timeline with 5 nodes: Step 1 (Mehrsan Registration), Step 2 (Inspection), Step 3 (PPA Contract), Step 4 (EPC Installation), Step 5 (Profit). Nodes: glass cards with `border-s-2 border-solar-gold`. Animated connecting lines (`stroke-solar-gold` dash animation).

- **Desktop Grid Architecture:**
  Single row horizontal timeline `flex gap-4 overflow-x-auto snap-x snap-mandatory`. Each step: `min-w-[240px] snap-center`.

- **Mobile Stacking:**
  Horizontal scroll strip `snap-x snap-mandatory`. Each step `min-w-[280px] snap-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy" x-data="{ currentStep: 1 }">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        مراحل ثبت نام برق خورشیدی در <span class="text-solar-gold">سامانه مهرسان</span>
      </h2>
      <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">1️⃣</span>
          <h4 class="font-bold text-pure-white text-lg">ثبت‌نام در مهرسان</h4>
          <p class="text-pure-white/60 text-sm mt-1">پورتال ملی نیروگاه‌های تجدیدپذیر</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">2️⃣</span>
          <h4 class="font-bold text-pure-white text-lg">بازرسی سایت</h4>
          <p class="text-pure-white/60 text-sm mt-1">بازرسی ظرفیت کنتور و استحکام بنا</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">3️⃣</span>
          <h4 class="font-bold text-pure-white text-lg">امضای قرارداد PPA</h4>
          <p class="text-pure-white/60 text-sm mt-1">عقد قرارداد ۲۰ ساله با ساتبا</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">4️⃣</span>
          <h4 class="font-bold text-pure-white text-lg">اجرا و نصب (EPC)</h4>
          <p class="text-pure-white/60 text-sm mt-1">نصب پنل، اینورتر، اتصال به شبکه</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">5️⃣</span>
          <h4 class="font-bold text-pure-white text-lg">سود و درآمد</h4>
          <p class="text-pure-white/60 text-sm mt-1">دریافت درآمد ۲۰ ساله</p>
        </div>
      </div>
      <div class="text-start max-w-3xl mx-auto mt-10">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">جزئیات مراحل اداری</h3>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ پیگیری صفر تا صد</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="مراحل ثبت‌نام در سامانه مهرسان"`.
  - `snap-x` for keyboard navigation.
  - Steps have semantic structure.

---

### [SEC_06]: نقش کنتورهای دوطرفه (طرح فهام)

- **Section Role:** Technical explainer — Smart meter diagram.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Central smart meter illustration (SVG) with two flow arrows: IN (consumption, `alert-red`) and OUT (export, `eco-green`). Two register displays. Glass card container.

- **Desktop Grid Architecture:**
  12-col. Meter visual: `lg:col-span-5 lg:sticky lg:top-20`. Text: `lg:col-span-7`.

- **Mobile Stacking:**
  Meter visual first (`h-[300px]`). Text below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-5 lg:sticky lg:top-20" aria-label="نمودار کنتور دوطرفه طرح فهام" role="img">
        <div class="glass-card p-8 flex flex-col items-center justify-center">
          <div class="relative w-[300px] h-[300px] mx-auto">
            <svg viewBox="0 0 300 300" class="w-full h-auto" role="img" aria-label="نمودار کنتور دوطرفه طرح فهام: جریان ورودی مصرف و جریان خروجی صادرات">
              <!-- Meter Body -->
              <rect x="50" y="50" width="200" height="200" rx="10" fill="#132F4C" stroke="#F5A623" stroke-width="2"/>
              <!-- Display -->
              <rect x="75" y="70" width="150" height="80" rx="5" fill="#0A1929" stroke="#F5A623" stroke-width="1"/>
              <text x="150" y="95" text-anchor="middle" fill="#F5A623" font-size="14" font-family="monospace" font-weight="bold">FAHAM</text>
              <text x="150" y="120" text-anchor="middle" fill="#FFFFFF" font-size="12" font-family="monospace">POSE: 12345 kWh</text>
              <text x="150" y="140" text-anchor="middle" fill="#2ECC71" font-size="12" font-family="monospace">NEGET: 45678 kWh</text>
              <!-- OUT Arrow (Export) -->
              <path d="M250,150 Q280,130 300,100" stroke="#2ECC71" stroke-width="3" fill="none" marker-end="url(#arrow-out)"/>
              <text x="305" y="100" text-anchor="start" fill="#2ECC71" font-size="14" font-weight="bold">⬆ صادرات (بيع)</text>
              <!-- IN Arrow (Import) -->
              <path d="M50,150 Q20,130 0,100" stroke="#E74C3C" stroke-width="3" fill="none" marker-end="url(#arrow-in)"/>
              <text x="-5" y="100" text-anchor="end" fill="#E74C3C" font-size="14" font-weight="bold">مصرف ⬇</text>
              <defs>
                <marker id="arrow-out" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
                  <polygon points="0 0, 10 3.5, 0 7" fill="#2ECC71"/>
                </marker>
                <marker id="arrow-in" markerWidth="10" markerHeight="7" refX="1" refY="3.5" orient="auto">
                  <polygon points="10 0, 0 3.5, 10 7" fill="#E74C3C"/>
                </marker>
              </defs>
            </svg>
          </div>
          <div class="flex justify-center gap-6 mt-6 text-sm">
            <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-alert-red"></span> مصرف (مصرفی)</span>
            <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-eco-green"></span> صادرات (فروش)</span>
          </div>
        </div>
      </div>
      <div class="lg:col-span-7 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          نقش <span class="text-solar-gold">کنتورهای دوطرفه</span> (طرح فهام)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">⚡ نکته فنی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Meter SVG `role="img"` + `aria-label`.
  - Color + text labels for flows.

---

### [SEC_07]: استقرار هورا نور سهند برای پیگیری پرونده‌های البرز و تهران

- **Section Role:** Local SEO anchor + proximity authority.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Interactive map with HQ pin at Karaj, pulse rings to Tavanir Alborz, Tehran distribution centers. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="نقشه استقرار هورا نور سهند و مراکز توزیع برق" role="img">
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d50000!2d50.9!3d35.8!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3f8d1e0000000000%3A0x0!2z2YbYsdin2KfZhdi4INin2YTYp9mE!5e0!3m2!1sfa!2sir!4v1"
                width="100%" height="400" style="border:0;" allowfullscreen="" loading="lazy"
                aria-label="موقعیت دفتر مرکزی هورا نور سهند در کرج و نزدیکی مراکز توزیع برق البرز و تهران"></iframe>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استقرار <span class="text-solar-gold">هورا نور سهند</span> برای پیگیری پرونده‌ها
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
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش اداری</p>
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

### [SEC_08]: مرجع رسمی قوانین و به‌روزرسانی‌ها (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (SATBA).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Trust badges grid. External link to `satba.gov.ir` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badges grid `grid-cols-3 gap-4`.

- **Mobile Stacking:**
  Badges `grid-cols-2`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مرجع رسمی قوانین و به‌روزرسانی‌ها
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://satba.gov.ir" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">سازمان ساتبا</a></h4>
          <p class="text-pure-white/60 text-sm">نرخ‌های ۱۴۰۳</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://moe.gov.ir" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">وزارت نیرو</a></h4>
          <p class="text-pure-white/60 text-sm">بخشنامه‌های ۱۴۰۳</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">📜</span>
          <h4 class="font-bold text-pure-white text-lg">اینماد / ساماندهی</h4>
          <p class="text-pure-white/60 text-sm">تأیید تجارت الکترونیک</p>
        </div>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
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

### [SEC_09]: گام اول: سنجش ظرفیت روی بام شما

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to calculator.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Single glass card with `border-b-4 border-solar-gold`. Internal link pill CTA.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Vertical stack.

- **Mobile Stacking:**
  CTA `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        گام اول: سنجش <span class="text-solar-gold">ظرفیت روی بام شما</span>
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
        </p>
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 ابزار دقیق</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
          </p>
        </div>
        <a href="/pricing/solar-calculator"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="محاسبه‌گر آنلاین برق خورشیدی — سنجش دقیق ظرفیت سقف">
          استفاده از ابزار محاسبه‌گر ظرفیت
          <svg class="w-5 h-5"><!-- Calculator --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - CTA `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile for touch target.

---

### [SEC_10]: بخش پاسخ به سوالات متداول درباره ساتبا (FAQ)

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
        سوالات متداول <span class="text-solar-gold">قرارداد ساتبا</span>
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
              پول فروش برق هر چند وقت یک‌بار واریز می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            سازمان ساتبا بر اساس قرائت‌های دوماهه کنتور شما توسط شرکت توزیع منطقه، صورت‌حساب‌ها را تایید کرده و مبلغ ریالی را مستقیماً به شماره شبای معرفی‌شده در زمان ثبت‌نام (معمولاً هر ۴۵ الی ۶۰ روز یک‌بار) واریز می‌کند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا می‌توانم برق تولیدی را خودم در خانه مصرف کنم؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر. در قراردادهای انشعابی خرید تضمینی ساتبا، مکانیزم "خالص تزریق" (Feed-in Tariff) حاکم است. شما کل برق تولیدی را به شبکه دولت تزریق می‌کنید (با نرخ بسیار بالا می‌فروشید) و برای مصارف خانگی خود، برق یارانه‌ای و ارزان‌قیمت شبکه را طبق روال عادی مصرف می‌کنید. این مدل سودآورترین حالت برای شماست.
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

### [SEC_11]: مشاوره سرمایه‌گذاری و آغاز فرآیند اجرایی (CTA)

- **Section Role:** CRO conversion — Guaranteed investment pitch.

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
          بام شما، قرارداد ۲۰ ساله دولت، درآمدی تا ۲۵ سال
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
        <a href="https://wa.me/989125728170?text=مشاوره%20سرمایه‌گذاری%20ساتبا"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="مشاوره سرمایه‌گذاری ساتبا در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
          مشاوره سرمایه‌گذاری
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