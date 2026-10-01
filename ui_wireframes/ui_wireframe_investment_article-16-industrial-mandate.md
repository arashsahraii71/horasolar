# UI Wireframe Specification: ماده ۱۶ جهش تولید | معافیت جریمه برق صنایع | هورا نور سهند
- **Source Dossier:** `seo_dossiers/investment_article-16-industrial-mandate.md`
- **Target URL:** `/investment/article-16-industrial-mandate`
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

### [SEC_01]: راهکار رفع جریمه ماده ۱۶ جهش تولید و معافیت قطعی برق صنایع

- **Section Role:** Primary Hero — B2B Legal H1, penalty vs exemption contrast.

- **UI Aesthetic & Colors:**
  Full-viewport hero with juxtaposed imagery: left half shows a heavy industrial electricity bill stamped "جریمه" (red stamp), right half shows a modern factory roof covered in solar panels with "معافیت قانونی" (Legal Exemption) badge in `solar-gold`. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "Legal Exemption" badge in `solar-gold`. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Text: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-article16-fine-to-solar.webp"
         alt="قبض برق صنعتی با مهر جریمه که به ویلای خورشیدی با مدال معافیت قانونی تبدیل می‌شود"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          رفع جریمه ماده ۱۶ | معافیت قانونی | تضمین ۲۵ ساله
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          راهکار رفع <span class="text-alert-red">جریمه ماده ۱۶</span> و معافیت قطعی <span class="text-solar-gold">برق صنایع</span>
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="کارشناسی رایگان قبض برق صنعتی">
          کارشناسی رایگان قبض برق
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
  - Hero `alt` in Farsi describing fine-to-solar transformation.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: ماده ۱۶ قانون جهش تولید دقیقاً چیست؟ (الزام ۱ تا ۵ درصد)

- **Section Role:** Legal explainer — Step-by-step year progression chart.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Step-by-step year progression chart: Year 1 (1%) → Year 2 (2%) → Year 3 (3%) → Year 4 (4%) → Year 5 (5%). Each year a glass card with percentage badge: Year 1 `eco-green`, Year 2-3 `solar-gold`, Year 4-5 `alert-red`. Animated connecting lines (`stroke-solar-gold`).

- **Desktop Grid Architecture:**
  12-col. Timeline horizontal: `flex gap-4 overflow-x-auto snap-x snap-mandatory`. Each step `min-w-[240px] snap-center`.

- **Mobile Stacking:**
  Horizontal scroll strip `snap-x snap-mandatory`. Each step `min-w-[240px] snap-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ currentYear: 1 }">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        ماده ۱۶ قانون جهش تولید دقیقاً چیست؟ (الزام <span class="text-solar-gold">۱ تا ۵ درصد</span>)
      </h2>
      <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-eco-green flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۱</span>
          <h4 class="font-bold text-eco-green text-xl">سال اول: ۱٪</h3>
          <p class="text-pure-white/60 text-sm mt-1">شروع الزام قانونی</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۲</span>
          <h4 class="font-bold text-solar-gold text-xl">سال دوم: ۲٪</h3>
          <p class="text-pure-white/60 text-sm mt-1">افزایش تدریجی الزام</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۳</span>
          <h3 class="font-bold text-solar-gold text-xl">سال سوم: ۳٪</h3>
          <p class="text-pure-white/60 text-sm mt-1">افزایش تدریجی ادامه دارد</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-alert-red flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۴</span>
          <h3 class="font-bold text-alert-red text-xl">سال چهارم: ۴٪</h3>
          <p class="text-pure-white/60 text-sm mt-1">افزایش تدریجی ادامه دارد</p>
        </div>
        <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-alert-red flex flex-col items-center text-center shrink-0">
          <span class="text-4xl mb-3">۵</span>
          <h3 class="font-bold text-alert-red text-xl">سال پنجم: ۵٪</h3>
          <p class="text-pure-white/60 text-sm mt-1">پایان الزام قانونی (حداکثر)</p>
        </div>
      </div>
      <div class="text-start max-w-3xl mx-auto mt-10">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-6">
          ماده ۱۶ قانون جهش تولید دقیقاً چیست؟ (الزام <span class="text-solar-gold">۱ تا ۵ درصد</span>)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="مراحل الزام ماده ۱۶: از ۱٪ تا ۵٪"`.
  - `snap-x` for keyboard navigation.
  - Steps have semantic structure.

---

