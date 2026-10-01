# UI Wireframe Specification: محاسبه‌گر آنلاین برق خورشیدی | فرمول ظرفیت و هزینه
- **Source Dossier:** `seo_dossiers/pricing_solar-calculator.md`
- **Target URL:** `/pricing/solar-calculator`
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

### [SEC_01]: محاسبه‌گر آنلاین ظرفیت و هزینه احداث سیستم برق خورشیدی

- **Section Role:** Primary Hero — Interactive Calculator Tool (SoftwareApplication entity), immediate value delivery.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a subtle animated grid background (`bg-[url('/images/grid-pattern.svg')]`) suggesting engineering precision. Deep-navy base (`bg-deep-navy`). The calculator card is the hero itself — a large Glassmorphism card (`glass-card`) anchored center, `lg:w-[90%] xl:w-[80%]`. H1 in `pure-white`, "ماشین‌حساب مهندسی" badge in `solar-gold`. Real-time output panel on the right (sticky) shows live-updating: Required kW, Battery Ah, Estimated Cost. GEO TL;DR in a floating Glassmorphism callout on the left sidebar.

- **Desktop Grid Architecture:**
  12-col. Calculator form: `lg:col-span-7`. Live output panel: `lg:col-span-5 lg:sticky lg:top-24`. GEO callout: `lg:col-span-4 lg:col-start-9 lg:sticky lg:top-24` (stacked below output).

