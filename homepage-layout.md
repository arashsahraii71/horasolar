# Visual Wireframe & Tailwind Layout Specification
## Mega Semantic Entity Hub - Hora Nor Sahand (horasahand.ir)

> **Document Type:** Architectural Blueprint for Frontend Agent (Qwen 3.8 Max)
> **Author:** Master UI/UX Architect & Layout Strategist
> **Status:** Final Specification - Ready for Implementation
> **Target:** RTL Farsi Solar EPC Company Homepage

---

## GLOBAL INSTRUCTION: MASTER @graph SCHEMA PAYLOAD (MANDATORY)

> **CRITICAL:** Do NOT scatter Schema markup across the page. Inject a single unified JSON-LD `@graph` object in the `<head>`. This connects the brand, local business, website, and FAQs into one massive Knowledge Graph node.

**The developer MUST place this exact payload in `<head>`:**

```json
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "EnergyBusiness",
      "@id": "https://horasahand.ir/#organization",
      "name": "شرکت برق خورشیدی هورا نور سهند",
      "alternateName": "Hora Nor Sahand",
      "url": "https://horasahand.ir",
      "logo": "https://horasahand.ir/logo.png",
      "foundingDate": "2016",
      "telephone": "+98-26-36506485",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "جاده ملارد، بعد از دانشگاه فرهنگیان، نرسیده به پل ارتش جنب فروشگاه بهداشتی ساختمانی سهند",
        "addressLocality": "Karaj",
        "addressRegion": "Alborz",
        "addressCountry": "IR"
      },
      "sameAs": [
        "https://t.me/horasolar",
        "https://instagram.com/hora.solar.panel",
        "https://ble.ir/horasolar",
        "https://eitaa.com/horasolar",
        "https://rubika.ir/horasolar"
      ]
    },
    {
      "@type": "WebSite",
      "@id": "https://horasahand.ir/#website",
      "url": "https://horasahand.ir",
      "name": "هورانور سهند | طراحی و اجرای نیروگاه خورشیدی",
      "publisher": {"@id": "https://horasahand.ir/#organization"}
    }
  ]
}
</script>
```

---

## GLOBAL DESIGN SYSTEM

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--solar-gold` | `#F5A623` | Primary accent, CTAs, energy/solar metaphor |
| `--solar-gold-light` | `#FFD580` | Hover states, glow effects |
| `--deep-navy` | `#0A1929` | Primary dark background (B2B sections, header, footer) |
| `--midnight-blue` | `#132F4C` | Card backgrounds on dark sections, glass base |
| `--trust-green` | `#22C55E` | Solution states, success, live indicators |
| `--danger-red` | `#EF4444` | Problem states, warning triggers, live beacons |
| `--pure-white` | `#FAFCFF` | Light section backgrounds |
| `--soft-gray` | `#F1F5F9` | Alternating light backgrounds |
| `--text-primary` | `#E2E8F0` | Body text on dark |
| `--text-dark` | `#1E293B` | Body text on light |
| `--glass-white` | `rgba(255,255,255,0.08)` | Glassmorphism fill |
| `--glass-border` | `rgba(255,255,255,0.12)` | Glassmorphism stroke |

### Typography Vibes

- **Farsi Headings:** "Vazirmatn" Black / ExtraBold (wght 800-900). Massive scale. Use `text-4xl` minimum on mobile, `text-6xl lg:text-7xl` on desktop for hero H1.
- **Farsi Body:** "Vazirmatn" Regular (wght 400). Line height `leading-relaxed` or `leading-loose` for readability in RTL.
- **English/Brand:** "Inter" or "Outfit" Medium for secondary English labels and brand entity text.
- **Monospace/Data:** "JetBrains Mono" or "Vazir Code" for data dashboard numbers and any technical readouts.
- **Type Scale Philosophy:** Extreme contrast between heading size and body. Headlines should feel monumental. Body text should feel clean and minimal.

### Interaction Physics

- **Default Transition:** `transition-all duration-300 ease-out` on all interactive elements.
- **Hover Lift:** Cards use `hover:scale-[1.02] hover:-translate-y-1 hover:shadow-2xl`.
- **Glass Hover Glow:** On dark sections, hovered elements gain `hover:shadow-[0_0_30px_rgba(245,166,35,0.15)]` (solar gold ambient glow).
- **Scroll Reveal:** All sections enter viewport with `opacity-0 translate-y-8` transitioning to `opacity-100 translate-y-0` via Intersection Observer. Stagger children by 100ms.
- **Micro-interactions:** Button press → scale to `0.97` for 100ms then back. Accordion arrows rotate `180deg`. Toggle switches slide with spring physics.
- **Navboost Principle:** Every section must offer at least ONE clickable, scrollable, or interactive element. Static blocks are forbidden.

### RTL Global Directives (CRITICAL)

The coder MUST:
1. Wrap the entire page in `<html dir="rtl" lang="fa">`.
2. Use Tailwind logical properties EVERYWHERE: `ms-` (margin-start) instead of `ml-`, `me-` (margin-end) instead of `mr-`, `ps-` (padding-start) instead of `pl-`, `pe-` (padding-end) instead of `pr-`, `start-0` instead of `left-0`, `end-0` instead of `right-0`.
3. Flex/Grid alignment: `text-start` instead of `text-left`, `items-start` for RTL. Icon placement on the START side is the RIGHT side.
4. SVG icons with directional meaning (arrows, chevrons) must be mirrored using `transform: scaleX(-1)` or Tailwind `-scale-x-100`.
5. The Tailwind config must include `darkMode: 'class'` for potential dark/light toggle.

---

## SECTION-BY-SECTION WIREFRAME SPECIFICATIONS

---

### SECTION 1: The Trust-Injected Header & Master Navigation

- **Overall UI Aesthetic:** "Dark Glassmorphism Command Bar." The header floats above content like a cockpit HUD. Deep navy base with glass blur overlay. The solar-gold accent pulses on the CTA. Premium, authoritative, and high-tech.

- **Desktop Layout Architecture:**
  A full-width sticky bar (`fixed top-0 z-50 w-full`). Internal structure is a 12-column grid:
  - **Columns 1-3 (RTL Right):** Brand lockup. The logo image (SVG, 40px height) sits beside a stacked text block: line 1 = "هورانور سهند" in `text-lg font-black text-white`, line 2 = "Hora Nor Sahand" in `text-xs font-medium text-slate-400 tracking-widest uppercase`.
  - **Columns 4-9 (Center):** Mega Menu navigation. Four top-level nav items displayed as horizontal `flex gap-8`. Each item (خانگی و ویلایی, صنعتی و سوله, کشاورزی, سرمایهگذاری) has a micro-icon (16x16 SVG) to its RIGHT (start side in RTL) and label text. On hover, a full-width mega-dropdown panel (`absolute start-0 w-full`) slides down with `backdrop-blur-xl bg-deep-navy/90 border-t border-glass-border`. Inside the dropdown: a 4-column Bento grid, each column showing the pillar's sub-links (3-4 links), a small descriptive paragraph, and a thumbnail image.
  - **Columns 10-12 (RTL Left):** Two elements side by side. (1) Phone number `026-36506485` as a clickable `tel:` link with a phone icon, in `text-sm text-slate-300`. (2) The WhatsApp CTA button: `bg-solar-gold text-deep-navy font-bold rounded-full px-6 py-2.5`. Text = "مشاوره رایگان". This button has a perpetual CSS pulse animation (`animate-pulse` but customized to be subtle: a soft glow ring expanding outward every 2 seconds using a `box-shadow` animation).

