# UI Wireframe Specification: صادرات تجهیزات خورشیدی و خدمات EPC (عراق و خلیج فارس) | هورا نور سهند
- **Source Dossier:** `seo_dossiers/international_epc-exports.md`
- **Target URL:** `/international/epc-exports`
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

### [SEC_01]: خدمات مهندسی EPC و صادرات تجهیزات خورشیدی به عراق و حوزه خلیج فارس

- **Section Role:** Primary Hero — International H1, export authority signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with aerial view of a solar farm in a desert landscape with modern city skyline in background (evoking Iraq/Gulf). Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "International EPC Contractor" badge in `solar-gold`. Trust badges row (SATBA, Ministry of Energy, E-Namad) below H1. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-international-epc.webp"
         alt="نیروگاه خورشیدی در عراق و خلیج فارس — خدمات EPC هورا نور سهند"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          صادرات تجهیزات و خدمات EPC | عراق و خلیج فارس
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          خدمات مهندسی EPC و صادرات تجهیزات خورشیدی به <span class="text-solar-gold">عراق و حوزه خلیج فارس</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره پروژه‌های بین‌المللی">
          مشاوره پروژه‌های بین‌المللی
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
  - Hero `alt` in Farsi describing solar farm in desert landscape.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: زنجیره تامین و تجهیزات رده‌اول جهانی (Tier-1)

- **Section Role:** Technical authority — Brand carousel with tooltips.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Grayscale logo grid → color on hover. Each logo: `bg-white/5 rounded-xl p-6 transition-colors`.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Logo carousel `flex gap-8 overflow-x-auto snap-x snap-mandatory`.

- **Mobile Stacking:**
  Carousel `snap-x` with `snap-center` items.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        زنجیره تامین <span class="text-solar-gold">Tier-1</span> جهانی
      </h2>
      <div class="flex gap-8 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             @mouseenter="$el.classList.remove('grayscale')" @mouseleave="$el.classList.add('grayscale')"
             class="grayscale transition-colors duration-300"
             role="figure" aria-label="پنل‌های Jinko Solar">
          <img src="/images/logo-jinko.webp" alt="Jinko Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Jinko Solar</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Trina Solar">
          <img src="/images/logo-trina.webp" alt="Trina Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Trina Solar</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های LONGi">
          <img src="/images/logo-longi.webp" alt="LONGi" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">LONGi</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های JA Solar">
          <img src="/images/logo-ja-solar.webp" alt="JA Solar" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">JA Solar</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Mana">
          <img src="/images/logo-mana.webp" alt="Mana" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Mana</span>
        </div>
        <div class="min-w-[160px] snap-center glass-card p-6 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پنل‌های Taban">
          <img src="/images/logo-taban.webp" alt="Taban" class="w-20 h-20 object-contain mb-2">
          <span class="font-bold text-pure-white text-lg">Taban</span>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
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

### [SEC_03]: مزایای همکاری با یک شرکت مورد تایید وزارت نیرو

- **Section Role:** E-E-A-T authority — Trust badges.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Trust badge grid: 4 cards with icons. Each badge: `glass-card p-5 border-s-4 border-solar-gold`. Outbound link to `moe.gov.ir` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Badges grid `grid-cols-3 gap-4`.

- **Mobile Stacking:**
  Badges `grid-cols-2`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مزایای همکاری با <span class="text-solar-gold">شرکت مورد تایید وزارت نیرو</span>
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://moe.gov.ir" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">وزارت نیرو</a></h4>
          <p class="text-pure-white/60 text-sm">استانداردهای IEC</p>
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
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
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

### [SEC_04]: تحلیل تخصصی بازار عراق: جایگزینی دیزل با خورشیدی

- **Section Role:** Pain-point — Split view: Diesel vs Solar.

- **UI Aesthetic & Colors:**
  Split screen. Left (start): `bg-navy-mid/90` with generator imagery, `alert-red` accents. Right: `bg-deep-navy` with solar factory, `eco-green` glow. Diagonal divider `skew-y-3`.

