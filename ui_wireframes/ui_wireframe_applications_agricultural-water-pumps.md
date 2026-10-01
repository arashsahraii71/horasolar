# UI Wireframe Specification: پمپ آب خورشیدی | سیستم پمپاژ چاه کشاورزی
- **Source Dossier:** `seo_dossiers/applications_agricultural-water-pumps.md`
- **Target URL:** `/applications/agricultural-water-pumps`
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

### [SEC_01]: راه‌اندازی سیستم پمپاژ و پمپ آب خورشیدی برای چاه کشاورزی

- **Section Role:** Primary Hero — First Contentful Paint anchor, H1 entity definition.

- **UI Aesthetic & Colors:**
  Full-viewport hero with a cinematic background photograph of an arid farm being irrigated under clear skies (see `needed_images.md`). A deep-navy gradient overlay (`bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy`) ensures text contrast. Headline in `pure-white`, sub-headline in `solar-gold`. The GEO TL;DR block renders as a Glassmorphism floating card with a `border-s-4 border-solar-gold` accent stripe.

- **Desktop Grid Architecture:**
  12-column CSS Grid. The text block occupies `lg:col-span-7 lg:col-start-1` (right-aligned in RTL), vertically centered. The GEO Callout card occupies `lg:col-span-4 lg:col-start-8`, positioned as `lg:sticky lg:top-24` so it stays visible during initial scroll.

- **Mobile Stacking:**
  Single column. Hero image as `object-cover h-[60vh]`. H1 + body text stacks below. GEO Callout card reflows to full-width below text with `mt-6`.

