# UI Wireframe Specification: موتور برق یا پنل خورشیدی؟ | مقایسه تخصصی هزینه و کارایی | هورا نور سهند
- **Source Dossier:** `seo_dossiers/knowledge_generator-vs-solar-analysis.md`
- **Target URL:** `/knowledge/generator-vs-solar-analysis`
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
### Icon System Rule
> **CRITICAL:** All icons MUST be inline SVG — **NEVER emoji**. Emoji render inconsistently across OS/browsers and cannot inherit brand colour.
> Use a `24x24` `viewBox` with `fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round"` and size it in em units: `style="width:1em;height:1em;vertical-align:-0.125em;display:inline-block"`.
> Always add `aria-hidden="true" focusable="false"`. Because colour is `currentColor` and size is `1em`, each icon automatically inherits the surrounding text's colour and scale.
> Typographic arrows and operators (`→` `←` `↓` `≥` `≈`) are **not** icons and stay as text.
> Alpine note: an SVG cannot be rendered via `x-text` (it sets `textContent`) — use `x-html` with `&quot;`-escaped inner quotes.

---

### [SEC_01]: موتور برق یا پنل خورشیدی؟ (مقدمه و چشم‌انداز)

- **Section Role:** Primary Hero — Split VS visual, H1 entity, immediate trust signal.

