# Claude Code Session Guide

## Project Overview

**Project:** Basic Pages — authentication UI templates and e-commerce analytics dashboard

**Purpose:** Reusable, responsive pages built with Tailwind CSS (CDN), Lucide icons, and vanilla JS. No build step — all pages are self-contained and can be opened directly in a browser.

**Repository:** `ngothanhtung/claude-code-basic-pages`

---

## File Structure

```
/
├── login.html      # Sign-in form (email + password + social login)
├── register.html   # Account creation form with multi-field validation
├── charts.html     # E-commerce dashboard (React + Recharts via CDN)
└── CLAUDE.md       # This file
```

---

## Pages

### login.html

Single-page sign-in form. Fields and behavior:

- **Email** — required, regex-validated (`/^[^\s@]+@[^\s@]+\.[^\s@]+$/`)
- **Password** — required, non-empty; toggle visibility button with Lucide `eye`/`eye-off`
- **Remember me** — optional checkbox
- **Forgot password?** — placeholder `<a>` link
- Social login buttons (Google, GitHub, Facebook) — inline SVGs, not Lucide
- Navigation link → `register.html`

### register.html

Multi-field account creation form. Required fields marked with `*` in the label:

| Field | Required | Validation |
|---|---|---|
| Full Name | ✅ | Non-empty |
| Email Address | — | Valid format if filled |
| Phone Number | — | None |
| Gender | — | Radio: Male / Female / Other |
| Address | — | None (textarea) |
| Password | ✅ | Non-empty |
| Confirm Password | ✅ | Must match Password |
| Terms of Service | ✅ | Checkbox must be checked |

- Social login buttons (Google, GitHub, Facebook)
- Navigation link → `login.html`

### charts.html

E-commerce analytics dashboard. Rendered with React 18 + Recharts via CDN; uses Babel standalone for JSX.

Layout sections:
- **Header** — `<h1>` (`font-heading font-extrabold`) + subtitle with year/period
- **KPI Cards** — `grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6`, each a `Card` component
- **Chart sections** — `ResponsiveContainer` inside surface cards; mixed `AreaChart`, `BarChart`, `LineChart`, `PieChart`
- **Tables** — Marketing channels + Top products with `hover:bg-surface-2/50` rows
- **Customer segments** — `grid grid-cols-2 lg:grid-cols-4` cards with color badges

---

## Tech Stack

### Auth pages (login.html, register.html)
- Tailwind CSS via CDN — configured inline per page
- Lucide icons via CDN (`https://unpkg.com/lucide@latest`)
- Google Fonts (Poppins + Inter)
- Vanilla JavaScript — no framework

### Dashboard (charts.html)
- React 18 via CDN
- Recharts `2.15.0` via CDN (`https://cdn.jsdelivr.net/npm/recharts@2.15.0/umd/Recharts.min.js`)
- Babel standalone for JSX (`type="text/babel"` on script tags)
- Lucide `dist/umd/lucide.min.js` variant
- Google Fonts (Be Vietnam Pro + Inter)
- `tailwind.config` declared in `<script>` tag in `<head>` (not a file)

---

## Design System

### Color Tokens

All colors are registered in `tailwind.config.theme.extend.colors`. Always use these tokens, never raw hex values.

| Token | Hex | Use |
|---|---|---|
| `bg` | `#090A14` | Page background (`class="bg-bg"`) |
| `primary` | `#DF6B33` | CTA buttons, links, accent |
| `primary-hover` | `#C45C2A` | Hover state for primary |
| `surface` | `#12141F` | Card background |
| `surface-2` | `#1A1D2E` | Input fields, inner surfaces |
| `border-subtle` | `#23263A` | Borders |
| `text-secondary` | `#8B8FA8` | Labels, placeholders, secondary text |

Chart-only accent colors (raw hex, no token): `#4F8EF7` (blue), `#10B981` (green), `#F59E0B` (amber).

### Typography

| Token | Font | Weights | Use |
|---|---|---|---|
| `font-heading` | `Poppins` | 700, 800 | Headings in auth pages |
| `font-heading` | `Be Vietnam Pro` | 700, 800 | Headings in charts.html (Vietnamese support) |
| `font-body` | `Inter` | 400, 500 | All body text and UI labels |