- **Desktop Grid Architecture:**
  12-col. Left: `lg:col-span-6`. Right: `lg:col-span-6`. Both `min-h-[500px]`. GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Diesel first (`h-[300px]`), then Solar. GEO between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/iraq-diesel-generator.webp" alt="ژنراتور دیزلی در عراق" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⛽</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">ژنراتور دیزلی در عراق: پرهزینه و آلاینده</h3>
          <p class="text-pure-white/60 mt-2 text-sm">قطعی برق + سوخت گران + آلودگی</p>
        </div>
      </div>
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/iraq-solar-factory.webp" alt="کارخانه عراقی با نیروگاه خورشیدی" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">☀️</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">نیروگاه خورشیدی: درآمد، معافیت، تداوم</h3>
          <p class="text-pure-white/70 mt-2 text-sm">تزریق به شبکه + بک‌آپ ۲۴ ساعته</p>
        </div>
      </div>
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 خلاصه تصمیم‌ساز</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        تحلیل تخصصی بازار <span class="text-alert-red">عراق</span>: جایگزینی <span class="text-alert-red">دیزل</span> با <span class="text-solar-gold">خورشیدی</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section id="sec-04">`.
  - Color + text labels for meaning.
  - GEO card `border-2 border-solar-gold`.

---

### [SEC_05]: افسانه در برابر واقعیت مهندسی: عملکرد در شرایط گرمسیری

- **Section Role:** Myth-busting — Heat resistance.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth: `bg-alert-red/10 border-alert-red/30` ❌. Reality: `bg-eco-green/10 border-eco-green/30` ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-05" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        افسانه در برابر واقعیت مهندسی: <span class="text-solar-gold">عملکرد در شرایط گرمسیری</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های خورشیدی در مناطق بسیار گرم خاورمیانه به دلیل حرارت بالا کارایی خود را به طور کامل از دست می‌دهند و نصب آن‌ها در جنوب عراق یا عمان توجیه اقتصادی ندارد.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            در حالی که افزایش دما موجب کاهش جزئی ولتاژ (بر اساس ضریب افت دمایی پنل) می‌شود، انتخاب تجهیزات مناسب می‌تواند این چالش را بی‌اثر کند. تیم مهندسی هورا نور سهند در طراحی پروژه‌های این مناطق، منحصراً از پنل‌های پیشرفته با کمترین ضریب افت دمایی (Temperature Coefficient) استفاده کرده و با طراحی استراکچرهای بلندتر جهت جریان هوای بهتر، راندمان سیستم را حفظ می‌کند.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت علمی</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside id="sec-05">`.
  - `x-intersect` decorative.
  - Meaning via icon + text.
  - Contrast: dark text on light cards.

---

### [SEC_06]: پروژه‌های خورشیدی در عمان: فرصت‌های سرمایه‌گذاری

- **Section Role:** Investment expansion — Image carousel.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Image carousel (auto + manual). Each project card: Glassmorphism with hover zoom. Rolling counter `data-value="1000"`. Trust badges row.

- **Desktop Grid Architecture:**
  12-col. Carousel: `lg:col-span-7`. Trust badges + GEO: `lg:col-span-5`.

- **Mobile Stacking:**
  Carousel `max-w-[300px]` snap-x. Badges stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="پروژه‌های پیشنهادی برای عمان">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">فرصتی‌های سرمایه‌گذاری در عمان</h3>
        <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
               role="figure" aria-label="پروژه پیشنهادی پورت جنوبی عمان">
            <img src="/images/oman-south-solar.webp" alt="پروژه پیشنهادی پورت جنوبی عمان" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">پورت جنوبی عمان</h4>
            <p class="text-pure-white/60 text-sm mt-1">نیروگاه ۱۰۰ مگاواتی ساحلی</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
               role="figure" aria-label="پروژه پیشنهادی صحار">
            <img src="/images/oman-sohar-solar.webp" alt="پروژه پیشنهادی صحار" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">شهرک صنعتی صحار</h4>
            <p class="text-pure-white/60 text-sm mt-1">نیروگاه ۵۰ مگاواتی بومی</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
               role="figure" aria-label="پروژه پیشنهادی مسقط">
            <img src="/images/oman-muscat-solar.webp" alt="پروژه پیشنهادی مسقط" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">منطقه مسقط</h4>
            <p class="text-pure-white/60 text-sm mt-1">نصب روی بام‌های اداری</p>
          </div>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پروژه‌های خورشیدی در <span class="text-solar-gold">عمان</span>: فرصت‌های سرمایه‌گذاری
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین کیفیت</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="پروژه‌های پیشنهادی عمان"`.
  - `loading="lazy"` on images.
  - Carousel keyboard navigable.

---

### [SEC_07]: فرآیند اجرای قراردادهای EPC بین‌المللی

- **Section Role:** Process transparency — Step-by-step timeline.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Horizontal timeline with 3 steps: E (Engineering), P (Procurement), C (Construction). Animated connecting lines (`stroke-solar-gold` dash animation).

- **Desktop Grid Architecture:**
  Single row horizontal timeline `flex gap-4 overflow-x-auto snap-x snap-mandatory`. Each step: `min-w-[280px] snap-center`.

- **Mobile Stacking:**
  Horizontal scroll strip `snap-x snap-mandatory`. Each step `min-w-[280px] snap-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-deep-navy" x-data="{ currentStep: 1 }">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        فرآیند اجرای قراردادهای <span class="text-solar-gold">EPC بین‌المللی</span>
      </h2>
      <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۱</span>
          <h4 class="font-bold text-pure-white text-lg">فاز مهندسی (E)</h4>
          <p class="text-pure-white/60 text-sm mt-1">بررسی میدانی، شبیه‌سازی PVsyst، طراحی نقشه‌ها</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۲</span>
          <h4 class="font-bold text-pure-white text-lg">فاز تامین (P)</h4>
          <p class="text-pure-white/60 text-sm mt-1">خرید تجهیزات Tier-1، خرید، ترخیص گمرکی</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۳</span>
          <h4 class="font-bold text-pure-white text-lg">فاز اجرا (C)</h4>
          <p class="text-pure-white/60 text-sm mt-1">نصب، کابل‌کشی، راه‌اندازی، تست و تحویل</p>
        </div>
      </div>
      <div class="text-start max-w-3xl mx-auto mt-10">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">جزئیات فرآیند EPC یکپارچه</h3>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="مراحل اجرای قرارداد EPC"`.
  - `snap-x` for keyboard navigation.
  - Steps have semantic structure.