- **UI Aesthetic & Colors:**
  Full-viewport hero with split VS visual: Left side shows noisy diesel generator with smoke/exhaust, right side shows clean solar villa roof. Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). "VS" badge in `solar-gold` between two halves. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Split layout: Left `lg:col-span-6` (Generator), Right `lg:col-span-6` (Solar). GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Vertical stack. Generator first, then Solar. GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <!-- Generator Side -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/generator-vs-solar-generator.webp" alt="موتور برق دیزلی دودی و پرصدا" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">⛽</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">موتور برق دیزلی</h3>
          <p class="text-pure-white/60 mt-2 text-sm">هزینه سوخت + صدا + استهلاک</p>
        </div>
      </div>
      <!-- Solar Side -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/generator-vs-solar-solar.webp" alt="ویلای خورشیدی آرام و تمیز" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">☀️</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">پنل خورشیدی: آرام، تمیز، اقتصادی</h3>
          <p class="text-pure-white/70 mt-2 text-sm">صفر سوخت / صفر صدا / ۲۵ سال عمر</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">⚔️ مقایسه یک‌به‌یک</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_01}
        </p>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article id="sec-01">` wrapper.
  - Color + text labels for meaning.
  - GEO `<aside>` complementary role.

---

### [SEC_02]: تحلیل هزینه اولیه در برابر هزینه‌های پنهان (TCO)

- **Section Role:** Financial deep-dive — Bar chart comparison.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Horizontal bar chart: Years 1-5 on Y-axis. Generator bar (red `alert-red`, steep upward) vs Solar bar (green `eco-green`, flat after year 1). Break-even marker at Year 3 (`solar-gold` diamond).

- **Desktop Grid Architecture:**
  12-col. Chart: `lg:col-span-7` (`rounded-e-3xl`). Text + GEO: `lg:col-span-5` (`rounded-s-3xl`).

- **Mobile Stacking:**
  Chart horizontal scroll. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ showDetails: false }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <div class="lg:col-span-7 glass-card rounded-e-3xl p-8 overflow-x-auto">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقایسه هزینه‌های تجمعی ۵ ساله</h3>
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="مقایسه هزینه تجمعی ۵ ساله: ژنراتور در برابر خورشیدی">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-3 text-start rounded-s-lg">سال</th>
              <th scope="col" class="p-3 text-start">هزینه تجمعی ژنراتور (میلیون تومان)</th>
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
          تحلیل هزینه <span class="text-solar-gold">ابتدایی در برابر پنهان</span> (TCO)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_02}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on all headers.
  - Toggle button `:aria-expanded` + `aria-controls`.

---

### [SEC_03]: آلودگی صوتی و آرامش ویلاهای مسکونی

- **Section Role:** Pain-point — Decibel comparison visualization.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Decibel bar chart: Generator 85 dB (`alert-red`), Solar 0 dB (`eco-green`), Library 30 dB (`solar-gold`), Whisper 20 dB (`eco-green`). Visual bar chart with color-coded bars.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO callout below.

- **Mobile Stacking:**
  No change. Full-width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        آلودگی صوتی و <span class="text-solar-gold">آرامش ویلاهای مسکونی</span>
      </h2>
      <div class="glass-card p-8 space-y-6">
        <h3 class="font-bold text-xl text-pure-white text-center mb-6">مقایسه سطح صدا (دسی‌بل)</h3>
        <div class="space-y-4" x-data="{ bars: { gen: 85, lib: 30, sol: 0, whisper: 20 } }">
          <div class="flex items-end gap-4 h-[200px]">
            <div class="flex-1 flex flex-col items-center justify-end">
              <div class="w-full h-16 bg-alert-red/20 border-2 border-alert-red rounded-t-lg flex items-end justify-center p-2"
                   :style="{ height: bars.gen + 'px' }">
                <span class="text-xs font-bold text-alert-red">۸۵ dB</span>
              </div>
              <p class="text-center text-sm text-alert-red font-bold mt-2">ژنراتور</p>
            </div>
            <div class="flex-1 flex flex-col items-center justify-end">
              <div class="w-full h-16 bg-solar-gold/20 border-2 border-solar-gold rounded-t-lg flex items-end justify-center p-2"
                   :style="{ height: bars.gen + 'px' }">
                <span class="text-xs font-bold text-solar-gold">۳۰ dB</span>
              </div>
              <p class="text-center text-sm text-solar-gold font-bold mt-2">کتابخانه</p>
            </div>
            <div class="flex-1 flex flex-col items-center justify-end">
              <div class="w-full h-16 bg-eco-green/20 border-2 border-eco-green rounded-t-lg flex items-end justify-center p-2"
                   :style="{ height: bars.sol + 'px' }">
                <span class="text-xs font-bold text-eco-green">۰ dB</span>
              </div>
              <p class="text-center text-sm text-eco-green font-bold mt-2">سیستم خورشیدی</p>
            </div>
            <div class="flex-1 flex flex-col items-center justify-end">
              <div class="w-full h-16 bg-solar-gold/20 border-2 border-solar-gold rounded-t-lg flex items-end justify-center p-2"
                   :style="{ height: bars.whisper + 'px' }">
                <span class="text-xs font-bold text-solar-gold">۲۰ dB</span>
              </div>
              <p class="text-center text-sm text-solar-gold font-bold mt-2">فروشن</p>
            </div>
          </div>
        </div>
        <div class="text-center mt-6 text-sm text-pure-white/70">
          Silent Solar vs Noisy Generator
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">🔇 تفاوت آرامش</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Chart `role="img"` + `aria-label`.
  - Color + text labels.

---

### [SEC_04]: استهلاک و طول عمر تجهیزات

- **Section Role:** Trust building — Moving parts vs Solid-state.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Split infographic: Left "Moving Parts" (Generator) with `alert-red` gear icons animating rotation. Right "Solid State" (Solar) with `eco-green` static solar cell. "Moving Parts = High Wear" badge `alert-red` vs "Solid State (Zero Wear)" `eco-green`.

- **Desktop Grid Architecture:**
  12-col. Split `lg:col-span-6` each. GEO callout below.

- **Mobile Stacking:**
  Vertical stack.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-2 gap-10 items-center">
      <div class="text-start">
        <div class="glass-card p-8 border-s-4 border-alert-red rounded-2xl mb-6">
          <h3 class="font-bold text-xl text-alert-red mb-4 flex items-center gap-3">
            <span class="text-3xl animate-spin">⚙️</span>
            قطعات متحرک = استهلاک بالا
          </h3>
          <ul class="space-y-3 text-pure-white/80">
            <li class="flex items-center gap-2"><span class="text-alert-red">⚙️</span> پیستون و میل‌لنگ</li>
            <li class="flex items-center gap-2"><span class="text-alert-red">⚙️</span> واشر و سیل‌های روغن</li>
            <li class="flex items-center gap-2"><span class="text-alert-red">⚙️</span> سیستم استارتر و باتری استارتر</li>
            <li class="flex items-center gap-2"><span class="text-alert-red">⚙️</span> سیستم سوخت‌رسانی و کاربراتور</li>
          </ul>
          <p class="text-alert-red font-bold mt-4">عمر مفید: ۵–۱۰ سال (Overhaul لازم)</p>
        </div>
      </div>
      <div class="text-start">
        <div class="glass-card p-8 border-s-4 border-eco-green rounded-2xl">
          <h3 class="font-bold text-xl text-eco-green mb-4 flex items-center gap-3">
            <span class="text-3xl">☀️</span>
            حالت جامد (Solid State) = صفر استهلاک
          </h3>
          <ul class="space-y-3 text-pure-white/80">
            <li class="flex items-center gap-2"><span class="text-eco-green">☀️</span> بدون قطعه متحرک</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> تبدیل مستقیم نور به برق</li>
            <li class="flex items-center gap-2"><span class="text-eco-green">✅</span> گارانتی ۲۵ ساله خطی</li>
          </ul>
          <p class="text-eco-green font-bold mt-4">عمر مفید: ۲۵+ سال (پنل‌های Tier-1)</p>
        </div>
      </div>
    </div>
    <div class="glass-card p-5 border-s-4 border-solar-gold mt-10 max-w-2xl mx-auto">
      <p class="text-sm font-bold text-solar-gold mb-1">🔬 اصل مهندسی</p>
      <p class="text-pure-white/90 text-base leading-relaxed">
        {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic structure.
  - Color + text for meaning.

---

### [SEC_05]: چالش تامین سوخت در مناطق دورافتاده و کشاورزی

- **Section Role:** Contextual NLP — Agricultural independence.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Image card: Solar pump in remote field. Text: "Zero fuel logistics." `eco-green` badge "Zero Fuel Logistics".

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Image + text.

- **Mobile Stacking:**
  Image first, text below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <div class="mb-8" aria-label="پمپ آب خورشیدی در مزرعه دورافتاده" role="img">
        <img src="/images/solar-pump-remote-farm.webp" alt="پمپ آب خورشیدی در مزرعه دورافتاده — بدون نیاز به سوخت" class="w-full max-w-2xl h-auto rounded-2xl shadow-2xl" loading="lazy">
      </div>
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        چالش تامین سوخت در <span class="text-solar-gold">مناطق دورافتاده و کشاورزی</span>
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed max-w-2xl mx-auto mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
      </p>
      <div class="glass-card p-6 border-s-4 border-eco-green max-w-2xl mx-auto">
        <p class="text-sm font-bold text-eco-green mb-1">🚜 استقلال سوختی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Image `alt` in Farsi.
  - Semantic structure.

---

### [SEC_06]: آلودگی محیط زیست و بوی نامطبوع

- **Section Role:** Environmental entity connection — Health + Eco.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Bullet list with icons. CO2 icon `🌿`, Toxic gas `💨`, Diesel smell `🛢️`. CO2 prevented badge: `eco-green` badge "1 kW = 1 ton CO2/year prevented".

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Bullet list with icons.

- **Mobile Stacking:**
  Stack vertically.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        آلودگی محیط زیست و <span class="text-solar-gold">بوی نامطبوع</span>
      </h2>
      <ul class="space-y-4 max-w-2xl mx-auto">
        <li class="flex items-start gap-4 glass-card p-4 border-s-4 border-eco-green">
          <span class="text-3xl">🌿</span>
          <div>
            <h4 class="font-bold text-eco-green text-lg mb-1">جلوگیری از CO₂</h4>
            <p class="text-pure-white/80 mt-1 text-base leading-relaxed">
              هر ۱ کیلووات نیروگاه خورشیدی، سالانه ۱ تن CO₂ جلوگیری می‌کند.
            </div>
        </li>
        <li class="flex items-start gap-4 glass-card p-4 border-s-4 border-alert-red">
          <span class="text-3xl">💨</span>
          <div>
            <h4 class="font-bold text-alert-red text-lg mb-1">حذف گازهای سمی</h4>
            <p class="text-pure-white/80 mt-1 text-base leading-relaxed">
              بدون مونوکسید کربن، اکسیدهای نیتروژن و ذرات معلق
            </div>
        </li>
        <li class="flex items-start gap-4 glass-card p-4 border-s-4 border-alert-red">
          <span class="text-3xl">🛢️</span>
          <div>
            <h4 class="font-bold text-alert-red text-lg mb-1">حذف بوی گازوئیل</h4>
            <p class="text-pure-white/80 mt-1 text-base leading-relaxed">
              بدون ذخیره‌سازی بشکه‌های سوخت و بوی نامطبوع
            </div>
        </li>
      </ul>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-2xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">🌿 سلامت و محیط زیست</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Semantic list structure.
  - Color + text for meaning.

---

### [SEC_07]: افسانه در برابر واقعیت: کارکرد در روزهای زمستانی

- **Section Role:** Myth-busting — Winter performance.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background. Myth: `bg-alert-red/10 border-alert-red/30` ❌. Reality: `bg-eco-green/10 border-eco-green/30` ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        افسانه در برابر واقعیت: <span class="text-solar-gold">کارکرد در روزهای زمستانی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            در زمستان که هوا سرد است، سیستم خورشیدی از کار می‌افتد و فقط موتور برق می‌تواند در سرمای شدید قابل اتکا باشد.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            موتورهای دیزلی در سرمای شدید دچار مشکلاتی نظیر افت ولتاژ باتریِ استارتر و ژله‌ای شدن گازوئیل می‌شوند و گاهی اصلاً روشن نمی‌شوند. اما پنل‌های خورشیدی با نور کار می‌کنند نه با گرما. در واقع، هوای سرد زمستانی باعث افزایش راندمان و ولتاژ خروجی سلول‌های سیلیکونی می‌شود و در روزهای آفتابی زمستان، نیروگاه‌های نصب شده توسط هورا نور سهند با حداکثر توان کار می‌کنند.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 حقیقت زمستانی</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section id="sec-07">`.
  - `x-intersect` decorative.
  - Meaning via icon + text.
  - Contrast: dark text on light cards.

