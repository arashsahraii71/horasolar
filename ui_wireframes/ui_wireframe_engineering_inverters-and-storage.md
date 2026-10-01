# UI Wireframe Specification: اینورتر خورشیدی و باتری ژل | تجهیزات نیروگاهی | هورا نور
- **Source Dossier:** `seo_dossiers/engineering_inverters-and-storage.md`
- **Target URL:** `/engineering/inverters-and-storage`
- **Page Language:** `fa` | **Direction:** `rtl`

---

## GLOBAL DESIGN SYSTEM

### Color Palette Variables
| Token | HEX | Tailwind Alias | Usage |
|-------|-----|----------------|-------|
| `--color-primary` | `#F5A623` | `solar-gold` | CTAs, GEO callout borders, active accents |
| `--color-dark` | `#0A1929` | `deep-navy` | Backgrounds, hero overlays, headings |
| `--color-light` | `#FFFFFF` | `pure-white` | Card surfaces, body text on dark |
| `--color-accent-1` | `#1E3A5F` | `navy-mid` | Secondary cards, table headers |
| `--color-accent-2` | `#FFF4E0` | `cream-warm` | Soft highlight backgrounds, GEO blocks on light |
| `--color-accent-3` | `#2ECC71` | `eco-green` | Success, pure sine wave, MPPT gain |
| `--color-danger` | `#E74C3C` | `alert-red` | Modified wave, starter battery fail, PWM loss |
| `--color-glass-bg` | `rgba(255,255,255,0.08)` | — | Glassmorphism fill |
| `--color-glass-border` | `rgba(255,255,255,0.18)` | — | Glassmorphism stroke |

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

### [SEC_01]: مشخصات اینورترهای متصل/منفصل و باتری‌های ذخیره‌ساز خورشیدی

- **Section Role:** Primary Hero — H1 entity optimization + engineering authority; brain/heart metaphor.

- **UI Aesthetic & Colors:**
  Full-viewport dark hero with glowing circuit-path animation: Solar Panels (solar-gold pulse) → Inverter (deep-navy chip with gold traces) → Battery Bank (eco-green glow). Background `bg-gradient-to-b from-deep-navy via-deep-navy/90 to-deep-navy` with subtle dot grid. Floating badge `bg-solar-gold/10 text-solar-gold border border-solar-gold/20`. GEO TL;DR in Glassmorphism with `border-s-4 border-solar-gold` and soft `bg-cream-warm/5`.

- **Desktop Grid Architecture:**
  12-col. Text + metaphor: `lg:col-span-7 lg:col-start-1` vertically centered, `text-start`. GEO sticky callout: `lg:col-span-4 lg:col-start-9 lg:sticky lg:top-24`. Circuit visual spans full hero as absolute layered SVG behind grid with `pointer-events-none`.

- **Mobile Stacking:**
  Single column. Circuit SVG `h-[280px] object-cover opacity-60`. H1 stacks first, GEO reflows full-width `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden bg-deep-navy" x-data="{ loaded: false }" x-init="setTimeout(()=> loaded=true, 100)">
    <!-- Glowing Circuit Path Background -->
    <svg class="absolute inset-0 w-full h-full pointer-events-none opacity-40" viewBox="0 0 1200 600" preserveAspectRatio="xMidYMid slice" role="img" aria-hidden="true">
      <path d="M80 300 H400 C420 300 430 280 450 280 H550 C570 280 580 300 600 300 H720 C740 300 750 280 770 280 H1100" stroke="#F5A623" stroke-width="2.5" fill="none" stroke-dasharray="8 8" opacity="0.7"/>
      <circle cx="450" cy="280" r="22" fill="#0A1929" stroke="#F5A623" stroke-width="2"/>
      <circle cx="770" cy="280" r="28" fill="#0A1929" stroke="#2ECC71" stroke-width="2"/>
    </svg>
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/60 via-transparent to-deep-navy"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <div class="lg:col-span-7 text-start">
        <span class="inline-flex items-center gap-2 px-4 py-1.5 bg-solar-gold/10 text-solar-gold text-sm font-bold rounded-full border border-solar-gold/20 mb-6">
          مغز و قلب نیروگاه — اینورتر + باتری
        </span>
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          مشخصات <span class="text-solar-gold">اینورترهای متصل/منفصل</span> و باتری‌های ذخیره‌ساز خورشیدی
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <div class="flex flex-wrap gap-4 mt-8">
          <a href="#sec-11" class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
             role="button" aria-label="استعلام قیمت اینورتر و باتری">
            استعلام قیمت اینورتر و باتری
            <svg class="w-5 h-5 rotate-180" aria-hidden="true"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>
          <a href="#sec-03" class="inline-flex items-center gap-2 px-6 py-4 glass-card text-pure-white font-bold rounded-2xl hover:bg-pure-white/10 transition-colors"
             role="button" aria-label="مشاهده برندهای گرووات و سانورتر">
            برندهای معتبر
          </a>
        </div>
      </div>
      <aside class="lg:col-span-4 lg:col-start-9 lg:sticky lg:top-24 glass-card p-6 border-s-4 border-solar-gold" role="complementary" aria-label="خلاصه کلیدی اینورتر و باتری">
        <p class="text-sm font-bold text-solar-gold mb-2">خلاصه کلیدی</p>
        <p class="text-base text-pure-white/90 leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_01}
        </p>
        <div class="mt-4 flex gap-2 text-xs font-bold">
          <span class="px-3 py-1 rounded-full bg-solar-gold/20 text-solar-gold">DC → AC</span>
          <span class="px-3 py-1 rounded-full bg-eco-green/20 text-eco-green">ذخیره پایدار</span>
        </div>
      </aside>
    </div>
  </header>
  ```