- **Mobile Stacking:**
  Single column. Calculator full-width. Output panel collapses into an accordion below form. GEO reflows as banner.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden bg-deep-navy py-16 md:py-24" x-data="calculatorApp()">
    <div class="absolute inset-0 bg-[url('/images/grid-pattern.svg')] opacity-5"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 py-12">
      <!-- Calculator Form -->
      <div class="lg:col-span-7 space-y-6">
        <div class="text-start">
          <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-4">
            ابزار مهندسی محاسبه‌گر آنلاین
          </span>
          <h1 class="font-vazirmatn font-black text-4xl md:text-5xl leading-tight text-pure-white mb-4">
            محاسبه‌گر آنلاین <span class="text-solar-gold">ظرفیت و هزینه</span> سیستم برق خورشیدی
          </h1>
          <p class="text-lg md:text-xl text-pure-white/80 max-w-2xl leading-relaxed mb-6">
            {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
          </p>
        </div>
        <div class="glass-card p-6 md:p-8 space-y-6" x-data="calculatorForm()">
          <h3 class="font-bold text-xl text-pure-white mb-4">مشخصات مصرف‌کننده‌ها</h3>
          <div class="space-y-4" x-data="{ appliances: { ac: {qty:0, hours:8}, fridge: {qty:1, hours:24}, lights: {qty:10, hours:5}, tv: {qty:1, hours:4}, pump: {qty:0, hours:2} } }">
            <template x-for="(app, key) in appliances" :key="key">
              <div class="glass-card p-4 rounded-xl border border-white/10">
                <div class="flex items-center justify-between mb-3">
                  <label class="font-bold text-lg text-pure-white" :for="key" x-text="key === 'ac' ? 'کولر گازی (اسپلیت)' : key === 'fridge' ? 'یخچال / فریز' : key === 'lights' ? 'روشنایی (LED)' : key === 'tv' ? 'تلویزیون / لپ‌تاپ' : 'پمپ آب / پمپ استخر'"></label>
                  <span class="text-solar-gold font-bold" x-text="appliances[key].watts + ' W'"></span>
                </div>
                <div class="grid grid-cols-2 gap-4">
                  <div>
                    <label class="text-sm text-pure-white/70 block mb-1">تعداد</label>
                    <input type="number" min="0" max="20" step="1"
                           x-model.number="appliances[key].qty"
                           class="w-full px-4 py-2 bg-deep-navy/50 border border-white/10 rounded-xl text-pure-white focus:border-solar-gold focus:outline-none">
                  </div>
                  <div>
                    <label class="text-sm text-pure-white/70 block mb-1">ساعات کارکرد روزانه</label>
                    <input type="number" min="0" max="24" step="0.5"
                           x-model.number="appliances[key].hours"
                           class="w-full px-4 py-2 bg-deep-navy/50 border border-white/10 rounded-xl text-pure-white focus:border-solar-gold focus:outline-none">
                  </div>
                </div>
              </div>
            </template>
          </div>
          <div class="pt-4 border-t border-white/10">
            <label class="text-sm text-pure-white/70 block mb-1">ساعات آفتابی مفید (PSH) منطقه شما</label>
            <select x-model="psh"
                    class="w-full px-4 py-2 bg-deep-navy/50 border border-white/10 rounded-xl text-pure-white focus:border-solar-gold focus:outline-none appearance-none bg-no-repeat bg-right pr-10"
                    style="background-image: url('data:image/svg+xml;charset=US-ASCII,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 24 24%22 fill=%22none%22 stroke=%22%23F5A623%22 stroke-width=%222%22><polyline points=%226 9 12 15 18 9%22></polyline></svg>'); background-size: 16px;">
              <option value="4.5">منطقه Abrri (PSH 4.5)</option>
              <option value="5.0" selected>منطقه Alborz/Tehran (PSH 5.0)</option>
              <option value="5.5">منطقه جنوبی ایران (PSH 5.5)</option>
              <option value="4.0">مناطق شمالی/مرتفع (PSH 4.0)</option>
            </select>
          </div>
          <div class="pt-4 border-t border-white/10">
            <label class="text-sm text-pure-white/70 block mb-1">معماری سیستم</label>
            <div class="flex gap-4">
              <label class="flex items-center gap-2 cursor-pointer">
                <input type="radio" name="systemType" value="offgrid" x-model="systemType"
                       class="w-5 h-5 accent-solar-gold">
                <span class="text-pure-white">آفگرید (Off-Grid) — با باتری</span>
              </label>
              <label class="flex items-center gap-2 cursor-pointer">
                <input type="radio" name="systemType" value="ongrid" x-model="systemType"
                       class="w-5 h-5 accent-solar-gold">
                <span class="text-pure-white">آنگرید (On-Grid) — متصل به شبکه</span>
              </label>
              <label class="flex items-center gap-2 cursor-pointer">
                <input type="radio" name="systemType" value="hybrid" x-model="systemType"
                       class="w-5 h-5 accent-solar-gold">
                <span class="text-pure-white">هیبریدی (Hybrid) — ترکیبی</span>
              </label>
            </div>
          </div>
          <button @click="calculate()"
                  class="w-full md:w-auto px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors text-lg"
                  aria-label="محاسبه ظرفیت و هزینه">
            محاسبه ظرفیت و هزینه
          </button>
        </div>
      </div>
      <!-- Live Output Panel -->
      <div class="lg:col-span-5 space-y-6">
        <aside class="lg:sticky lg:top-24 glass-card p-6 border-s-4 border-solar-gold space-y-6" aria-label="خروجی محاسبه لحظه‌ای">
          <h3 class="font-bold text-xl text-pure-white text-start mb-4">خروجی محاسبه لحظه‌ای</h3>
          <div class="glass-card p-4 border-s-4 border-solar-gold space-y-3">
            <div class="flex justify-between items-center">
              <span class="text-pure-white/80">توان مورد نیاز</span>
              <span class="text-2xl font-black text-solar-gold" x-text="requiredKw + ' kW'"></span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-pure-white/80">تعداد پنل‌های پیشنهادی</span>
              <span class="text-xl font-bold text-solar-gold" x-text="panelCount + ' عدد'"></span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-pure-white/80">ظرفیت باتری پیشنهادی</span>
              <span class="text-xl font-bold text-solar-gold" x-text="batteryAh + ' Ah'"></span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-pure-white/80">سایز اینورتر پیشنهادی</span>
              <span class="text-xl font-bold text-solar-gold" x-text="inverterKw + ' kW'"></span>
            </div>
            <div class="flex justify-between items-center pt-4 border-t border-white/10">
              <span class="text-pure-white/80">برآورد هزینه تقریبی</span>
              <span class="text-2xl font-black text-eco-green" x-text="estimatedCost + ' میلیون تومان'"></span>
            </div>
          </div>
          <!-- GEO Callout -->
          <div class="glass-card p-5 border-s-4 border-solar-gold">
            <p class="text-sm font-bold text-solar-gold mb-1">🔑 نکته کلیدی</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_01}
            </p>
          </div>
        </aside>
      </div>
    </div>
  </header>
  ```

- **Accessibility & ARIA:**
  - `<header id="sec-01">` landmark.
  - Form inputs have `<label>` with `for` attributes.
  - Output panel `aria-live="polite"` for live updates.
  - `fetchpriority="high"` not needed (no hero image).

---

### [SEC_02]: فرمول محاسبه برق خورشیدی (مبانی ریاضی و فیزیک)

- **Section Role:** Technical authority — LaTeX-rendered formula block, Information Gain.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Centered LaTeX-rendered formula block using MathJax/KaTeX. Formula: `Total Array (W) = (Daily Wh × 1.3) ÷ PSH`. Color-coded variables: `Daily Wh` in `solar-gold`, `PSH` in `eco-green`, `Loss Factor` in `alert-red`. Below: interactive variable explainer cards.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Formula block full-width. Variable cards: `grid-cols-3 gap-4` below.

- **Mobile Stacking:**
  Formula centered. Variable cards stack vertically.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-10">
        فرمول <span class="text-solar-gold">محاسبه برق خورشیدی</span> (مبانی ریاضی و فیزیک)
      </h2>
      <!-- LaTeX Formula Block -->
      <div class="glass-card p-8 rounded-2xl mb-10 text-center" style="font-family: 'KaTeX_Main', serif;">
        <p class="text-pure-white/70 text-sm mb-4 text-start">فرمول پایه محاسبه آرایه پنل خورشیدی</p>
        <div class="text-2xl md:text-3xl font-black text-pure-white leading-relaxed" style="font-family: 'KaTeX_Main', serif;">
          $$P_{array} = \frac{E_{daily} \times (1 + L_{factor})}{PSH}$$
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-8 text-start">
          <div class="glass-card p-4 border-s-4 border-solar-gold">
            <span class="text-solar-gold font-bold text-lg">E<sub>daily</sub></span>
            <p class="text-pure-white/80 mt-1 text-sm">مصرف روزانه (وات-ساعت)</p>
          </div>
          <div class="glass-card p-4 border-s-4 border-alert-red">
            <span class="text-alert-red font-bold text-lg">L<sub>factor</sub></span>
            <p class="text-pure-white/80 mt-1 text-sm">ضریب تلفات (۱.۲–۱.۳)</p>
          </div>
          <div class="glass-card p-4 border-s-4 border-eco-green">
            <span class="text-eco-green font-bold text-lg">PSH</span>
            <p class="text-pure-white/80 mt-1 text-sm">ساعات آفتابی مفید (Peak Sun Hours)</p>
          </div>
        </div>
      </div>
      <div class="text-start space-y-6">
        <h3 class="font-bold text-xl text-pure-white mb-4">تفاوت <span class="text-solar-gold">وات</span> و <span class="text-eco-green">وات-ساعت</span></h3>
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
  - MathJax/KaTeX rendered formulas need `role="math"` and `aria-label` with Farsi description.
  - Variable cards have semantic structure.

---

### [SEC_03]: متغیر اقلیمی: تاثیر تابش منطقه البرز بر محاسبات

- **Section Role:** Regional data integration — PSH map, regional relevance.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Infographic: Sun arc over Alborz map with `solar-gold` arc line showing "5.5 PSH" window. Map uses `solar-gold` pulse dots for Karaj, Mehrshahr, Kordan. PSH value badge: `bg-eco-green text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map/Illustration: `lg:col-span-6 lg:sticky lg:top-20`. Text: `lg:col-span-6`.