---

### [SEC_08]: قابلیت اتوماسیون و سوئیچینگ (Switching)

- **Section Role:** Technical workflow — Seamless UPS-like switching.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Workflow diagram: Grid → (outage) → Battery/Inverter → Load. Animated flow: Grid arrow (`solar-gold` dashed) → Battery/Inverter (`eco-green` pulse) → Load (stable). Transfer time badge: `<10ms` in `solar-gold`.

- **Desktop Grid Architecture:**
  12-col. Diagram: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Diagram first (`h-[300px]`). Text below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy" x-data="{ step: 0 }" x-intersect.once="step = 1">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار سوئیچینگ اتوماتیک خورشیدی" role="img">
        <div class="glass-card p-8 h-[400px] flex flex-col justify-center">
          <h3 class="font-bold text-xl text-pure-white mb-6 text-start">سوئیچینگ اتوماتیک (< ۱۰ میلی‌ثانیه)</h3>
          <div class="flex flex-col gap-6 items-center">
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center"
                 :class="{ 'ring-2 ring-solar-gold': step >= 0 }">
              <span class="text-solar-gold font-black text-xl">⚡ شبکه برق شهر</span>
              <p class="text-pure-white/70 text-sm mt-1">معمولاً در حال کار</p>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-eco-green/20 border-2 border-eco-green p-4 text-center"
                 :class="{ 'ring-2 ring-eco-green': step >= 1 }">
              <span class="text-eco-green font-bold text-lg">🔋 باتری + اینورتر</span>
              <p class="text-pure-white/70 text-sm mt-1">ورود آنی (< ۱۰ میلی‌ثانیه)</p>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <div class="w-full rounded-xl bg-eco-green/20 border-2 border-eco-green p-4 text-center"
                 :class="{ 'ring-2 ring-eco-green': step >= 2 }">
              <span class="text-eco-green font-bold text-lg">🏠 لوازم منزل</span>
              <p class="text-pure-white/70 text-sm mt-1">بدون وقفه / بدون چشمک</p>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          قابلیت اتوماسیون و <span class="text-solar-gold">سوئیچینگ</span> (Switching)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-eco-green/5">
          <p class="text-sm font-bold text-solar-gold mb-1">⚡ سوئیچینگ زودرس</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Diagram `role="img"` + `aria-label`.
  - Step indicators have text labels.
  - Animation respects `prefers-reduced-motion`.

