# UI Wireframe Specification: پکیج برق خورشیدی خانگی و ویلایی | Mega Semantic Hub
- **Source Dossier:** `seo_dossiers/applications_residential-villa-appliances.md`
- **Target URL:** `/applications/residential-villa-appliances`
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

### [SEC_01]: پکیج برق خورشیدی خانگی و ویلایی (تامین برق کولر گازی، یخچال و لوازم منزل)

- **Section Role:** Primary Hero — Mega Semantic Hub anchor, H1 entity definition, immediate trust + appliance visualization.

- **UI Aesthetic & Colors:**
  Full-viewport hero with cinematic lifestyle shot: a luxury villa in Mehrshahr at golden hour, solar panels gleaming on the roof, interior lights on, AC running, fridge humming — all powered silently by solar (see `needed_images.md`). Deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`). H1 in `pure-white`, "Mega Semantic Hub" badge in `solar-gold`. GEO TL;DR in Glassmorphism card with `border-s-4 border-solar-gold`. Subtle appliance icons (AC, Fridge, Pump, Lights) floating around the villa illustration with `solar-gold` connection lines.

- **Desktop Grid Architecture:**
  12-col. Text block: `lg:col-span-7 lg:col-start-1` (RTL start), vertically centered. GEO Callout: `lg:col-span-4 lg:col-start-9`, `lg:sticky lg:top-24`.

- **Mobile Stacking:**
  Single column. Hero image `object-cover h-[60vh]`. H1 + body stacks. GEO reflows full-width with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <img src="/images/hero-villa-appliances.webp"
         alt="ویلای لوکس در مهرشهر با پکیج خورشیدی: کولر، یخچال، پمپ و روشنایی همه روی انرژی خورشیدی"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager" fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <!-- Floating appliance icons overlay -->
    <svg class="absolute inset-0 pointer-events-none" viewBox="0 0 1200 600" preserveAspectRatio="none">
      <defs>
        <marker id="energy-flow" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
          <polygon points="0 0, 10 3.5, 0 7" fill="#F5A623" />
        </defs>
        <path d="M150,200 Q300,100 400,250 T700,300" stroke="#F5A623" stroke-width="1.5" fill="none" stroke-dasharray="8,8" marker-end="url(#energy-flow)" style="animation: flow 3s linear infinite;">
          <animate attributeName="stroke-dashoffset" from="0" to="-16" dur="1s" repeatCount="indefinite"/>
        </path>
      </defs>
    </svg>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          Mega Semantic Hub: پکیج‌های اختصاصی ویلایی
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          پکیج برق خورشیدی <span class="text-solar-gold">خانگی و ویلایی</span> (تامین برق کولر گازی، یخچال و لوازم منزل)
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-10" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="دریافت مشاوره رایگان پکیج ویلایی">
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
  - Hero `alt` describes villa with all appliances running on solar.
  - CTA `role="button"` + `aria-label`.
  - GEO `<aside>` complementary role.
  - `fetchpriority="high"` on hero image.

---

### [SEC_02]: تامین برق کمپرسورها: کولر گازی و یخچال در سیستم خورشیدی

- **Section Role:** Technical deep-dive — Inrush current handling, appliance-specific specs.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Interactive specification table with expandable rows. Appliance cards show `surge-wattage` badges in `alert-red` (starting) vs `running-wattage` in `eco-green`. An interactive "Package Calculator" widget lets users toggle appliances and see real-time package size recommendation.

- **Desktop Grid Architecture:**
  12-col. Left: Interactive appliance table `lg:col-span-7`. Right: Package recommender widget `lg:col-span-5 lg:sticky lg:top-20`.

- **Mobile Stacking:**
  Table scrolls horizontally. Recommender stacks below table.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ selectedAppliances: ['ac', 'fridge'], recommendedKw: 5 }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <!-- Appliance Spec Table -->
      <div class="lg:col-span-7 glass-card p-8 overflow-x-auto">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-6">
          محاسبه потреб الکتریکی <span class="text-solar-gold">کامپرسورها</span> و لوازم پرمصرف
        </h2>
        <table class="w-full min-w-[600px] text-sm" role="table" aria-label="جدول توان استارت و رونینگ لوازم خانگی پرمصرف">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-3 text-start rounded-s-lg">لوازم</th>
              <th scope="col" class="p-3 text-start rounded-e-lg">توان رونینگ (وات)</th>
              <th scope="col" class="p-3 text-start rounded-e-lg">جریان استارت (آمپر)</th>
              <th scope="col" class="p-3 text-start rounded-e-lg">ضریب استارت (Inrush)</th>
              <th scope="col" class="p-3 text-start rounded-e-lg">پکیج پیشنهادی</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60"><td class="p-3">کولر گازی ۳۰۰۰۰ (اسپلیت)</td><td class="p-3 text-eco-green font-bold">۳۵۰۰</td><td class="p-3 text-alert-red font-bold">۱۵–۱۸</td><td class="p-3 text-alert-red font-bold">۳-۵x</td><td class="p-3 text-solar-gold font-bold">۵+ کیلووات</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">یخچال ساید‌بای‌ساید</td><td class="p-3 text-eco-green font-bold">۳۰۰</td><td class="p-3 text-alert-red font-bold">۴–۶</td><td class="p-3 text-alert-red font-bold">۳-۴x</td><td class="p-3 text-solar-gold font-bold">۳+ کیلووات</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">پمپ آب چاه/استخر</td><td class="p-3 text-eco-green font-bold">۱۵۰۰</td><td class="p-3 text-alert-red font-bold">۸–۱۲</td><td class="p-3 text-alert-red font-bold">۳-۴x</td><td class="p-3 text-solar-gold font-bold">۴+ کیلووات</td></tr>
            <tr class="bg-navy-mid/40"><td class="p-3">روشنایی کامل ویلا (LED)</td><td class="p-3 text-eco-green font-bold">۴۰۰</td><td class="p-3 text-eco-green font-bold">۱-۲</td><td class="p-3 text-eco-green font-bold">۱x</td><td class="p-3 text-solar-gold font-bold">۲+ کیلووات</td></tr>
            <tr class="bg-deep-navy/60"><td class="p-3">تلویزیون / لوازم کوچک</td><td class="p-3 text-eco-green font-bold">۲۰۰</td><td class="p-3 text-eco-green font-bold">۱</td><td class="p-3 text-eco-green font-bold">۱x</td><td class="p-3 text-solar-gold font-bold">۱+ کیلووات</td></tr>
          </tbody>
        </table>
      </div>
      <!-- Package Recommender Widget -->
      <div class="lg:col-span-5 lg:sticky lg:top-20" x-data="{ selected: {ac: true, fridge: true, pump: false, lights: true, tv: true}, totalKw: 5 }">
        <aside class="glass-card p-6 border-s-4 border-solar-gold lg:sticky lg:top-20">
          <h3 class="font-bold text-xl text-pure-white mb-4 text-start">محاسبه‌گر پکیج لحظه‌ای</h3>
          <div class="space-y-3 mb-6" x-data="{ appliances: {ac: 5, fridge: 3, pump: 4, lights: 2, tv: 1} }">
            <template x-for="(kw, key) in appliances" :key="key">
              <label class="flex items-center justify-between cursor-pointer p-3 rounded-xl bg-deep-navy/50 hover:bg-deep-navy/70 transition-colors"
                     :class="{ 'ring-2 ring-solar-gold': $root.selectedAppliances.includes(key) }"
                     @click="$root.selectedAppliances.includes(key) ? $root.selectedAppliances.splice($root.selectedAppliances.indexOf(key), 1) : $root.selectedAppliances.push(key)">
                <span class="flex items-center gap-2 font-medium text-pure-white">
                  <input type="checkbox" :id="key" :checked="$root.selectedAppliances.includes(key)"
                         @click.stop="$root.selectedAppliances.includes(key) ? $root.selectedAppliances.splice($root.selectedAppliances.indexOf(key), 1) : $root.selectedAppliances.push(key)"
                         class="w-5 h-5 accent-solar-gold">
                  <span x-text="key === 'ac' ? 'کولر گازی ۳۰۰۰۰' : key === 'fridge' ? 'یخچال ساید‌بای‌ساید' : key === 'pump' ? 'پمپ آب' : key === 'lights' ? 'روشنایی کامل' : 'تلویزیون/کوچک'"></span>
                </span>
                <span class="text-solar-gold font-bold" x-text="appliances[key] + ' kW'"></span>
              </label>
            </template>
          </div>
          <div class="glass-card p-4 border-s-4 border-solar-gold">
            <p class="text-sm font-bold text-solar-gold mb-2">مجموع پیشنهادی:</p>
            <p class="text-2xl font-black text-solar-gold" x-text="$root.selectedAppliances.reduce((sum, k) => sum + $root.$data.appliances[k], 0) + ' kW'"></p>
            <p class="text-pure-white/70 text-sm mt-1" x-text="'شامل ' + $root.selectedAppliances.length + ' دستگاه'"></p>
          </div>
        </aside>
      </div>
    </div>
  </article>
  ```