- **Accessibility & ARIA:**
  - `<header id="sec-01">` landmark for H1.
  - Circuit SVG `aria-hidden="true"` (decorative).
  - GEO `<aside role="complementary">` with `aria-label`.
  - CTAs `role="button"` + explicit `aria-label`.
  - `dir="rtl"` + `text-start` throughout.

---

### [SEC_02]: تکنولوژی اینورتر سینوسی خالص (Pure Sine Wave)

- **Section Role:** Semantic depth — technical information gain; why cheap inverters burn compressors.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Two-wave comparison: Pure Sine (smooth `eco-green` sine, `solar-gold` glow) vs Modified (blocky red `alert-red`). Burnt motor icon pulses red on modified side. THD badge `bg-eco-green text-deep-navy` with “THD < ۳٪”. Card container `rounded-3xl glass-card`.

- **Desktop Grid Architecture:**
  12-col. Wave graphic: `lg:col-span-6 lg:sticky lg:top-20 h-[420px]`. Text + GEO: `lg:col-span-6`.

- **Mobile Stacking:**
  Graphic first `h-[320px]`. Text stacks below with GEO banner `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy" x-data="{ activeWave: 'pure' }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" role="img" aria-label="مقایسه موج سینوسی خالص در برابر شبه‌سینوسی و آسیب به موتور">
        <div class="glass-card p-6 md:p-8 overflow-hidden">
          <div class="flex gap-2 mb-6" role="tablist" aria-label="انتخاب نوع موج">
            <button @click="activeWave='pure'" :class="activeWave==='pure' ? 'bg-eco-green text-deep-navy' : 'bg-pure-white/10 text-pure-white/70'" class="flex-1 py-2.5 rounded-xl font-bold text-sm transition-colors" role="tab" :aria-selected="activeWave==='pure' ? 'true' : 'false'">سینوسی خالص ✅</button>
            <button @click="activeWave='modified'" :class="activeWave==='modified' ? 'bg-alert-red text-pure-white' : 'bg-pure-white/10 text-pure-white/70'" class="flex-1 py-2.5 rounded-xl font-bold text-sm transition-colors" role="tab" :aria-selected="activeWave==='modified' ? 'true' : 'false'">شبه‌سینوسی ❌</button>
          </div>
          <svg viewBox="0 0 500 200" class="w-full h-[160px]" role="img" aria-label="نمودار موج">
            <!-- Pure sine wave -->
            <path x-show="activeWave==='pure'" d="M10 100 Q 60 10, 110 100 T 210 100 T 310 100 T 410 100 T 490 100" stroke="#2ECC71" stroke-width="3.5" fill="none" stroke-linecap="round" />
            <!-- Modified square-ish -->
            <path x-show="activeWave==='modified'" d="M10 100 H60 V40 H110 V100 H160 V160 H210 V100 H260 V40 H310 V100 H360 V160 H410 V100 H460 V40 H490" stroke="#E74C3C" stroke-width="3.5" fill="none" stroke-linejoin="round" />
          </svg>
          <div class="mt-4 flex items-center justify-between">
            <span class="text-xs font-bold px-3 py-1 rounded-full" :class="activeWave==='pure' ? 'bg-eco-green/20 text-eco-green' : 'bg-alert-red/20 text-alert-red'" x-text="activeWave==='pure' ? 'THD < ۳٪ — ایمن برای کمپرسور' : 'THD بالا — لرزش و سوختن موتور'"></span>
            <span class="text-2xl" aria-hidden="true" x-text="activeWave==='pure' ? '✅' : '🔥'"></span>
          </div>
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تکنولوژی اینورتر <span class="text-solar-gold">سینوسی خالص</span> (Pure Sine Wave)
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <div class="glass-card p-5 border-s-4 border-eco-green bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">⚡ چرا سینوسی خالص؟</p>
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
  - Toggle buttons `role="tab"` + `aria-selected` bound to Alpine `activeWave`.
  - SVG `role="img"` + descriptive `aria-label`.
  - Color + icon + text convey meaning (not color alone).
  - `prefers-reduced-motion` respected via Alpine transitions.

---

### [SEC_03]: بررسی برندهای معتبر: اینورتر خورشیدی گرووات و سانورتر

- **Section Role:** Entity expansion — product targeting; industrial On-Grid vs villa Off-Grid.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Asymmetrical Bento Grid: Growatt (large `lg:col-span-7` with `navy-mid` + `solar-gold` accent, Wi-Fi monitor mock) vs Sunverter All-in-One ( `lg:col-span-5` compact, MPPT+Inverter merged icon). Badges: `bg-solar-gold text-deep-navy` for Growatt “راندمان ۹۸٪” and `bg-eco-green text-deep-navy` for Sunverter “All-in-One”.

- **Desktop Grid Architecture:**
  12-col Bento. Growatt: `lg:col-span-7`. Sunverter: `lg:col-span-5`. GEO callout spans `lg:col-span-12` below grid as `border-s-4 border-solar-gold` glass banner.

- **Mobile Stacking:**
  Single column stack `gap-6`. Cards `rounded-2xl`. GEO banner full-width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="py-20 md:py-32 bg-deep-navy" x-data="{ selectedBrand: 'growatt' }">
    <div class="container mx-auto px-4 max-w-6xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        برندهای معتبر: <span class="text-solar-gold">گرووات</span> و <span class="text-eco-green">سانورتر</span>
      </h2>
      <p class="text-pure-white/70 text-center max-w-2xl mx-auto mb-10">
        انتخاب استراتژیک برند — از نیروگاه مگاواتی تا ویلای آفگرید
      </p>
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 mb-8">
        <!-- Growatt -->
        <div class="lg:col-span-7 glass-card p-6 md:p-8 border-s-4 border-solar-gold hover:shadow-xl transition-all text-start" :class="selectedBrand==='growatt' ? 'ring-1 ring-solar-gold/40' : ''" @click="selectedBrand='growatt'" role="button" tabindex="0" aria-label="اینورتر گرووات — صنعتی و متصل به شبکه" @keydown.enter="selectedBrand='growatt'">
          <div class="flex items-start justify-between mb-4">
            <div>
              <span class="inline-flex px-3 py-1 bg-solar-gold text-deep-navy text-xs font-black rounded-full">Growatt — On-Grid</span>
              <h3 class="font-bold text-xl text-pure-white mt-3">اینورتر خورشیدی گرووات</h3>
              <p class="text-pure-white/60 text-sm mt-1">مانیتورینگ Wi-Fi • راندمان ۹۸٪+ • نیروگاه هوشمند</p>
            </div>
            <span class="text-3xl" aria-hidden="true">🏭</span>
          </div>
          <div class="bg-navy-mid rounded-xl p-4 flex items-center gap-4">
            <div class="w-16 h-10 rounded bg-solar-gold/20 border border-solar-gold/30 flex items-center justify-center text-solar-gold font-bold text-xs">Wi-Fi</div>
            <div class="flex-1 h-2 bg-pure-white/10 rounded-full overflow-hidden"><div class="h-full bg-solar-gold w-[98%] rounded-full"></div></div>
            <span class="text-solar-gold font-bold text-sm">۹۸٪</span>
          </div>
        </div>
        <!-- Sunverter -->
        <div class="lg:col-span-5 glass-card p-6 md:p-8 border-s-4 border-eco-green hover:shadow-xl transition-all text-start" :class="selectedBrand==='sunverter' ? 'ring-1 ring-eco-green/40' : ''" @click="selectedBrand='sunverter'" role="button" tabindex="0" aria-label="سانورتر — آفگرید ویلایی All-in-One" @keydown.enter="selectedBrand='sunverter'">
          <span class="inline-flex px-3 py-1 bg-eco-green text-deep-navy text-xs font-black rounded-full">Sunverter — All-in-One</span>
          <h3 class="font-bold text-xl text-pure-white mt-3">اینورتر سانورتر خورشیدی</h3>
          <p class="text-pure-white/60 text-sm mt-1">اینورتر + شارژ کنترلر MPPT در یک پکیج</p>
          <div class="mt-4 flex gap-2">
            <span class="flex-1 text-center py-2 rounded-xl bg-pure-white/5 border border-pure-white/10 text-xs font-bold text-pure-white">کاهش سیم‌کشی</span>
            <span class="flex-1 text-center py-2 rounded-xl bg-pure-white/5 border border-pure-white/10 text-xs font-bold text-pure-white">کاهش فضا</span>
          </div>
        </div>
      </div>
      <p class="text-pure-white/85 text-base leading-relaxed max-w-4xl mx-auto text-start mb-6">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
      <div class="glass-card p-5 border-s-4 border-solar-gold max-w-4xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">🏷️ انتخاب برند</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Cards `role="button"` + `tabindex="0"` + `aria-label` + keyboard `@keydown.enter`.
  - Alpine `selectedBrand` for focus state.
  - Semantic headings.

---

### [SEC_04]: چرا باتری خودرو برای پنل خورشیدی مناسب نیست؟ (Deep Cycle)

- **Section Role:** Pain-point trigger — component failure myth-busting.

- **UI Aesthetic & Colors:**
  `bg-cream-warm` section (light for contrast). Side-by-side infographic cards: Starter ( `bg-alert-red/10 border-alert-red/30` with thin plates icon, `alert-red` header) vs Deep Cycle ( `bg-eco-green/10 border-eco-green/30` with thick plates, `eco-green` header). `rounded-3xl shadow-xl` container. Scolded badge “سولفاته می‌شود” vs success “هزاران سیکل”.

- **Desktop Grid Architecture:**
  Centered `max-w-5xl`. Two-col `grid-cols-2 gap-6`. GEO banner `bg-pure-white border-s-4 border-solar-gold` full-width below.

- **Mobile Stacking:**
  `grid-cols-1` stack. Cards `p-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }" x-intersect.once="revealed=true">
    <div class="container mx-auto px-4 max-w-5xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-10">
        چرا باتری خودرو برای پنل خورشیدی <span class="text-alert-red">مناسب نیست؟</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
        <div class="rounded-2xl p-6 bg-pure-white border border-alert-red/30 border-s-4 border-s-alert-red transition-all duration-700" :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'">
          <div class="flex items-center gap-3 mb-3">
            <span class="w-10 h-10 rounded-xl bg-alert-red/15 flex items-center justify-center text-lg" aria-hidden="true">🚗</span>
            <h3 class="font-bold text-deep-navy text-lg">باتری استارتر خودرو</h3>
            <span class="ms-auto px-2 py-1 bg-alert-red text-pure-white text-xs font-bold rounded-full">۳ ثانیه</span>
          </div>
          <svg viewBox="0 0 260 80" class="w-full h-[80px] mb-3" role="img" aria-label="صفحات نازک باتری استارتر">
            <g fill="none" stroke="#E74C3C" stroke-width="1.5" opacity="0.6">
              <rect x="10" y="20" width="18" height="50" rx="2" fill="#E74C3C" opacity="0.15"/>
              <rect x="34" y="20" width="18" height="50" rx="2" fill="#E74C3C" opacity="0.15"/>
              <rect x="58" y="20" width="18" height="50" rx="2" fill="#E74C3C" opacity="0.15"/>
              <rect x="82" y="20" width="18" height="50" rx="2" fill="#E74C3C" opacity="0.15"/>
              <rect x="106" y="20" width="18" height="50" rx="2" fill="#E74C3C" opacity="0.15"/>
            </g>
            <text x="130" y="45" text-anchor="middle" fill="#E74C3C" font-size="11" font-weight="bold">صفحات نازک — جریان انفجاری</text>
            <text x="130" y="62" text-anchor="middle" fill="#0A1929" opacity="0.6" font-size="10">سولفاته شدن پس از چند تخلیه ۵۰٪</text>
          </svg>
          <p class="text-deep-navy/70 text-sm leading-relaxed">برای استارت ۳ ثانیه‌ای طراحی شده — تخلیه مکرر = مرگ باتری.</p>
        </div>
        <div class="rounded-2xl p-6 bg-pure-white border border-eco-green/30 border-s-4 border-s-eco-green transition-all duration-700 delay-150" :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'">
          <div class="flex items-center gap-3 mb-3">
            <span class="w-10 h-10 rounded-xl bg-eco-green/15 flex items-center justify-center text-lg" aria-hidden="true">🔋</span>
            <h3 class="font-bold text-deep-navy text-lg">باتری دیپ‌سایکل</h3>
            <span class="ms-auto px-2 py-1 bg-eco-green text-pure-white text-xs font-bold rounded-full">۱۰ ساعت</span>
          </div>
          <svg viewBox="0 0 260 80" class="w-full h-[80px] mb-3" role="img" aria-label="صفحات ضخیم باتری دیپ‌سایکل">
            <g fill="#2ECC71" opacity="0.2" stroke="#2ECC71" stroke-width="1.5">
              <rect x="10" y="20" width="28" height="50" rx="3"/>
              <rect x="44" y="20" width="28" height="50" rx="3"/>
              <rect x="78" y="20" width="28" height="50" rx="3"/>
              <rect x="112" y="20" width="28" height="50" rx="3"/>
            </g>
            <text x="130" y="45" text-anchor="middle" fill="#2ECC71" font-size="11" font-weight="bold">صفحات ضخیم — تخلیه تدریجی</text>
            <text x="130" y="62" text-anchor="middle" fill="#0A1929" opacity="0.6" font-size="10">تحمل تخلیه ۵۰٪ هر شب — سال‌ها عمر</text>
          </svg>
          <p class="text-deep-navy/70 text-sm leading-relaxed">آزادسازی ۱۰ ساعته — طراحی برای چرخه‌های عمیق روزانه.</p>
        </div>
      </div>
      <p class="text-deep-navy/80 text-base leading-relaxed max-w-4xl mx-auto text-start mb-6">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
      </p>
      <div class="bg-pure-white rounded-2xl p-5 border-s-4 border-solar-gold shadow-lg max-w-4xl mx-auto">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 نکته کلیدی</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
        </p>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section id="sec-04">` with light bg — dark text ensures contrast.
  - SVGs `role="img"` + `aria-label`.
  - Meaning via text + icon, not color alone.
  - Reveal animation respects `prefers-reduced-motion`.

---

### [SEC_05]: تکنولوژی باتری ژل خورشیدی و برند Vmax

- **Section Role:** Product authority — storage technology + brand trust.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Feature highlight card: Heavy-duty Vmax battery render with `solar-gold` badges “Maintenance Free” + “Leak-proof Gel” + “VRLA”. Gel texture illustration: liquid acid (red, leaking) vs gel (gold, solid) with silica dots. Weight badge “سرب خالص — وزن بالا = کیفیت” in `eco-green`.

- **Desktop Grid Architecture:**
  12-col. Visual: `lg:col-span-6 lg:sticky lg:top-20`. Text + GEO: `lg:col-span-6`.

- **Mobile Stacking:**
  Visual `h-[360px]`. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-05" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-6 lg:sticky lg:top-20" role="img" aria-label="باتری ژل Vmax — تکنولوژی خمیر سیلیسی بدون نشتی">
        <div class="glass-card p-6 md:p-8">
          <div class="flex items-center justify-between mb-6">
            <h3 class="font-bold text-xl text-pure-white text-start">Vmax — باتری ژل خورشیدی</h3>
            <span class="px-3 py-1 bg-eco-green text-deep-navy text-xs font-black rounded-full">Maintenance Free</span>
          </div>
          <div class="grid grid-cols-2 gap-4 mb-6">
            <div class="rounded-xl p-4 bg-alert-red/10 border border-alert-red/20 text-center">
              <span class="text-2xl" aria-hidden="true">🧪</span>
              <p class="text-alert-red font-bold text-sm mt-2">اسید مایع</p>
              <p class="text-pure-white/60 text-xs">تبخیر + نشتی + یخ‌زدگی</p>
            </div>
            <div class="rounded-xl p-4 bg-eco-green/10 border border-eco-green/20 text-center ring-1 ring-eco-green/30">
              <span class="text-2xl" aria-hidden="true">🟡</span>
              <p class="text-eco-green font-bold text-sm mt-2">ژل سیلیسی</p>
              <p class="text-pure-white/60 text-xs">بدون تبخیر • ضد یخ • بدون نشتی</p>
            </div>
          </div>
          <div class="flex flex-wrap gap-2">
            <span class="px-3 py-1.5 rounded-full bg-solar-gold/15 text-solar-gold text-xs font-bold border border-solar-gold/20">Leak-proof Gel</span>
            <span class="px-3 py-1.5 rounded-full bg-solar-gold/15 text-solar-gold text-xs font-bold border border-solar-gold/20">گرما/سرما مقاوم</span>
            <span class="px-3 py-1.5 rounded-full bg-eco-green/15 text-eco-green text-xs font-bold border border-eco-green/20">VRLA — بدون سرویس</span>
          </div>
          <img src="/images/battery-vmax-gel.webp" alt="باتری ژل Vmax — نمایش تکنولوژی ژل بدون نیاز به سرویس" class="w-full h-auto mt-6 rounded-xl object-cover" loading="lazy" />
        </div>
      </div>
      <div class="lg:col-span-6 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          تکنولوژی <span class="text-solar-gold">باتری ژل خورشیدی</span> و برند Vmax
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_05}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold bg-cream-warm/5">
          <p class="text-sm font-bold text-solar-gold mb-1">🛡️ ایمن‌ترین ذخیره‌ساز</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_05}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Image `alt` in Farsi describing gel tech.
  - Badges have text labels.
  - Visual comparison uses icon + text.

---

### [SEC_06]: باورهای غلط درباره باتری‌های لیتیومی (Myth vs. Reality)

- **Section Role:** SGE bait — myth-busting lithium safety; BMS authority.

- **UI Aesthetic & Colors:**
  `bg-cream-warm`. Myth `bg-alert-red/10 border-alert-red/30` with ❌ + “خطرناک/زود خراب”. Reality `bg-eco-green/10 border-eco-green/30` with ✅ + “LiFePO4 تا ۱۵ سال با BMS”. Container `rounded-3xl shadow-2xl`. Icons + callout.

- **Desktop Grid Architecture:**
  Centered `max-w-4xl`. `grid-cols-2 gap-6`. GEO banner `border-t-4 border-solar-gold`.

- **Mobile Stacking:**
  `grid-cols-1` per pair.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-06" class="py-20 md:py-32 bg-cream-warm" x-data="{ revealed: false }" x-intersect.once="revealed=true">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط درباره <span class="text-solar-gold">باتری‌های لیتیومی</span>
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
        <div class="rounded-2xl p-6 bg-pure-white border border-alert-red/30 border-s-4 border-s-alert-red transition-all duration-700" :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl" aria-hidden="true">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">باتری‌های لیتیومی با وجود قیمت بالا، به سرعت خراب و خطرناک هستند.</p>
        </div>
        <div class="rounded-2xl p-6 bg-pure-white border border-eco-green/30 border-s-4 border-s-eco-green transition-all duration-700 delay-200" :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl" aria-hidden="true">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت مهندسی</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">باتری‌های دست‌دوم و بدون گرید خطرناک‌اند — اما LiFePO4 نو با BMS هوشمند تا ۹۰٪ دشارژ، ۱۵ سال عمر و ایمنی ۱۰۰٪ دارد.</p>
          <span class="inline-flex mt-3 px-3 py-1 bg-eco-green/15 text-eco-green text-xs font-bold rounded-full">LiFePO4 + BMS = ۱۰+ سال</span>
        </div>
      </div>
      <p class="text-deep-navy/80 text-base leading-relaxed max-w-3xl mx-auto text-start mb-6">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
      </p>
      <div class="border-t-4 border-solar-gold bg-pure-white rounded-2xl p-6 shadow-lg">
        <p class="text-sm font-bold text-solar-gold mb-1">🔬 واقعیت لیتیوم</p>
        <p class="text-deep-navy text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_06}
        </p>
      </div>
    </div>
  </aside>
  ```