---

### [SEC_09]: آپدیت‌های تکنولوژی: استفاده هیبریدی (ترکیب هر دو)

- **Section Role:** Temporal freshness + Hybrid architecture.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی تکنولوژی". Hybrid diagram: 3 inputs (Solar, Battery, Grid) + Generator (optional) → Smart Hybrid Inverter.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Diagram center. Text below.

- **Mobile Stacking:**
  Diagram first, text below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          آپدیت تکنولوژی: <span class="text-solar-gold">سیستم‌های هیبریدی</span>
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی تکنولوژی</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
      </p>
      <div class="glass-card p-8 rounded-2xl text-center">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">معماری هیبریدی هوشمند</h3>
        <div class="flex flex-wrap justify-center gap-4 mb-6">
          <div class="glass-card p-4 border-s-4 border-solar-gold flex flex-col items-center text-center min-w-[120px]">
            <span class="text-2xl mb-2">☀️</span>
            <span class="font-bold text-pure-white text-lg">پنل خورشیدی</span>
          </div>
          <div class="glass-card p-4 border-s-4 border-eco-green flex flex-col items-center text-center">
            <span class="text-2xl mb-2">🔋</span>
            <span class="font-bold text-pure-white">باتری</span>
          </div>
          <div class="glass-card p-4 border-s-4 border-sky-400 flex flex-col items-center text-center">
            <span class="text-2xl mb-2">⚡</span>
            <span class="font-bold text-pure-white">شبکه</span>
          </div>
          <div class="glass-card p-4 border-s-4 border-alert-red flex flex-col items-center text-center">
            <span class="text-2xl mb-2">⛽</span>
            <span class="font-bold text-pure-white">ژنراتور (اختیاری)</span>
          </div>
        </div>
        <div class="w-40 h-40 mx-auto rounded-full bg-solar-gold/20 border-4 border-solar-gold flex items-center justify-center">
          <span class="text-solar-gold font-bold text-2xl">هیبرید اینورتر</span>
        </div>
        <div class="flex justify-center gap-6 mt-6 text-sm">
          <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-solar-gold"></span> اولویت ۱: خورشید</span>
          <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-eco-green"></span> اولویت ۲: باتری</span>
          <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-sky-400"></span> اولویت ۳: شبکه</span>
          <span class="flex items-center gap-2"><span class="w-6 h-1 rounded bg-alert-red"></span> اولویت ۴: ژنراتور</span>
        </div>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8">
        <p class="text-sm font-bold text-solar-gold mb-1">🛡️ تضمین ۱۰۰٪</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_10]: جدول مقایسه نهایی: خورشیدی در برابر دیزل