- **Mobile Layout Architecture:**
  Collapses to a single row (`flex items-center justify-between px-4 h-16`). Right side (RTL start): Logo icon only (no text). Left side (RTL end): Hamburger icon + WhatsApp icon (solar-gold, always visible). The hamburger opens a full-screen overlay (`fixed inset-0 bg-deep-navy/95 backdrop-blur-2xl z-[60]`). Inside: the 4 pillar links stacked vertically with large tap targets (`py-4 text-xl`), each with its micro-icon. At the bottom of the overlay: the phone numbers and the WhatsApp CTA button full-width.

- **Interactive "Navboost" Specs:**
  1. Mega Menu hover-to-reveal creates an interaction event (non-passive hover).
  2. WhatsApp CTA pulse animation draws eye movement and click. Track clicks as `navboost_cta_header`.
  3. On mobile, the hamburger open/close creates a toggle interaction logged as engagement.
  4. Each mega-menu pillar card is independently hoverable with a `border-b-2 border-transparent hover:border-solar-gold` transition.

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. The entire Mega-Menu MUST be wrapped in `<nav aria-label="Main Navigation">`.
  2. Do NOT use `href="#"` for the 4 pillar dropdown headers. They MUST be real `<a>` tags linking to internal silo pages to pass PageRank:
     - `<a href="/residential-solar">خانگی و ویلایی</a>`
     - `<a href="/industrial-solar">صنعتی و سوله</a>`
     - `<a href="/agricultural-solar">کشاورزی</a>`
     - `<a href="/satba-investment">سرمایهگذاری</a>`
  3. Add `data-track="whatsapp_header"` attribute to the WhatsApp CTA button for GA4 Navboost click-through tracking.

- **Tailwind Structural Directives:**
  ```
  Container: fixed top-0 inset-x-0 z-50 backdrop-blur-xl bg-deep-navy/80 border-b border-glass-border
  Inner: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 items-center h-16 lg:h-20 px-4 lg:px-8
  Logo area: col-span-3 flex items-center gap-3
  Nav area: col-span-6 hidden lg:flex justify-center gap-8
  CTA area: col-span-3 flex items-center justify-end gap-4
  Mobile: lg:hidden flex items-center justify-between
  Mega dropdown: absolute start-0 end-0 top-full backdrop-blur-2xl bg-midnight-blue/95 border-t border-glass-border shadow-2xl
  ```

---

### SECTION 2: Hero Section & Navboost Micro-App (The Click-Loop Engine)

- **Overall UI Aesthetic:** "Cinematic Dark Energy." A full-viewport hero with a dark gradient base layered with a subtle solar panel texture/pattern overlay at 5% opacity. The left (RTL: right) text block commands authority. The right (RTL: left) interactive calculator glows with glassmorphism. The feel is an energy company command center, not a brochure.

- **Desktop Layout Architecture:**
  Full viewport height (`min-h-screen`). Internal 12-column grid with vertical centering (`items-center`):
  - **Columns 1-6 (RTL Right):** The text block.
    - Above the H1: A small "badge" element (`inline-flex items-center gap-2 bg-solar-gold/10 text-solar-gold text-sm px-4 py-1.5 rounded-full border border-solar-gold/20`) containing text like "پیشرو در انرژی خورشیدی البرز".
    - The H1: "پایان قطعی برق در تابستان و زمستان" in `text-4xl lg:text-6xl font-black text-white leading-tight`. The word "قطعی" or "پایان" can be accented in `text-solar-gold`.
    - Below H1: A subtitle paragraph in `text-lg text-slate-400 mt-4 max-w-lg leading-relaxed`: "نیروگاههای خورشیدی هورانور سهند با بیش از ۸۵ پروژه موفق، برق مطمئن و پایدار شما را تضمین میکند."
    - Below subtitle: Two side-by-side CTAs. Primary: "مشاوره رایگان" (WhatsApp link) in `bg-solar-gold text-deep-navy`. Secondary: "نمونه پروژهها" (anchor to Section 7) in `border border-white/20 text-white hover:bg-white/5`.
  - **Columns 7-12 (RTL Left):** The 3-Click Solar Calculator Micro-App.
    - Container: A glassmorphism card (`backdrop-blur-xl bg-glass-white border border-glass-border rounded-3xl p-8 shadow-[0_0_60px_rgba(245,166,35,0.1)]`).
    - **Step 1 (Active by default):** Title: "نوع مصرف خود را مشخص کنید". Three large, tappable icon-cards arranged in a `grid grid-cols-3 gap-3`. Each card: an icon (villa/factory/farm) + label underneath. Cards have `border-2 border-transparent` and on selection become `border-solar-gold bg-solar-gold/10`.
    - **Step 2 (Revealed after Step 1):** Title: "مبلغ قبض برق شما چقدر است؟". A range slider with custom styling (track = `bg-slate-700`, thumb = `bg-solar-gold w-6 h-6 rounded-full shadow-lg`, fill = `bg-solar-gold`). Value label displays dynamically above the thumb. Range: 500,000 to 50,000,000 Rial.
    - **Step 3 (Revealed after Step 2):** Title: "توان مورد نیاز شما". A large animated number display (e.g., "۵ کیلووات") in `text-5xl font-black text-solar-gold`. Below it: a CTA button "دریافت قیمت دقیق" linking to WhatsApp with pre-filled message.
    - A step indicator at the top of the card: 3 dots/circles, the active one filled with solar-gold, others are outline.

- **Mobile Layout Architecture:**
  Stack vertically. The text block comes FIRST (`order-1` in flex column), followed by the calculator card (`order-2`). The H1 scales down to `text-3xl`. The calculator card becomes full-width with `mx-4 rounded-2xl p-6`. The 3 icon-cards in Step 1 remain in `grid-cols-3` but shrink (`gap-2`). The slider in Step 2 must have a large touch target (thumb at least `w-8 h-8`). The hero is NOT full viewport on mobile — it's `min-h-[auto] pt-24 pb-12` to avoid scroll traps.

- **Interactive "Navboost" Specs:**
  1. **Click 1:** User taps one of 3 property types. This is a selection interaction. Animate the chosen card with a quick `scale-105` bounce and a checkmark icon fading in. Transition to Step 2 with a slide-up animation (200ms).
  2. **Click 2:** User drags the range slider. This is a continuous interaction. The displayed value updates in real-time. On release, transition to Step 3 with a slide-up.
  3. **Click 3:** The "result" appears with an animated counter (numbers rolling up to the final value over 1 second). Then the CTA button pulses.
  4. These 3 clicks create 3+ interaction events in under 15 seconds. This is the Navboost goldmine.