- **Accessibility & ARIA:**
  - `<aside id="sec-06">`.
  - `x-intersect` decorative only.
  - Icon + text ensures meaning without color dependence.

---

### [SEC_07]: اهمیت سیستم شارژ کنترلر MPPT

- **Section Role:** Semantic depth — converter efficiency; winter/cloudy gain.

- **UI Aesthetic & Colors:**
  `bg-deep-navy`. Animated graph: PWM (flat/clipping red `alert-red`, dashed) vs MPPT (tracking green `eco-green` curve, solar-gold dot follows peak). Badge “تا ۳۰٪ انرژی بیشتر” in `solar-gold`. Power curve area fill `eco-green/15`.

- **Desktop Grid Architecture:**
  12-col. Graph: `lg:col-span-7 lg:sticky lg:top-20 h-[400px]`. Text + GEO: `lg:col-span-5`.

- **Mobile Stacking:**
  Graph `h-[320px]`. Text stacks below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-deep-navy" x-data="{ mpptOn: true }" x-intersect.once="mpptOn=true">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <div class="lg:col-span-7 lg:sticky lg:top-20" role="img" aria-label="نمودار راندمان MPPT در برابر PWM — استخراج ۳۰٪ بیشتر انرژی در هوای ابری">
        <div class="glass-card p-6 md:p-8">
          <div class="flex items-center justify-between mb-4">
            <h3 class="font-bold text-lg text-pure-white text-start">MPPT vs PWM</h3>
            <label class="inline-flex items-center gap-2 cursor-pointer" role="switch" :aria-checked="mpptOn ? 'true' : 'false'" tabindex="0" @keydown.space.prevent="mpptOn=!mpptOn">
              <span class="text-xs font-bold" :class="mpptOn ? 'text-eco-green' : 'text-pure-white/50'">MPPT فعال</span>
              <button @click="mpptOn=!mpptOn" class="relative w-11 h-6 rounded-full transition-colors" :class="mpptOn ? 'bg-eco-green' : 'bg-pure-white/20'" aria-label="تغییر نمایش MPPT">
                <span class="absolute top-0.5 start-0.5 w-5 h-5 bg-pure-white rounded-full transition-all" :class="mpptOn ? 'translate-x-5 rtl:-translate-x-5' : ''"></span>
              </button>
            </label>
          </div>
          <svg viewBox="0 0 500 220" class="w-full h-[200px]" role="img" aria-label="منحنی توان MPPT در برابر PWM">
            <line x1="40" y1="180" x2="480" y2="180" stroke="#FFFFFF" stroke-width="1" opacity="0.3"/>
            <line x1="40" y1="180" x2="40" y2="20" stroke="#FFFFFF" stroke-width="1" opacity="0.3"/>
            <!-- PWM flat clipping -->
            <path d="M40 120 H180 V140 H320 V120 H480" stroke="#E74C3C" stroke-width="2.5" fill="none" stroke-dasharray="6 4" opacity="0.9"/>
            <!-- MPPT tracking curve -->
            <path d="M40 160 Q120 40, 250 90 T480 110" stroke="#2ECC71" stroke-width="3" fill="none" />
            <path d="M40 160 Q120 40, 250 90 T480 110 L480 180 L40 180 Z" fill="#2ECC71" opacity="0.12"/>
            <circle cx="250" cy="90" r="6" fill="#F5A623" stroke="#FFFFFF" stroke-width="2">
              <animate attributeName="r" values="6;8;6" dur="2s" repeatCount="indefinite"/>
            </circle>
          </svg>
          <div class="flex justify-center gap-4 mt-4 text-xs font-bold">
            <span class="flex items-center gap-1.5"><span class="w-6 h-1 rounded bg-alert-red"></span> PWM — کلیپ/هدررفت</span>
            <span class="flex items-center gap-1.5"><span class="w-6 h-1 rounded bg-eco-green"></span> MPPT — نقطه حداکثر توان</span>
          </div>
          <p class="text-center mt-3 text-solar-gold font-bold text-sm">⚡ تا ۳۰٪ انرژی بیشتر در زمستان و هوای ابری</p>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          اهمیت سیستم <span class="text-eco-green">شارژ کنترلر MPPT</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <div class="glass-card p-5 border-s-4 border-eco-green bg-eco-green/5">
          <p class="text-sm font-bold text-eco-green mb-1">📈 ردیابی لحظه‌ای</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Graph `role="img"` + `aria-label`.
  - Toggle `role="switch"` + `aria-checked` + keyboard support.
  - Legend uses color + text + dash pattern.