- **Mobile Stacking:**
  Map first (`h-[300px]`), then text.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" aria-label="نمودار قوس خورشید و PSH منطقه البرز" role="img">
        <div class="relative h-[500px] bg-navy-mid/50 rounded-2xl overflow-hidden flex items-center justify-center">
          <img src="/images/alborz-psh-map.svg" alt="نمودار قوس خورشید و PSH ۵.۵ منطقه البرز" class="w-full h-full object-contain" loading="lazy">
          <div class="absolute top-1/3 start-1/4 transform -translate-x-1/2 -translate-y-1/2">
            <div class="bg-eco-green text-deep-navy text-xs font-bold px-3 py-1 rounded-full">۵.۵ PSH</div>
          </div>
          <div class="absolute top-1/2 start-3/4 transform -translate-x-1/2 -translate-y-1/2">
            <div class="w-6 h-6 rounded-full bg-solar-gold animate-ping"></div>
            <div class="absolute inset-0 w-6 h-6 rounded-full bg-solar-gold/30 animate-ping"></div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          متغیر اقلیمی: تاثیر <span class="text-solar-gold">تابش منطقه البرز</span> بر محاسبات
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
        </p>
        <div class="glass-card p-5 border-s-4 border-eco-green bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">☀️ مزیت اقلیمی البرز</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Map `role="img"` + `aria-label`.
  - Color + text for PSH badge.

