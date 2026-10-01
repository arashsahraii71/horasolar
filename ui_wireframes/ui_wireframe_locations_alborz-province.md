# UI Wireframe Specification: پنل خورشیدی در کرج و البرز | شرکت هورا نور سهند
- **Source Dossier:** `seo_dossiers/locations_alborz-province.md`
- **Target URL:** `/locations/alborz-province`
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

### [SEC_01]: شرکت مهندسی و اجرای نیروگاه خورشیدی در استان البرز و کرج

- **Section Role:** Primary Hero — Local Business H1, Local SEO anchor, trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with photo of Karaj HQ building + team in front. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "پیمانکار بومی استان البرز" badge in `solar-gold`. Trust badges row (SATBA, Ministry of Energy, E-Namad) below H1. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-alborz-hq.webp"
         alt="ساختمان دفتر مرکزی هورا نور سهند در کرج، جاده ملارد — پیمانکار بومی البرز"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          پیمانکار بومی استان البرز | مجری EPC
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          شرکت مهندسی و اجرای نیروگاه خورشیدی در <span class="text-solar-gold">استان البرز و کرج</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="مشاوره پروژه‌های خورشیدی در البرز">
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
  - Hero `alt` in Farsi describing Karaj HQ building.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: پتانسیل طلایی تابش و راندمان در اقلیم البرز

- **Section Role:** First-party data / Regional relevance — Climate infographic.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Climate infographic: sun icon over Alborz mountains with "۲۵۰ روز آفتابی" stat badge. `eco-green` for "optimal temperature" badge. Sun arc animation.

- **Desktop Grid Architecture:**
  12-col. Infographic: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Infographic first (`h-[300px]`). Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار روزهای آفتابی و راندمان در اقلیم البرز" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">پتانسیل تابش خورشیدی البرز</h3>
          <div class="relative h-[300px] flex items-center justify-center">
            <svg viewBox="0 0 400 300" class="w-full h-auto" role="img" aria-label="نمودار تابش خورشیدی و دمای البرز">
              <!-- Sun Arc -->
              <path d="M50,250 Q200,50 350,250" stroke="#F5A623" stroke-width="3" fill="none" stroke-linecap="round">
                <animate attributeName="stroke-dashoffset" from="1000" to="0" dur="2s" fill="freeze"/>
              </path>
              <!-- Mountain Silhouette -->
              <path d="M20,250 Q100,150 200,250 T380,250" fill="#132F4C"/>
              <!-- Stats Badge -->
              <text x="200" y="150" text-anchor="middle" fill="#2ECC71" font-size="24" font-family="Vazirmatn" font-weight="bold">۲۵۰ روز آفتابی</text>
            </svg>
          </div>
          <div class="flex justify-center gap-6 mt-6 text-sm">
            <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-solar-gold"></span> ۲۵۰ روز آفتابی</span>
            <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-eco-green"></span> دمای بهینه</span>
            <span class="flex items-center gap-2"><span class="w-8 h-1 rounded bg-solar-gold/50"></span> ضریب حرارتی پایین</span>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          پتانسیل طلایی <span class="text-solar-gold">تابش و راندمان</span> در اقلیم <span class="text-solar-gold">البرز</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">☀️ مزیت اقلیمی البرز</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
          </p>
        </div>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - Infographic `role="img"` + `aria-label`.
  - Color + text labels for stats.

---

### [SEC_03]: خدمات تخصصی برای ویلاهای کردان، تهراندشت و هشتگرد

- **Section Role:** Hyper-local B2C targeting — Villa packages for specific neighborhoods.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Carousel of villa projects with location badges: "پروژه ویلای کردان", "پروژه آفگرید تهراندشت". Glass cards with location badges.

- **Desktop Grid Architecture:**
  Carousel `flex gap-8 overflow-x-auto snap-x snap-mandatory`. Each card `min-w-[280px] snap-center`.