---

### [SEC_08]: توزیع مستقیم تجهیزات از کرج به مناطق ویلایی و صنعتی

- **Section Role:** Local SEO map anchor — supply chain + heavy logistics authority.

- **UI Aesthetic & Colors:**
  `bg-deep-navy` with logistics network visual. Stylized vector map of Alborz/Tehran with Karaj HQ gold pulse + radiating lines to Kordan, Chaharbagh, Tehran-Dasht, Lavasanat and industrial parks. Heavy battery icon with truck. `<address>` in `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  12-col. Map visual: `lg:col-span-7` (`rounded-2xl glass-card overflow-hidden h-[420px]`). Content + address: `lg:col-span-5`.

- **Mobile Stacking:**
  Map `h-[300px]`. Address full-width below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7" role="img" aria-label="نقشه لجستیک از کرج به مناطق ویلایی و صنعتی">
        <div class="glass-card p-6 h-[420px] flex flex-col">
          <h3 class="font-bold text-lg text-pure-white text-start mb-4">ارسال سریع از هاب کرج</h3>
          <svg viewBox="0 0 500 300" class="w-full flex-1" role="img" aria-label="شبکه توزیع از کرج">
            <!-- HQ pulse -->
            <circle cx="220" cy="150" r="18" fill="#F5A623" opacity="0.2"><animate attributeName="r" values="18;28;18" dur="2s" repeatCount="indefinite"/></circle>
            <circle cx="220" cy="150" r="8" fill="#F5A623" stroke="#FFFFFF" stroke-width="2"/>
            <text x="220" y="178" text-anchor="middle" fill="#F5A623" font-size="10" font-weight="bold">کرج — هاب</text>
            <!-- Radiating lines -->
            <g stroke="#F5A623" stroke-width="1.5" opacity="0.6" stroke-dasharray="4 4">
              <line x1="220" y1="150" x2="120" y2="80"/><line x1="220" y1="150" x2="320" y2="60"/><line x1="220" y1="150" x2="380" y2="140"/><line x1="220" y1="150" x2="340" y2="220"/><line x1="220" y1="150" x2="140" y2="220"/>
            </g>
            <g fill="#0A1929" stroke="#F5A623" stroke-width="1.2">
              <circle cx="120" cy="80" r="5"/><circle cx="320" cy="60" r="5"/><circle cx="380" cy="140" r="5"/><circle cx="340" cy="220" r="5"/><circle cx="140" cy="220" r="5"/>
            </g>
            <g fill="#FFFFFF" font-size="9" font-weight="bold" text-anchor="middle">
              <text x="120" y="68">کردان</text><text x="320" y="48">لواسانات</text><text x="380" y="158">تهراندشت</text><text x="340" y="238">چهارباغ</text><text x="140" y="238">هشتگرد</text>
            </g>
          </svg>
          <p class="text-center text-pure-white/60 text-xs mt-3">حمل تخصصی باتری‌های سنگین دیپ‌سایکل با لجستیک اختصاصی</p>
        </div>
      </div>
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          توزیع مستقیم از <span class="text-solar-gold">کرج</span> به مناطق ویلایی و صنعتی
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_08}
        </p>
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-1.5 text-sm leading-relaxed">
          <p class="text-base">🏢 دفتر و انبار: کرج، جاده ملارد، بعد از دانشگاه فرهنگیان</p>
          <p dir="ltr" class="text-start">📞 026-36506485</p>
          <p dir="ltr" class="text-start">📱 09124641442</p>
          <p class="text-xs font-normal opacity-80 pt-2 border-t border-deep-navy/20">ضمانت‌نامه شرکتی • حذف ریسک کالای تقلبی</p>
        </address>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">🚚 لجستیک سنگین</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Map `role="img"` + `aria-label` in Farsi.
  - `<address>` semantic NAP.
  - Phones `dir="ltr"` + `text-start`.

---

### [SEC_09]: استانداردهای ملی و بین‌المللی تجهیزات (آپدیت 1403)

- **Section Role:** Temporal freshness + outbound trust (INSO / NRI) + Anti-Islanding E-E-A-T.

- **UI Aesthetic & Colors:**
  `bg-navy-mid` band with trust badge row. Badge row `grid-cols-3 gap-4` with `glass-card border-s-4 border-solar-gold` + shield icons. Inline external link to `inso.gov.ir` with `solar-gold underline`. “بروزرسانی ۱۴۰۳” pill `bg-solar-gold text-deep-navy`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl` single column. Badge grid `grid-cols-3`.

