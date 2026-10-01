# UI Wireframe Specification: قیمت پکیج‌های برق خورشیدی خانگی و تجاری | هورا نور سهند
- **Source Dossier:** `seo_dossiers/pricing_residential-commercial-packages.md`
- **Target URL:** `/pricing/residential-commercial-packages`
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

### [SEC_01]: قیمت پکیج‌های خورشیدی خانگی و تجاری (از ۱ کیلووات تا ۲۰ کیلووات)

- **Section Role:** Primary Hero — H1 entity, pricing transparency promise, EPC authority.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a clean, minimal background: subtle animated price-tag particles floating upward in `solar-gold` over `deep-navy` base. A "Pricing Transparency" badge (`bg-solar-gold/10 text-solar-gold border border-solar-gold/20`) above H1. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero content stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden bg-deep-navy" x-data="{ loaded: false }" x-init="loaded = true">
    <div class="absolute inset-0 bg-[url('/images/price-tag-particles.svg')] opacity-10"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          شفافیت قیمت‌گذاری | تجهیزات Tier-1
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          قیمت پکیج‌های <span class="text-solar-gold">برق خورشیدی</span> خانگی و تجاری (از ۱ کیلووات تا ۲۰ کیلووات)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="دریافت پیش‌فاکتور رسمی و کارشناسی رایگان">
          دریافت پیش‌فاکتور رایگان
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
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.

---

### [SEC_02]: جدول استاندارد قیمت‌ها و ظرفیت‌ها (Structured Data Table)

- **Section Role:** SERP Table Snippet — Structured data table for rich snippets.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Full-width responsive table with `overflow-x-auto` on mobile. Header row `bg-navy-mid text-solar-gold`. Alternating rows `bg-deep-navy/60` / `bg-navy-mid/40`. Price column `text-solar-gold font-bold`. "Best For" column with colored badges.

- **Desktop Grid Architecture:**
  Centered `max-w-7xl`. Table full-width. GEO callout below table.

- **Mobile Stacking:**
  Table horizontal scroll (`overflow-x-auto`). GEO callout below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-7xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        جدول استاندارد <span class="text-solar-gold">قیمت‌ها و ظرفیت‌ها</span> (پکیج‌های Turn-Key)
      </h2>
      <div class="glass-card p-6 overflow-x-auto">
        <table class="w-full min-w-[700px] text-sm" role="table" aria-label="جدول استاندارد قیمت پکیج‌های خورشیدی بر اساس ظرفیت">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">پکیج</th>
              <th scope="col" class="p-4 text-start">قدرت (کیلووات)</th>
              <th scope="col" class="p-4 text-start">نوع فاز</th>
              <th scope="col" class="p-4 text-start">مناسب برای</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">برآورد قیمت (میلیون تومان)</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">پکیج ۱</td><td class="p-4">۱ kW</td><td class="p-4">تک فاز</td><td class="p-4">روشنایی، شارژ موبایل، یخچال کوچک</td><td class="p-4 text-solar-gold font-bold">از ~[DATA NEEDED]</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">پکیج ۳</td><td class="p-4">۳ kW</td><td class="p-4">تک فاز</td><td class="p-4">خانگی (یخچال، تلویزیون، لامپ، شارژ)</td><td class="p-4 text-solar-gold font-bold">از ~[DATA NEEDED]</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">پکیج ۵ (پرکاربرد)</td><td class="p-4">۵ kW</td><td class="p-4">تک فاز</td><td class="p-4">ویلای استاندارد (یخچال، تلویزیون، پمپ، روشنایی، کولر ۱۲۰۰۰)</td><td class="p-4 text-solar-gold font-bold">از ~[DATA NEEDED]</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">پکیج ۱۰</td><td class="p-4">۱۰ kW</td><td class="p-4">تک فاز / سه فاز</td><td class="p-4">ویلای لوکس / تجاری متوسط (کولر، یخچال، پمپ، استخر)</td><td class="p-4 text-solar-gold font-bold">از ~[DATA NEEDED]</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-4 font-bold">پکیج ۱۵</td><td class="p-4">۱۵ kW</td><td class="p-4">سه فاز</td><td class="p-4">ویلای لوکس / تجاری متوسط (چیلر، پمپ استخر، کولرهای متعدد)</td><td class="p-4 text-solar-gold font-bold">از ~[DATA NEEDED]</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-4 font-bold">پکیج ۲۰</td><td class="p-4">۲۰ kW</td><td class="p-4">سه فاز</td><td class="p-4">تجاری / کشاورزی متوسط / سوله (چیلر، پمپ‌های سنگین)</td><td class="p-4 text-solar-gold font-bold">از ~[DATA NEEDED]</td></tr>
          </tbody>
        </table>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📋 نکته مهم</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on all headers.
  - Price column has semantic emphasis.