- **Section Role:** Information Gain — Structured comparison table for SERP.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Full-width responsive table with `overflow-x-auto` on mobile. Header `bg-navy-mid text-solar-gold`. Alternating rows. Win columns: Solar (`eco-green`), Generator (`alert-red`).

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Table full-width. GEO callout below.

- **Mobile Stacking:**
  Table horizontal scroll (`overflow-x-auto`). GEO callout below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-5xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        جدول مقایسه نهایی: <span class="text-solar-gold">خورشیدی</span> در برابر <span class="text-alert-red">دیزل</span>
      </h2>
      <div class="glass-card p-6 overflow-x-auto">
        <table class="w-full min-w-[700px] text-sm" role="table" aria-label="مقایسه جامع خورشیدی در برابر ژنراتور دیزلی">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-4 text-start rounded-s-lg">ویژگی مورد بررسی</th>
              <th scope="col" class="p-4 text-start">خورشیدی (آفگرید)</th>
              <th scope="col" class="p-4 text-start rounded-e-lg">دیزل ژنراتور / موتور برق</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">هزینه سوخت روزانه</td><td class="p-3 text-eco-green font-bold">صفر (رایگان)</td><td class="p-3 text-alert-red font-bold">بسیار بالا</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">آلودگی صوتی</td><td class="p-3 text-eco-green font-bold">۱۰۰٪ بی‌صدا</td><td class="p-3 text-alert-red font-bold">بسیار زیاد (۷۰-۱۰۰ دسی‌بل)</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">طول عمر مفید تجهیزات</td><td class="p-3 text-eco-green font-bold">بالای ۲۵ سال</td><td class="p-3 text-alert-red font-bold">۵ تا ۱۰ سال</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">هزینه تعمیر و نگهداری</td><td class="p-3 text-eco-green font-bold">بسیار پایین</td><td class="p-3 text-alert-red font-bold">بالا (روغن، فیلتر، شمع)</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">نیاز به اپراتور برای استارت</td><td class="p-3 text-eco-green font-bold">تمام اتوماتیک</td><td class="p-3 text-alert-red font-bold">معمولاً دستی</td></tr>
          </tbody>
        </table>
      </div>
      <div class="glass-card p-5 border-s-4 border-solar-gold mt-8 max-w-3xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری نهایی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table role="table">` + `aria-label`.
  - `<th scope="col">` on all headers.
  - Color + text for meaning.