- **Mobile Stacking:**
  Badges `grid-cols-1` stack.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-16 md:py-24 bg-navy-mid">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          استانداردهای ملی و بین‌المللی تجهیزات
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-black rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_09 — para 1}
      </p>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2" aria-hidden="true">🛡️</span>
          <h4 class="font-bold text-pure-white text-sm">Anti-Islanding</h4>
          <p class="text-pure-white/60 text-xs mt-1">حفاظت ضد جزیره‌ای — قطع فوری در خاموشی شبکه</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2" aria-hidden="true">🏛️</span>
          <h4 class="font-bold text-pure-white text-sm"><a href="https://www.inso.gov.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">سازمان ملی استاندارد ایران</a></h4>
          <p class="text-pure-white/60 text-xs mt-1">تایید رله‌های حفاظتی اینورترهای On-Grid</p>
        </div>
        <div class="glass-card p-5 border-s-4 border-solar-gold flex flex-col items-center text-center">
          <span class="text-3xl mb-2" aria-hidden="true">🔬</span>
          <h4 class="font-bold text-pure-white text-sm">پژوهشگاه نیرو</h4>
          <p class="text-pure-white/60 text-xs mt-1">آزمایشگاه مرجع وزارت نیرو</p>
        </div>
      </div>
      <p class="text-pure-white/70 text-sm leading-relaxed">
        مراجعه به <a href="https://www.inso.gov.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">سازمان ملی استاندارد ایران</a> برای استعلام گواهینامه‌های حفاظتی.
      </p>
      <!-- CODER INSTRUCTION: External link MUST include rel="external" as requested in dossier SEC_09 -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External links `rel="external noopener"` + `target="_blank"` + visible focus ring.
  - Badge icons `aria-hidden="true"`.
  - Update pill has sufficient contrast.