---

### [SEC_08]: مدیریت چالش‌های لجستیک و گمرک

- **Section Role:** Operations depth — Supply chain transparency.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Bullet list with icons: `📦` Packaging, `🚢` Shipping, `🛡️` Insurance, `🏛️` Customs. Each in glass card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Bullet list.

- **Mobile Stacking:**
  No change.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        مدیریت چالش‌های <span class="text-solar-gold">لجستیک و گمرک</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
      </p>
      <div class="space-y-4">
        <div class="flex items-start gap-4 glass-card p-4 border-s-4 border-solar-gold">
          <span class="text-3xl shrink-0">📦</span>
          <div>
            <h4 class="font-bold text-pure-white text-lg">بسته‌بندی تخصصی</h4>
            <p class="text-pure-white/70 text-sm mt-1">پالت‌بندی پیچ‌وپنج پنل‌ها با فوم ضد شوک برای جلوگیری از تخریب در ترانزیت</p>
          </div>
        </div>
        <div class="flex items-start gap-4 glass-card p-4 border-s-4 border-solar-gold">
          <span class="text-3xl">🚢</span>
          <div>
            <h4 class="font-bold text-pure-white text-lg">ترانزیت بین‌المللی</h4>
            <p class="text-pure-white/70 text-sm mt-1">حمل زمینی/دریایی با بیمه کامل تا مرز مقصد</p>
          </div>
        </div>
        <div class="flex items-start gap-4 glass-card p-4 border-s-4 border-solar-gold">
          <span class="text-3xl">🛡️</span>
          <div>
            <h4 class="font-bold text-pure-white text-lg">بیمه بین‌المللی کالا</h4>
            <p class="text-pure-white/70 text-sm mt-1">پوشش کامل در برابر آسیب، دزدی و تاخیر</p>
          </div>
        </div>
        <div class="flex items-start gap-4 glass-card p-4 border-s-4 border-solar-gold">
          <span class="text-3xl">🏛️</span>
          <div>
            <h4 class="font-bold text-pure-white text-lg">ترخیص گمرکی</h4>
            <p class="text-pure-white/70 text-sm mt-1">مدیریت کامل اسناد گمرکی در مرزهای ایران-عراق و سایر مراب</p>
          </div>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic list structure.
  - Icon + text for meaning.

---

### [SEC_09]: آپدیت‌های تکنولوژی و استانداردهای روز جهانی

- **Section Role:** Temporal freshness + outbound trust (IRENA).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی تکنولوژی". External link to `irena.org` with `rel="external noopener"`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. Badges grid `grid-cols-3 gap-4`.

- **Mobile Stacking:**
  Badges `grid-cols-2`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          آپدیت‌های تکنولوژی و استانداردهای روز جهانی
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی تکنولوژی</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">📊</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://www.irena.org/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">آژانس بین‌المللی انرژی‌های تجدیدپذیر (IRENA)</a></h4>
          <p class="text-pure-white/60 text-sm">رتبه‌بندی Tier-1 ۲۰۲۴</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://www.iec.ch/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">IEC Standards</a></h4>
          <p class="text-pure-white/60 text-sm">استانداردهای ۶۱۷۲۴</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">📜</span>
          <h4 class="font-bold text-pure-white text-lg">اینماد / ساماندهی</h4>
          <p class="text-pure-white/60 text-sm">تأیید تجارت الکترونیک</p>
        </div>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
      </p>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        مراجعه به <a href="https://www.irena.org/" rel="external noopener" target="_blank"
           class="text-solar-gold underline hover:text-solar-gold/80">آژانس بین‌المللی انرژی‌های تجدیدپذیر (IRENA)</a> برای اطلاع از استانداردهای مرجع جهانی.
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External links `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_10]: سوالات متداول (FAQ) درباره صادرات پنل خورشیدی

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
        سوالات متداول <span class="text-solar-gold">صادرات پنل خورشیدی</span>
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
              آیا امکان ارسال پکیج‌های کوچک ویلایی به عراق وجود دارد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، علاوه بر پروژه‌های مگاواتی، پکیج‌های استاندارد آفگرید ویلایی نیز به صورت کامل و آماده نصب صادر می‌شوند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              چه برندهایی در پروژه‌های صادراتی استفاده می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            صرفاً برندهای دارای رنکینگ Tier-1 جهانی مانند لانگی (LONGi)، جینکو و ترینا که دارای ضمانت‌نامه‌های ۲۵ ساله افت راندمان هستند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا اجرای پروژه (نصب) نیز توسط تیم شما انجام می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، قراردادهای ما به صورت EPC بوده و تیم مهندسین و تکنیسین‌های نصب هورا نور سهند جهت اجرای پروژه به کشورهای مقصد اعزام می‌گردند.
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

[VERIFIED_UI_END_OF_FILE]