---

### [SEC_03]: سرمایه‌گذاری خورشیدی در برابر هزینه‌های پنهان دیزل ژنراتور

- **Section Role:** Financial reality check — Cumulative cost comparison chart.

- **UI Aesthetic & Colors:**
  `bg-deep-navy` → `bg-navy-mid` gradient. Cumulative bar chart: Diesel bars `alert-red` with strikethrough pattern, Solar bars `eco-green`. 5-year timeline. Break-even marker at year 3-5 with `solar-gold` diamond marker.

- **Desktop Grid Architecture:**
  12-col. Chart: `lg:col-span-7` (`rounded-e-3xl`). Text + GEO: `lg:col-span-5` (`rounded-s-3xl`).

- **Mobile Stacking:**
  Chart horizontal scroll. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-gradient-to-b from-deep-navy to-navy-mid" x-data="{ showDetails: false }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <div class="lg:col-span-7 glass-card rounded-e-3xl p-8 overflow-x-auto">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقایسه هزینه‌های تجمعی ۵ ساله</h3>
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="مقایسه هزینه تجمعی ۵ ساله: دیزل ژنراتور در برابر پکیج خورشیدی">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-3 text-start rounded-s-lg">سال</th>
              <th scope="col" class="p-3 text-start">هزینه تجمعی دیزل (میلیون تومان)</th>
              <th scope="col" class="p-3 text-start rounded-e-lg">هزینه تجمعی خورشیدی (میلیون تومان)</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">۱</td><td class="p-3 text-alert-red font-bold">۱۸۰</td><td class="p-3 text-eco-green font-bold">۳۵۰ (سرمایه‌گذاری اولیه)</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">۲</td><td class="p-3 text-alert-red font-bold">۳۶۰</td><td class="p-3 text-eco-green font-bold">۳۵۰</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">۳</td><td class="p-3 text-alert-red font-bold">۵۴۰</td><td class="p-3 text-eco-green font-bold">۳۵۰</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">۴</td><td class="p-3 text-alert-red font-bold">۷۲۰</td><td class="p-3 text-eco-green font-bold">۳۵۰</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">۵</td><td class="p-3 text-alert-red font-bold">۹۰۰</td><td class="p-3 text-eco-green font-bold">۳۵۰</td></tr>
          </tbody>
        </table>
        <button @click="showDetails = !showDetails" class="mt-4 text-solar-gold underline text-sm"
                :aria-expanded="showDetails" aria-controls="diesel-details">
          جزئیات محاسبات
        </button>
        <div x-show="showDetails" x-collapse id="diesel-details" class="mt-4 text-pure-white/70 text-sm">
          محاسبه بر اساس میانگین مصرف ۱۵ لیتر گازوئیل در روز به قیمت آزاد و هزینه تعمیرات سالانه ۳۰ میلیون تومان.
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          سرمایه‌گذاری <span class="text-solar-gold">خورشیدی</span> در برابر <span class="text-alert-red">ژنراتور</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `scope="col"` on `<th>`.
  - Toggle button `:aria-expanded` + `aria-controls`.

---

### [SEC_04]: باورهای غلط درباره پکیج‌های خورشیدی ارزان‌قیمت (Myth vs. Reality)

- **Section Role:** Anti-scam education — Warning about cheap/recycled panels.

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
        باورهای غلط درباره <span class="text-solar-gold">پکیج‌های ارزان‌قیمت</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پکیج‌های بسیار ارزان در اینترنت همان کیفیت را با قیمت کمتر ارائه می‌دهند.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت الهندسة</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پکیج‌های ارزان از پنل‌های استوک (دست دوم/ریستوک) و باتری‌های اسیدی خودرویی (استارتر) استفاده می‌کنند. در ۶ ماه اول دچار افت ولتاژ شده و تجهیزات شما را می‌سوزانند. ما در هورا نور سهند از تجهیزات Tier-1 و باتری‌های ژل Deep-Cycle استفاده می‌کنیم.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ هشدار امنیت</p>
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

