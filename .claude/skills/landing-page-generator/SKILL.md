---
name: landing-page-generator
description: Xây dựng Landing Page hoàn chỉnh cho mọi ngành nghề với cấu trúc 10 sections chuẩn đổi mới (Navigation, Hero, Problem, Solution, Target Audience, Details, Social Proof, CTA, FAQ, Footer). Hỗ trợ tuỳ chỉnh hoàn toàn về màu sắc, font, theme (dark/light), và design system theo yêu cầu cụ thể.
---

## Ngữ cảnh dự án

Dự án sử dụng:

- **Công nghệ cốt lõi**:
  - **HTML5 Semantic** cho cấu trúc (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`).
  - **Tailwind CSS** qua CDN (https://cdn.tailwindcss.com) để tùy biến giao diện và bố cục nhanh chóng.
  - **JavaScript thuần** (Vanilla JS) cho menu mobile, form validation, smooth scroll, animations, và IntersectionObserver.
  - **Lucide Icons** (CDN: https://unpkg.com/lucide@latest) cho hệ thống biểu tượng.
  - **Google Fonts** cho font chất lượng cao.
- **Mục tiêu**: Xây dựng Landing Page chuẩn chuyên nghiệp, tỷ lệ chuyển đổi cao, áp dụng cho mọi ngành nghề và lĩnh vực kinh doanh.
- **Thiết kế**: Hiện đại, mượt mà, responsive (mobile → desktop), tối ưu SEO và accessibility (Lighthouse score > 90).

---

## Quy trình bắt buộc — Xác định tham số (MANDATORY)

**QUAN TRỌNG:** Mỗi lần chạy skill, nếu người dùng **không cung cấp đủ** các tham số bên dưới, **PHẢI hỏi họ** trước khi bắt đầu code. Không tự suy luận giá trị mặc định khi người dùng chưa nói rõ.

### Bắt buộc hỏi (nếu thiếu)

| Tham số                 | Hỏi như thế nào                                                                                |
| ----------------------- | ---------------------------------------------------------------------------------------------- |
| **Chủ đề / Ngành nghề** | "Chủ đề / ngành nghề của landing page là gì? (VD: Spa, Nhà hàng, SaaS, Khóa học, Cửa hàng...)" |
| **Tông màu chính**      | "Bạn muốn tông màu chính là gì? (VD: tím, xanh dương, cam, xanh lá, đỏ...)"                    |
| **Theme**               | "Giao diện bạn muốn là **Dark** hay **Light**?"                                                |

### Các tham số TUỲ CHỌN (nếu không nêu → dùng gợi ý bên dưới)

| Tham số                      | Mặc định nếu không nói                              |
| ---------------------------- | --------------------------------------------------- |
| **Primary Color (hex)**      | `#9333EA` (tím) — chuyển từ tên màu sang hex        |
| **Secondary / Accent Color** | Tự chọn bổ sung cho đa dạng, hoặc bỏ qua            |
| **Brand Name**               | Tạo tên giả phù hợp ngành: "BrandX", "Zenith", v.v. |
| **CTA Text**                 | "Đăng Ký Ngay" hoặc tương đương ngành               |
| **Contact Phone**            | Số giả: "0xxx.xxx.xxx"                              |
| **Content tuỳ chỉnh**        | Tự tạo nội dung phù hợp ngành                       |

### Luồng xử lý khi chạy skill

```
1. Nhận yêu cầu từ người dùng
2. Kiểm tra: Đủ 3 tham số bắt buộc chưa?
   ├─ ĐỦ → Tiến hành xây dựng (bước 3)
   └─ THIẾU → Dùng AskUserQuestion hỏi từng tham số còn thiếu
3. Chuyển tên màu → hex code (VD: "tím" → "#9333EA")
4. Xây dựng landing page theo 10 sections
5. Xuất file index.html
```

---

### Gợi ý chuyển màu thông dụng

| Tên màu           | Hex       |
| ----------------- | --------- |
| Tím / Violet      | `#9333EA` |
| Xanh dương / Blue | `#3B82F6` |
| Cam / Orange      | `#F97316` |
| Xanh lá / Green   | `#10B981` |
| Đỏ / Red          | `#EF4444` |
| Hồng / Pink       | `#EC4899` |
| Vàng / Yellow     | `#F59E0B` |
| Teal              | `#14B8A6` |

---

## Cấu trúc Landing Page (10 Sections)

Mỗi section có mục đích riêng: dẫn khách hàng từ **nhận biết → quan tâm → quyết định mua**.

1. **Navigation** — Menu chính sticky, logo, CTA button, hamburger mobile
2. **Hero** — Tiêu đề thu hút, subtitle, 2 CTA buttons, stats bar, visual
3. **Problem** — 3-4 pain points (cards: icon + title + desc)
4. **Solution** — 4-6 features giới thiệu dịch vụ/sản phẩm
5. **Target Audience** — 2-4 nhóm đối tượng phù hợp
6. **Details** — Chi tiết chương trình / dịch vụ (timeline hoặc grid)
7. **Social Proof** — Testimonials, stats, bằng chứng xã hội
8. **CTA** — Form đăng ký/liên hệ + hotline nổi bật
9. **FAQ** — Accordion 6-8 câu hỏi (`<details>` + `<summary>`)
10. **Footer** — Brand, contact, social links, newsletter, copyright

---

## Design System — Linh hoạt theo tham số

### CSS Variables (động, dựa trên tham số đầu vào)

```css
:root {
  --bg-primary: #090a14; /* Nền trang chính (dark) / #ffffff (light) */
  --bg-secondary: #13141f; /* Nền card (dark) / #f5f5f7 (light) */
  --bg-tertiary: #1a1d2e; /* Input, inner surfaces (dark) / #eeeeee (light) */
  --border-subtle: #23263a; /* Border (dark) / #e5e5e5 (light) */
  --text-primary: #ffffff; /* Text chính (dark) / #090a14 (light) */
  --text-secondary: #a0a0b0; /* Text phụ (dark) / #666666 (light) */
  --primary: #9333ea; /* Màu chủ đạo — THAY ĐỔI THEO USER */
  --primary-hover: #7c22d9; /* Hover state */
  --accent: #f472b6; /* Màu phụ — THAY ĐỔI THEO USER */
}
```

### Typography

- **Headings**: Plus Jakarta Sans (weight 700-800)
- **Body / UI**: Inter (weight 400-500)
- Font Sizes: H1 48/32px, H2 36/24px, H3 28/20px, Body 16/14px

### Spacing & Layout

- Section padding: Desktop 80px top/bottom, Mobile 48px top/bottom
- Container: max-width 1200px, `mx-auto`
- Grid: 3-4 cols (desktop), 2 cols (tablet), 1 col (mobile)

### Responsive Breakpoints

- Mobile: < 768px
- Tablet: 768px–1024px
- Desktop: > 1024px

---

## Content Structure — Từng Section

### Section 1: Navigation

- Sticky, backdrop blur, z-50
- Logo (brand name, gradient text với primary color)
- Menu links (desktop): 4-5 items, `text-sm`
- CTA button (phải): primary color
- Hamburger + mobile menu slide-in (JS toggle)

### Section 2: Hero

- 2 cột (desktop) / 1 cột (mobile)
- Badge trên: "Ưu đãi", "Khai giảng", "Top đánh giá"...
- H1 gradient text (primary → accent)
- Subtitle: 2-3 dòng mô tả giá trị
- 2 buttons: Primary CTA + Secondary (outline hoặc "Xem thêm")
- Right: Visual placeholder với gradient bg + Lucide icon + glow effect
- Stats bar: 3-4 items (số to primary color + label)
- Fade-in animation (IntersectionObserver)

### Section 3: Problem Statement

- Header: H2 + subtitle
- Grid: 2x2 (desktop) / 1 col (mobile)
- Cards: Lucide icon (40px, màu riêng) + H3 + description
- Hover: border → primary, translateY(-4px), transition 300ms

### Section 4: Solution

- Header: H2 + subtitle
- Grid: 3 cols (desktop) / 1 col (mobile)
- Cards: icon (32px) + title + description + tags
- 4-6 feature cards tùy ngành

### Section 5: Target Audience

- Header: H2
- Grid: 2x2 (desktop) / 1 col (mobile)
- Cards: icon + title + description + badge "Phù hợp"
- 2-4 nhóm đối tượng phù hợp ngành

### Section 6: Details

- Header: H2 + subtitle
- **Timeline 1 bên** (recommended): số bên trái, card bên phải, đường kẻ dọc gradient nối các nodes
- Hoặc grid cards cho nội dung ngắn
- Mỗi step: số thứ tự + title + duration badge + description

### Section 7: Social Proof

- Header: H2
- Testimonials: 3 cards (avatar initials + quote + stars)
- Stats row: 3-4 con số nổi bật (primary color, to)
- Optional: quote lớn ở giữa, logo clients

### Section 8: CTA

- Header: H2 + subtitle khuyến khích
- Form (max-width 500px, centered):
  - Họ và tên (required)
  - Email (required, regex validation)
  - Số điện thoại (optional)
  - Nút submit (primary, full-width)
  - Form validation → error messages → toast on success
- Divider "hoặc"
- Secondary CTA: outline button + hotline lớn (gradient text)

### Section 9: FAQ

- Header: H2
- `<details>` + `<summary>` (native, không cần JS)
- 6-8 Q&A pairs
- Chevron icon rotate 180° khi mở (CSS)
- Content: `mt-4 text-text-secondary line-height: 1.8`

### Section 10: Footer

- Background: `#050610` (dark) / `#f0f0f0` (light)
- Grid 4 cột (desktop) / 1 cột (mobile):
  1. Brand: logo + tagline
  2. Contact: địa chỉ, phone, email, giờ mở cửa
  3. Quick links: các trang/phần quan trọng
  4. Newsletter: input email + button
- Divider + copyright căn giữa

---

## JavaScript Requirements

1. **Mobile Menu Toggle** — `[data-hamburger]` + `[data-mobile-menu]`, class toggle
2. **Smooth Scroll** — `html { scroll-behavior: smooth; }` + anchor links
3. **Form Validation** — required fields, email regex, phone regex, error display
4. **Form Submit** — `e.preventDefault()`, validate, show toast, reset form
5. **Navbar Scroll** — `window.scrollY > 50` → toggle class `scrolled`
6. **Stats Counter** — IntersectionObserver + setInterval từ 0 → target
7. **Scroll Reveal** — IntersectionObserver + class `visible` cho `.reveal`
8. **Lucide Icons** — `lucide.createIcons()` cuối `<body>`

---

## Images and Assets

1. Get image from Unsplash site or use placeholder (https://via.placeholder.com) based on industry keywords (e.g., "spa", "restaurant", "technology", "education").

## Animations & Effects

- Using **animate.stylehttps://animate.style/**
- **Buttons**: `transition duration-300 hover:scale-95 hover:shadow-lg`
- **Cards**: `transition duration-300 hover:border-primary hover:-translate-y-1`
- **Gradient Text**: `linear-gradient(primary → accent)` → `-webkit-background-clip: text`
- **Glow**: `box-shadow: 0 0 80px rgba(primary, 0.3)`
- **FadeInUp**: `@keyframes fadeInUp { from { opacity:0; transform:translateY(30px) } to { opacity:1; transform:translateY(0) } }`
- **FAQ Chevron**: `details[open] .faq-chevron { transform: rotate(180deg); }`
- **Navbar**: `background: rgba(bg, 0.7)` → `rgba(bg, 0.95)` khi scroll

---

## Meta Tags & SEO

```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>{Brand} — {Tagline}</title>
<meta name="description" content="{Mô tả dưới 160 ký tự}" />
<meta name="theme-color" content="{primary color}" />
<meta property="og:title" content="..." />
<meta property="og:description" content="..." />
<link rel="canonical" href="..." />
```

---

## Output Requirements

- ✅ File: `index.html` duy nhất (all-in-one)
- ✅ CSS: Inline `<style>`, Tailwind utilities + CSS Variables
- ✅ JavaScript: Inline `<script>` cuối `<body>`
- ✅ Assets: CDN (Tailwind, Lucide, Google Fonts)
- ✅ Hoạt động: Mở trực tiếp trên trình duyệt, không cần server
- ✅ Responsive: Mobile-first, test 768px / 1024px / 1280px
- ✅ Performance: Lighthouse > 90, Accessibility > 95
- ✅ SEO: title 50-60 chars, meta description < 160 chars
- ✅ Accessibility: semantic HTML, contrast > 4.5:1, ARIA labels

---

## Presets gợi ý (không bắt buộc)

### Preset: Spa / Thẩm mỹ

- Primary: `#9333EA` (tím), Accent: `#F472B6` (hồng)
- Problem: mụn, nám, da khô, lão hóa
- Solution: trị mục laser, cấy ẩm, pico, massage
- Details: timeline 8 bước liệu trình
- CTA: "Đặt Lịch Tư Vấn Miễn Phí"

### Preset: Nhà hàng / F&B

- Primary: `#F97316` (cam), Accent: `#EF4444` (đỏ)
- Problem: chất lượng không ổn định, vệ sinh, thực đơn nhàm chán
- Solution: nguyên liệu tươi, đầu bếp chuyên nghiệp, không gian
- Details: thực đơn đặc trưng, quy trình chế biến
- CTA: "Đặt Bàn Ngay"

### Preset: SaaS / Công nghệ

- Primary: `#3B82F6` (xanh dương), Accent: `#14B8A6` (teal)
- Problem: công cụ phức tạp, chi phí cao, tích hợp khó
- Solution: giao diện đơn giản, tiết kiệm chi phí, API mạnh
- Details: tính năng chính, pricing tiers
- CTA: "Dùng Thử Miễn Phí"

### Preset: Khóa học / Giáo dục

- Primary: `#10B981` (xanh lá), Accent: `#F59E0B` (vàng)
- Problem: học lý thuyết nhàm chán, không có dự án thực tế, kém thực hành
- Solution: học qua dự án, mentor 1-1, cam kết kết quả
- Details: timeline buổi học, syllabus
- CTA: "Đăng Ký Ngay"

---

## Lời khuyên & Best Practices

1. **Copywriting**: Viết từ góc độ khách hàng (benefits-driven)
2. **Color Contrast**: Đảm bảo text vs background đủ contrast (> 4.5:1 WCAG AA)
3. **CTA Buttons**: Luôn có CTA visible ở mọi section (ít nhất 2-3 buttons)
4. **Mobile-first**: Thiết kế mobile trước
5. **Form đơn giản**: 3-5 fields tối đa để tăng conversion
6. **Trust Signals**: Hiển thị reviews, testimonials, stats, badges
7. **Visual Hierarchy**: Heading phân cấp rõ, guide mắt từ trên xuống
8. **Content tuỳ ngành**: Nội dung mỗi section phải phù hợp với ngành nghề cụ thể

---

## FAQ (Về Skill này)

**Q: Tôi có thể dùng framework (React, Vue) không?**
A: Skill này tập trung vanilla HTML/CSS/JS để đơn giản deployment. Nếu cần framework, yêu cầu skill riêng cho React/Next.js.

**Q: Làm sao để sửa nội dung sau khi tạo?**
A: `index.html` là one-file, dễ edit trực tiếp trong code editor.

**Q: Host ở đâu?**
A: Vercel, Netlify, GitHub Pages, AWS S3, Heroku, hoặc shared hosting.

**Q: Performance?**
A: Mục tiêu Lighthouse Performance > 90. Optimize bằng image compression, minify CSS/JS.

---

## Resources

- **Tailwind CSS**: https://tailwindcss.com/docs
- **Lucide Icons**: https://lucide.dev/
- **Google Fonts**: https://fonts.google.com/
- **Lighthouse**: https://developers.google.com/web/tools/lighthouse
- **WCAG 2.1**: https://www.w3.org/WAI/WCAG21/quickref/
- **Color Picker**: https://webaim.org/resources/contrastchecker/
