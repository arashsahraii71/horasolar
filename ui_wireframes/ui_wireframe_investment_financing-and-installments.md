# UI Wireframe Specification: پنل خورشیدی اقساطی | وام نیروگاه خورشیدی | هورا نور سهند
- **Source Dossier:** `seo_dossiers/investment_financing-and-installments.md`
- **Target URL:** `/investment/financing-and-installments`
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

### [SEC_01]: شرایط دریافت تسهیلات بانکی و خرید اقساطی تجهیزات خورشیدی

- **Section Role:** Primary Hero — H1 entity, financial intent, trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with subtle finance/solar blend: deep-navy base, animated floating chart bars (`solar-gold`) rising behind text. "تسهیلات مالی پروژه‌های خورشیدی" badge in `solar-gold`. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-finance-solar.webp"
         alt="نمادهای مالی و بانکی ادغام شده با پنل‌های خورشیدی — تسهیلات مالی پروژه‌های خورشیدی"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          تسهیلات مالی پروژه‌های خورشیدی
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          شرایط دریافت <span class="text-solar-gold">تسهیلات بانکی</span> و خرید <span class="text-solar-gold">اقساطی تجهیزات خورشیدی</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره تسهیلات بانکی و خرید اقساطی">
          مشاوره تسهیلات بانکی
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
  - Hero `alt` in Farsi describing finance + solar blend.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: فروش اقساطی پکیج‌های خورشیدی ویلایی (B2C)

- **Section Role:** Consumer solution — Installment breakdown visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Breakdown chart: two pie slices side-by-side (donut charts). "پیش‌پرداخت اولیه" slice: `solar-gold` (50-60%). "اقساط چند ماهه" slice: `eco-green`. Center text shows total package value. Glass card container.

- **Desktop Grid Architecture:**
  12-col. Chart: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Chart first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ total: 100, down: 55 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار دایره‌ای تقسیم پیش‌پرداخت و اقساط" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">تقسیم هزینه پکیج ویلایی</h3>
          <div class="relative w-[250px] h-[250px] mx-auto mb-6" x-data="{ start: 0 }" x-intersect.once="start = 1">
            <svg viewBox="0 0 200 200" class="w-full h-auto" role="img" aria-label="نمودار دایره‌ای تقسیم پیش‌پرداخت و اقساط">
              <path d="M100,100 L100,20 A90,90 0 0,1 190,100 L100,100 Z" fill="#F5A623" opacity="0.85">
                <animate attributeName="d" from="M100,100 L100,20 A90,90 0 0,1 100,20 L100,100 Z" to="M100,100 L100,20 A90,90 0 0,1 190,100 L100,100 Z" dur="1.5s" fill="freeze"/>
              </path>
              <path d="M100,100 L190,100 A90,90 0 0,1 10,190 L100,100 Z" fill="#2ECC71" opacity="0.85">
                <animate attributeName="d" from="M100,100 L190,100 A90,90 0 0,1 190,100 L100,100 Z" to="M100,100 L190,100 A90,90 0 0,1 10,190 L100,100 Z" dur="1.5s" fill="freeze"/>
              </path>
            </svg>
            <div class="absolute inset-0 flex items-center justify-center">
              <div class="text-center">
                <p class="text-2xl font-black text-solar-gold" x-text="down + '%'"></p>
                <p class="text-pure-white/70 text-xs">پیش‌پرداخت</p>
                <p class="text-eco-green text-xs mt-1" x-text="100 - down + '%'"></p>
                <p class="text-eco-green text-xs">اقساط</p>
              </div>
            </div>
          </div>
          <div class="flex flex-col gap-3 mt-6 text-sm">
            <div class="flex items-center gap-2"><span class="w-4 h-4 rounded-full bg-solar-gold"></span> پیش‌پرداخت: <span class="font-bold text-solar-gold" x-text="down + '%'"></span></div>
            <div class="flex items-center gap-2"><span class="w-4 h-4 rounded-full bg-eco-green"></span> اقساط: <span class="font-bold text-eco-green" x-text="100 - down + '%'"></span></div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          فروش اقساطی <span class="text-solar-gold">پکیج‌های ویلایی</span> (B2C)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 تقسیم بندی</p>
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
  - Chart `role="img"` + `aria-label`.
  - Chart animation respects `prefers-reduced-motion`.

---

### [SEC_03]: تسهیلات کلان صنعتی (وام‌های میلیاردی برای صنایع)

- **Section Role:** B2B financing — Corporate info box.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Info box: `bg-solar-gold/10 border border-solar-gold/20`. Header: "تسهیلات ویژه صنایع و کارخانجات". Document checklist list with check icons.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO callout below.