> When adding a page with Vietnamese text in headings, use `Be Vietnam Pro` for `font-heading`. For English-only pages, `Poppins` is acceptable.

Google Fonts import for auth pages:
```html
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@700;800&family=Inter:wght@400;500&display=swap" rel="stylesheet" />
```

Google Fonts import for charts/Vietnamese pages:
```html
<link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@700;800&family=Inter:wght@400;500&display=swap" rel="stylesheet" />
```

### Tailwind Config Template

Paste this `<script>` block in `<head>` before the Tailwind CDN tag:

```html
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          bg: '#090A14',
          primary: '#DF6B33',
          'primary-hover': '#C45C2A',
          surface: '#12141F',
          'surface-2': '#1A1D2E',
          'border-subtle': '#23263A',
          'text-secondary': '#8B8FA8',
        },
        fontFamily: {
          heading: ['Be Vietnam Pro', 'sans-serif'], // or Poppins for English-only
          body: ['Inter', 'sans-serif'],
        },
      },
    },
  };
</script>
```

---

## HTML Patterns

### Page Layout (auth pages)

> **Important:** The page background is set via `body { background-color: #090A14; }` in the `<style>` block — NOT via a `bg-bg` class on `<body>`.

```html
<!-- Required <style> block in <head> (auth pages) -->
<style>
  body { background-color: #090A14; }
  .input-icon { color: #8B8FA8; }
  .input-field:focus ~ .input-icon { color: #DF6B33; }
  .social-btn:hover { border-color: #DF6B33; }
  .divider-line { background-color: #23263A; }
</style>

<!-- login.html body tag -->
<body class="min-h-screen flex items-center justify-center px-4 font-body text-white">

<!-- register.html body tag (adds py-10 for taller scrollable page) -->
<body class="min-h-screen flex items-center justify-center px-4 py-10 font-body text-white">

<div class="w-full max-w-md">
  <!-- Brand icon -->
  <div class="text-center mb-10">
    <div class="inline-flex items-center justify-center w-14 h-14 rounded-2xl bg-surface border border-border-subtle mb-4">
      <i data-lucide="layout-dashboard" class="w-7 h-7 text-primary"></i>
    </div>
    <h1 class="font-heading font-extrabold text-3xl tracking-tight">Page Title</h1>
    <p class="text-text-secondary mt-2 text-sm">Subtitle text</p>
  </div>

  <!-- Card -->
  <div class="bg-surface border border-border-subtle rounded-2xl p-8 shadow-2xl shadow-black/50">
    <!-- Form content -->
  </div>

  <!-- Navigation link -->
  <p class="text-center mt-8 text-sm text-text-secondary">
    Text <a href="other.html" class="text-primary hover:text-primary-hover transition-colors duration-200 font-medium">Link</a>
  </p>
</div>
```

### Input Field

Every input field follows this exact structure:

```html
<div class="mb-5">
  <label class="block text-sm font-medium mb-2 text-text-secondary" for="fieldId">
    Label Text <span class="text-primary">*</span>  <!-- * only for required -->
  </label>
  <div class="relative">
    <input
      id="fieldId"
      type="text"
      placeholder="Placeholder text"
      class="input-field w-full bg-surface-2 border border-border-subtle rounded-xl px-4 py-3 pl-11 text-sm placeholder-text-secondary focus:outline-none focus:border-primary transition-colors duration-200"
    />
    <i data-lucide="icon-name" class="input-icon absolute left-3.5 top-1/2 -translate-y-1/2 w-4 h-4 transition-colors duration-200"></i>
  </div>
  <p id="fieldIdError" class="hidden text-xs text-red-400 mt-1.5">Error message here.</p>
</div>
```

The CSS that drives icon focus color (must be in `<style>` block):

```css
.input-icon { color: #8B8FA8; }
.input-field:focus ~ .input-icon { color: #DF6B33; }
```

### Primary Button