---

### [SEC_10]: بخش پاسخ به سوالات متداول درباره اینورتر و باتری (FAQ)

- **Section Role:** GEO/SGE bait — long-tail question targeting; FAQPage schema.

- **UI Aesthetic & Colors:**
  `bg-deep-navy` with `bg-navy-mid` accordion. Collapsed: `border-s-4 border-pure-white/10`. Expanded: `border-s-4 border-solar-gold` + `text-solar-gold` summary + `shadow-lg`. GEO preamble `bg-cream-warm/5 border border-solar-gold/20`.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl` single column. GEO banner top, two `<details>` blocks.

- **Mobile Stacking:**
  Full-width `<summary>` with `py-5 px-6` touch target 44px+.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-navy-mid" x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">اینورتر و باتری</span>
      </h2>
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
        </p>
      </div>
      <div class="space-y-4" role="list">
        <details class="glass-card overflow-hidden group" :class="openFaq===1 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'" @toggle="openFaq = $el.open ? 1 : (openFaq===1 ? null : openFaq)" role="listitem">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start list-none" role="button" :aria-expanded="openFaq===1 ? 'true' : 'false'" aria-controls="faq-1">
            <span class="font-bold text-lg" :class="openFaq===1 ? 'text-solar-gold' : 'text-pure-white'">باتری ژل خورشیدی چند سال عمر می‌کند؟</span>
            <svg class="w-5 h-5 text-solar-gold transition-transform shrink-0 ms-4" :class="openFaq===1 ? 'rotate-180' : ''" viewBox="0 0 20 20" fill="none" aria-hidden="true"><path d="M5 7l5 5 5-5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </summary>
          <div id="faq-1" class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            طول عمر باتری مستقیماً به نحوه طراحی سیستم (ممانعت از تخلیه بیش از حد) بستگی دارد. اگر مهندسی سیستم به گونه‌ای باشد که عمق دشارژ (DoD) باتری هر شب به زیر ۵۰٪ نرسد، یک باتری ژل Vmax با کیفیت می‌تواند به راحتی بین ۵ تا ۷ سال روی سیستم خورشیدی شما بدون افت محسوس کار کند.
          </div>
        </details>
        <details class="glass-card overflow-hidden group" :class="openFaq===2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'" @toggle="openFaq = $el.open ? 2 : (openFaq===2 ? null : openFaq)" role="listitem">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start list-none" role="button" :aria-expanded="openFaq===2 ? 'true' : 'false'" aria-controls="faq-2">
            <span class="font-bold text-lg" :class="openFaq===2 ? 'text-solar-gold' : 'text-pure-white'">تفاوت اینورتر هیبریدی با اینورتر آفگرید (سانورتر) چیست؟</span>
            <svg class="w-5 h-5 text-solar-gold transition-transform shrink-0 ms-4" :class="openFaq===2 ? 'rotate-180' : ''" viewBox="0 0 20 20" fill="none" aria-hidden="true"><path d="M5 7l5 5 5-5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </summary>
          <div id="faq-2" class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            سانورترهای معمولی آفگرید، توانایی تزریق برق مازاد به شبکه شهری را ندارند و صرفاً یک سیستم ایزوله هستند. اما اینورتر هیبریدی یک سیستم کاملاً پیشرفته است که می‌تواند همزمان باتری‌ها را شارژ کند، برق ویلا را تامین کند و در صورت لزوم، برق مازاد را برای درآمدزایی به شبکه شهری تزریق (فروش) نماید.
          </div>
        </details>
      </div>
      <!-- CODER NOTE: Wrap this section strictly in FAQPage JSON-LD schema per dossier. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>`/`<summary>` + `role="button"` + `aria-expanded` via Alpine binding.
  - `aria-controls` links summary to content.
  - Touch target `py-5 px-6` ≥44px.
  - Keyboard fully native.