- **Tailwind Structural Directives:**
  ```
  Section: relative min-h-screen flex items-center bg-deep-navy overflow-hidden
  Background: absolute inset-0 bg-gradient-to-bl from-deep-navy via-midnight-blue to-deep-navy
  Grid: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-16 px-4 lg:px-8
  Text block: col-span-1 lg:col-span-6 order-1
  Calculator: col-span-1 lg:col-span-6 order-2
  Glass card: backdrop-blur-xl bg-white/[0.06] border border-white/[0.1] rounded-3xl p-6 lg:p-8
  Step cards: grid grid-cols-3 gap-3
  Each step card: flex flex-col items-center justify-center p-4 rounded-2xl border-2 border-transparent cursor-pointer transition-all
  Selected: border-solar-gold bg-solar-gold/10
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. The calculator widget MUST be wrapped in `<section aria-roledescription="calculator">`.
  2. Step 3 result container (the kW number output) MUST have `aria-live="polite"`. When the number updates dynamically via JS, this ARIA tag forces screen readers and Google's rendering engine to register the DOM change as a high-value user interaction.
  3. The hero background image MUST use this exact alt text for LSI keyword injection: `alt="نصب پنل خورشیدی در کرج و استان البرز توسط هورانور سهند"`.

---

### SECTION 3: Entity Hijacking Trust Bar (Government & Syndicate Binding)

- **Overall UI Aesthetic:** "Institutional Authority Strip." Cool, muted, high-contrast. Grayscale logos against a slightly lighter dark background. Feels like an official government certification panel, not a marketing section. Minimal, structured, and legally credible.

- **Desktop Layout Architecture:**
  Narrow-height section (`py-8 lg:py-12`). Background: `bg-slate-900` (slightly lighter than the hero to create visual separation). Internal structure: A single horizontal row of 4-5 trust items using `flex items-center justify-center gap-12 lg:gap-20`.
  Each trust item is a vertical stack:
  - Top: Grayscale logo/emblem (64x64px, `filter grayscale opacity-60 hover:opacity-100 hover:grayscale-0 transition-all`).
  - Bottom: One line of micro-text in `text-xs text-slate-500`, e.g., "تایید شده توسط ساتبا".
  
  Alternatively (Architect's preferred layout): A 4-column Bento block inside a glass container. Each cell is a mini-card with the logo centered and the micro-text below. The entire block has `backdrop-blur-md bg-white/[0.03] border border-white/[0.06] rounded-2xl p-6`.

- **Mobile Layout Architecture:**
  Convert to a 2x2 grid (`grid grid-cols-2 gap-4 px-4`). Each trust item becomes a compact card with the logo (48x48) and micro-text centered. Alternatively, use an auto-scrolling horizontal marquee (`overflow-x-auto scrollbar-hide flex gap-8 snap-x snap-mandatory`) where each item has `snap-center min-w-[140px]`. The marquee approach is preferred for mobile because it creates scroll interaction.

- **Interactive "Navboost" Specs:**
  1. On desktop, each logo desaturates to grayscale by default and reveals full color + slight scale-up on hover. This creates hover-intent interaction.
  2. On mobile, the horizontal marquee auto-scrolls slowly (CSS `@keyframes` or JS `requestAnimationFrame`). User can manually swipe to override, creating a touch interaction event.
  3. Optional: each logo links to the relevant government entity's official page (`target="_blank" rel="noopener"`) which counts as an outbound engagement signal.

- **Tailwind Structural Directives:**
  ```
  Section: bg-slate-900 py-8 lg:py-12 border-y border-white/[0.05]
  Desktop: hidden lg:flex items-center justify-center gap-16 max-w-5xl mx-auto
  Mobile: lg:hidden flex overflow-x-auto scrollbar-hide gap-6 px-4 snap-x snap-mandatory
  Each item: flex flex-col items-center gap-2 snap-center min-w-[140px] lg:min-w-0
  Logo: w-16 h-16 object-contain filter grayscale opacity-60 hover:opacity-100 hover:grayscale-0 transition-all duration-300
  Label: text-xs text-slate-500 text-center
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. Government entity names MUST be wrapped in `<abbr>` or `<cite>` tags to feed exact entity definitions into Google's NLP parser:
     - `تایید شده توسط <abbr title="سازمان انرژیهای تجدیدپذیر و بهرهوری انرژی برق">ساتبا</abbr>`
     - `مطابق با استانداردهای <abbr title="وزارت نیرو جمهوری اسلامی ایران">وزارت نیرو</abbr>`
     - `مورد تایید <abbr title="شرکت توزیع نیروی برق استان البرز">توزیع برق البرز</abbr>`
  2. Each micro-text label under logos must contain these exact semantic strings for NLP co-citation entity transference.

---

### SECTION 4: Pain-Point Context & Legal Trigger (The "Why")

- **Overall UI Aesthetic:** "Dual-Threat Split — Dark Warning vs. Bright Solution." The section is literally split into two contrasting visual zones. The "Problem" zone uses dark/red tones and harsh, angular shapes suggesting urgency. The "Solution" zone uses bright/green/gold tones with rounded, calming shapes. The visual tension between them is the storytelling vehicle.

- **Desktop Layout Architecture:**
  Full-width section. Background transitions from `bg-slate-950` on the right (RTL start / Problem side) to `bg-pure-white` on the left (RTL end / Solution side) using a diagonal clip-path or angled gradient.
  Internal 12-column grid:
  - **Columns 1-6 (RTL Right — The Problem):** Dark background (`bg-slate-950`).
    - Section label: Small tag "چرا خورشیدی؟" in `text-danger-red text-sm font-bold uppercase tracking-wide`.
    - H2: "تهدیدی که نادیده میگیرید" in `text-3xl lg:text-4xl font-black text-white`.
    - Below: An asymmetrical Bento grid of 3 "threat cards" (`grid grid-cols-2 gap-4`). Card 1 spans full width (`col-span-2`), cards 2 and 3 sit side-by-side.
      - **Card 1 (B2B Legal):** `bg-red-950/50 border border-red-500/20 rounded-2xl p-6`. Icon: gavel/law. Title: "جریمه ماده ۱۶ جهش تولید". Body: Short text about factory fines for not using 1-5% renewable energy.
      - **Card 2 (B2C Noise):** Same style. Icon: noise/speaker. Title: "صدای آزاردهنده ژنراتور". Body: Diesel generator noise and cost in villa zones.
      - **Card 3 (Blackout):** Same style. Icon: lightning/power-off. Title: "قطعی برق و توقف خط تولید". Body: Production shutdowns from grid failures.
  - **Columns 7-12 (RTL Left — The Solution):** Light background (`bg-pure-white`).
    - Section label: Small tag "راهحل هورانور سهند" in `text-trust-green text-sm font-bold`.
    - H2: "انرژی پایدار، سود تضمینی" in `text-3xl lg:text-4xl font-black text-text-dark`.
    - Below: A Bento grid of 3 "solution cards" with the same layout structure.
      - **Card 1:** `bg-green-50 border border-green-200 rounded-2xl p-6`. Icon: solar panel. Title: "برق مستقل و بدون قطعی". Body: 24/7 off-grid power.
      - **Card 2:** `bg-amber-50 border border-amber-200`. Icon: money/ROI. Title: "بازگشت سرمایه ۳-۵ سال". Body: ROI guarantee.
      - **Card 3:** `bg-blue-50 border border-sky-200`. Icon: certificate. Title: "رفع کامل جریمه ماده ۱۶". Body: Legal compliance.

