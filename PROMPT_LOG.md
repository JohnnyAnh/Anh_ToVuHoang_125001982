# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Tô Vũ Hoàng Anh
- **MSSV:** 125001982
- **Tên đề tài Website:** Viet Green Travel – Du lịch sinh thái bền vững cho giới trẻ
- **Công cụ AI đã sử dụng:** Claude (Anthropic), Gemini, Antigravity IDE

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> Đóng vai chuyên gia thiết kế web. Tạo website du lịch sinh thái "Viet Green Travel" (Du lịch sinh thái bền vững cho giới trẻ) chỉ bằng HTML5 và CSS, đúng 2 file index.html và style.css, kèm assets/ (favicon.svg, images/). Tuyệt đối không dùng JavaScript: không thẻ `<script>`, không file .js, không onclick/onsubmit.
> Nội dung gồm 6 khối: hero (3 số liệu: 100% Không Rác Nhựa, 4.800+ Cây Đã Đóng Rừng, 12.500+ Bạn Trẻ Đồng Hành), 4 điểm đến (Cúc Phương, Côn Đảo, Mù Cang Chải, Tràm Chim), 4 giá trị bền vững cùng khối Cam Kết Xanh 2026, hành trình mẫu một ngày gồm 6 mốc giờ, form nhận e-book miễn phí, footer 4 cột.
> Kỹ thuật: Semantic HTML5, CSS Variables, Flexbox/Grid, Animate.css nhúng bằng `<link>`, hover/focus tự viết, responsive, tiếng Việt, font Plus Jakarta Sans.

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration)

### Lần 1: Dựng khung Semantic HTML
- **Prompt đã dùng:** "Dựng khung HTML trước, chưa viết CSS. Dùng `<header>` chứa logo và `<nav>`, `<main>` chứa 5 `<section>` có id (hero, destinations, values, itinerary, newsletter), mỗi điểm đến là `<article>`, hành trình là `<ol>` với `<time>`, form dùng `<label>`/`<input>`, footer có `<address>`. Không dùng `<div>`. Không dùng `<aside>` cho nội dung chính. Mọi `<img>` có alt tiếng Việt, width/height và loading=\"lazy\" (trừ ảnh hero)."
- **Kết quả AI tạo ra:** Khung HTML không có thẻ `<div>`, có 1 thẻ `<h1>`, 5 section, 4 card điểm đến, 6 mốc hành trình và footer 4 cột.
- **Nhận xét & Tinh chỉnh của SV:** AI lạm dụng `<aside>` (14 chỗ) cho các khối không phải phụ chú như nhóm nút hero, số liệu, nhãn cam kết và mốc giờ. Tôi yêu cầu sửa lại thành `<p>`, `<section>`, `<footer>` của card cho đúng ngữ nghĩa, chỉ giữ `<aside>` cho khối cam kết xanh và popup cảm ơn.

### Lần 2: CSS Variables và bảng màu
- **Prompt đã dùng:** "Viết style.css, bắt đầu bằng :root. Bảng màu thiên nhiên: xanh rừng (--forest, --forest-deep, --leaf, --mint), xanh hồ (--lagoon, --ocean, --water), vàng nắng (--sun, --sun-warm), san hô (--coral), nền kem (--sand...), chữ (--text-main, --text-muted). Mỗi điểm đến có một gradient riêng và một gradient phủ cho hero. Thêm biến font, thang cỡ chữ --fs-xs đến --fs-4xl, line-height, spacing, bo góc, bóng đổ, transition. Toàn bộ CSS chỉ dùng var(), không viết mã màu cứng ngoài :root."
- **Kết quả AI tạo ra:** Khoảng 70 biến trong :root, hơn 400 chỗ dùng `var()`, mỗi điểm đến có gradient riêng (`--grad-cucphuong`, `--grad-condao`, `--grad-mucangchai`, `--grad-tramchim`).
- **Nhận xét & Tinh chỉnh của SV:** Tôi kiểm tra và không còn mã màu hex hay rgba nằm ngoài :root. Các bóng đổ và lớp phủ dùng `color-mix()` từ biến màu.

### Lần 3: Bố cục Flexbox/Grid và responsive
- **Prompt đã dùng:** "Hero dạng 2 cột với ảnh bên phải và lớp phủ gradient, 3 số liệu xếp hàng ngang. Điểm đến dùng Grid, mỗi card có ảnh, tiêu đề, mô tả, nhãn nổi bật và nút. Giá trị dùng Grid kèm khối cam kết. Hành trình dạng timeline dọc. Footer Grid 4 cột. Responsive 3 mốc: 1024px, 800px, 560px. Menu mobile bằng CSS thuần: checkbox + label hamburger + :checked, hamburger biến thành dấu X khi mở. Thêm scroll-behavior: smooth và scroll-padding-top."
- **Kết quả AI tạo ra:** Lưới `auto-fit` cho card, 3 breakpoint, menu hamburger không cần JS.
- **Nhận xét & Tinh chỉnh của SV:** Menu dùng checkbox ẩn nên tôi kiểm tra thêm focus bàn phím và `aria-label` cho checkbox.