- **Tailwind & Alpine Directives:**
  ```html
  <header id="sec-01" class="relative min-h-screen flex items-center overflow-hidden" x-data="{ loaded: false }" x-init="loaded = true">
    <!-- Background Image -->
    <img src="/images/hero-agri-pump.webp"
         alt="سیستم پمپاژ آب خورشیدی در مزرعه کشاورزی"
         class="absolute inset-0 w-full h-full object-cover"
         loading="eager"
         fetchpriority="high"
         :class="loaded ? 'opacity-100 scale-100' : 'opacity-0 scale-105'"
         style="transition: opacity 1.2s ease, transform 1.2s ease;">
    <!-- Gradient Overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-deep-navy/80 via-deep-navy/50 to-deep-navy"></div>
    <!-- Content Grid -->
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-center py-24">
      <!-- Text Block -->
      <div class="lg:col-span-7 text-start">
        <h1 class="font-vazirmatn font-black text-4xl md:text-6xl leading-tight text-pure-white mb-6">
          راه‌اندازی سیستم پمپاژ و <span class="text-solar-gold">پمپ آب خورشیدی</span> برای چاه کشاورزی
        </h1>
        <p class="text-lg md:text-xl text-pure-white/90 max-w-2xl leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_01}
        </p>
        <a href="#sec-11" class="inline-flex items-center gap-2 mt-8 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-2xl hover:bg-solar-gold/90 transition-colors"
           role="button" aria-label="درخواست مشاوره رایگان پمپ خورشیدی">
          مشاوره رایگان
          <svg><!-- Arrow icon --></svg>
        </a>
      </div>
      <!-- GEO Callout (Sticky) -->
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
  - `<header>` landmark wraps the entire hero.
  - Hero image has descriptive `alt` in Farsi.
  - CTA `<a>` has `role="button"` and explicit `aria-label`.
  - GEO callout `<aside>` is semantically separated as complementary content.
  - `fetchpriority="high"` on hero image for LCP optimization.

---

### [SEC_02]: مکانیزم عملکرد درایو فرکانس متغیر (VFD) در آبیاری

- **Section Role:** Deep technical explainer with visual flowchart — builds Information Gain.

- **UI Aesthetic & Colors:**
  Deep navy background (`bg-deep-navy`). Content area uses an asymmetrical Bento Grid with a large flowchart visual on one side and stacked glass cards for the text on the other. The flowchart nodes use `solar-gold` borders on a `navy-mid` background. Connecting arrows rendered as animated SVG lines (dashed, `stroke-solar-gold`).

- **Desktop Grid Architecture:**
  12-column grid. Flowchart illustration block: `lg:col-span-5`. Text + GEO callout block: `lg:col-span-7`. The flowchart is sticky (`lg:sticky lg:top-20`) so it stays visible while reading.

- **Mobile Stacking:**
  Flowchart collapses to a horizontal scroll strip (`overflow-x-auto snap-x snap-mandatory`) at the top. Text content stacks below in full width.

- **Tailwind & Alpine Directives:**
  ```html
  <article id="sec-02" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
      <!-- Flowchart Visual -->
      <div class="lg:col-span-5 lg:sticky lg:top-20" aria-label="نمودار جریان عملکرد سیستم VFD" role="img">
        <div class="glass-card p-8">
          <!-- 4-node horizontal/vertical flowchart -->
          <div class="flex flex-col gap-6 items-center">
            <!-- Node: Panels -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">☀️ پنل‌های فتوولتائیک</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: VFD -->
            <div class="w-full rounded-xl bg-solar-gold/20 border-2 border-solar-gold p-4 text-center">
              <span class="text-pure-white font-black text-xl">⚡ درایو VFD هوشمند</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: Deep Well Pump -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">💧 پمپ شناور چاه عمیق</span>
            </div>
            <svg class="w-1 h-10"><line x1="50%" y1="0" x2="50%" y2="100%" stroke="#F5A623" stroke-width="2" stroke-dasharray="6"/></svg>
            <!-- Node: Irrigation -->
            <div class="w-full rounded-xl bg-navy-mid border border-solar-gold/40 p-4 text-center">
              <span class="text-solar-gold font-bold text-lg">🌾 شبکه آبیاری</span>
            </div>
          </div>
        </div>
      </div>
      <!-- Text Content -->
      <div class="lg:col-span-7 space-y-8 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مکانیزم عملکرد <span class="text-solar-gold">درایو فرکانس متغیر (VFD)</span> در آبیاری
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_02}
        </p>
        <!-- GEO Callout Inline -->
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
  - `<article>` semantically wraps the self-contained technical content.
  - Flowchart container has `role="img"` with Farsi `aria-label` describing the diagram.
  - GEO callout is a `<div>` with visual border emphasis (not `<aside>` here, since it's inline within the article flow).

---

### [SEC_03]: پایان دادن به بحران مجوز شبکه و هزینه‌های تیرگذاری

- **Section Role:** Pain-point emotional trigger — Split-view contrast layout.

- **UI Aesthetic & Colors:**
  Split-screen composition. Left panel (in RTL: the start-side panel) has a muted, desaturated palette (`bg-navy-mid/90` with faded power-line imagery) representing the "pain." Right panel (end-side) has a vibrant `bg-deep-navy` with a solar-gold glow halo behind an independent solar well system image representing "freedom." Divider is a diagonal SVG clip-path or a `skew-y-3` Tailwind transform.

- **Desktop Grid Architecture:**
  12-column grid. Pain side: `lg:col-span-6`. Freedom side: `lg:col-span-6`. Both are `min-h-[500px]`. The GEO callout floats as an absolute-positioned glass card overlapping the center divider (`lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20`).

- **Mobile Stacking:**
  Vertical stack. Pain panel first (reduced height `h-[300px]` with overlay text), then freedom panel. GEO card reflows between them as a full-width banner.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-03" class="relative py-20 md:py-0 overflow-hidden">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 lg:min-h-[600px]">
      <!-- Pain Side -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-navy-mid/90 overflow-hidden">
        <img src="/images/power-lines-bureaucracy.webp" alt="خطوط برق و کاغذبازی اداری" class="absolute inset-0 w-full h-full object-cover opacity-20" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">🏗️</span>
          <h3 class="text-alert-red font-bold text-xl mt-4">هزینه تیرگذاری و مجوز شبکه</h3>
          <p class="text-pure-white/60 mt-2 text-sm">کاغذبازی بی‌پایان + هزینه‌های نجومی</p>
        </div>
      </div>
      <!-- Freedom Side -->
      <div class="lg:col-span-6 relative flex items-center justify-center p-8 bg-deep-navy overflow-hidden">
        <img src="/images/independent-solar-well.webp" alt="سیستم مستقل چاه خورشیدی" class="absolute inset-0 w-full h-full object-cover opacity-30" loading="lazy">
        <div class="relative z-10 text-center">
          <span class="text-6xl">☀️</span>
          <h3 class="text-eco-green font-bold text-xl mt-4">استقلال کامل با پمپ خورشیدی</h3>
          <p class="text-pure-white/70 mt-2 text-sm">بدون مجوز، بدون کاغذبازی</p>
        </div>
      </div>
      <!-- GEO Overlap Card -->
      <div class="lg:absolute lg:start-1/2 lg:top-1/2 lg:-translate-x-1/2 lg:-translate-y-1/2 z-20 w-full lg:max-w-md mx-auto mt-6 lg:mt-0 glass-card p-6 border-2 border-solar-gold">
        <p class="text-sm font-bold text-solar-gold mb-1">💡 خلاصه تصمیم‌ساز</p>
        <p class="text-pure-white/90 text-base leading-relaxed">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_03}
        </p>
      </div>
    </div>
    <!-- Full Text Below -->
    <div class="container mx-auto px-4 py-12 text-start max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        پایان دادن به بحران <span class="text-solar-gold">مجوز شبکه</span> و هزینه‌های تیرگذاری
      </h2>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
        {PRODUCTION-READY FARSI TEXT from dossier SEC_03}
      </p>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<section>` semantic wrapper with `id="sec-03"`.
  - Both background images have descriptive `alt` text.
  - Color is never the sole indicator of meaning; textual labels ("هزینه" vs "استقلال") accompany color coding.
  - GEO card is visually prominent with `border-2 border-solar-gold` for high contrast.

---

### [SEC_04]: مقایسه پمپ خورشیدی با موتور دیزل (حذف سوخت و استهلاک)

- **Section Role:** Data-visualization comparison — drives business-case conviction.

- **UI Aesthetic & Colors:**
  Gradient background from `deep-navy` to `navy-mid`. The comparison chart is rendered as a stylized Data-Viz bar chart inside a glass card. Diesel bars use `alert-red` with a subtle strikethrough pattern. Solar bars use `eco-green`. The 5-year cumulative line chart uses `solar-gold` for the solar line and `alert-red/50` dashed for diesel. Table rows alternate `bg-deep-navy/60` and `bg-navy-mid/40`.

- **Desktop Grid Architecture:**
  12-column grid. Chart/Data-Viz block: `lg:col-span-7`. Key takeaway text + GEO callout: `lg:col-span-5`. Asymmetrical Bento layout: the chart card has `rounded-e-3xl` (end-side rounded in RTL) and the text card has `rounded-s-3xl`.

- **Mobile Stacking:**
  Chart scrolls horizontally inside `overflow-x-auto` container. Text + GEO block stacks below at full width.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-04" class="py-20 md:py-32 bg-gradient-to-b from-deep-navy to-navy-mid"
           x-data="{ showDetails: false }">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
      <!-- Chart Block -->
      <div class="lg:col-span-7 glass-card rounded-e-3xl p-8 overflow-x-auto">
        <h3 class="font-bold text-xl text-pure-white mb-6 text-start">مقایسه هزینه‌های تجمعی ۵ ساله</h3>
        <table class="w-full min-w-[500px] text-sm" role="table" aria-label="جدول مقایسه هزینه دیزل و خورشیدی در ۵ سال">
          <thead>
            <tr class="bg-navy-mid text-solar-gold">
              <th scope="col" class="p-3 text-start rounded-s-lg">سال</th>
              <th scope="col" class="p-3 text-start">هزینه تجمعی دیزل (میلیون تومان)</th>
              <th scope="col" class="p-3 text-start rounded-e-lg">هزینه تجمعی خورشیدی (میلیون تومان)</th>
            </tr>
          </thead>
          <tbody>
            <tr class="bg-deep-navy/60">
              <td class="p-3">۱</td>
              <td class="p-3 text-alert-red font-bold">۱۸۰</td>
              <td class="p-3 text-eco-green font-bold">۳۵۰ (سرمایه‌گذاری اولیه)</td>
            </tr>
            <tr class="bg-navy-mid/40">
              <td class="p-3">۲</td>
              <td class="p-3 text-alert-red font-bold">۳۶۰</td>
              <td class="p-3 text-eco-green font-bold">۳۵۰</td>
            </tr>
            <tr class="bg-deep-navy/60">
              <td class="p-3">۳</td>
              <td class="p-3 text-alert-red font-bold">۵۴۰</td>
              <td class="p-3 text-eco-green font-bold">۳۵۰</td>
            </tr>
            <tr class="bg-navy-mid/40">
              <td class="p-3">۴</td>
              <td class="p-3 text-alert-red font-bold">۷۲۰</td>
              <td class="p-3 text-eco-green font-bold">۳۵۰</td>
            </tr>
            <tr class="bg-deep-navy/60">
              <td class="p-3">۵</td>
              <td class="p-3 text-alert-red font-bold">۹۰۰</td>
              <td class="p-3 text-eco-green font-bold">۳۵۰</td>
            </tr>
          </tbody>
        </table>
        <button @click="showDetails = !showDetails"
                class="mt-4 text-solar-gold underline text-sm"
                :aria-expanded="showDetails"
                aria-controls="diesel-details">
          جزئیات بیشتر محاسبات
        </button>
        <div x-show="showDetails" x-collapse id="diesel-details" class="mt-4 text-pure-white/70 text-sm">
          محاسبات بر اساس میانگین مصرف ۱۵ لیتر گازوئیل در روز به قیمت آزاد و هزینه تعمیرات سالانه ۳۰ میلیون تومان.
        </div>
      </div>
      <!-- Text + GEO -->
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مقایسه <span class="text-solar-gold">پمپ خورشیدی</span> با موتور دیزل
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_04}
        </p>
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📊 نتیجه‌گیری کلیدی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_04}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<table>` has `role="table"` and descriptive `aria-label`.
  - All `<th>` elements use `scope="col"`.
  - Expand/collapse button uses `:aria-expanded` bound to Alpine state and `aria-controls` pointing to the details panel.
  - Color-coded values are also accompanied by text labels (column headers clarify which is diesel vs solar).