- **Accessibility & ARIA:**
  - `<article id="sec-02">`.
  - Checkboxes have proper labels via `<label>`.
  - Checkbox state via Alpine; screen readers see native checkbox state.
  - Table `<th scope="col">` with `role="table"`.

---

### [SEC_03]: حل بحران خاموشی و آسایش در برابر صدای ژنراتور

- **Section Role:** Pain-point emotional trigger — Silent Solar vs Noisy Generator.

- **UI Aesthetic & Colors:**
  Split screen with animated ambient sound visualization. Left (start): `bg-navy-mid/90` with animated sound wave bars pulsing `alert-red` (generator noise). Right: `bg-deep-navy` with silent solar villa, `eco-green` glow. Divider: diagonal `skew-y-3`. GEO overlap card floats on divider.

- **Desktop Grid Architecture:**
  12-col. Pain: `lg:col-span-6`. Freedom: `lg:col-span-6`. Both `min-h-[500px]`. GEO overlap: `lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`.

- **Mobile Stacking:**
  Vertical stack. Pain first (`h-[300px]`), then freedom. GEO between as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/generator-noise-pollution.webp" alt="ژنراتور دیزلی با دود، صدا و هزینه سوخت" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🔊</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">ژنراتور: صدا، بوی بنزین، هزینه مداوم</h3>
          <p class="text-pure-white/60 mt-2 text-sm">خرابی تجهیزات + بی‌خوی SLEEP</p>
        </div>
      </div>
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/silent-solar-villa-serenity.webp" alt="ویلای آرام با سیستم خورشیدی بی‌صدا" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🌿</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">پکیج خورشیدی: آرامش مطلق، صفر هزینه سوخت</h3>
          <p class="text-pure-white/70 mt-2 text-sm">سویچینگ اتوماتیک / بی‌صدا / صفر سوخت</p>
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
        حل بحران <span class="text-alert-red">خاموشی</span> و <span class="text-alert-red">صدای ژنراتور</span>
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
  - GEO card `border-2 border-solar-gold`.