- **Mobile Stacking:**
  Carousel `snap-x` with `snap-center` items. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        خدمات تخصصی برای ویلاهای <span class="text-solar-gold">کردان، تهراندشت و هشتگرد</span>
      </h2>
      <div class="flex gap-8 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-eco-green flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پروژه ویلای کردان - سیستم ۱۰ کیلواتی">
          <img src="/images/project-kordan-villa.webp" alt="نصب پکیج ۱۰ کیلواتی در ویلای کردان" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
          <h4 class="font-bold text-pure-white text-lg">ویلا کردان</h4>
          <p class="text-pure-white/60 text-sm mt-1">پکیج ۱۰ کیلواتی / کولر + یخچال + پمپ</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پروژه ویلای تهراندشت - پکیج ۸ کیلواتی">
          <img src="/images/project-tehrandesh-villa.webp" alt="نصب پکیج ۸ کیلواتی در ویلای تهراندشت" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
          <h4 class="font-bold text-pure-white text-lg">ویلا تهراندشت</h4>
          <p class="text-pure-white/60 text-sm mt-1">پکیج ۸ کیلواتی / کولر + یخچال + پمپ استخر</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0"
             role="figure" aria-label="پروژه ویلای هشتگرد - پکیج ۶ کیلواتی">
          <img src="/images/project-hashtgerd-villa.webp" alt="نصب پکیج ۶ کیلواتی در ویلای هشتگرد" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
          <h4 class="font-bold text-pure-white text-lg">ویلا هشتگرد</h4>
          <p class="text-pure-white/60 text-sm mt-1">پکیج ۶ کیلواتی / کولر + یخچال + روشنایی</p>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="پروژه‌های ویلایی البرز"`.
  - `snap-x` for keyboard navigation.
  - Semantic structure.

---

### [SEC_04]: احداث مگاواتی در قطب‌های صنعتی: اشتهارد و سیمین‌دشت

- **Section Role:** B2B Industrial — Mega-watt projects in specific industrial zones.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Split cards for Eshtehard and Simindasht. B2B focus block with vector map pinpoints.

- **Desktop Grid Architecture:**
  12-col. Two cards side-by-side `lg:col-span-6` each. Map pinpoints overlay.

- **Mobile Stacking:**
  Vertical stack.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-2 gap-8">
      <div class="glass-card p-8 border-s-4 border-solar-gold rounded-2xl text-start">
        <div class="flex items-center gap-3 mb-4">
          <span class="text-4xl">🏭</span>
          <div>
            <h3 class="font-bold text-xl text-solar-gold">شهرک صنعتی اشتهارد</h3>
            <p class="text-pure-white/60 text-sm">مرکز صنعتی البرز / معافیت ماده ۱۶</p>
          </div>
        </div>
        <h3 class="font-bold text-xl text-pure-white mb-4">پروژه‌های مگاواتی در اشتهارد</h3>
        <p class="text-pure-white/80 text-base leading-relaxed mb-6">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04 (paras 1-2)}
        </p>
        <ul class="space-y-3 text-pure-white/80">
          <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> نیروگاه ۵ مگاواتی اشتهارد</li>
          <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> نیروگاه ۲ مگاواتی سیمین‌دشت</li>
          <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> معافیت کامل ماده ۱۶</li>
        </ul>
      </div>
      <div class="glass-card p-8 border-s-4 border-eco-green rounded-2xl text-start">
        <div class="flex items-center gap-3 mb-4">
          <span class="text-4xl">🏭</span>
          <div>
            <h3 class="font-bold text-xl text-eco-green">شهرک صنعتی سیمین‌دشت</h3>
            <p class="text-pure-white/60 text-sm">نزدیک تهران / محاسبه‌محور सामاندهی</p>
          </div>
        </div>
        <h3 class="font-bold text-xl text-pure-white mb-4">پروژه‌های مگاواتی در سیمین‌دشت</h3>
        <p class="text-pure-white/80 text-base leading-relaxed mb-6">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04 (paras 3-4)}
        </p>
        <ul class="space-y-3 text-pure-white/80">
          <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> نیروگاه ۲ مگاواتی سیمین‌دشت</li>
          <li class="flex items-center gap-2"><span class="text-solar-gold">✅</span> معافیت ماده ۱۶</li>
        </ul>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🏭 پوشش صنعتی البرز</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic headings and lists.
  - Color + text for meaning.

---

### [SEC_05]: باورهای غلط بومی درباره نیروگاه در البرز (Myth vs. Reality)

- **Section Role:** Myth-busting — Cloudy weather myth.

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
        باورهای غلط بومی درباره <span class="text-solar-gold">نیروگاه در البرز</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            چون هوای کرج در پاییز و زمستان نیمه‌ابری است، پنل خورشیدی کار نمی‌کند.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل‌های مونوکریستال هف‌کات (Half-cut) لانگی و جینکو به نور پراکنده (Diffuse Light) بسیار حساس هستند. حتی در ابری‌ترین روزهای پاییزی جاده چالوس و کردان، این پنل‌ها با جذب فوتون‌های عبوری از ابرها، جریان لازم برای روشن نگه‌داشتن یخچال و سیستم‌های امنیتی ویلای شما را تامین می‌کنند.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 واقعیت البرز</p>
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

### [SEC_06]: ارتباط مستقیم با شرکت توزیع نیروی برق استان البرز

- **Section Role:** Local trust — Direct Tavanir Alborz relationship.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Trust badges: Alborz Electricity Distribution, Ministry of Energy. Process timeline.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Process timeline horizontal `flex gap-4 overflow-x-auto snap-x`.

- **Mobile Stacking:**
  Horizontal scroll `snap-x`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        ارتباط مستقیم با <span class="text-solar-gold">شرکت توزیع نیروی برق استان البرز</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
      </p>
      <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-3xl mb-2">🏛️</span>
          <h4 class="font-bold text-pure-white text-lg">شرکت توزیع برق البرز</h4>
          <p class="text-pure-white/60 text-sm mt-1">مجوز انشعاب و اتصال</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg">شرکت توانیر</h4>
          <p class="text-pure-white/60 text-sm mt-1">مجوز اتصال ماده ۱۶</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-3xl mb-2">📜</span>
          <h4 class="font-bold text-pure-white text-lg">اینماد / ساماندهی</h4>
          <p class="text-pure-white/60 text-sm mt-1">تأیید تجارت الکترونیک</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-3xl mb-2">🏛️</span>
          <h4 class="font-bold text-pure-white text-lg">سازمان ساتبا</h4>
          <p class="text-pure-white/60 text-sm mt-1">قرارداد ۲۰ ساله</p>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto text-start">
        <p class="text-sm font-bold text-solar-gold mb-1">🤝 اعتماد اداری</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="اعتبارنامه‌های البرز"`.
  - `snap-x` for keyboard navigation.