- **Mobile Layout Architecture:**
  Stack the two zones vertically. Problem zone first (dark background), Solution zone second (light background). Each zone takes full width. The Bento grid inside each zone collapses to `grid-cols-1 gap-3`. The diagonal split becomes a simple horizontal boundary. No clip-path on mobile.

- **Interactive "Navboost" Specs:**
  1. Each threat card has a `hover:border-red-500/40 hover:bg-red-950/70` transition creating hover engagement.
  2. Each solution card has a `hover:border-green-400 hover:shadow-lg hover:-translate-y-1` lift effect.
  3. On mobile, add a subtle horizontal scroll indicator suggesting there's more content (even though it stacks, the cards can slide-in from the side as the user scrolls using Intersection Observer stagger).
  4. The H2 text in the Problem zone should have a slow, subtle red `text-shadow` pulse (like a warning beacon) — use a CSS keyframe.

- **Tailwind Structural Directives:**
  ```
  Section: relative overflow-hidden
  Desktop wrapper: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 min-h-[600px]
  Problem zone: col-span-6 bg-slate-950 p-8 lg:p-12 flex flex-col justify-center
  Solution zone: col-span-6 bg-white p-8 lg:p-12 flex flex-col justify-center
  Threat cards: grid grid-cols-1 lg:grid-cols-2 gap-4 mt-8
  Card 1: lg:col-span-2
  Each card: rounded-2xl p-6 border transition-all duration-300
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. Each Problem card and Solution card MUST be wrapped in `<article>` tags for semantic HTML5 structure.
  2. NLP TF-IDF Saturation: The following exact-match Farsi phrases MUST appear in the text content of this section (Google's AI specifically looks for these industry terms):
     - `قطعی مکرر برق صنایع` (Frequent industrial power outages)
     - `خرید تضمینی برق` (Guaranteed electricity purchase)
     - `کاهش هزینه قبض برق` (Reducing electricity bill costs)
     - `تامین برق استخراج` (Mining power supply — optional but highly searched)

---

### SECTION 5: The 4 Core Service Pillars (Semantic Silo Gateways)

- **Overall UI Aesthetic:** "Premium Service Showcase — Dark Luxury." Background is deep navy. The four service pillars appear as large, equal-height Bento cards with atmospheric imagery. On hover, a secondary "reveal layer" slides up from the bottom of each card, exposing LSI keywords and the CTA. Feels like a high-end corporate annual report.

- **Desktop Layout Architecture:**
  Section background: `bg-deep-navy`. Generous padding `py-20 lg:py-28`.
  Top: Centered section header. Label: "خدمات ما" in `text-solar-gold text-sm tracking-widest uppercase`. H2: "چهار ستون تخصص هورانور سهند" in `text-3xl lg:text-5xl font-black text-white text-center`.
  Below: A 4-column Bento grid (`grid grid-cols-4 gap-5`). Each card is `aspect-[3/4]` or fixed height `h-[480px]`.
  Each Pillar Card structure (from bottom to top in Z-axis):
  - **Layer 0 (Background):** A relevant background image covering the full card (`bg-cover bg-center`). Images: Villa in Kordan, Factory rooftop, Agricultural field with pump, SATBA contract/powerplant. Apply `brightness-[0.3]` by default.
  - **Layer 1 (Default visible content):** Positioned at the bottom of the card (`absolute bottom-0 inset-x-0`). Contains: a pillar icon (48x48, white), pillar title in `text-xl font-bold text-white`, and a one-line description in `text-sm text-slate-300`.
  - **Layer 2 (Hover reveal):** A panel that slides up from below the card (`translate-y-full` by default, `group-hover:translate-y-0` on hover). Contains: `backdrop-blur-2xl bg-deep-navy/90` background, 3 bulleted LSI keywords in `text-sm text-slate-200`, and a CTA link "بیشتر بدانید ←" in `text-solar-gold`.

  **The 4 Pillars:**
  1. **خانگی و ویلایی:** LSI: سیستم آفگرید, باتری خورشیدی ویلا, تامین برق ویلای کردان.
  2. **صنعتی و سوله:** LSI: نیروگاه آنگرید سقف سوله, رفع جریمه ماده ۱۶, کاهش هزینه برق صنعتی.
  3. **کشاورزی:** LSI: پمپ آب خورشیدی, برق چاه کشاورزی, آبیاری بدون شبکه.
  4. **سرمایهگذاری ساتبا:** LSI: فروش تضمینی برق, قرارداد ۲۰ ساله ساتبا, درآمد پایدار خورشیدی.

- **Mobile Layout Architecture:**
  The 4-column grid collapses to a horizontal scroll container (`flex overflow-x-auto snap-x snap-mandatory gap-4 px-4 -mx-4`). Each card becomes `min-w-[280px] snap-center`. The hover-reveal layer is ALWAYS visible on mobile (no hover on touch), positioned as a semi-transparent overlay at the bottom third of the card. A subtle left-arrow indicator at the edge of the screen hints at scrollability (a gradient fade `bg-gradient-to-l from-deep-navy via-deep-navy/50 to-transparent` overlaying the right edge).

- **Interactive "Navboost" Specs:**
  1. Desktop: Hover triggers the reveal panel slide-up (a rich hover interaction creating dwell-time signals).
  2. Desktop: The background image brightness increases from `0.3` to `0.5` on hover, creating visual reward.
  3. Mobile: Horizontal swipe/scroll creates continuous touch interaction events.
  4. Each card's CTA navigates to the respective service deep page (internal link, distributing PageRank).

- **Tailwind Structural Directives:**
  ```
  Section: bg-deep-navy py-16 lg:py-28
  Header: text-center mb-12 lg:mb-16
  Grid: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-4 gap-5 px-4 lg:px-8
  Mobile override: lg:grid flex overflow-x-auto snap-x snap-mandatory gap-4
  Each card: group relative overflow-hidden rounded-3xl h-[400px] lg:h-[480px] min-w-[280px] snap-center cursor-pointer
  Card image: absolute inset-0 bg-cover bg-center brightness-[0.3] group-hover:brightness-50 transition-all duration-500
  Default content: absolute bottom-0 inset-x-0 p-6 z-10
  Reveal panel: absolute inset-0 flex flex-col justify-end p-6 z-20 backdrop-blur-2xl bg-deep-navy/85 translate-y-full group-hover:translate-y-0 transition-transform duration-500
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. The section title MUST be an `<h2>` tag. Each pillar card title MUST be an `<h3>` tag. This strict `H1 → H2 → H3` hierarchy is non-negotiable for Google's indexing algorithm.
  2. Image SEO: Background images for the 4 pillars MUST have exact-match descriptive filenames. **WRONG:** `img_4992.jpg`. **RIGHT:**
     - `solar-panel-villa-kordan-offgrid.jpg`
     - `industrial-solar-power-plant-eshtehard.jpg`
     - `solar-water-pump-agricultural-hashtgerd.jpg`
     - `satba-solar-investment-power-plant.jpg`