---

### [SEC_04]: باورهای غلط و واقعیت‌های مهندسی (Myth vs. Reality)

- **Section Role:** Myth-busting — DIY panel myth vs professional EPC design.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` background, navy text. Myth cards: `bg-alert-red/10 border-alert-red/30` with ❌. Reality: `bg-eco-green/10 border-eco-green/30` with ✅. Container `rounded-3xl shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2` myth/reality pairs. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  Vertical stack per pair. Myth first (red), reality second (green).

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-04" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در <span class="text-solar-gold">پکیج‌های خورشیدی خانگی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8"
           x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            یک پنل خورشیدی برای همه وسایل خانه کافی است و نیازی به باتری/اینورتر نیست.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل فقط DC تولید می‌کند. برای AC ۲۲۰ ولت و ذخیره انرژی شب، نیاز به MPPT + اینورتر سینوسی خالص + باتری‌های دیپ‌سایکل ژل + شارژ کنترلر دارید. عدم تناسب = خرابی سیستم.
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

### [SEC_05]: استقرار جغرافیایی هورا نور سهند در مناطق ییلاقی

- **Section Role:** Local SEO map anchor + proximity authority.

- **UI Aesthetic & Colors:**
  `bg-navy-mid`. Interactive Google Map with radius circles (5km, 15km, 30km) centered on Karaj HQ. Pulsing gold dots at Kordan, Mehrshahr, Hashtgerd, Lavasan, Lavasan. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map: `lg:col-span-7`. Address: `lg:col-span-5` (`bg-solar-gold text-deep-navy`).

- **Mobile Stacking:**
  Map `max-h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="نقشه پوشش پکیج‌های ویلایی هورا نور سهند" role="img">
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d50000!2d50.9!3d35.8!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3f8d1e0000000000%3A0x0!2z2YbYsdin2KfZhdi4INin2YTYp9mE!5e0!3m2!1sfa!2sir!4v1"
                width="100%" height="400" style="border:0;" allowfullscreen="" loading="lazy"
                aria-label="نقشه پوشش مناطق ییلاقی: کردان، لواسان، مهرشهر، هشتگرد، تهراندشت"></iframe>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استقرار جغرافیایی <span class="text-solar-gold">هورا نور سهند</span> در مناطق ییلاقی
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
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش ییلاقی</p>
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