---

### [SEC_04]: باورهای غلط در محاسبه سایز سیستم (Myth vs. Reality)

- **Section Role:** Myth-busting — Daytime vs Nighttime calculation error.

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
        باورهای غلط در <span class="text-solar-gold">محاسبه سایز سیستم</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8" x-intersect.once="revealed = true">
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            اگر دستگاه ۱۰۰۰ وات دارید، یک پنل ۱۰۰۰ واتی برای آن کافی است.
          </p>
        </div>
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت محاسباتی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پنل ۱۰۰۰ واتی در روز فقط مصرف لحظه‌ای را پوشش می‌دهد. برای تامین برق شب، باید پannel‌های بیشتری نصب کنید که هم روز مصرف را پوشش دهند و هم باتری‌ها را برای شب شارژ کنند. فرمول دوگانه: بار روزانه + شارژ باتری شبانه.
          </p>
        </div>
      </div>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔑 خطای محاسباتی رایج</p>
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

### [SEC_05]: محاسبه ظرفیت باتری (عمق دشارژ DoD)

- **Section Role:** Component-level sizing — Battery DoD progress bar.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Animated battery progress bar: Green zone (0-50% DoD) → `eco-green`, Yellow zone (50-80%) → `solar-gold`, Red zone (80-100%) → `alert-red`. Animated battery icon fills to 50% (green zone) on scroll.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Battery animation center. Text below.

- **Mobile Stacking:**
  Same vertical stack.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy" x-data="{ doD: 50 }">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        محاسبه ظرفیت <span class="text-solar-gold">باتری</span> (عمق دشارژ <span class="text-eco-green">DoD</span>)
      </h2>
      <!-- Animated Battery Visual -->
      <div class="relative w-[200px] h-[300px] mx-auto mb-10" x-data="{ fillPercent: 50 }" x-intersect.once="fillPercent = 50">
        <div class="relative w-full h-full">
          <svg viewBox="0 0 100 200" class="w-full h-full">
            <!-- Battery Outline -->
            <rect x="10" y="10" width="80" height="160" rx="5" fill="none" stroke="#F5A623" stroke-width="3"/>
            <rect x="40" y="0" width="20" height="10" rx="2" fill="#F5A623"/>
            <!-- Fill -->
            <rect x="13" y="170" width="74" height="1" rx="2" fill="#E74C4C"/>
            <rect x="13" y="130" width="74" height="40" rx="2" fill="#F5A623"/>
            <rect x="13" y="30" width="74" height="100" rx="2" fill="#2ECC71"/>
            <!-- Liquid Fill Animation -->
            <rect x="13" y="170" width="74" height="1" rx="2" fill="#E74C4C">
              <animate attributeName="y" from="170" to="70" dur="2s" fill="freeze"/>
              <animate attributeName="height" from="1" to="100" dur="2s" fill="freeze"/>
            </rect>
          </svg>
          <!-- Zone Labels -->
          <div class="flex justify-between mt-4 text-xs">
            <span class="text-eco-green font-bold">امن (۰-۵۰٪ DoD)</span>
            <span class="text-solar-gold font-bold">هشدار (۵۰-۸۰٪)</span>
            <span class="text-alert-red font-bold">خطر (۸۰-۱۰۰٪)</span>
          </div>
        </div>
      </div>
      <h3 class="font-bold text-xl text-pure-white mb-4">عمق دشارژ (DoD) و عمر باتری</h3>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed text-center mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
      </p>
      <div class="glass-card p-5 border-s-4 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">🔋 اصل مهندسی</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - SVG `role="img"` + `aria-label`.
  - Color + text labels for zones.
  - Animation is decorative (`prefers-reduced-motion` respected via CSS).