---

### SECTION 6: Information Gain & Alborz Data Hub (Proprietary Data Patent)

- **Overall UI Aesthetic:** "Command Center Analytics Dashboard." Light background section for contrast after the dark pillars. The data points are displayed in a Bento grid of "stat cards" that feel like a Bloomberg terminal or NASA mission control — large bold numbers, supporting graphs, and precise data labels. Clean, authoritative, data-driven.

- **Desktop Layout Architecture:**
  Background: `bg-pure-white` or `bg-soft-gray`. Padding: `py-20 lg:py-28`.
  Top: Centered header. Label: "دادههای عملیاتی" in `text-solar-gold`. H2: "هاب داده خورشیدی استان البرز" in `text-3xl lg:text-5xl font-black text-text-dark text-center`.
  Below: An asymmetrical Bento grid using `grid-cols-12 grid-rows-2 gap-5`:
  - **Stat Card 1 (Large — spans cols 1-5, rows 1-2):** "+85 پروژه موفق". The number "+85" is in `text-7xl lg:text-8xl font-black text-deep-navy`. An animated counter ticks up from 0 to 85 on scroll-into-view. Below: a small sparkline chart or bar chart showing project growth YoY. Background: `bg-white rounded-3xl shadow-sm border border-slate-100 p-8`.
  - **Stat Card 2 (Medium — spans cols 6-9, row 1):** "۲۵۰ روز آفتابی". Number "۲۵۰" in `text-5xl font-black text-solar-gold`. Below: a radial/circular progress bar filling to ~68% (250/365). The ring uses `stroke: solar-gold` on a `stroke: slate-200` track.
  - **Stat Card 3 (Medium — spans cols 10-12, row 1):** "بازگشت سرمایه". "۳-۵ سال" in `text-4xl font-black text-trust-green`. Below: a simple horizontal bar showing investment recovery timeline.
  - **Stat Card 4 (Wide — spans cols 6-12, row 2):** "ظرفیت ۱ کیلووات تا ۱۰ مگاوات". This card shows a visual scale/gauge from 1kW to 10MW. Use a horizontal progress bar or a thermometer-style gauge. Text: "از سقف ویلا تا نیروگاه صنعتی" as supporting copy.

- **Mobile Layout Architecture:**
  The Bento grid collapses to `grid-cols-1 gap-4 px-4`. Each stat card stacks vertically, all full-width. The large stat card (+85) still uses its big typography. The radial chart for 250 days renders at a smaller size (`w-32 h-32` centered). All animated counters still fire on mobile scroll-into-view.

- **Interactive "Navboost" Specs:**
  1. Animated number counters trigger on Intersection Observer (scroll into view). Numbers roll from 0 to target value over 2 seconds with easing.
  2. The radial progress bar animates its fill from 0 to 68% with a smooth stroke-dashoffset transition.
  3. The horizontal gauge for capacity animates its fill width.
  4. Optional: a subtle tooltip on hover over each stat card showing source ("بر اساس دادههای اجرایی شرکت هورانور سهند").
  5. All animations ONLY fire once, on first scroll intersection.

- **Tailwind Structural Directives:**
  ```
  Section: bg-slate-50 py-16 lg:py-28
  Grid: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 lg:grid-rows-2 gap-5 px-4 lg:px-8
  Card 1: lg:col-span-5 lg:row-span-2 bg-white rounded-3xl p-8 shadow-sm border border-slate-100
  Card 2: lg:col-span-4 bg-white rounded-3xl p-8 shadow-sm border border-slate-100
  Card 3: lg:col-span-3 bg-white rounded-3xl p-8 shadow-sm border border-slate-100
  Card 4: lg:col-span-7 bg-white rounded-3xl p-8 shadow-sm border border-slate-100
  Number: text-6xl lg:text-8xl font-black tabular-nums
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. **The `<data>` tag trick (Featured Snippet weapon):** Do NOT just render numbers as plain text. Wrap all proprietary data in HTML5 `<data>` tags so Google's AI scraper can extract them for Featured Snippets:
     - `بیش از <data value="85">۸۵</data> پروژه موفق در البرز`
     - `پتانسیل <data value="250">۲۵۰</data> روز آفتابی`
     - `بازگشت سرمایه <data value="4">۳ تا ۵</data> سال`
     - `ظرفیت نصب از <data value="1">۱</data> کیلووات تا <data value="10000">۱۰</data> مگاوات`

---

### SECTION 7: Proof of Life (Live Operations Widget)

- **Overall UI Aesthetic:** "Dark Operational Radar." Returns to a dark background to create rhythm. Feels like a military/logistics operations room. A map with pulsing dots. A scrolling feed of deployment statuses. Active, alive, in-motion.

- **Desktop Layout Architecture:**
  Background: `bg-deep-navy`. Padding: `py-20 lg:py-28`.
  Internal 12-column grid:
  - **Columns 1-7 (RTL Right):** An interactive map visualization of Alborz province. Use an SVG map of Alborz or a simplified illustrated map. Key cities (Karaj, Kordan, Hashtgerd, Eshtehard, Simindasht, Mehrshahr) are marked with pulsing beacon dots. Active projects pulse in `danger-red` (🔴 در حال اجرا). Completed projects pulse in `trust-green` (🟢 تکمیل شده). On hover over a dot, a tooltip card appears showing: "نصب پنل ۵۰ کیلوواتی - شهرک صنعتی اشتهارد".
  - **Columns 8-12 (RTL Left):** A vertical "Live Feed" ticker. A scrolling list of 5-8 project status entries. Each entry is a card (`bg-white/[0.04] border border-white/[0.06] rounded-xl p-4 mb-3`). Entry structure: Top row = status badge (red "در حال اجرا" or green "تکمیل شده") + location name. Bottom row = project description in `text-sm text-slate-400`. The feed auto-scrolls upward slowly (one entry every 4 seconds) via CSS animation or JS interval.

- **Mobile Layout Architecture:**
  Stack vertically. The map appears first but at reduced height (`h-[250px]`). The map is scrollable/zoomable by touch. Below: the Live Feed ticker as a horizontal card carousel (`flex overflow-x-auto snap-x gap-3 px-4`), each entry card `min-w-[260px] snap-center`. Alternatively, stack vertically as a simple list with 4-5 visible items.

- **Interactive "Navboost" Specs:**
  1. Map dot hover/tap → tooltip reveal = interaction event.
  2. Auto-scrolling feed creates passive "motion" on the page, increasing perceived liveliness and dwell time.
  3. Mobile: horizontal swipe on feed cards = touch interaction.
  4. The pulsing beacon dots use CSS `@keyframes` with `scale` and `opacity` creating a "radar ping" effect (concentric rings expanding outward every 2s).

- **Tailwind Structural Directives:**
  ```
  Section: bg-deep-navy py-16 lg:py-28
  Grid: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 gap-8 px-4 lg:px-8
  Map area: col-span-7 relative h-[300px] lg:h-[500px] rounded-3xl overflow-hidden bg-midnight-blue border border-white/[0.06]
  Feed area: col-span-5 flex flex-col gap-3 max-h-[500px] overflow-hidden
  Feed card: bg-white/[0.04] border border-white/[0.06] rounded-xl p-4
  Pulse dot: absolute w-4 h-4 rounded-full animate-ping
  Dot core: absolute w-3 h-3 rounded-full bg-trust-green (or bg-danger-red)
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. All scrolling dates/timestamps in the live feed MUST be wrapped in `<time>` tags for Google Freshness signals:
     - `<time datetime="2024-05-12">امروز</time> - نصب پنل ۵۰ کیلوواتی در شهرک صنعتی اشتهارد`
     - `<time datetime="2024-04-28">هفته گذشته</time> - راهاندازی پمپ آب خورشیدی در هشتگرد`
  2. The scrolling ticker container MUST have `aria-live="polite"`. This forces Googlebot to read the page as a continuously updating news source, triggering more frequent crawling via the Freshness algorithm.