---

### [SEC_05]: باورهای غلط در سیستم آبیاری خورشیدی (Myth vs. Reality)

- **Section Role:** Myth-busting engagement block — SGE/GEO bait for snippet extraction.

- **UI Aesthetic & Colors:**
  Warm `cream-warm` background (`bg-cream-warm`) with deep navy text — a visual palette break to signal a different type of content. Myth cards have `bg-alert-red/10 border-alert-red/30` with a ❌ icon. Reality cards have `bg-eco-green/10 border-eco-green/30` with a ✅ icon. The entire block has a subtle `rounded-3xl` container with `shadow-2xl`.

- **Desktop Grid Architecture:**
  Centered single column, max-width `max-w-4xl mx-auto`. Each myth/reality pair is a Bento row: `grid-cols-2` with the myth on `col-span-1` and reality on `col-span-1`. The GEO callout sits below as a full-width `border-t-4 border-solar-gold` banner.

- **Mobile Stacking:**
  Each myth/reality pair stacks vertically. Myth card first (with red accent), reality card second (with green accent), separated by `gap-3`.

- **Tailwind & Alpine Directives:**
  ```html
  <aside id="sec-05" class="py-20 md:py-32 bg-cream-warm">
    <div class="container mx-auto px-4 max-w-4xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy text-center mb-12">
        باورهای غلط در <span class="text-solar-gold">آبیاری خورشیدی</span>
      </h2>
      <!-- Myth vs Reality Row -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8"
           x-data="{ revealed: false }"
           x-intersect.once="revealed = true">
        <!-- Myth Card -->
        <div class="rounded-2xl p-6 bg-alert-red/10 border border-alert-red/30 transition-all duration-700"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">❌</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">باور غلط</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            پمپ‌های خورشیدی فقط در ساعت ۱۲ ظهر که آفتاب عمود است کار می‌کنند.
          </p>
        </div>
        <!-- Reality Card -->
        <div class="rounded-2xl p-6 bg-eco-green/10 border border-eco-green/30 transition-all duration-700 delay-200"
             :class="revealed ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'">
          <span class="text-3xl">✅</span>
          <h3 class="font-bold text-deep-navy text-lg mt-3">واقعیت</h3>
          <p class="text-deep-navy/80 mt-2 text-base leading-relaxed">
            درایوهای هوشمند MPPT از ساعت ۷ صبح تا ۶ عصر، جریان آب را به طور پیوسته (با دبی متغیر) برقرار می‌کنند.
          </p>
        </div>
      </div>
      <!-- GEO Callout -->
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
  - `<aside>` is used per SEO Dossier semantic instruction.
  - `x-intersect` used for scroll-triggered reveal animation (non-essential, decorative only — content is present in DOM from load).
  - Myth/Reality labels use both color AND icon + text so meaning doesn't rely solely on color.
  - Sufficient contrast ensured: dark text on light card backgrounds.

---

### [SEC_06]: سخت‌افزار پروژه‌های کشاورزی (تجهیزات Tier-1)

- **Section Role:** E-E-A-T authority builder via hardware gallery.

- **UI Aesthetic & Colors:**
  Return to `bg-deep-navy`. Image gallery cards use Glassmorphism with hover-reveal captions. Each card has a thin `border-b-2 border-solar-gold` bottom accent. Image overlay gradient (`from-transparent to-deep-navy/70`) shows caption text on hover.

- **Desktop Grid Architecture:**
  Asymmetrical Bento Grid of 3 images: one large card `lg:col-span-8 lg:row-span-2` and two smaller stacked cards `lg:col-span-4`. Text block below spans `lg:col-span-8` with GEO callout on `lg:col-span-4`.

- **Mobile Stacking:**
  Horizontal scroll carousel with `snap-x snap-mandatory`. Each card is `w-[85vw] snap-center`. Text and GEO callout stack vertically below.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-06" class="py-20 md:py-32 bg-deep-navy">
    <div class="container mx-auto px-4">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-start mb-10">
        سخت‌افزار <span class="text-solar-gold">Tier-1</span> پروژه‌های کشاورزی
      </h2>
      <!-- Bento Image Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 mb-12" x-data="{ activeImage: null }">
        <!-- Large Card -->
        <div class="lg:col-span-8 lg:row-span-2 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[400px]"
             @mouseenter="activeImage = 1" @mouseleave="activeImage = null"
             role="figure" aria-label="استراکچر فولادی روی فونداسیون بتنی در مزرعه">
          <img src="/images/agri-mounting-structure.webp" alt="استراکچر فولادی نصب پنل در مزرعه" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-6">
            <p class="text-pure-white font-bold text-lg">استراکچر فولادی با فونداسیون بتنی عمیق</p>
          </div>
        </div>
        <!-- Small Card 1 -->
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="پنل مونوکریستال ۶۰۰ وات">
          <img src="/images/tier1-panel-closeup.webp" alt="پنل مونوکریستال Tier-1" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">پنل مونوکریستال ۶۰۰+ وات</p>
          </div>
        </div>
        <!-- Small Card 2 -->
        <div class="lg:col-span-4 relative rounded-2xl overflow-hidden group cursor-pointer min-h-[190px]"
             role="figure" aria-label="تابلو برق ضد آب IP65">
          <img src="/images/ip65-control-panel.webp" alt="تابلو برق کنترل پمپ IP65" class="w-full h-full object-cover" loading="lazy">
          <div class="absolute inset-0 bg-gradient-to-t from-deep-navy/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
            <p class="text-pure-white font-bold">تابلو برق کنترل IP65</p>
          </div>
        </div>
      </div>
      <!-- Text + GEO Row -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
        <div class="lg:col-span-8 text-start">
          <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
            {PRODUCTION-READY FARSI TEXT from dossier SEC_06}
          </p>
        </div>
        <div class="lg:col-span-4 glass-card p-5 border-s-4 border-solar-gold">
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
  - Each image card has `role="figure"` and `aria-label` in Farsi.
  - Hover captions are decorative overlays; `alt` text on images provides the equivalent information for screen readers.
  - `loading="lazy"` on all gallery images for performance.

---

### [SEC_07]: استقرار کشوری و مناطق تحت پوشش هورا نور سهند

- **Section Role:** Local SEO map anchor and service area declaration.

- **UI Aesthetic & Colors:**
  Dark background (`bg-navy-mid`). A stylized SVG/illustrated map of Iran with glowing gold connection lines radiating from the Karaj HQ marker to agricultural hubs (Qazvin, Yazd, Isfahan, Mazandaran). Map rendered as an embedded SVG or a high-quality WebP with animated pulse dots at each hub location using CSS `@keyframes`. The `<address>` block uses `bg-solar-gold text-deep-navy` for strong NAP signal contrast.

- **Desktop Grid Architecture:**
  12-column grid. Map visual: `lg:col-span-7`. Text + address card: `lg:col-span-5`. The address card is a solid `bg-solar-gold` card to visually anchor the NAP data.

- **Mobile Stacking:**
  Map reduces to `max-h-[300px]` with pinch-zoom disabled. Text and address stack below. Address card is full-width with prominent display.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-07" class="py-20 md:py-32 bg-navy-mid">
    <div class="container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- Map Visual -->
      <div class="lg:col-span-7" aria-label="نقشه مناطق تحت پوشش هورا نور سهند" role="img">
        <img src="/images/iran-coverage-map.svg" alt="نقشه پوشش خدمات پمپ خورشیدی در ایران - کرج، قزوین، یزد، اصفهان، مازندران" class="w-full h-auto" loading="lazy">
      </div>
      <!-- Text + Address -->
      <div class="lg:col-span-5 space-y-6 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          مناطق تحت پوشش <span class="text-solar-gold">هورا نور سهند</span>
        </h2>
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_07}
        </p>
        <!-- NAP Address Card -->
        <address class="not-italic bg-solar-gold text-deep-navy rounded-2xl p-6 font-bold space-y-2">
          <p class="text-lg">🏢 دفتر مرکزی: کرج، جاده ملارد</p>
          <p>📞 026-36506485</p>
          <p>📱 09125728170</p>
        </address>
        <!-- GEO Callout -->
        <div class="glass-card p-5 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📍 پوشش سراسری</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_07}
          </p>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - `<address>` HTML element used per SEO Dossier directive (semantic NAP signal).
  - Map image has comprehensive `alt` text listing all served regions.
  - Map container has `role="img"` with Farsi `aria-label`.
  - Phone numbers are plain text (will be auto-linked on mobile) — could optionally use `<a href="tel:...">`.

---

### [SEC_08]: توسعه کشاورزی نوین (آپدیت قوانین 1403)

- **Section Role:** Temporal freshness signal with authoritative outbound link.

- **UI Aesthetic & Colors:**
  Soft informational block. Background: `bg-cream-warm/10` on deep-navy base — a subtle warm tint. The tip box uses a `border-2 border-solar-gold` with a 📰 news icon. The outbound link to `maj.ir` is styled as a `text-solar-gold underline hover:text-solar-gold/80` inline link. A small "بروزرسانی ۱۴۰۳" badge in `bg-solar-gold text-deep-navy text-xs rounded-full px-3 py-1` sits next to the H2.

- **Desktop Grid Architecture:**
  Centered content column: `max-w-3xl mx-auto`. Single column layout — no grid split needed for this informational block.

- **Mobile Stacking:**
  No change needed; already single-column centered. Badge wraps to next line naturally.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-08" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <div class="flex flex-wrap items-center gap-3 mb-6">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white">
          توسعه کشاورزی نوین
        </h2>
        <span class="bg-solar-gold text-deep-navy text-xs font-bold rounded-full px-3 py-1">بروزرسانی ۱۴۰۳</span>
      </div>
      <p class="text-pure-white/85 text-base md:text-lg leading-relaxed mb-8">
        {PRODUCTION-READY FARSI TEXT — with inline link:}
        ... سیاست‌های کلان <a href="https://maj.ir/" rel="external noopener" target="_blank" class="text-solar-gold underline hover:text-solar-gold/80">وزارت جهاد کشاورزی</a> در سال ۱۴۰۳ ...
      </p>
      <!-- Informational Tip Box / GEO Block -->
      <div class="border-2 border-solar-gold rounded-2xl p-6 bg-cream-warm/5">
        <div class="flex items-start gap-3">
          <span class="text-2xl mt-1">📰</span>
          <div>
            <p class="text-sm font-bold text-solar-gold mb-1">نکته مهم قانونی ۱۴۰۳</p>
            <p class="text-pure-white/90 text-base leading-relaxed">
              {GEO EXTRACTION BLOCK TL;DR from dossier SEC_08}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - External link has `rel="external noopener"` and `target="_blank"`.
  - Freshness badge is decorative and doesn't convey critical info (the heading already contextualizes the year).
  - Tip box uses semantic grouping with icon + text; icon is decorative (emoji).

---

### [SEC_09]: پارامترهای برآورد هزینه سیستم پمپ خورشیدی

- **Section Role:** Internal linking bridge — redirects to solar calculator, prevents keyword cannibalization.

- **UI Aesthetic & Colors:**
  Minimal, clean block on `bg-deep-navy`. A single glass card with a `border-b-4 border-solar-gold` bottom accent. The internal link to `/pricing/solar-calculator` is a prominent pill-shaped CTA button (`bg-solar-gold text-deep-navy`).

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. The text block and CTA are vertically stacked.

- **Mobile Stacking:**
  No change. CTA button becomes `w-full` on mobile for easy tapping.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-09" class="py-16 md:py-24 bg-deep-navy">
    <div class="container mx-auto px-4 max-w-3xl text-start">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white mb-6">
        پارامترهای <span class="text-solar-gold">برآورد هزینه</span> سیستم پمپ خورشیدی
      </h2>
      <div class="glass-card p-8 border-b-4 border-solar-gold space-y-6">
        <p class="text-pure-white/85 text-base md:text-lg leading-relaxed">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_09}
        </p>
        <!-- GEO Callout Inline -->
        <div class="bg-cream-warm/5 rounded-xl p-4 border-s-4 border-solar-gold">
          <p class="text-sm font-bold text-solar-gold mb-1">📐 فرمول کلیدی</p>
          <p class="text-pure-white/90 text-base leading-relaxed">
            {GEO EXTRACTION BLOCK TL;DR from dossier SEC_09}
          </p>
        </div>
        <!-- Internal Link CTA -->
        <a href="/pricing/solar-calculator"
           class="inline-flex items-center gap-2 px-8 py-4 bg-solar-gold text-deep-navy font-bold rounded-full hover:bg-solar-gold/90 transition-colors w-full md:w-auto justify-center"
           role="button"
           aria-label="محاسبه‌گر آنلاین برق خورشیدی - برآورد هزینه سیستم پمپ خورشیدی">
          محاسبه‌گر آنلاین برق خورشیدی
          <svg><!-- Calculator icon --></svg>
        </a>
      </div>
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Internal link CTA has `role="button"` with full descriptive `aria-label`.
  - `w-full` on mobile ensures large touch target (min 48px height from `py-4`).

---

### [SEC_10]: سوالات متداول درباره آبیاری خورشیدی (FAQ)

- **Section Role:** GEO/SGE bait — FAQ with FAQPage JSON-LD schema, accordion UI.

- **UI Aesthetic & Colors:**
  Background: `bg-navy-mid`. Each FAQ item is a glass card with `border-s-4 border-solar-gold` when expanded, `border-s-4 border-pure-white/10` when collapsed. The summary text uses `text-solar-gold` when open. Smooth `x-collapse` transition.

- **Desktop Grid Architecture:**
  Centered `max-w-3xl mx-auto`. Single column stack of accordion items. GEO callout at top as a `bg-cream-warm/5` banner.

- **Mobile Stacking:**
  No change; already single-column. Touch targets for `<summary>` elements are full-width with `py-5` padding.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-10" class="py-20 md:py-32 bg-navy-mid"
           x-data="{ openFaq: null }">
    <div class="container mx-auto px-4 max-w-3xl">
      <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-pure-white text-center mb-4">
        سوالات متداول <span class="text-solar-gold">آبیاری خورشیدی</span>
      </h2>
      <!-- GEO Preamble -->
      <div class="bg-cream-warm/5 rounded-xl p-4 mb-10 border border-solar-gold/20 text-center">
        <p class="text-pure-white/80 text-sm">
          {GEO EXTRACTION BLOCK TL;DR from dossier SEC_10}
        </p>
      </div>
      <!-- FAQ Accordion -->
      <div class="space-y-4">
        <!-- FAQ Item 1 -->
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 1 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 1 ? null : 1">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   aria-expanded="false"
                   :aria-expanded="openFaq === 1 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 1 ? 'text-solar-gold' : 'text-pure-white'">
              آیا برای سیستم خورشیدی باید پمپ شناور فعلی چاه را تعویض کنم؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 1 ? 'rotate-180' : ''">
              <!-- Chevron icon -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            در ۹۰ درصد مواقع خیر! اگر الکتروموتور پمپ فعلی شما (اعم از تک‌فاز یا سه فاز) سالم باشد، مهندسین هورا نور سهند درایو خورشیدی (VFD) را دقیقاً متناسب با توان پمپ شما کالیبره می‌کنند و نیازی به خرید پمپ جدید و پرداخت هزینه مجدد ندارید.
          </div>
        </details>
        <!-- FAQ Item 2 -->
        <details class="glass-card overflow-hidden group"
                 :class="openFaq === 2 ? 'border-s-4 border-solar-gold' : 'border-s-4 border-pure-white/10'"
                 x-data @toggle="openFaq = openFaq === 2 ? null : 2">
          <summary class="cursor-pointer py-5 px-6 flex items-center justify-between text-start"
                   role="button"
                   aria-expanded="false"
                   :aria-expanded="openFaq === 2 ? 'true' : 'false'">
            <span class="font-bold text-lg" :class="openFaq === 2 ? 'text-solar-gold' : 'text-pure-white'">
              آیا پمپ آب خورشیدی در شب هم آب می‌کشد؟
            </span>
            <svg class="w-5 h-5 text-solar-gold transition-transform" :class="openFaq === 2 ? 'rotate-180' : ''">
              <!-- Chevron icon -->
            </svg>
          </summary>
          <div class="px-6 pb-5 text-pure-white/80 text-base leading-relaxed">
            سیستم‌های پمپاژ خورشیدی استاندارد به دلیل عدم استفاده از باتری (برای کاهش هزینه‌ها)، فقط در طول روز کار می‌کنند. بهترین روش برای مدیریت آب، پمپاژ در طول روز و ذخیره آب در استخرهای کشاورزی برای آبیاری شبانه است.
          </div>
        </details>
      </div>
      <!-- JSON-LD Reminder for Developer -->
      <!-- CODER NOTE: Wrap above FAQ content in FAQPage JSON-LD schema as per dossier directive. -->
    </div>
  </section>
  ```