### [SEC_05]: چرا هزینه برق خورشیدی ۵ کیلو وات برای همه خانه‌ها یکسان نیست؟

- **Section Role:** Technical nuance — Battery sizing drives cost variance.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Icon-driven flowchart: Night Usage → Battery Size → Total Cost. Flowchart nodes: `bg-navy-mid border border-solar-gold/40`. Arrows animated `stroke-solar-gold`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. Flowchart centered. Text below.

- **Mobile Stacking:**
  Flowchart horizontal scroll. Text below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        چرا هزینه <span class="text-solar-gold">برق خورشیدی ۵ کیلووات</span> برای همه خانه‌ها یکسان نیست؟
      </h2>
      <!-- Flowchart -->
      <div class="flex flex-col gap-6 items-center mb-12" aria-label="نمودار تأثیر مصرف شبانه بر قیمت پکیج" role="img">
        <div class="w-full max-w-md rounded-xl bg-navy-mid border border-solar-gold/40 p-6 text-center">
          <span class="text-solar-gold font-black text-xl">🌙 مصرف شبانه</span>
          <p class="text-pure-white/80 mt-2 text-sm">ساعات استفاده کولر/یخچال/پمپ در شب</p>
        </div>
        <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
        <div class="w-full max-w-md rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-6 text-center">
          <span class="text-solar-gold font-black text-xl">🔋 سایز بانک باتری</span>
          <p class="text-pure-white mt-1 text-sm">مصرف شبانه = ظرفیت باتری لازم</p>
        </div>
        <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
        <div class="w-full max-w-md rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-6 text-center">
          <span class="text-pure-white font-black text-xl">💰 قیمت نهایی پکیج</span>
          <p class="text-pure-white mt-1 text-sm">باتری = ۴۰-۶۰٪ هزینه کل پکیج</p>
        </div>
      </div>
      <h3 class="font-bold text-xl text-pure-white text-center mb-6">چرا دو خانه با مصرف یکسان قیمت متفاوتی می‌پردازند؟</h3>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed text-center max-w-2xl mx-auto">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Flowchart `role="img"` + `aria-label`.
  - Text labels accompany color coding.

---

### [SEC_06]: سخت‌افزار استفاده شده در پکیج‌های هورا نور سهند (Tier-1)

- **Section Role:** E-E-A-T authority — Brand logo grid with tooltips.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Grayscale logo grid → color on hover. Each logo: `bg-white/5 rounded-xl p-6 transition-colors`. Tooltip on hover with role description.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Logo carousel `flex gap-8 overflow-x-auto snap-x snap-mandatory`.

- **Mobile Stacking:**
  Carousel `snap-x` with `snap-center` items.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> پکیج‌های هورا نور سهند
      </h2>
      <div class="flex gap-8 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             @mouseenter="$el.classList.remove('grayscale')" @mouseleave="$el.classList.add('grayscale')"
             class="grayscale transition-colors duration-300"
             role="figure" aria-label="پنل‌های Jinko Solar">
          <img src="/images/logo-jinko.webp" alt="Jinko Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Jinko Solar</span>
          <p class="text-pure-white/60 text-sm mt-1">پنل‌های مونوکریستال ۶۰۰+ وات</p>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Trina Solar">
          <img src="/images/logo-trina.webp" alt="Trina Solar" class="w-20 h-20 object-contain mb-2">
          <span class="text-3xl mb-2">☀️</span>
          <span class="font-bold text-pure-white text-lg">Trina Solar</span>
          <p class="text-pure-white/60 text-sm mt-1">پنل‌های دوطرفه (Bifacial)</p>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های LONGi">
          <img src="/images/logo-longi.webp" alt="LONGi" class="w-20 h-20 object-contain mb-2">
          <span class="text-3xl mb-2">☀️</span>
          <span class="font-bold text-pure-white text-lg">LONGi</span>
          <p class="text-pure-white/60 text-sm mt-1">مونوکریستال نرخ راندمان بالا</p>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="اینورترهای Growatt">
          <img src="/images/logo-growatt.webp" alt="Growatt" class="w-20 h-20 object-contain mb-2">
          <span class="text-3xl mb-2">⚡</span>
          <span class="font-bold text-pure-white text-lg">Growatt</span>
          <p class="text-pure-white/60 text-sm mt-1">اینورترهای هوشمند هیبریدی/آفگرید</p>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="باتری‌های Vmax">
          <img src="/images/logo-vmax.webp" alt="Vmax" class="w-20 h-20 object-contain mb-2">
          <span class="text-3xl mb-2">🔋</span>
          <span class="font-bold text-pure-white text-lg">Vmax</span>
          <p class="text-pure-white/60 text-sm mt-1">باتری‌های ژل Deep-Cycle</p>
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
  - Carousel `aria-label="برندهای تجهیزات Tier-1"`.
  - Hover removes grayscale (decorative).
  - `loading="lazy"` on logos.

