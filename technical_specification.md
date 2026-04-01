# 📘 TECHNICAL SPECIFICATION: OmniBook Search & Download

## 1. Tổng quan Dự án (Project Overview)
**OmniBook** là một ứng dụng Web tĩnh (Static Web App) cho phép người dùng tra cứu và truy cập đa phương tiện (Ebooks, Audiobooks, Podcasts, YouTube) từ các nguồn mở toàn cầu.

### 🎯 Mục tiêu:
- Tích hợp tìm kiếm đa nguồn (Library + iTunes + YouTube).
- Cung cấp khả năng preview nội dung trực tiếp (Audio previews & YouTube Embed).
- Hiển thị đầy đủ Metadata (Thời lượng thực tế, Tác giả) để phân biệt nội dung Full/Tóm tắt.
- Xây dựng cơ chế "System Bridge" để AI có thể hỗ trợ tải file về máy tính cá nhân.

---

## 2. Giải pháp Kỹ thuật (Technical Solutions)

### 🧩 Kiến trúc Front-end:
- **Core:** HTML5, CSS3, Vanilla JS (Không dùng framework).
- **Styling:** Glassmorphism UI, HSL Colors, Modern Typography (Google Fonts 'Outfit').
- **Responsive:** Mobile-first design, Grid layout linh hoạt.

### 📡 API & Data Sources:
1. **Open Library API:** Sử dụng cho tìm kiếm Ebooks. Hỗ trợ kiểm tra trạng thái `has_fulltext`.
2. **Apple iTunes Search API:** Cung cấp metadata chất lượng cao cho Audiobooks và Podcasts (Cover art 600x600, Preview audio clips, `trackTimeMillis` cho thời lượng chính xác).
3. **YouTube Real-time Integration (v3):** Chuyển đổi từ Mock Data sang **Invidious API (Public Instance)** để thực hiện tìm kiếm video thật sự. Tích hợp **YouTube Iframe Embed API** để xem/nghe trực tiếp trên UI.

### 🛠️ Cơ chế "System Bridge" (Download Flow):
- **Giao diện:** Khi người dùng nhấn nút Download, JS sẽ ghi một log đặc biệt `[SYSTEM_DOWNLOAD_REQUEST]`.
- **Thực thi:** AI (Antigravity) sẽ "lắng nghe" các yêu cầu này và sử dụng skill `tai-video` cùng công cụ `yt-dlp` trong Terminal để tải file về thư mục `workspace/download_book/`.

---

## 3. Timeline & Quá trình Thay đổi

- **v1.0 (01/04/2026):** Khởi tạo Web tìm kiếm sách cơ bản (Open Library API).
- **v1.1 (01/04/2026):** Mở rộng sang Audiobook & Podcast, thêm Audio Player tích hợp.
- **v1.2 (01/04/2026):** Tích hợp YouTube, chế độ "All Media" và System Bridge.
- **v1.3 (01/04/2026):** 
    - Nhúng trực tiếp **YouTube Preview Player**.
    - Hiển thị **Thời lượng (Duration)** cho Audiobooks/Podcasts/Videos.
- **v1.4 (Bản vá lỗi 01/04/2026 - Mới nhất):** 
    - Thay thế Mock Data YouTube bằng **Real-time Search API**. 
    - Sửa lỗi hiển thị thời lượng ảo (khắc phục lỗi trình duyệt hiện 4:59).
    - Đồng bộ hóa Metadata thời gian thực cho mọi kết quả media.

---

## 4. Phân tích Rủi ro & Hạn chế (Risk & Limitations)

### ⚠️ Rủi ro:
- **Bản quyền (Copyright):** Một số nguồn sách yêu cầu đăng nhập hoặc mượn số.
- **Độ trễ API:** Sử dụng public Invidious instances có thể gặp độ trễ vào giờ cao điểm.

### 🔍 Hạn chế Kỹ thuật:
- **YouTube:** Việc lấy metadata thời lượng video YouTube có thể thay đổi tùy theo instance API sử dụng.
- **Mobile Browsing:** Trải nghiệm xem Iframe trên màn hình quá nhỏ cần tối ưu thêm CSS.

---
*📍 Tài liệu được cập nhật ngày 01/04/2026 theo RULES.md.*