### Lần 4: Animate.css và hiệu ứng cuộn
- **Prompt đã dùng:** "Tích hợp Animate.css bằng thẻ `<link>`, áp dụng cho hero: tiêu đề fadeInDown, đoạn mô tả fadeInUp, nhóm nút fadeInUp với delay-2s, số liệu fadeIn với delay-3s. Với các section bên dưới, làm hiệu ứng xuất hiện khi cuộn bằng CSS thuần: animation-timeline: view() trong @supports, animation-fill-mode: backwards để hover không bị mất. Nút CTA chính có @keyframes subtlePulse nhẹ. Không dùng quá 3 kiểu hiệu ứng."
- **Kết quả AI tạo ra:** Hero có chuỗi hiện lần lượt bằng Animate.css, nút CTA có hiệu ứng nhịp đập nhẹ.
- **Thách thức gặp phải:** Bản đầu chỉ có hiệu ứng ở hero, các section bên dưới xuất hiện tĩnh. Không dùng thư viện AOS vì AOS cần JavaScript.
- **Cách sửa prompt (Debug prompt):** "Thêm hiệu ứng xuất hiện khi cuộn cho .section-head, .destination-card, .value-card, .values-pledge, .timeline-step, .newsletter-card bằng @keyframes revealUp và animation-timeline: view(), chỉ chạy khi người dùng không bật prefers-reduced-motion." → AI thêm khối @supports ở cuối style.css.

### Lần 5: Hover, focus và form không JS
- **Prompt đã dùng:** "Viết hover và focus bằng CSS cho nút, card điểm đến (nhấc lên, ảnh phóng nhẹ), link menu, link footer, link mạng xã hội, ô nhập. Dùng :focus-visible và :focus-within cho form. Form có 3 trường (họ tên, email, ô tick cam kết xanh) đều required, action=\"#newsletter-success\". Popup cảm ơn bằng CSS thuần: khối id=\"newsletter-success\" ẩn mặc định, hiện bằng :target kèm @keyframes modalFadeIn, có link đóng href=\"#\". Thêm @media (prefers-reduced-motion: reduce)."
- **Kết quả AI tạo ra:** Hiệu ứng hover/focus cho hơn 14 thành phần, popup cảm ơn chạy bằng `:target`.
- **Nhận xét & Tinh chỉnh của SV:** Tôi thử gửi form, popup hiện đúng. Vì không có JS nên form chỉ kiểm tra bằng HTML (`required`, `type="email"`) và không gửi dữ liệu đi đâu.

### Lần 6: Rà soát theo thang điểm
- **Prompt đã dùng:** "Rà soát theo thang điểm đề thi: (1) có `<script>`, onclick/onsubmit, file .js nào không, nếu có thì xóa hết; (2) liệt kê mọi `<div>` và `<aside>` dùng sai nghĩa; (3) tìm mã màu nằm ngoài :root; (4) hiệu ứng nào quá tay; (5) repo đã đủ index.html, style.css, assets/, PROMPT_LOG.md chưa."
- **Kết quả AI tạo ra:** Xác nhận không có JavaScript trong index.html và style.css, không có thẻ `<div>`, không có mã màu cứng. Phát hiện lỗi `<aside>` và thiếu hiệu ứng cuộn đã nêu ở Lần 1 và Lần 4. File chính đang tên `index_1.html`.
- **Nhận xét & Tinh chỉnh của SV:** Tôi đổi tên thành `index.html` rồi commit từng bước: `init structure`, `add css variables`, `add layout and responsive`, `add animations`, `add prompt log`.

## 3. Đánh giá cá nhân về quá trình Vibe Coding

- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?** Dựng bộ 70 biến CSS với bảng màu và gradient riêng cho từng điểm đến, bố cục Grid responsive và popup không cần JavaScript. Làm tay phần này sẽ mất nhiều thời gian thử màu và căn khoảng cách.
- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?**
  1. Nói rõ ràng buộc ngay từ đầu, ví dụ "không dùng JavaScript", nếu không AI có thể tự thêm.
  2. Chia nhỏ yêu cầu (khung, biến, bố cục, hiệu ứng) dễ kiểm soát hơn xin cả trang một lần.
  3. Phải tự kiểm tra code, vì AI dùng sai thẻ `<aside>` và bỏ sót hiệu ứng cuộn.