---

### SECTION 8: Geographic Authority Matrix (Local SEO Grid)

- **Overall UI Aesthetic:** "Segmented Luxury/Industrial Dual Grid." Light background. Two distinct visual zones within the same section: B2C (villa/luxury aesthetic — warm tones, serif-ish accents, property imagery) and B2B (industrial/factory aesthetic — steel tones, bold sans-serif, factory imagery). The contrast visually communicates "we serve everyone."

- **Desktop Layout Architecture:**
  Background: `bg-pure-white`. Padding: `py-20 lg:py-28`.
  Top: Centered header. Label: "حوزه فعالیت". H2: "نقشه پوشش خورشیدی هورانور سهند" in `text-3xl lg:text-5xl font-black text-text-dark text-center`.
  Below: Two sub-sections separated by a vertical divider (or clear spacing):
  - **B2C Zone (RTL Right — cols 1-6):**
    - Zone title: "مناطق ویلایی و مسکونی" with a 🏡 icon, in `text-xl font-bold text-amber-800`.
    - A `grid grid-cols-2 gap-4` of location cards. Each card: `bg-amber-50/50 border border-amber-100 rounded-2xl p-5`. Contains: city name in bold (کردان, مهرشهر, لواسان, هشتگرد, بهارستان), and a one-line tagline like "برق خورشیدی ویلای لوکس".
  - **B2B Zone (RTL Left — cols 7-12):**
    - Zone title: "مناطق صنعتی و تولیدی" with a 🏭 icon, in `text-xl font-bold text-slate-700`.
    - A `grid grid-cols-2 gap-4` of location cards. Each card: `bg-slate-100 border border-slate-200 rounded-2xl p-5`. Contains: city name (شهرک صنعتی اشتهارد, سیمین دشت, کرج, شهرک صنعتی هشتگرد), and a tagline like "نیروگاه ۲۰۰ کیلووات سقف سوله".
  - **Below both zones:** A secondary row for national expansion: a simple flex row of city badges/tags. Each tag: `inline-flex px-3 py-1.5 bg-slate-100 text-slate-600 text-sm rounded-full`. Cities: تهران, قزوین, بابل, یزد, اصفهان, رشت, ساری, گرگان.

- **Mobile Layout Architecture:**
  Stack the B2C and B2B zones vertically. B2C zone first (villa audience is 80% mobile). Each zone's internal grid collapses to `grid-cols-2 gap-3`. The national expansion tags wrap to multiple lines (`flex flex-wrap gap-2`). Consider a horizontal swipe for the tags on very small screens.

- **Interactive "Navboost" Specs:**
  1. Each location card links to a dedicated location landing page (e.g., /solar-kordan/) — this distributes PageRank and creates click events.
  2. Hover on desktop: cards lift (`hover:-translate-y-1 hover:shadow-md`) and the border color intensifies.
  3. Mobile: cards are tappable with `active:scale-[0.98]` press feedback.
  4. National expansion tags could have a subtle slide-in animation on scroll.

