---
name: landing-page-generator
description: Xây dựng Landing Page hoàn chỉnh với cấu trúc 10 sections chuẩn đổi mới (Hero, Problem, Solution, Benefits, Content, Social Proof, Pricing, CTA, FAQ, Footer) với tuỳ chọn chủ đề, primary color và theme (dark/light).
---

## Ngữ cảnh dự án

Dự án sử dụng:

- **Công nghệ cốt lõi**:
  - **HTML thuần** cho cấu trúc ngữ nghĩa (Semantic).
  - **CSS thuần** (kết hợp với **Tailwind CSS** qua CDN hoặc build step) để linh hoạt tùy chỉnh giao diện và bố cục.
  - **JavaScript thuần** (Vanilla JS) để xử lý logic, sự kiện và tương tác cơ bản.
  - **Lucide Icons** cho hệ thống biểu tượng (icons) sắc nét và nhất quán.
  - **Animate.css** (https://animate.style/) cho các hiệu ứng chuyển động có sẵn.
- **Mục tiêu**: Xây dựng một Landing Page chuẩn, tập trung vào chuyển đổi (conversion rate) với nội dung được tối ưu cho các chủ đề khác nhau (Khóa Học, Thẩm Mỹ Viện, ...).
- **Thiết kế**: Đảm bảo Landing Page trông hiện đại, mượt mà, hỗ trợ Responsive và chuẩn SEO.

### Cấu trúc Landing Page

Một Landing Page hoàn chỉnh sẽ được tạo thành từ 10 sections theo trình tự sau:

1. **Hero Section** - Phần chào mừng đầu tiên, chứa tiêu đề thu hút, phụ đề mô tả giá trị, và nút Call-to-Action (CTA) chính.
2. **Problem Statement** - Phát biểu vấn đề, đánh vào nỗi đau (pain points) của khách hàng.
3. **Solution Section** - Giới thiệu giải pháp (khóa học, dịch vụ), cách giải quyết vấn đề.
4. **Benefits Section** - Lợi ích cụ thể mà khách hàng nhận được khi sử dụng giải pháp.
5. **Course Content / Service Details** - Chi tiết chương trình học, hoặc các bước dịch vụ.
6. **Social Proof** - Bằng chứng xã hội, bao gồm các con số thống kê (stats), logo đối tác, và đánh giá từ khách hàng (testimonials).
7. **Pricing** - Bảng giá các gói sản phẩm/dịch vụ (tuỳ chọn, có thể có 1-3 gói).
8. **CTA Section** - Phần chốt sale cuối trang với các nút hành động mạnh mẽ.
9. **FAQ** - Câu hỏi thường gặp, giải đáp các thắc mắc phổ biến để giảm rào cản mua hàng.
10. **Footer** - Phần chân trang chứa thông tin liên hệ, links, bản quyền, chính sách bảo mật.

## Tham số đầu vào (Params)

Khi sử dụng skill này, người dùng cần cung cấp các tham số sau (nếu không cung cấp, Claude sẽ hỏi lại hoặc sử dụng mặc định):

1. **Chủ đề**: Lĩnh vực kinh doanh (Ví dụ: Khóa Học Tiếng Anh, Thẩm Mỹ Viện, Phần Mềm SaaS, ...). Nội dung văn bản (copywriting) và hình ảnh placeholder sẽ được tạo dựa trên chủ đề này.
2. **Primary Color**: Màu sắc chủ đạo của trang web (Ví dụ: `#3b82f6` cho màu xanh, `#ef4444` cho màu đỏ, v.v.). Sẽ được áp dụng cho nút bấm, icon, text nổi bật, và các thành phần chính.
3. **Theme**: Giao diện sáng (Light) hoặc Giao diện tối (Dark). Sẽ quyết định màu nền và màu chữ toàn trang.
4. **Font** (tuỳ chọn): Nếu người dùng muốn sử dụng một font cụ thể, họ có thể cung cấp tên font (ví dụ: `Roboto`, `Open Sans`). Nếu không, Claude sẽ sử dụng một font mặc định từ Google Fonts.

## Quy ước Code & Styling

- Dùng Google Fonts (ví dụ: `Roboto`, `Open Sans` - nếu người dùng không chỉ định) để đảm bảo tính thẩm mỹ và dễ đọc.
- **Tailwind CSS & Cấu hình**: Sử dụng Tailwind utility classes. Cấu hình màu sắc (Primary color, Dark/Light theme) trong Tailwind config hoặc bằng CSS Variables kết hợp với Tailwind để dễ dàng tùy biến giao diện theo từng chủ đề.
- **Semantic HTML**: Sử dụng các thẻ như `<header>`, `<section>`, `<article>`, `<footer>`, `<nav>`, `<main>`.
- **Responsive Design**: Mobile-first approach với Tailwind (sử dụng `md:`, `lg:`, `xl:` modifiers). Các section phải hiển thị đẹp trên điện thoại trước khi scale lên màn hình desktop.
- **Aesthetics & Animations**:
  - Sử dụng Tailwind classes (`transition`, `duration-300`, `hover:`) cho các tương tác mượt mà như hover nút bấm, thẻ bài (cards).
  - Tích hợp **Animate.css** bằng cách thêm các class (ví dụ: `animate__animated animate__fadeInUp`) để tăng tính sinh động cho trang web.
- **Lucide Icons**: Dùng script CDN của Lucide để render icon. Nút CTA nên có icon để nổi bật và kêu gọi hành động mạnh mẽ.
- **Accessibility & SEO**: Các thẻ `<img>` cần có `alt`, sử dụng cấu trúc heading (`<h1>`, `<h2>`, `<h3>`) hợp lý (chỉ có 1 thẻ `<h1>` duy nhất ở Hero Section).
- Hình ảnh lấy từ placeholder ([unsplash.com](https://unsplash.com)) với kích thước phù hợp cho từng section (ví dụ: 1200x600 cho Hero, 400x300 cho các thẻ bài).

## Các bước thực hiện (Dành cho Claude)

1. **Phân tích yêu cầu**: Xác nhận lại 3 params (Chủ đề, Primary Color, Theme) từ người dùng.
2. **Setup Base**: Khởi tạo `index.html` và `style.css`. Trong `index.html`, nhúng script/CSS qua CDN của Tailwind CSS, Lucide Icons, và Animate.style(https://animate.style).
3. **Phác thảo Copywriting**: Tạo nội dung giả định (nhưng thực tế) phù hợp với Chủ đề được yêu cầu cho cả 10 sections.
4. **Xây dựng Sections**: Sử dụng HTML thuần kết hợp utility classes của Tailwind để code từng section tuần tự. Đảm bảo cấu trúc rõ ràng, đúng semantic.
5. **Tinh chỉnh UI & Hiệu ứng**:
   - Áp dụng cấu hình Primary Color và Dark/Light Theme.
   - Thêm hiệu ứng hover của Tailwind cho tương tác.
   - Gọi script `lucide.createIcons()` trong file JavaScript thuần để hiển thị icon.
   - Gắn các class của Animate.css (`animate__animated`, `animate__fadeIn`, v.v.) vào các thành phần chính để giao diện mượt mà và thu hút.
6. **Kiểm tra Responsive**: Đảm bảo tất cả các phần (nhất là Navbar, Grid lợi ích, và Bảng giá) tự động co giãn tốt trên mobile.
7. **Tối ưu SEO & Accessibility**: Kiểm tra lại cấu trúc heading, alt text cho hình ảnh, và đảm bảo trang web thân thiện với người dùng và công cụ tìm kiếm.
8. Sau đó test lại bằng /chrome-devtools để đảm bảo mọi thứ hoạt động tốt trên cả desktop và mobile.
9. Tránh các block bị đè lên nhau, đảm bảo khoảng cách (spacing) hợp lý giữa các section và thành phần.
10. **Hoàn thiện**: Cung cấp mã nguồn hoàn chỉnh cho người dùng và hướng dẫn cách chạy hoặc tích hợp vào dự án của họ.