---

### [SEC_06]: استانداردهای وزارت نیرو در برآورد ظرفیت (آپدیت ۱۴۰۳)

- **Section Role:** Temporal freshness + outbound trust (SATBA).

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Badge `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` "بروزرسانی ۱۴۰۳". Trust badges grid. External link to `satba.gov.ir` with `rel="external noopener"`.

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
          استانداردهای وزارت نیرو در برآورد ظرفیت
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2">⚡</span>
          <h4 class="font-bold text-pure-white text-lg"><a href="https://satba.gov.ir" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">سازمان ساتبا</a></h4>
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

### [SEC_07]: استخراج لیست قیمت پس از تعیین ظرفیت

- **Section Role:** Internal linking bridge — Anti-cannibalization flow to pricing pages.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Two distinct pill buttons in glass card: one to `/pricing/residential-commercial-packages` (Villa), one to `/pricing/industrial-power-plants` (Industrial). Each with distinct icon.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Two-button row side-by-side on desktop, stacked on mobile.

- **Mobile Stacking:**
  Stacked vertically, each `w-full`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        استخراج لیست <span class="text-solar-gold">قیمت</span> پس از تعیین ظرفیت
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <a href="/pricing/residential-commercial-packages"
             class="inline-flex items-center gap-3 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
             role="button"
             aria-label="مشاهده قیمت پکیج‌های ویلایی و تجاری">
            <svg class="w-6 h-6"><!-- Home Icon --></svg>
            <span class="font-bold text-lg">مشاهده قیمت پکیج‌های خانگی</span>
          </a>
          <a href="/pricing/industrial-power-plants"
             class="inline-flex items-center gap-3 px-8 py-4 bg-eco-green text-pure-white font-bold rounded-2xl hover:bg-eco-green/90 transition-colors w-full md:w-auto justify-center"
             role="button"
             aria-label="مشاهده قیمت نیروگاه‌های صنعتی">
            <svg class="w-6 h-6"><!-- Factory Icon --></svg>
            <span class="font-bold text-lg">مشاهده قیمت نیروگاه‌های صنعتی</span>
          </a>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Buttons `role="button"` + descriptive `aria-label`.
  - `w-full` on mobile for touch target.

---

### [SEC_08]: محاسبه نرخ بازگشت سرمایه (ROI)

- **Section Role:** Value proposition — Dynamic ROI gauge.