```html
<button type="submit" class="w-full bg-primary hover:bg-primary-hover text-white font-heading font-bold text-base py-3 rounded-xl transition-all duration-200 active:scale-[0.98] cursor-pointer">
  Button Label
</button>
```

### Social Login Buttons

```html
<!-- Divider — flex layout, NOT absolute positioning -->
<div class="flex items-center gap-3 my-8">
  <div class="flex-1 h-px divider-line"></div>
  <span class="text-text-secondary text-xs uppercase tracking-widest">or continue with</span>
  <div class="flex-1 h-px divider-line"></div>
</div>

<!-- Grid of 3 buttons — inline SVGs, NOT Lucide icons -->
<div class="grid grid-cols-3 gap-3">
  <button class="social-btn flex items-center justify-center gap-2 bg-surface-2 border border-border-subtle rounded-xl py-3 px-2 hover:bg-opacity-80 transition-all duration-200 cursor-pointer">
    <svg class="w-5 h-5" viewBox="0 0 24 24"><!-- Google paths with fill="#fff" --></svg>
    <span class="text-xs font-medium hidden sm:inline">Google</span>
  </button>
  <!-- repeat for GitHub (path fill="#fff"), Facebook (path fill="#fff") -->
</div>
```

The `.social-btn:hover` and `.divider-line` styles are defined in the `<style>` block (see Page Layout above). Label text color is inherited from `text-white` on `<body>` — not `text-text-secondary`.

### Card Component (charts.html)

```html
<div class="bg-surface rounded-2xl p-5 border border-border-subtle">
  <!-- content -->
</div>
```

### Responsive Table (charts.html)

```html
<div class="overflow-x-auto">
  <table class="w-full text-sm font-body">
    <thead>
      <tr class="border-b border-border-subtle text-text-secondary text-xs uppercase tracking-wide">
        <th class="text-left py-3 px-3">Column</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-b border-border-subtle/50 hover:bg-surface-2/50 transition-colors">
        <td class="py-3 px-3">Value</td>
      </tr>
    </tbody>
  </table>
</div>
```

---

## JavaScript Patterns

### Lucide Icons

```html
<!-- CDN (auth pages) -->
<script src="https://unpkg.com/lucide@latest"></script>

<!-- CDN (charts.html uses UMD variant) -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
```

Initialize once at the end of `<body>`:
```javascript
lucide.createIcons();
```

When changing an icon dynamically, call `createIcons()` again:
```javascript
element.setAttribute('data-lucide', 'eye-off');
lucide.createIcons();
```

### Password Visibility Toggle

```javascript
function setupToggle(toggleBtn, inputEl, iconEl) {
  toggleBtn.addEventListener('click', () => {
    const isPassword = inputEl.type === 'password';
    inputEl.type = isPassword ? 'text' : 'password';
    iconEl.setAttribute('data-lucide', isPassword ? 'eye-off' : 'eye');
    lucide.createIcons();
  });
}
```

### Form Validation (auth pages)

```javascript
// Error state helper
function setError(input, errorEl, show) {
  if (show) {
    errorEl.classList.remove('hidden');
    input.classList.add('border-red-400');
  } else {
    errorEl.classList.add('hidden');
    input.classList.remove('border-red-400');
  }
}

const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

form.addEventListener('submit', (e) => {
  e.preventDefault();
  let valid = true;

  // Required field
  if (!nameInput.value.trim()) {
    setError(nameInput, nameError, true);
    valid = false;
  } else {
    setError(nameInput, nameError, false);
  }

  // Optional email with format check
  const emailVal = emailInput.value.trim();
  if (emailVal && !emailRegex.test(emailVal)) {
    setError(emailInput, emailError, true);
    valid = false;
  } else {
    setError(emailInput, emailError, false);
  }

  if (valid) {
    console.log('Form submitted:', { /* collect values */ });
  }
});

// Clear error on re-input
nameInput.addEventListener('input', () => setError(nameInput, nameError, false));
```

### React Component Patterns (charts.html)