- **Accessibility & ARIA:**
  - Native `<details>` / `<summary>` elements ensure keyboard accessibility and screen reader support out of the box.
  - `aria-expanded` is dynamically bound via Alpine for enhanced state communication.
  - `role="button"` on `<summary>` for consistent interaction model.
  - Touch target height is generous (`py-5 px-6`).

---

### [SEC_11]: تماس برای مشاوره و طراحی مهندسی سیستم چاه شما

- **Section Role:** Final CRO conversion block — high-contrast CTA for farmers.

- **UI Aesthetic & Colors:**
  Full-width high-contrast block. Background: `bg-solar-gold`. All text: `text-deep-navy`. Phone numbers are oversized (`text-3xl md:text-5xl font-black`), clickable with `<a href="tel:...">`. Messenger icons (WhatsApp, Bale, Eitaa) are circular icon buttons in `bg-deep-navy text-solar-gold`. A subtle grain texture overlay for premium feel.

- **Desktop Grid Architecture:**
  12-column grid. Text + CTA column: `lg:col-span-7`. Messenger icons + secondary info: `lg:col-span-5`. Both centered vertically.

- **Mobile Stacking:**
  Single column, centered text. Phone numbers stack vertically. Messenger icons row with `flex gap-4 justify-center`. Full-width tap targets.