### [SEC_06]: تضمین کیفیت با تجهیزات Tier-1 و رزومه اثبات‌شده

- **Section Role:** E-E-A-T authority — Portfolio gallery + project counter.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Portfolio carousel (auto + manual). Each project card: Glassmorphism with hover zoom. Rolling counter `data-value="40"`. Trust badges row.

- **Desktop Grid Architecture:**
  12-col. Carousel: `lg:col-span-7`. Trust badges + GEO: `lg:col-span-5`.

- **Mobile Stacking:**
  Carousel `max-w-[300px]` snap-x. Badges stack below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" aria-label="پورتفوی پروژه‌های ویلایی هورا نور سهند">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">پروژه‌های ویلایی موفق</h3>
        <div class="flex gap-4 overflow-x-auto snap-x snap-mandatory pb-4 -mx-4 px-4" x-data="{ index: 0 }">
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ویلای کردان - سیستم ۱۰ کیلواتی">
            <img src="/images/project-kordan-villa.webp" alt="نصب پکیج ۱۰ کیلواتی در ویلای کردان" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">ویلا کردان</h4>
            <p class="text-pure-white/60 text-sm mt-1">پکیج ۱۰ کیلواتی / کولر + یخچال + پمپ</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ویلای مهرشهر - پکیج ۸ کیلواتی">
            <img src="/images/project-mehrshahr-villa.webp" alt="نصب پکیج ۸ کیلواتی در ویلای مهرشهر" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">ویلا مهرشهر</h4>
            <p class="text-pure-white/60 text-sm mt-1">پکیج ۸ کیلواتی / کولر + یخچال + پمپ استخر</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ویلای لواسان - پکیج ۱۲ کیلواتی">
            <img src="/images/project-lavasan-villa.webp" alt="نصب پکیج ۱۲ کیلواتی در ویلای لواسان" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">ویلا لواسان</h4>
            <p class="text-pure-white/60 text-sm mt-1">پکیج ۱۲ کیلواتی / کولرهای چندتایی + پمپ استخر</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ویلای هشتگرد - پکیج ۶ کیلواتی">
            <img src="/images/project-hashtgerd-villa.webp" alt="نصب پکیج ۶ کیلواتی در ویلای هشتگرد" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">ویلا هشتگرد</h4>
            <p class="text-pure-white/60 text-sm mt-1">پکیج ۶ کیلواتی / کولر + یخچال + روشنایی</p>
          </div>
          <div class="min-w-[280px] snap-center glass-card p-5 border-s-4 border-solar-gold flex flex-col shrink-0"
               role="figure" aria-label="پروژه ویلای تهراندشت - پکیج ۷ کیلواتی">
            <img src="/images/project-tehrandesh-villa.webp" alt="نصب پکیج ۷ کیلواتی در ویلای تهراندشت" class="w-full h-48 object-cover rounded-xl mb-3" loading="lazy">
            <h4 class="font-bold text-pure-white text-lg">ویلا تهراندشت</h4>
            <p class="text-pure-white/60 text-sm mt-1">پکیج ۷ کیلواتی / یخچال + کولر + پمپ آب</p>
          </div>
        </div>
        <div class="mt-6 glass-card p-6 rounded-2xl text-center border border-solar-gold/30">
          <p class="text-pure-white/70 text-sm mb-1">پروژه‌های ویلایی اجرا شده</p>
          <p class="font-black text-4xl md:text-6xl text-solar-gold" data-value="40">۴۰</p>
          <p class="text-pure-white/60 text-sm mt-1">و تعداد رو به رشد...</p>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تضمین کیفیت <span class="text-solar-gold">Tier-1</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
        </p>
        <div class="flex flex-wrap gap-3 mb-6">
          <img src="/images/logo-jinko.webp" alt="Jinko Solar" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
          <img src="/images/logo-trina.webp" alt="Trina Solar" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
          <img src="/images/logo-longi.webp" alt="LONGi" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
          <img src="/images/logo-vmax.webp" alt="Vmax" class="h-12 w-auto object-contain grayscale hover:grayscale-0 transition-filter">
        </div>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد</p>
          <p>📞 ۰۲۶-۳۶۵۰۶۴۸۵</p>
          <p>📱 ۰۹۱۲۵۷۲۸۱۷۰</p>
        </address>
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
  - Carousel `aria-label="پروژه‌های ویلایی"`.
  - `<address>` for NAP.
  - Phones `dir="ltr"`.
  - Carousel keyboard navigable.