```javascript
// Reusable KPI Card
const Card = ({ title, value, sub, icon, color = 'text-primary' }) => (
  <div className="bg-surface rounded-2xl p-5 border border-border-subtle">
    <div className="flex items-start justify-between mb-3">
      <p className="text-text-secondary text-xs font-medium uppercase tracking-wide">{title}</p>
      <span className={`text-lg ${color}`}>{icon}</span>
    </div>
    <p className="text-2xl font-heading font-bold">{value}</p>
    {sub && <p className="text-text-secondary text-xs mt-1">{sub}</p>}
  </div>
);

// Section heading
const SectionTitle = ({ children }) => (
  <h2 className="text-lg font-heading font-bold text-gray-100 mb-4">{children}</h2>
);

// Custom tooltip
const CustomTooltip = ({ active, payload, label, formatter }) => {
  if (!active || !payload?.length) return null;
  return (
    <div className="bg-surface-2 border border-border-subtle rounded-lg p-3 text-sm">
      <p className="text-text-secondary mb-1">{label}</p>
      {payload.map((p, i) => (
        <p key={i} style={{ color: p.color }}>
          {p.name}: {formatter ? formatter(p.value) : p.value}
        </p>
      ))}
    </div>
  );
};
```

### Formatting Helpers (charts.html)

```javascript
const formatVND = (n) => {
  if (n >= 1e9) return (n / 1e9).toFixed(1) + ' tỷ';
  if (n >= 1e6) return (n / 1e6).toFixed(0) + ' tr';
  return n.toLocaleString('vi-VN') + ' đ';
};

const formatNum = (n) => n.toLocaleString('vi-VN');
```

---

## Recharts Conventions (charts.html)

- Wrap every chart in `<ResponsiveContainer width="100%" height={N}>`.
- Use `SectionTitle` for all section headings.
- Axis ticks: `tick={{ fill: '#8B8FA8', fontSize: 12 }}`, `axisLine={false}`, `tickLine={false}`.
- Legend: `wrapperStyle={{ color: '#8B8FA8', fontSize: 12 }}`.
- Gradient fills: define `<linearGradient>` in `<defs>` inside the chart.
- Chart accent colors (in order): `#DF6B33` (orange/primary), `#4F8EF7` (blue), `#10B981` (green), `#F59E0B` (amber).

---

## Design Rules for New Pages

1. **Theme consistency** — Use only the defined color tokens. Do not introduce raw hex values or new colors without adding them to the config.

2. **Responsive baseline** — `min-h-screen`, `w-full max-w-md`, `px-4`. For dashboards use `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`.

3. **Icons** — Lucide via CDN, initialized with `lucide.createIcons()` at end of `<body>`. Social buttons use inline SVGs only.

4. **Input constraints** — Required fields get `*` in label (red `text-primary`). Errors hidden by default; shown on submit failure; cleared on re-input. Error styling: `border-red-400` + visible error `<p>`.

5. **Navigation links** — Every auth page links to its counterpart. Login → `register.html`. Register → `login.html`.

6. **Form behavior** — `e.preventDefault()` on submit, client-side validation, `console.log` form data on success.

7. **Accessibility** — Every `<input>` paired with a `<label for="id">`. Placeholders are descriptive. Error `<p>` can use `aria-describedby` on the input.

8. **Buttons** — Always include `active:scale-[0.98]` for press feedback and `transition-all duration-200` for smoothness.

9. **No build step** — All pages must work by opening the HTML file directly. Keep all config and scripts inline or CDN-sourced.

---

## CDN Reference

```html
<!-- Tailwind CSS -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Lucide icons (auth pages) -->
<script src="https://unpkg.com/lucide@latest"></script>

<!-- Lucide icons (charts.html — UMD variant) -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>

<!-- React 18 (charts.html only) -->
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

<!-- PropTypes (charts.html only — required by Recharts) -->
<script src="https://unpkg.com/prop-types@15.8.1/prop-types.min.js"></script>

<!-- Recharts (charts.html only) -->
<script src="https://cdn.jsdelivr.net/npm/recharts@2.15.0/umd/Recharts.min.js"></script>

<!-- Babel standalone for JSX (charts.html only — load after React + Recharts) -->
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```
