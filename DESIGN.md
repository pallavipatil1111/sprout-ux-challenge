# Sprout 2.0: design rationale

## The problem in one line

40,000 downloads → 9,000 completed KYC (22%) → 3,000 first investments (33% of those). The biggest leak is **between download and KYC**. Support complaints point to two causes we can fix with design:

- people don't have PAN and Aadhaar ready;
- people think the app crashed while it is verifying them.

## How much I trust the data

| Data | Problem | How I used it |
|---|---|---|
| 78% bounce rate | Measured during a paid ad campaign, which brings low-intent visitors | Treated as inflated. I measure organic bounce separately before judging the new page |
| 62% drop at KYC, "cause unknown" | No funnel breakdown by step | Matched with support complaints (documents not ready, waiting looks like a crash) and designed for those first |
| 91% mobile, 40% on phones under ₹10,000 | Reliable and decisive | Mobile-first, system fonts, no images, CSS-only animation |
| 6.2 s load on 4G | Too slow; likely heavy media | Hard budget: no video, no web fonts, page well under the 1.5 MB limit (this prototype is under 100 KB) |
| "Investing feels scary" (65%, n = 40) | Small sample of **existing** users, so it misses the people who left | Used as a hint, not a fact; the plan is to interview people who dropped off |
| "Many" prefer Hindi | No number | Built so Hindi can be added without a redesign, but launch in English |

## Resolving the stakeholder conflicts

| Stakeholder | Asked for | Decision | Why |
|---|---|---|---|
| CEO | Minimal and premium, no cartoons | **Yes to minimal:** one accent colour, lots of space, no clutter | Trust matters most for first-time investors |
| Marketing | Mascot, video, live ticker, 3 pop-ups, referral banner | **Mascot yes, as an abstract seedling ("Ankur") drawn in SVG.** No video, ticker or pop-ups. Referral moves to after the first investment | Pop-ups and a ticker add weight and anxiety; a live ticker of falling prices makes investing feel scarier. A simple geometric seedling satisfies both CEO and marketing |
| Compliance | Risk disclaimer of at least 12 px, visible without scrolling; no "guaranteed", "safe" or "risk-free" | **A 13 px risk bar at the very top of every page** and next to the invest button; copy checked for banned words | Non-negotiable |
| Lead developer | Under 1.5 MB, CSS/Lottie animation under 100 KB, 1 developer, 3 weeks | **Plain HTML/CSS, system fonts, one SVG mascot with a CSS sway animation** (well under 1 KB), reused components | Buildable by one developer in 3 weeks |
| Customer support | Documents not ready; waiting feels like a crash | **"Keep these ready" checklist** on the homepage and in onboarding screen 1; a **step-by-step progress screen** with a time estimate | Directly targets the main known causes of the KYC drop |

## The connected story

1. **Homepage:** "Start investing with ₹100. Learn as you grow." The page promises about 5 minutes and shows the same 3-item checklist that onboarding uses, so expectations match.
2. **Screen 1, before you start:** the same checklist, with a "Remind me later" option instead of failing halfway.
3. **Screen 2, phone OTP:** one decision per screen, SMS auto-fill, large inputs.
4. **Screen 3, PAN:** explains why PAN is needed and how the data is used; only two fields.
5. **Screen 4, verification wait:** real steps (PAN matched ✓ → Aadhaar → account), moving progress, "you can close the app". This fixes "I thought it crashed".
6. **Screen 5, first investment:** a small, reversible amount, with the risk line next to the button.

**Ankur the seedling** appears only at moments of doubt: the hero, before KYC and while waiting. That keeps it meaningful rather than decorative. Its gentle sway stops for users who turn on "reduce motion".

## Accessibility (WCAG AA)

- **Contrast:** text colours were chosen for 7:1 or more (green #0b5d3b on white is 7.9:1, ink #14213d is 15.9:1). The saffron accent only ever sits behind dark text.
- **Touch targets** are at least 44 px; buttons and inputs are 48 px.
- **Text sizes:** body text is 16 px and the disclaimers are 13 px.
- **Other:** labels on every input, live status messages for screen readers on the waiting screen, and support for reduced motion.

## Hindi later, without a redesign

- **Layout:** no text is baked into images, and every container is flexible, because Devanagari text is often longer and taller than English.
- **Fonts:** the font stack already includes Noto Sans Devanagari.
- **Language switch:** the "हिंदी" link sits in the header from day one.

## How we will know it worked

| Metric | Target | Why it matters |
|---|---|---|
| Download → KYC completion | 22% → 35% | The main leak |
| Drop-off at the PAN/Aadhaar step | 62% → under 40% | The step support complaints point to |
| Share of KYC users making a first investment | 33% → 45% | The end goal |
| Mobile load time on 4G | under 2.5 s | Was 6.2 s |

Before trusting these numbers, run a 2-week A/B test **without paid traffic**, and talk to 8–10 people who dropped off.
