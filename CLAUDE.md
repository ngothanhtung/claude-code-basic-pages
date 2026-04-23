# Claude Code Session Guide

## Project Overview

**Project:** Basic Pages — login and registration UI templates

**Purpose:** Reusable, responsive authentication pages built with Tailwind CSS and Lucide icons

## Pages

### charts.html

E-Commerce report dashboard with charts. Structure:

- **Header** — `<h1>` with `font-heading font-extrabold`, subtitle with year/period
- **KPI Cards** — `grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6`, each card uses a `Card` component (`bg-surface rounded-2xl p-5 border border-border-subtle`)
- **Chart sections** — `ResponsiveContainer` from Recharts inside `bg-surface rounded-2xl p-5` cards
- **Tables** — `w-full text-sm font-body`, `thead` with `uppercase tracking-wide`, `tbody` rows with hover state (`hover:bg-surface-2/50`)
- **Customer segments** — `grid grid-cols-2 lg:grid-cols-4` cards with border/color badges

Data helpers: `formatVND(n)` returns VND string (e.g. "5.6 tỷ"), `formatNum(n)` returns `toLocaleString('vi-VN')`.

### login.html

- Single-page sign-in form with email + password
- "Remember me" checkbox, "Forgot password?" link
- Social login buttons (Google, GitHub, Facebook)
- Navigation link to register page

### register.html

Account creation form with fields (required marked with `*`):

- **Full Name** — `*` text, non-empty validation
- **Email Address** — no, email, valid format if filled
- **Phone Number** — no, tel
- **Gender** — no, radio (Male / Female / Other)
- **Address** — no, textarea
- **Password** — `*` password, non-empty
- **Confirm Password** — `*` password, must match
- **Terms of Service** — `*` checkbox, must be checked

- Social login buttons (Google, GitHub, Facebook)
- Navigation link back to login page

## Design System

### Color Theme

- `bg` / `#090A14` — Page background
- `primary` / `#DF6B33` — CTA buttons, links, accent
- `primary-hover` / `#C45C2A` — Hover state for primary
- `surface` / `#12141F` — Card background
- `surface-2` / `#1A1D2E` — Input fields, inner surfaces
- `border-subtle` / `#23263A` — Borders
- `text-secondary` / `#8B8FA8` — Labels, placeholders, secondary text

### Typography

- **Headings** — `Be Vietnam Pro`, weights 700 and 800 *(chosen for full Vietnamese character support)*
- **Body / UI** — `Inter`, weights 400 and 500

Google Fonts import:

```html
<link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@700;800&family=Inter:wght@400;500&display=swap" rel="stylesheet" />
```

> **Note:** Use `Be Vietnam Pro` for any heading text that may contain Vietnamese characters. Fall back to `Poppins` for English-only headings only if strictly necessary.

### Tailwind Config

All colors and fonts are registered in `tailwind.config.theme.extend`. Always reference these tokens instead of raw hex values so pages stay consistent.

## Design Rules for Future Pages

1. **Theme consistency** — Inherit the color palette and font family from the config above. Do not introduce new colors or typefaces without updating this file.

2. **Responsive** — Use `min-h-screen`, `w-full max-w-md`, and `px-4` as baseline. Test on mobile and desktop.

3. **Icons** — Use [Lucide](https://lucide.dev/) via CDN. Initialize with `lucide.createIcons()` at the end of `<body>`.

4. **Input constraints** — Required fields marked with `*` in the label. Inline validation errors below each field (hidden by default, shown on failure). Clear error styling (`border-red-400` + error text) when invalid.

5. **Navigation links** — Every auth page must link to its counterpart:
   - Login page → "Create account" → `register.html`
   - Register page → "Sign in" → `login.html`

6. **Form behavior** — `e.preventDefault()` on submit, validate client-side, log form data on success.

7. **Accessibility** — Every `<input>` has a `<label>`, placeholder text is descriptive, error messages are announced via `aria-describedby` (optional but recommended).

## Recharts Conventions (charts.html)

- Always wrap charts in `<ResponsiveContainer width="100%" height={N}>` for responsiveness.
- Use `SectionTitle` component for all section headings: `<SectionTitle>Tiêu đề</SectionTitle>`.
- Custom tooltips: define a `CustomTooltip` component with `bg-surface-2 border border-border-subtle rounded-lg`.
- Chart colors: use project color tokens (`#DF6B33`, `#4F8EF7`, `#10B981`, `#F59E0B`) consistently.
- Gradient fills: use `<linearGradient>` in `<defs>` inside AreaChart.
- Axis ticks: `tick={{ fill: '#8B8FA8', fontSize: 12 }}` with `axisLine={false} tickLine={false}`.
- Legend: `wrapperStyle={{ color: '#8B8FA8', fontSize: 12 }}` for dark-theme consistency.

## Tech Stack

- Tailwind CSS via CDN
- Lucide icons via CDN
- Google Fonts (Be Vietnam Pro + Inter)
- Vanilla JS (no framework)

## charts.html Stack

- Recharts via CDN (`https://cdn.jsdelivr.net/npm/recharts@2.15.0/umd/Recharts.min.js`)
- React 18 via CDN
- Babel standalone for JSX (`type="text/babel"` on script tags)
- `tailwind.config` declared in a `<script>` tag before use (not in a separate JS file)