- **Tailwind Structural Directives:**
  ```
  Section: bg-white py-16 lg:py-28
  Grid: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-12 px-4 lg:px-8
  B2C zone: col-span-6
  B2B zone: col-span-6
  Location cards: grid grid-cols-2 gap-3 lg:gap-4
  Each card: rounded-2xl p-5 border transition-all duration-300 hover:-translate-y-1 hover:shadow-md cursor-pointer
  B2C card: bg-amber-50/50 border-amber-100 hover:border-amber-300
  B2B card: bg-slate-100 border-slate-200 hover:border-slate-400
  Tags row: flex flex-wrap gap-2 mt-8 justify-center
  Tag: inline-flex px-3 py-1.5 bg-slate-100 text-slate-600 text-sm rounded-full
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. Location names (Kordan, Mehrshahr, Eshtehard, etc.) MUST be actual `<a>` links to location-specific service pages (e.g., `/solar-panels-in-kordan/`, `/solar-eshtehard/`). If those pages don't exist yet, wrap cities in `<address>` tags or localized semantic clusters.
  2. **Google Maps Binding:** Embed a small Google Map iframe of the exact Karaj HQ location, or link directly to the Google Business Profile CID to lock the geographic Knowledge Graph entity. Place this near the B2C zone or at the section bottom.

---

### SECTION 9: Hardware Ecosystem & Global Brand Integration

- **Overall UI Aesthetic:** "Minimalist Tech Showcase." Dark section for contrast. The brand logos float on a dark canvas, presented in a premium, high-fashion layout — think of the "Partners" section on a Tier-1 tech company site. Crisp, mono-toned logos with subtle hover reveals. No clutter.

- **Desktop Layout Architecture:**
  Background: `bg-slate-950`. Padding: `py-16 lg:py-24`.
  Top: Centered header. Label: "تجهیزات Tier-1". H2: "زنجیره تامین جهانی هورانور سهند" in `text-white text-2xl lg:text-4xl font-black text-center`.
  Subtext: "استفاده از تجهیزات Tier-1 جهانی" in `text-slate-400 text-center mt-3`.
  Below: Option A — Infinite scroll marquee: Two rows of logos scrolling in opposite directions (row 1 scrolls left, row 2 scrolls right in RTL context). Each logo: 100x50 SVG, white/monochrome, `opacity-40 hover:opacity-100 transition-opacity`.
  Option B (Preferred) — A `grid grid-cols-4 lg:grid-cols-7 gap-6` centered grid. Each cell: a glass card (`bg-white/[0.03] border border-white/[0.06] rounded-2xl p-6 flex items-center justify-center aspect-[3/2]`). Logo inside centered. On hover: card glows with `shadow-[0_0_20px_rgba(245,166,35,0.1)]` and logo goes from `opacity-50` to `opacity-100`.
  **Brands:** Trina Solar (ترینا), JinkoSolar (جینکو), LONGi (لنگی), JA Solar (جی ای), Vmax (وی مکس), Mana (مانا), Taban (تابان).

- **Mobile Layout Architecture:**
  Grid collapses to `grid-cols-3 gap-3 px-4`. Logos scale down. The glass cards shrink in padding (`p-4`). Alternatively, use the marquee approach on mobile for continuous passive animation (scrolling logos always in motion).

- **Interactive "Navboost" Specs:**
  1. If using marquee: auto-scroll creates continuous motion on the page. User can grab/swipe to interact.
  2. If using grid: hover glow effect creates interaction events on desktop. On mobile, tap to reveal brand name as a tooltip.
  3. Each logo can optionally link to the manufacturer's official site (`target="_blank" rel="noopener"`) — outbound link trust signal.

- **Tailwind Structural Directives:**
  ```
  Section: bg-slate-950 py-12 lg:py-24
  Grid: max-w-6xl mx-auto grid grid-cols-3 lg:grid-cols-7 gap-3 lg:gap-6 px-4 lg:px-8
  Each cell: bg-white/[0.03] border border-white/[0.06] rounded-2xl p-4 lg:p-6 flex items-center justify-center aspect-[3/2] transition-all duration-300
  Hover: hover:shadow-[0_0_20px_rgba(245,166,35,0.1)] hover:border-solar-gold/20
  Logo img: w-full max-w-[80px] h-auto object-contain opacity-50 hover:opacity-100 transition-opacity filter brightness-200 (for white-on-dark)
  Marquee alt: flex animate-scroll whitespace-nowrap gap-12
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. Brand names MUST be wrapped in `<strong>` tags inside a `<ul>` / `<li>` list layout for crawler list-extraction:
     - `<li>تجهیزات <strong>Trina Solar</strong> (ترینا)</li>`
     - `<li>تجهیزات <strong>JinkoSolar</strong> (جینکو)</li>`
     - `<li>تجهیزات <strong>LONGi</strong> (لنگی)</li>`
     - `<li>تجهیزات <strong>JA Solar</strong> (جی ای)</li>`
     - `<li>تجهیزات <strong>Vmax</strong> (وی مکس)</li>`
     - `<li>تجهیزات <strong>Mana</strong> (مانا)</li>`
     - `<li>تجهیزات <strong>Taban</strong> (تابان)</li>`
  2. This `<ul>` can be visually hidden (`sr-only`) if it disrupts the logo grid layout, but MUST exist in the DOM for Googlebot crawling.

---

### SECTION 10: E-E-A-T Executive FAQ (SGE & Voice Search Capture)

- **Overall UI Aesthetic:** "Clean Editorial Accordion." Light background. Minimal design. The focus is on readability and the FAQPage schema structure. Clean borders, generous whitespace, and smooth expand/collapse animations. Think of a premium Q&A section from a government or university site.

- **Desktop Layout Architecture:**
  Background: `bg-pure-white` or `bg-soft-gray`. Padding: `py-20 lg:py-28`.
  Top: Centered header. Label: "سوالات متداول". H2: "پاسخهای تخصصی به سوالات شما" in `text-3xl lg:text-5xl font-black text-text-dark text-center`.
  Below: A single-column accordion container (`max-w-3xl mx-auto`). Each FAQ item:
  - Container: `border-b border-slate-200 py-5`.
  - Question row: `flex items-center justify-between cursor-pointer group`. The question text in `text-lg font-semibold text-text-dark group-hover:text-solar-gold transition-colors`. An icon on the left (RTL end): a `+` that rotates to `×` on expand, using `transition-transform duration-300 rotate-0 → rotate-45`.
  - Answer panel: Hidden by default (`max-h-0 overflow-hidden transition-all duration-500`). On expand: `max-h-[500px]`. Content inside: `pt-3 text-slate-600 leading-relaxed`. Key terms inside answers are `<strong>` with `text-text-dark`.

  **The 3 Core FAQs:**
  1. "شرایط فروش تضمینی برق به ساتبا در سال جدید چیست؟"
  2. "آیا نیروگاه خورشیدی جریمه ماده ۱۶ صنایع را رفع میکند؟"
  3. "هزینه احداث نیروگاه خورشیدی برای ویلا در کردان چقدر است؟"

- **Mobile Layout Architecture:**
  Same single-column structure. The accordion is naturally mobile-friendly. Ensure question text doesn't truncate — use `text-base` on mobile. The tap target for the entire question row must be at least `min-h-[48px]` for accessibility. Increase padding to `py-4 px-4`.

- **Interactive "Navboost" Specs:**
  1. Each accordion open/close is a click interaction event logged by Navboost.
  2. The `+` → `×` icon rotation is a satisfying micro-interaction that encourages exploring multiple questions.
  3. Smooth height animation (`max-h` transition with `ease-[cubic-bezier(0.4,0,0.2,1)]`) prevents jarring layout shifts.
  4. Consider: a subtle highlight/glow on the question text when it's in the expanded state (`text-solar-gold`).