- **UI Aesthetic & Colors:**
  `bg-deep-navy` → `bg-navy-mid` gradient. Gauge visual: semicircular gauge (`svg`) with pointer. Red zone (0-3y) → `alert-red`, Yellow (3-5y) → `solar-gold`, Green (5+y) → `eco-green`. Pointer animates to ~4y on load.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl`. Gauge centered. Text below.

- **Mobile Stacking:**
  Gauge smaller, stacks above text.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-gradient-to-b from-deep-navy to-navy-mid" x-data="{ roiYears: 4 }" x-intersect.once="roiYears = 4">
    <div class="container mx-auto px-4 max-w-3xl text-center">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-8">
        محاسبه نرخ <span class="text-solar-gold">بازگشت سرمایه</span> (ROI)
      </h2>
      <!-- ROI Gauge -->
      <div class="relative w-[250px] h-[250px] mx-auto mb-10" x-data="{ angle: -90 }" x-intersect.once="angle = 45">
        <svg viewBox="0 0 300 300" class="w-full h-full">
          <!-- Background Arc -->
          <path d="M 150 150 L 150 30 A 120 120 0 0 1 270 150" stroke="#E74C4C" stroke-width="20" fill="none" stroke-linecap="round"/>
          <path d="M 150 150 L 270 150 A 120 120 0 0 1 30 150" stroke="#F5A623" stroke-width="20" fill="none" stroke-linecap="round"/>
          <path d="M 150 150 L 30 150 A 120 120 0 0 0 150 30" stroke="#2ECC71" stroke-width="20" fill="none" stroke-linecap="round"/>
          <!-- Pointer -->
          <line x1="150" y1="150" x2="150" y2="30" stroke="#FFFFFF" stroke-width="4" stroke-linecap="round">
            <animateTransform attributeName="transform" type="rotate" from="-90 150 150" to="45 150 150" dur="1.5s" fill="freeze"/>
          </line>
        </svg>
        <div class="flex justify-center gap-6 mt-6 text-xs">
          <span class="text-alert-red font-bold">۳ سال (قرمز)</span>
          <span class="text-solar-gold font-bold">۳-۵ (طلایی)</span>
          <span class="text-eco-green font-bold">۵+ (سبز)</span>
        </div>
      </div>
      <h3 class="font-bold text-xl text-pure-white mb-4">نرخ بازگشت سرمایه</h3>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed max-w-2xl mx-auto mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
      </p>
      <div class="glass-card p-5 border-s-4 border-solar-gold max-w-2xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Gauge `role="img"` + `aria-label="نمودار بازگشت سرمایه: ۴ سال در ناحیه طلایی"`.
  - Color + text labels for zones.
  - Animation respects `prefers-reduced-motion`.

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
        سوالات متداول <span class="text-solar-gold">ماشین‌حساب خورشیدی</span>
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
              تفاوت "وات" و "وات-ساعت" در محاسبه برق خورشیدی چیست؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            "وات" (Watt) توان لحظه‌ای است (مثلا لامپ ۱۰ وات). "وات-ساعت" (Wh) انرژی مصرفی در زمان است. لامپ ۱۰ وات در ۱۰ ساعت = ۱۰۰ وات‌ساعت. محاسبات باتری/پنل بر اساس وات‌ساعت است.
          </div>
        </details>
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button" aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا توان استارت (Surge) یخچال را باید در ماشین‌حساب وارد کنم؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            بله. توان استارت یخچال/پمپ ۳ تا ۵ برابر توان نامی است. محاسبه‌گر پیشرفته ما این ضریب را به صورت خودکار برای موتورهای القایی لحاظ می‌کند.
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

### [SEC_10]: رزرو وقت برای طراحی دقیق نقشه الکتریکال (CTA)

- **Section Role:** CRO conversion — NAP + Send-to-WhatsApp feature.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width. Text `text-deep-navy`. Oversized phones. "Send to WhatsApp" button with share intent.

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
          همین امروز، طراحی دقیق سیستم خورشیدی خود را آغاز کنید
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
        <a href="https://wa.me/989125728170?text=سلام،%20نتیجه%20محاسبه‌گر%20خورشیدی%20را%20بررسی%20کنید"
           class="inline-flex items-center gap-2 mt-6 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors"
           role="button" aria-label="ارسال نتیجه محاسبه به واتس‌اپ">
          <svg class="w-5 h-5"><!-- WhatsApp --></svg>
          ارسال نتیجه محاسبه به واتس‌اپ
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