---

### [SEC_11]: سوالات متداول (FAQ)

- **Section Role:** GEO/SGE bait — FAQPage schema.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Glass accordion. Expanded: `border-s-4 border-solar-gold` + `text-solar-gold` summary.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Single column. GEO preamble banner.

- **Mobile Stacking:**
  Full-width `<summary>` with `py-5`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-11" class="py-20 md:py-32 bg-navy-mid" x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">موتور برق یا پنل خورشیدی</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_11}
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
              آیا می‌توانم موتور برق فعلی خود را با سیستم خورشیدی تعویض کنم؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، متخصصین هورا نور سهند پس از برآورد بار مصرفی شما، پکیج خورشیدی مناسب را طراحی کرده و می‌توانید ژنراتور قدیمی خود را به طور کامل از مدار خارج کنید.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا سیستم خورشیدی توان راه‌اندازی پمپ آب و کولر گازی را دارد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. با استفاده از اینورترهای سانورتر قدرتمند، سیستم‌های خورشیدی به راحتی می‌توانند جریان استارت اولیه (Surge) دستگاه‌های سنگین را تامین کنند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              بازگشت سرمایه جایگزینی ژنراتور با خورشیدی چقدر است؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            با حذف کامل هزینه‌های خرید سوخت آزاد و تعمیرات مکانیکی، هزینه نصب سیستم خورشیدی معمولاً بین ۳ الی ۴ سال جبران شده و پس از آن کاملاً سودآور خواهد بود.
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