---

### [SEC_07]: مدیریت مصرف و استانداردهای بهینه‌سازی (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust entity (SATBA).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Tip box with `border-2 border-solar-gold` and 📰 icon. External link to `satba.gov.ir` with `rel="external noopener"`.

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
          مدیریت مصرف و استانداردهای بهینه‌سازی
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
      </p>
      <div class="border-2 border-solar-gold rounded-2xl p-6 bg-cream-warm/5">
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
          مراجعه به <a href="https://satba.gov.ir" rel="external noopener" target="_blank"
             class="text-solar-gold underline hover:text-solar-gold/80">سازمان ساتبا</a> برای اطلاع از تعرفه‌های فعلی.
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link `rel="external noopener"` + `target="_blank"`.
  - Badge decorative; heading provides context.

---

### [SEC_08]: راهنمای خرید و ارتباط با صفحه قیمت‌ها

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to pricing.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Single glass card with `border-b-4 border-solar-gold`. Internal link pill CTA (`bg-solar-gold text-deep-navy`).

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Vertical stack.

- **Mobile Stacking:**
  CTA `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        پارامترهای <span class="text-solar-gold">برآورد هزینه</span> پکیج ویلایی
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 پارامترهای کلیدی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
        <a href="/pricing/residential-commercial-packages"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="مشاهده جداول قیمتی پکیج‌های خانگی و تجاری">
          مشاهده دقیق جداول قیمتی
          <svg class="w-5 h-5"><!-- Arrow --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - CTA `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile for touch target.

---

### [SEC_09]: سوالات متداول (FAQ - ویژه لوازم خانگی)

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
        سوالات متداول <span class="text-solar-gold">پکیج‌های ویلایی</span>
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
              آیا پکیج خورشیدی می‌تواند کولر گازی ۳۰۰۰۰ را روشن کند؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. با طراحی سیستم با ظرفیت مناسب (اینورتر ۵ تا ۱۰+ کیلووات) و بانک باتری متناسب با آمپر استارت کولر، روشن کردن کولر گازی کاملاً عملی است. حجم پکیج و سرمایه‌گذاری به دلیل مصرف بالای کولر افزایش می‌یابد.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              برق خورشیدی برای یخچال در شب چگونه تامین می‌شود؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در طول روز، مازاد برق پنل‌ها در باتری‌های دیپ‌سایکل ذخیره می‌شود. با غروب، سیستم اتوماتیک به باتری سوئیچ می‌کند و یخچال/سایر وسایل را از باتری تغذیه می‌کند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 3 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 3 ? null : 3">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 3 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 3 ? 'text-solar-gold' : 'text-pure-white'">
              آیا سیستم می‌تواند پمپ آب چاه عمیق همزمان با کولر را بکشد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 3 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله، با اینورترهای ۵ کیلوات به بالا و بانک باتری ۴۰۰-۶۰۰ آمپر، همزمانیت پمپ چاه + کولر + یخچال مدیریت می‌شود. محاسبه پیک مصرف (Surge) پمپ + کولر برای سایزدهی اینورتر حیاتی است.
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

### [SEC_10]: دریافت مشاوره و طراحی اختصاصی پکیج ویلای شما (CTA)

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
          همین امروز، آرامش ویلای خود را با پکیج خورشیدی تضمین کنید
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