---

### [SEC_11]: مشاوره برای ارتقاء سیستم و سفارش قطعات

- **Section Role:** CRO conversion — component upgrades & battery price inquiry; NAP.

- **UI Aesthetic & Colors:**
  `bg-solar-gold` full-width with `deep-navy` text. Grain texture overlay `opacity-[0.04]`. Oversized phones `text-3xl md:text-5xl font-black`. Messenger FABs `w-14 h-14 bg-deep-navy text-solar-gold rounded-full`. Dual CTA: “استعلام قیمت باتری” (primary) + “دریافت Datasheet” (secondary glass).

- **Desktop Grid Architecture:**
  12-col. Text + phones: `lg:col-span-7 text-start`. Messenger + GEO: `lg:col-span-5 flex flex-col items-center lg:items-start`.

- **Mobile Stacking:**
  Single column. Phones stack with `dir="ltr"`. Messenger row `flex gap-3 justify-center`.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-11" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden" x-data="{ copied: false }">
    <div class="absolute inset-0 opacity-[0.04] bg-[url('/images/grain-texture.png')] bg-repeat pointer-events-none" aria-hidden="true"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          مشاوره برای <span class="underline decoration-deep-navy/20 underline-offset-8">ارتقاء سیستم</span> و سفارش قطعات
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_11}
        </p>
        <div class="space-y-3">
          <a href="tel:02636506485" class="block text-3xl md:text-5xl font-black text-deep-navy hover:text-deep-navy/70 transition-colors" dir="ltr" aria-label="تماس دفتر کرج: ۰۲۶-۳۶۵۰۶۴۸۵">026-36506485</a>
          <a href="tel:09124641442" class="block text-2xl md:text-4xl font-bold text-deep-navy/80 hover:text-deep-navy/60 transition-colors" dir="ltr" aria-label="تماس موبایل: ۰۹۱۲۴۶۴۱۴۴۲">09124641442</a>
        </div>
        <div class="flex flex-wrap gap-3 mt-8">
          <a href="https://wa.me/989124641442?text=استعلام%20قیمت%20باتری%20ژل%20و%20اینورتر%20گرووات" class="inline-flex items-center gap-2 px-8 py-4 bg-deep-navy text-solar-gold font-bold rounded-2xl hover:bg-deep-navy/90 transition-colors" role="button" aria-label="استعلام قیمت باتری در واتس‌اپ">
            <svg class="w-5 h-5" aria-hidden="true" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2a10 10 0 00-8.7 15L2 22l5.2-1.3A10 10 0 1012 2z"/></svg>
            استعلام قیمت باتری
          </a>
          <button @click="navigator.clipboard.writeText('02636506485'); copied=true; setTimeout(()=>copied=false,2000)" class="inline-flex items-center gap-2 px-6 py-4 bg-pure-white text-deep-navy font-bold rounded-2xl border-2 border-deep-navy/10 hover:bg-pure-white/90 transition-colors" role="button" :aria-label="copied ? 'شماره کپی شد' : 'کپی شماره دفتر'">
            <span x-text="copied ? 'کپی شد ✓' : 'کپی شماره'"></span>
          </button>
        </div>
        <p class="text-deep-navy/60 text-xs mt-3">واتس‌اپ • بله • ایتا — ارسال بروشور و Datasheet فوری</p>
      </div>
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-deep-navy font-bold text-lg">ارسال Datasheet از طریق پیام‌رسان‌ها:</p>
        <div class="flex gap-3">
          <a href="https://wa.me/989124641442" target="_blank" rel="noopener" class="w-14 h-14 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center hover:scale-110 transition-transform" aria-label="واتس‌اپ"><span class="font-bold text-sm">WA</span></a>
          <a href="https://ble.ir/horasolar" target="_blank" rel="noopener" class="w-14 h-14 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center hover:scale-110 transition-transform" aria-label="بله"><span class="font-bold text-sm">بله</span></a>
          <a href="https://eitaa.com/horasolar" target="_blank" rel="noopener" class="w-14 h-14 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center hover:scale-110 transition-transform" aria-label="ایتا"><span class="font-bold text-sm">ایتا</span></a>
        </div>
        <div class="bg-deep-navy/10 rounded-2xl p-5 border-2 border-deep-navy/15 w-full">
          <p class="text-deep-navy text-base leading-relaxed font-medium">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_11}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Tel links `dir="ltr"` + `aria-label` in Farsi.
  - Buttons `role="button"` + `aria-label`; copy button announces state via `x-text`.
  - Messenger FABs `w-14 h-14` ≥44px, `aria-label` per platform.
  - External messengers `rel="noopener"`.
  - Grain overlay `aria-hidden="true"`.

---

[VERIFIED_UI_END_OF_FILE]