- **Mobile Stacking:**
  No change.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        تسهیلات کلان <span class="text-solar-gold">صنعتی</span> (وام‌های میلیاردی برای صنایع)
      </h2>
      <div class="glass-card p-8 border-t-4 border-solar-gold space-y-6">
        <h3 class="font-bold text-xl text-solar-gold mb-6 text-start">مدارک مورد نیاز برای اخذ تسهیلات صنعتی</h3>
        <ul class="space-y-4" role="list">
          <li class="flex items-start gap-3">
            <span class="w-6 h-6 flex-shrink-0 text-solar-gold">✅</span>
            <span class="text-pure-white/90">جواز کارخانه / مجوز فعالیت</span>
          </li>
          <li class="flex items-start gap-3">
            <span class="w-6 h-6 flex-shrink-0 text-solar-gold">✅</span>
            <span class="text-pure-white/90">شناسنامه تجاری / پروانه کسب</span>
          </li>
          <li class="flex items-start gap-3">
            <span class="w-6 h-6 flex-shrink-0 text-solar-gold">✅</span>
            <span class="text-pure-white/90">گزارش‌های مالیAudit شده (۳ سال اخیر)</span>
          </li>
          <li class="flex items-start gap-3">
            <span class="w-6 h-6 flex-shrink-0 text-solar-gold">✅</span>
            <span class="text-pure-white/90">مجوزهای محیط زیست و الکترونیکی</span>
          </li>
          <li class="flex items-start gap-3">
            <span class="w-6 h-6 flex-shrink-0 text-solar-gold">✅</span>
            <span class="text-pure-white/90">پیش‌فاکتور رسمی EPC (مهر شرکت گریددار)</span>
          </li>
        </ul>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
        <p class="text-sm font-bold text-solar-gold mb-1">🏭 اطلاعات کلیدی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - List `role="list"`.
  - Checkmarks decorative; text carries meaning.

---

### [SEC_04]: باورهای غلط در خصوص وام‌های خورشیدی (Myth vs. Reality)

- **Section Role:** Myth-busting — Interest rates vs Guaranteed SATBA income.

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
        باورهای غلط در خصوص <span class="text-solar-gold">وام‌های خورشیدی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            سود وام بانکی باعث می‌شود احداث نیروگاه خورشیدی توجیه اقتصادی خود را از دست بدهد.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت اقتصادی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            درآمد فروش تضمینی برق به ساتبا یا رفع جریمه بورس انرژی، به راحتی اقساط وام را پوشش داده و سود خالص ایجاد می‌کند. چک‌های دریافتی از ساتبا، نه تنها به طور کامل اقساط ماهانه بانک را پوشش می‌دهد (Self-liquidating)، بلکه از همان سال اول جریان نقدینگی مثبتی برای شما به جا می‌گذارد.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 منطق اقتصادی</p>
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

### [SEC_05]: طرح‌های حمایتی: برق خورشیدی کمیته امداد و روستایی

- **Section Role:** Social impact — Compassionate visual block.

- **UI Aesthetic & Colors:**
  `bg-eco-green/10` background. Warm, compassionate tone. Card with `bg-eco-green/20 border-eco-green/30`. Heart icon. "Social Responsibility" badge.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO callout.

- **Mobile Stacking:**
  No change.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-eco-green/10">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-8">
        طرح‌های حمایتی: <span class="text-eco-green">برق خورشیدی کمیته امداد و روستایی</span>
      </h2>
      <div class="glass-card p-8 border-s-4 border-eco-green mb-8">
        <span class="text-4xl mb-4">❤️</span>
        <h3 class="font-bold text-deep-navy text-xl mb-4">قدرت시킨‌سازی روستاییان با انرژی خورشیدی</h3>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
      </div>
      <div class="glass-card p-5 border-s-4 border-eco-green">
        <p class="text-sm font-bold text-eco-green mb-1">🤝 توانمندسازی اجتماعی</p>
        <p class="text-deep-navy/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic heading structure.
  - Color + text for meaning.

---

### [SEC_06]: نقش هورا نور سهند در صدور پیش‌فاکتور معتبر بانکی

- **Section Role:** E-E-A-T authority — Document showcase.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Image showcase: stamped engineering docs + proforma invoice + handshake. Glass cards for each doc type.

- **Desktop Grid Architecture:**
  12-col. Doc grid: `grid-cols-3 gap-4`. Image cards with hover zoom.