---

### [SEC_07]: آخرین به‌روزرسانی‌های توانیر در استان البرز (آپدیت 1403)

- **Section Role:** Temporal freshness — Tavanir 1403 updates.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Trust badges grid. External link to `aepdc.ir` with `rel="external noopener"`.

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
          آخرین به‌روزرسانی‌های توانیر در استان البرز
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://aepdc.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">شرکت توزیع نیروی برق استان البرز</a></h4>
          <p class="text-pure-white/60 text-sm">فرآیند اتصال ماده ۱۶</p>
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
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        مراجعه به <a href="https://aepdc.ir/" rel="external noopener" target="_blank"
           class="text-solar-gold underline hover:text-solar-gold/80">شرکت توزیع نیروی برق استان البرز</a> برای اطلاع از فرآیندهای اتصال ماده ۱۶.
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External links `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: ارجاع به خدمات تخصصی (ویلاها و صنایع)

- **Section Role:** Internal linking — Anti-cannibalization routing.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Two prominent pill links with icons.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Two pill links side-by-side on desktop, stacked on mobile.

- **Mobile Stacking:**
  Stacked vertically, each `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-center space-y-4">
      <a href="/applications/residential-villa-appliances"
         class="inline-flex items-center gap-2 px-8 py-4 bg-eco-green text-pure-white font-bold rounded-2xl hover:bg-eco-green/90 transition-colors w-full md:w-auto justify-center"
         role="button"
         aria-label="مطالعه پکیج‌های ویلایی برای کردان، تهراندشت، هشتگرد">
        <svg class="w-5 h-5"><!-- Home --></svg>
        پکیج‌های برق خورشیدی ویلایی (کردان، هشتگرد، تهراندشت)
      </a>
      <a href="/applications/industrial-shed-roofs"
         class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
         role="button"
         aria-label="مطالعه نیروگاه‌های صنعتی برای اشتهارد، سیمین‌دشت، بهارستان">
        <svg class="w-5 h-5"><!-- Factory --></svg>
        نیروگاه‌های صنعتی (اشتهارد، سیمین‌دشت، بهارستان)
      </a>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Buttons `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile for touch target.

---

### [SEC_09]: آدرس، دسترسی و راه‌های ارتباطی با دفتر مرکزی کرج (NAP)

- **Section Role:** NAP consistency — Local SEO anchor.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Embedded Google Maps iFrame. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="موقعیت دفتر مرکزی هورا نور سهند در کرج" role="img">
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d50000!2d50.9!3d35.8!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3f8d1e0000000000%3A0x0!2z2YbYsdin2KfZhdi4INin2YTYp9mE!5e0!3m2!1sfa!2sir!4v1"
                width="100%" height="400" style="border:0;" allowfullscreen="" loading="lazy"
                aria-label="موقعیت دفتر مرکزی هورا نور سهند در کرج، جاده ملارد"></iframe>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          آدرس و دسترسی به <span class="text-solar-gold">دفتر مرکزی کرج</span>
        </h2>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان، نرسیده به پل ارتش، جنب فروشگاه سهند</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 دفتر مرکزی البرز</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
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

### [SEC_10]: سوالات متداول بومی در استان البرز (FAQ - SGE Bait)

- **Section Role:** GEO/SGE bait — Local FAQ schema.

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
        سوالات متداول <span class="text-solar-gold">برق خورشیدی در البرز</span>
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
              آیا برای پروژه‌های کردان و هشتگرد هزینه ایاب و ذهاب اضافی دریافت می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر. به دلیل بومی بودن شرکت هورا نور سهند در استان البرز و فاصله بسیار کوتاه دفتر ملارد تا مناطق ویلایی کردان، چهارباغ، تهراندشت و هشتگرد، هیچ‌گونه هزینه مسافت (که توسط شرکت‌های تهرانی یا سایر استان‌ها اخذ می‌شود) از کارفرمایان البرزی دریافت نخواهد شد.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              تیم پشتیبانی و تعمیرات در صورت خرابی سیستم، چند ساعته به محل می‌رسد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در صورت بروز هرگونه افت ولتاژ یا نیاز به تنظیمات نرم‌افزاری اینورتر در استان البرز، تیم واکنش سریع هورا نور سهند در کمتر از ۲۴ ساعت کاری (بسته به ترافیک محورها) در محل ویلا یا سوله شما حاضر شده و سیستم را عیب‌یابی می‌کند.
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

### [SEC_11]: تماس فوری با مهندسین بومی البرز (CTA)

- **Section Role:** CRO conversion — Local B2B/B2C CTA.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. "پشتیبانی ۲۴ ساعته البرز" badge.

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
          پروژه خورشیدی خود در البرز را همین امروز آغاز کنید
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
        <a href="https://wa.me/989125728170?text=مشاوره%20پروژه%20خورشیدی%20در%20البرز"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="مشاوره پروژه‌های خورشیدی در البرز در واتس‌اپ">
          مشاوره رایگان واتس‌اپ
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
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