- **Tailwind & Alpine Directives:**
  ```html
  <section id="sec-11" class="py-20 md:py-32 bg-solar-gold relative overflow-hidden">
    <!-- Subtle grain overlay -->
    <div class="absolute inset-0 opacity-5 bg-[url('/images/grain-texture.png')] bg-repeat"></div>
    <div class="relative z-10 container mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-10 items-center">
      <!-- CTA Text Block -->
      <div class="lg:col-span-7 text-start">
        <h2 class="font-vazirmatn font-extrabold text-2xl md:text-4xl text-deep-navy mb-6">
          همین امروز، آینده مزرعه خود را تضمین کنید
        </h2>
        <p class="text-deep-navy/80 text-base md:text-lg leading-relaxed mb-8">
          {PRODUCTION-READY FARSI TEXT from dossier SEC_11}
        </p>
        <!-- Phone Numbers -->
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
      <!-- Messenger Icons -->
      <div class="lg:col-span-5 flex flex-col items-center lg:items-start gap-6">
        <p class="text-deep-navy font-bold text-lg">ارتباط از طریق پیام‌رسان‌ها:</p>
        <div class="flex gap-4">
          <a href="https://wa.me/989125728170" target="_blank" rel="noopener"
             class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در واتس‌اپ">
            <!-- WhatsApp Icon -->
            <svg><!-- WA --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در بله">
            <!-- Bale Icon -->
            <svg><!-- Bale --></svg>
          </a>
          <a href="#" class="w-16 h-16 rounded-full bg-deep-navy text-solar-gold flex items-center justify-center text-2xl hover:scale-110 transition-transform"
             aria-label="ارسال پیام در ایتا">
            <!-- Eitaa Icon -->
            <svg><!-- Eitaa --></svg>
          </a>
        </div>
        <!-- GEO Callout -->
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
  - Phone links use `<a href="tel:...">` with explicit `aria-label` in Farsi including the formatted number.
  - Phone number elements have `dir="ltr"` to ensure correct digit rendering in RTL context.
  - Messenger icon buttons have individual `aria-label` describing the messenger platform.
  - Minimum touch target: `w-16 h-16` (64px) exceeds WCAG 2.5.8 minimum of 44px.
  - External links have `rel="noopener"`.

---

[VERIFIED_UI_END_OF_FILE]