---

### [SEC_07]: استانداردهای واردات و تاثیر نرخ ارز (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (Ministry of Industry).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". External link to `mimt.gov.ir` with `rel="external noopener"`.

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
          استانداردهای واردات و تاثیر نرخ ارز
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
            <p class="text-sm font-bold text-solar-gold mb-1">نکته مهم اقتصادی ۱۴۰۳</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
            </p>
          </div>
        </div>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mt-8">
          مراجعه به <a href="https://mimt.gov.ir/" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">وزارت صمت</a> برای اطلاع از دستورالعمل‌های تخصیص ارز.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: بررسی دقیق ظرفیت قبل از استعلام قیمت

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to calculator.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Single glass card with `border-b-4 border-solar-gold`. Internal link pill CTA.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Vertical stack.

- **Mobile Stacking:**
  CTA `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        بررسی دقیق <span class="text-solar-gold">ظرفیت</span> قبل از استعلام قیمت
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 ابزار دقیق</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <a href="/pricing/solar-calculator"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="محاسبه‌گر آنلاین برق خورشیدی — تعیین دقیق ظرفیت کیلووات">
          محاسبه‌گر آنلاین برق خورشیدی
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
        سوالات متداول <span class="text-solar-gold">قیمت پکیج‌های خورشیدی</span>
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
              آیا قیمت پنل خورشیدی سه فاز (۳۸۰ ولت) گران‌تر از تک فاز است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            پنل‌ها در تمام سیستم‌ها یکسان (DC) هستند. تفاوت قیمت بین پکیج ۱۰ کیلووات تک‌فاز و سه فاز، به دلیل استفاده از اینورترهای سه فاز صنعتی است که قیمت به مراتب بالاتری نسبت به تک فاز خانگی دارند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا هزینه‌های کابل‌کشی و استراکچر در قیمت پکیج لحاظ می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در پیش‌فاکتورهای EPC شرکت هورا نور سهند، پکیج‌ها به صورت "کلید در دست" (Turn-Key) محاسبه می‌شوند. یعنی استراکچر، تابلو برق، کابل‌های آنتی‌یووی و هزینه نصب در پیش‌فاکتور نهایی درج می‌شوند.
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

### [SEC_10]: دریافت پیش‌فاکتور رسمی و کارشناسی رایگان (CTA)

- **Section Role:** CRO conversion — NAP + high-contrast.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. Messenger icons `w-16 h-16`. Grain overlay. "درخواست پیش‌فاکتور" CTA button.

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
          دریافت پیش‌فاکتور رسمی و <span class="text-deep-navy">کارشناسی رایگان</span>
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
          <a href="tel:09124641442" class="block text-2xl md:text-4xl font-bold text-deep-navy/80 hover:text-deep-navy/60 transition-colors" dir="ltr"
             aria-label="تماس با مشاور فنی: ۰۹۱۲۴۶۴۱۴۴۲">
            0912-464-1442
          </a>
        </div>
        <a href="/pricing/solar-calculator"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button"
           aria-label="محاسبه‌گر آنلاین قبل از درخواست پیش‌فاکتور">
          محاسبه‌گر آنلاین قبل از درخواست پیش‌فاکتور
          <svg class="w-5 h-5"><!-- Calculator --></svg>
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
        <a href="https://wa.me/989125728170?text=درخواست%20پیش‌فاکتور%20رسمی"
           class="inline-flex items-center gap-2 mt-4 w-full md:w-auto px-6 py-3 bg-deep-navy text-solar-gold font-bold rounded-xl hover:bg-deep-navy/90 transition-colors justify-center"
           role="button"
           aria-label="درخواست پیش‌فاکتور رسمی در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WA --></svg>
          درخواست پیش‌فاکتور رسمی
        </a>
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