- **Tailwind Structural Directives:**
  ```
  Section: bg-slate-50 py-16 lg:py-28
  Container: max-w-3xl mx-auto px-4 lg:px-0
  Each FAQ item: border-b border-slate-200
  Question button: w-full flex items-center justify-between py-5 text-start cursor-pointer group
  Question text: text-base lg:text-lg font-semibold text-slate-800 group-hover:text-solar-gold transition-colors
  Icon: w-6 h-6 text-slate-400 transition-transform duration-300 [&.open]:rotate-45
  Answer: overflow-hidden transition-all duration-500 max-h-0 [&.open]:max-h-[500px]
  Answer text: pt-3 pb-2 text-slate-600 leading-relaxed text-sm lg:text-base
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. The visual accordion MUST be synced with an invisible `FAQPage` JSON-LD schema payload in the `<head>`. If a question is visible on the page but missing from the JSON-LD, Google will not generate Voice Search or Gemini AI Overview results.
  2. UI/UX SEO: Use `<details>` and `<summary>` native HTML5 tags for the accordion structure. They require zero JavaScript to function and are prioritized by Googlebot for FAQ rich snippets.

---

### SECTION 11: The NAP-W Entity Footer Hub (Semantic Closure)

- **Overall UI Aesthetic:** "Dark Mega Footer — Information Dense." Deep navy background. Structured, multi-column layout with clear hierarchy. Every piece of data is machine-readable and human-scannable. The footer feels substantial and authoritative — not an afterthought. It's the final trust handshake with both the user and Googlebot.

- **Desktop Layout Architecture:**
  Background: `bg-deep-navy`. Top border: `border-t border-white/[0.06]`. Padding: `pt-16 pb-8 lg:pt-20 lg:pb-10`.
  Internal grid: `grid grid-cols-12 gap-8`.
  - **Column 1 (cols 1-4): Brand & NAP.**
    - Logo (SVG, larger than header version, `h-12`).
    - Below: Dual-language brand name ("هورانور سهند" / "Hora Nor Sahand").
    - Below: Full exact-match address text in `text-sm text-slate-400 leading-relaxed mt-4`: "کرج، جاده ملارد، بعد از دانشگاه فرهنگیان، نرسیده به پل ارتش جنب فروشگاه بهداشتی ساختمانی سهند، شرکت برق خورشیدی هورا نور سهند".
    - Below: Phone numbers as clickable `tel:` links, each on its own line, styled as `text-slate-300 hover:text-solar-gold transition-colors`.
    - Below: "تاسیس: ۱۳۹۵" in `text-xs text-slate-500`.
  - **Column 2 (cols 5-6): Quick Links — Services.**
    - Title: "خدمات" in `text-white font-bold mb-4`.
    - 4 links: خانگی و ویلایی, صنعتی و سوله, کشاورزی, سرمایهگذاری ساتبا. Each: `block text-sm text-slate-400 hover:text-solar-gold py-1.5 transition-colors`.
  - **Column 3 (cols 7-9): Quick Links — Resources & Pages.**
    - Title: "منابع" in `text-white font-bold mb-4`.
    - Links: درباره ما, بلاگ, نمونه پروژهها, تماس با ما, سوالات متداول. Same styling as Column 2.
  - **Column 4 (cols 10-12): Social & Trust.**
    - Title: "ارتباط با ما" in `text-white font-bold mb-4`.
    - Social icons grid: `grid grid-cols-4 gap-3`. Each icon: a `w-10 h-10 rounded-xl bg-white/[0.05] border border-white/[0.06] flex items-center justify-center hover:bg-solar-gold/20 hover:border-solar-gold/30 transition-all`. Icons for: Telegram, Instagram, WhatsApp, Bale, Eitaa, Rubika. CRITICAL: Use the official icons for Bale (بله), Eitaa (ایتا), and Rubika (روبیکا) — these are Farsi-specific social networks and must not be represented by generic icons.
    - Below: Trust badges row. E-Namad badge, SATBA badge, Engineering Syndicate badge. Each `h-14` displayed inline with `flex gap-4 mt-6`.

  **Copyright Bar:** Below all columns, separated by `border-t border-white/[0.06] mt-12 pt-6`. Centered text: "تمامی حقوق محفوظ است. شرکت هورا نور سهند | ۱۳۹۵ - ۱۴۰۴" in `text-xs text-slate-600 text-center`.

- **Mobile Layout Architecture:**
  Grid collapses to `grid-cols-1 gap-8 px-4`. Columns stack: Brand & NAP first → Services links → Resources links → Social & Trust. The social icons grid goes to `grid-cols-6` (all 6 icons in a single row). Trust badges center horizontally. The copyright bar stays centered.

- **Interactive "Navboost" Specs:**
  1. Phone numbers: clickable `tel:` links create direct conversion interactions.
  2. Social icons: hover glow effects create hover interaction. Tap on mobile opens the respective app.
  3. Quick links: hover color transition to solar-gold.
  4. Trust badges: optional hover tooltip showing "نماد اعتماد الکترونیک شماره XXXXX" — creates a hover interaction.

- **Tailwind Structural Directives:**
  ```
  Footer: bg-deep-navy border-t border-white/[0.06]
  Inner: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-12 gap-8 pt-12 pb-6 lg:pt-20 lg:pb-10 px-4 lg:px-8
  Col 1: lg:col-span-4
  Col 2: lg:col-span-2
  Col 3: lg:col-span-3
  Col 4: lg:col-span-3
  Social grid: grid grid-cols-4 lg:grid-cols-3 gap-3
  Social icon: w-10 h-10 rounded-xl bg-white/[0.05] border border-white/[0.06] flex items-center justify-center transition-all hover:bg-solar-gold/20 hover:border-solar-gold/30
  Copyright: border-t border-white/[0.06] mt-8 lg:mt-12 pt-6 text-center text-xs text-slate-600
  ```

- **Semantic HTML5 & SEO Directives (MANDATORY):**
  1. The NAP (Name, Address, Phone) MUST use standard schema microformats directly in the HTML.
  2. Phone numbers must use `itemprop="telephone"`:
     - `<a href="tel:+982636506485" itemprop="telephone">026-36506485</a>`
  3. Address must use the exact format:
     ```html
     <address itemprop="address" itemscope itemtype="https://schema.org/PostalAddress">
        <span itemprop="addressLocality">کرج</span>، <span itemprop="streetAddress">جاده ملارد، بعد از دانشگاه فرهنگیان، نرسیده به پل ارتش جنب فروشگاه بهداشتی ساختمانی سهند</span>
     </address>
     ```

---

## APPENDIX: SECTION RHYTHM & BACKGROUND ALTERNATION

The page follows a deliberate dark/light rhythm to prevent visual monotony and create natural scroll landmarks:

| Section | Background | Theme |
|---|---|---|
| 1 - Header | Dark (Glass) | `bg-deep-navy/80 backdrop-blur` |
| 2 - Hero | Dark | `bg-deep-navy` gradient |
| 3 - Trust Bar | Dark (slightly lighter) | `bg-slate-900` |
| 4 - Pain Points | Split Dark/Light | `bg-slate-950` / `bg-white` |
| 5 - Service Pillars | Dark | `bg-deep-navy` |
| 6 - Data Hub | Light | `bg-slate-50` |
| 7 - Live Radar | Dark | `bg-deep-navy` |
| 8 - Geographic Grid | Light | `bg-white` |
| 9 - Hardware Brands | Dark | `bg-slate-950` |
| 10 - FAQ | Light | `bg-slate-50` |
| 11 - Footer | Dark | `bg-deep-navy` |

This Dark → Dark → Dark/Light → Dark → Light → Dark → Light → Dark → Light → Dark cadence creates a natural scroll momentum where the user's brain registers "new zone" at each contrast shift.

---

## APPENDIX: MOBILE-FIRST PERFORMANCE DIRECTIVES

Since mobile is 80% of traffic, instruct the coder:

1. **Lazy-load all images** below the fold using `loading="lazy"` and `IntersectionObserver`.
2. **No heavy JS libraries.** The calculator and accordion must be vanilla JS or Alpine.js (lightweight).
3. **Critical CSS inline** for the header and hero section. Defer all other CSS.
4. **Font subsetting:** Only load the Farsi character range of Vazirmatn (wght 400, 700, 900). Do not load Latin characters from Vazirmatn.
5. **Image format:** Use WebP with AVIF fallback. Max width for mobile images: 640px.
6. **Scroll animations:** Use `will-change: transform, opacity` on animated elements and `content-visibility: auto` on below-fold sections.
7. **Target LCP < 2.5s**, **FID < 100ms**, **CLS < 0.1**.

---

**END OF WIREFRAME & LAYOUT SPECIFICATION**
*Hand this document to Agent 3 (Qwen 3.8 Max) for implementation.*