- **Mobile Stacking:**
  Carousel `snap-x snap-mandatory`, `min-w-[280px]`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        نقش هورا نور سهند در صدور <span class="text-solar-gold">پیش‌فاکتور معتبر بانکی</span>
      </h2>
      <div class="flex gap-8 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[280px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پیش‌فاکتور رسمی مهربندی شده">
          <img src="/images/doc-proforma.webp" alt="پیش‌فاکتور رسمی مهربندی شده با مهر شرکت" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
          <h4 class="font-bold text-pure-white text-lg">پیش‌فاکتور رسمی مهربندی شده</h4>
          <p class="text-pure-white/60 text-sm mt-1">مهر شرکت، برند Tier-1، تفکیک هزینه</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="مستندات مهندسی مهربندی شده">
          <img src="/images/doc-engineering.webp" alt="مستندات مهندسی مهربندی شده" class="w-full h-48 object-contain rounded-xl mb-3" loading="lazy">
          <h4 class="font-bold text-pure-white text-lg">مستندات مهندسی مهربندی شده</h4>
          <p class="text-pure-white/60 text-sm mt-1">تاییدیه توانیر، طرح điện، محاسبات</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="دست‌دادی mãos">
          <img src="/images/doc-handshake.webp" alt="دست‌دادی مذاکره با بانک" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
          <h4 class="font-bold text-pure-white text-lg">دست‌دادی مذاکره با بانک</h4>
          <p class="text-pure-white/60 text-sm mt-1">پیش‌فاکتور معتبر برای کمیته اعتباری</p>
        </div>
      </div>
      <div class="mt-8 glass-card p-5 border-s-4 border-solar-gold text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">📋 مستندات بانکی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="مستندات بانکی پیش‌فاکتور"`.
  - `loading="lazy"` on images.
  - Carousel keyboard navigable.

---

### [SEC_07]: بودجه و دستورالعمل‌های بانک مرکزی (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (Central Bank).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". External link to `cbi.ir` with `rel="external noopener"`.

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
          بودجه و دستورالعمل‌های بانک مرکزی
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
          مراجعه به <a href="https://cbi.ir/" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">بانک مرکزی جمهوری اسلامی ایران</a> برای اطلاع از دستورالعمل‌های تخصیص ارز.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: محاسبه قیمت و استخراج مبلغ مورد نیاز برای وام

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to pricing.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Single glass card with `border-b-4 border-solar-gold`. Internal link pill CTA to `/pricing/residential-commercial-packages`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Vertical stack.

- **Mobile Stacking:**
  CTA `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        محاسبه قیمت و استخراج مبلغ مورد نیاز برای <span class="text-solar-gold">وام</span>
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
        <a href="/pricing/residential-commercial-packages"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="مشاهده قیمت پکیج‌های ویلایی و تجاری برای تعیین مبلغ وام">
          مشاهده قیمت پکیج‌های ویلایی و تجاری
          <svg class="w-5 h-5"><!-- Calculator --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - CTA `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile.

---

### [SEC_09]: بخش پاسخ به سوالات متداول درباره وام خورشیدی (FAQ)

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
        سوالات متداول <span class="text-solar-gold">وام خورشیدی</span>
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
              برای خرید پنل خورشیدی قسطی از هورا نور به ضامن نیاز است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در طرح‌های خرید اقساطی درون‌شرکتی ما (برای بخشی از فاکتور)، ارائه چک‌های صیادی معتبر بنفش (ثبت شده در سامانه) که فاقد سابقه برگشتی باشند، به عنوان ضمانت اصلی کفایت می‌کند و نیازی به ضامن کارمند نیست.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              بازپرداخت وام‌های بانکی نیروگاه خورشیدی چند ساله است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            مدت زمان بازپرداخت بستگی به نوع خط اعتباری بانک دارد. وام‌های حمایتی (کمیته امداد) معمولاً با اقساط بلندمدت (۶۰ تا ۸۴ ماهه) و تنفس اولیه ارائه می‌شوند. وام‌های صنعتی و تجاری نیز بین ۳۶ تا ۶۰ ماه بازپرداخت دارند تا جریان درآمدی نیروگاه به خوبی پاسخگوی اقساط باشد.
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

### [SEC_10]: دریافت مشاوره اعتباری و صدور پیش‌فاکتور (CTA)

- **Section Role:** CRO conversion — Financial solutions CTA.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. "درخواست پیش‌فاکتور برای بانک" CTA button.

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
          همین امروز، قفل مالی پروژه خورشیدی خود را باز کنید
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
        <a href="/pricing/residential-commercial-packages"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button"
           aria-label="مشاهده قیمت پکیج‌ها برای تعیین مبلغ وام">
          محاسبه قیمت پکیج‌ها
          <svg class="w-5 h-5"><!-- Calculator --></svg>
        </a>
        <a href="/pricing/industrial-power-plants"
           class="inline-flex items-center gap-2 mt-3 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button"
           aria-label="مشاهده قیمت نیروگاه‌های صنعتی برای وام‌های کلان">
          قیمت نیروگاه‌های صنعتی
          <svg class="w-5 h-5"><!-- Factory --></svg>
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
        <a href="https://wa.me/989125728170?text=درخواست%20پیش‌فاکتور%20بانکی"
           class="inline-flex items-center gap-2 mt-4 w-full md:w-auto px-6 py-3 bg-deep-navy text-solar-gold font-bold rounded-xl hover:bg-deep-navy/90 transition-colors justify-center"
           role="button"
           aria-label="درخواست پیش‌فاکتور بانکی در واتس‌اپ">
          <svg class="w-5 h-5"><!-- WA --></svg>
          درخواست پیش‌فاکتور بانکی
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