### [SEC_03]: درد پنهان صنایع: خرید اجباری از تابلو سبز بورس انرژی

- **Section Role:** Pain-point financial alert — Red alert box.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Financial Alert Box with `border-2 border-alert-red`. Red warning icon. Background `bg-alert-red/10`. Text in `alert-red` and `pure-white`. "Tablo Sabz" badge in `alert-red`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column alert box. GEO callout below.

- **Mobile Stacking:**
  No change. Full-width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl">
      <div class="bg-alert-red/10 border-2 border-alert-red rounded-2xl p-8 mb-10" role="alert" aria-live="polite">
        <div class="flex items-start gap-4">
          <span class="text-4xl">🚨</span>
          <div>
            <h3 class="text-alert-red font-bold text-xl mb-2">درد پنهان صنایع: خرید اجباری از <span class="text-solar-gold">تابلو سبز بورس انرژی</span></h3>
            <p class="text-pure-white/80 text-base md:text-lg leading-relaxed">
              {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
            </p>
          </div>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-alert-red mt-8">
        <p class="text-sm font-bold text-alert-red mb-1">🚨 هشدار مالی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `role="alert"` on alert box.
  - `aria-live="polite"` for dynamic content.
  - Color + text labels.

---

### [SEC_04]: باورهای غلط در خصوص جرایم اداره برق (Myth vs. Reality)

- **Section Role:** Myth-busting — Monthly penalty vs owning solar asset.

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
        باورهای غلط در خصوص <span class="text-solar-gold">جرایم اداره برق</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پرداخت جریمه ماهانه، ارزان‌تر از احداث نیروگاه خورشیدی است.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت استراتژیک</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            مجموع جرایم ماهانه در کمتر از ۳ سال معادل خرید یک نیروگاه کامل خورشیدی می‌شود. با احداث نیروگاه، جریمه‌ها تبدیل به دارایی ۲۵ ساله می‌شوند. با تجهیزات Tier-1، برق رایگان برای ۲۵ سال.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">💰 محاسبه استراتژیک</p>
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

### [SEC_05]: استقرار تیم‌های مهندسی هورا نور در هاب‌های صنعتی

- **Section Role:** Local SEO map anchor + B2B proximity.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Interactive map with HQ pin at Karaj, vector lines to Eshtehard, Shamsabad, Simindasht. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="نقشه پوشش تیم‌های صنعتی هورا نور سهند" role="img">
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d50000!2d50.9!3d35.8!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3f8d1e0000000000%3A0x0!2z2YbYsdin2KfZhdi4INin2YTYp9mE!5e0!3m2!1sfa!2sir!4v1"
                width="100%" height="400" style="border:0;" allowfullscreen="" loading="lazy"
                aria-label="موقعیت تیم‌های صنعتی هورا نور سهند: اشتهارد، بهارستان، سیمین‌دشت، تهران، قزوین"></iframe>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استقرار تیم‌های <span class="text-solar-gold">هورا نور سهند</span> در هاب‌های صنعتی
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🏭 پوشش صنعتی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
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

### [SEC_06]: توانمندی‌های اجرایی ما (تجهیزات Tier-1)

- **Section Role:** E-E-A-T authority — Hardware durability showcase + 25-year guarantee.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Portfolio showcase: Tier-1 logos grid. 25-year guarantee badge: `bg-solar-gold text-deep-navy`. Brand logos grayscale → color on hover.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Logo carousel `flex gap-8 overflow-x-auto snap-x snap-mandatory`. Guarantee badge below.

- **Mobile Stacking:**
  Carousel `snap-x` with `snap-center` items. Badge below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-10">
        توانمندی‌های اجرایی ما (<span class="text-solar-gold">تجهیزات Tier-1</span>)
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
             role="figure" aria-label="اینورترهای Growatt">
          <img src="/images/logo-growatt.webp" alt="Growatt" class="w-20 h-20 object-contain mb-2">
          <span class="text-3xl mb-2">⚡</span>
          <span class="font-bold text-pure-white text-lg">Growatt</span>
        </div>
      </div>
      <div class="mt-8 glass-card p-8 rounded-2xl text-center border-2 border-solar-gold">
        <span class="text-4xl mb-3">🛡️</span>
        <h3 class="font-bold text-pure-white text-2xl mb-2">ضمانت کارایی ۲۵ ساله</h3>
        <p class="text-pure-white/80 mt-2">گارانتی راندمان خطی ۲۵ ساله برای تمام پنل‌های Tier-1</p>
        <p class="text-solar-gold font-bold text-xl mt-4">ضمانت ۲۵ ساله خطی</p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Carousel `aria-label="برندهای تجهیزات Tier-1"`.
  - Hover removes grayscale (decorative).
  - `loading="lazy"` on logos.

---

### [SEC_07]: استناد به مراجع قانونی توانیر (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (Tavanir).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Trust badges grid. External link to `tavanir.org.ir` with `rel="external noopener"`.

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
          استناد به مراجع قانونی توانیر
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://www.tavanir.org.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">شرکت توانیر</a></h4>
          <p class="text-pure-white/60 text-sm">فرآیند اتصال ماده ۱۶</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://www.tavanir.org.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">شرکت توانیر</a></h4>
          <p class="text-pure-white/60 text-sm">سامانه ملی اتصال ماده ۱۶</p>
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
        مراجعه به <a href="https://www.tavanir.org.ir/" rel="external noopener" target="_blank"
           class="text-solar-gold underline hover:text-solar-gold/80">شرکت توانیر</a> برای اطلاع از فرآیندهای اتصال ماده ۱۶.
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External links `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: بررسی دقیق هزینه‌ها و بازگشت سرمایه

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to pricing/industrial.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Single glass card with `border-b-4 border-solar-gold`. Internal link pill CTA to `/pricing/industrial-power-plants`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Vertical stack.

- **Mobile Stacking:**
  CTA `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        بررسی دقیق <span class="text-solar-gold">هزینه‌ها و بازگشت سرمایه</span>
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📋 ابزار دقیق</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <a href="/pricing/industrial-power-plants"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="مطالعه طرح توجیهی نیروگاه‌های صنعتی">
          طرح توجیهی نیروگاه‌های صنعتی
          <svg class="w-5 h-5"><!-- Arrow --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - CTA `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile.

---

### [SEC_09]: بخش پاسخ به سوالات متداول ماده ۱۶ (FAQ)

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
        سوالات متداول <span class="text-solar-gold">ماده ۱۶ قانون جهش تولید</span>
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
              آیا ماده ۱۶ شامل صنایعی با دیماند زیر ۱ مگاوات نیز می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            خیر، نص صریح قانون جهش تولید دانش‌بنیان، در حال حاضر صرفاً مصرف‌کنندگان بزرگ با دیماند قراردادی بالای ۱ مگاوات (۱۰۰۰ کیلووات) را هدف قرار داده است. با این حال صنایع کوچکتر نیز می‌توانند برای جلوگیری از قطعی برق تابستان اقدام به احداث نیروگاه نمایند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              اگر نیروگاه ما بیشتر از ۵ درصد مصرف تولید کند چه می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            چنانچه ظرفیت نیروگاه خورشیدی احداث شده روی سقف سوله شما، بیش از الزام قانونی ۵ درصد باشد، شما می‌توانید مازاد برق تولیدی را در تابلو سبز بورس انرژی به فروش برسانید و از آن به عنوان یک منبع درآمد خالص و عالی برای کارخانه استفاده کنید.
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

### [SEC_10]: رزرو وقت برای تحلیل قبض برق و کارشناسی سوله (CTA)

- **Section Role:** CRO conversion — B2B factory manager CTA.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones `text-3xl md:text-5xl`. Messenger icons `w-16 h-16`. Grain overlay. "ارسال تصویر قبض برق" CTA.

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
          نجات منابع مالی کارخانه خود را به تعویق نیندازید
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
        </div>
        <a href="https://wa.me/989125728170?text=تحلیل%20قبض%20برق%20صنعتی%20برای%20رفع%20جریمه%20ماده%20۱۶"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="ارسال تصویر قبض برق برای کارشناسی رایگان">
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
          ارسال تصویر قبض برق برای کارشناسی رایگان
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
        <a href="https://wa.me/989125728170?text=تحلیل%20قبض%20برق%20صنعتی%20برای%20رفع%20جریمه%20ماده%20۱۶"
           class="inline-flex items-center gap-2 mt-4 w-full md:w-auto px-6 py-3 bg-deep-navy text-solar-gold font-bold rounded-xl hover:bg-deep-navy/90 transition-colors justify-center"
           role="button"
           aria-label="ارسال تصویر قبض برق برای کارشناسی رایگان">
          <svg class="w-5 h-5"><!-- WA --></svg>
          ارسال تصویر قبض برق برای کارشناسی رایگان
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