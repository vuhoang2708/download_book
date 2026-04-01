# 📘 TECHNICAL SPECIFICATION: OmniBook Search & Download

## 1. Tổng quan Dự án (Project Overview)
**OmniBook** là một ứng dụng Web tĩnh (Static Web App) cho phép người dùng tra cứu và truy cập đa phương tiện (Ebooks, Audiobooks, Podcasts, YouTube) từ các nguồn mở toàn cầu.

### 🎯 Mục tiêu:
- Tích hợp tìm kiếm đa nguồn (Library + iTunes + YouTube).
- Cung cấp khả năng preview nội dung trực tiếp (Audio previews).
- Xây dựng cơ chế "System Bridge" để AI có thể hỗ trợ tải file về máy tính cá nhân.

---

## 2. Giải pháp Kỹ thuật (Technical Solutions)

### 🧩 Kiến trúc Front-end:
- **Core:** HTML5, CSS3, Vanilla JS (Không dùng framework để đảm bảo tốc độ và sự đơn giản).
- **Styling:** Glassmorphism UI, HSL Colors, Modern Typography (Google Fonts 'Outfit').
- **Responsive:** Mobile-first design, Grid layout linh hoạt.

### 📡 API & Data Sources:
1. **Open Library API:** Sử dụng cho tìm kiếm Ebooks. Hỗ trợ kiểm tra trạng thái `has_fulltext` để cung cấp link đọc miễn phí.
2. **Apple iTunes Search API:** Cung cấp metadata chất lượng cao cho Audiobooks và Podcasts (Cover art 600x600, Preview audio clips).
3. **YouTube Integration (v1):** Hiện tại đang dùng cơ chế Search giả lập hiển thị dựa trên bộ từ khóa của người dùng (Có thể nâng cấp lên YouTube Data API v3).

### 🛠️ Cơ chế "System Bridge" (Download Flow):
- **Giao diện:** Khi người dùng nhấn nút Download, JS sẽ ghi một log đặc biệt `[SYSTEM_DOWNLOAD_REQUEST]`.
- **Thực thi:** AI (Antigravity) sẽ "lắng nghe" các yêu cầu này và sử dụng skill `tai-video` cùng công cụ `yt-dlp` trong Terminal để tải file về thư mục `workspace/download_book/`.

---

## 3. Timeline & Quá trình Thay đổi

- **v1.0 (01/04/2026):** Khởi tạo Web tìm kiếm sách cơ bản (Open Library API).
- **v1.1 (01/04/2026):** Mở rộng sang Audiobook & Podcast, thêm Audio Player tích hợp.
- **v1.2 (01/04/2026):** Tích hợp YouTube, chế độ "All Media" (Tầm nhìn đa phương tiện), và System Bridge cho download.

---

## 4. Phân tích Rủi ro & Hạn chế (Risk & Limitations)

### ⚠️ Rủi ro:
- **Bản quyền (Copyright):** Một số nguồn sách có thể yêu cầu đăng nhập hoặc mượn số thông qua Archive.org. Việc tải tự động chỉ áp dụng cho nội dung Public Domain.
- **CORS Policy:** Một số API có thể chặn yêu cầu trực tiếp từ trình duyệt nếu không thông qua Proxy/Backend.

### 🔍 Hạn chế Kỹ thuật:
- **YouTube:** Hiện tại vì chạy trên Static Web (Local), việc search YouTube chưa thể lấy đầy đủ hàng triệu kết quả như trang chủ chính thức (Hạn chế về API Key).
- **Audio Quality:** Preview audios từ iTunes thường chỉ có độ dài 30-90 giây. Để nghe đầy đủ, cần thực hiện quy trình Download qua AI.

---
*📍 Tài liệu được cập nhật ngày 01/04/2026 theo RULES.md.*
