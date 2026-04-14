# 漢字 Kho — Hán Tự Cá Nhân

Công cụ học và quản lý Hán tự cá nhân, chạy hoàn toàn trên trình duyệt, không cần server. Dữ liệu lưu trong `localStorage`.

---

## Tính năng

**Graph view** — hiển thị toàn bộ kho chữ dưới dạng mạng lưới node. Ba loại kết nối:
- Tím: cùng bộ thủ
- Vàng: đồng âm Hán Việt (so sánh chính xác, có dấu thanh)
- Xanh ngọc: từ ghép chung

**List view** — bảng danh sách, có thể sort theo Hán Việt / Pinyin / Jyutping (click vào tiêu đề cột).

**Flashcard — 3 chế độ:**

| Chế độ | Pool | Cơ chế |
|--------|------|--------|
| ✦ Học mới | `status: new` | Nhập âm HV → đúng → mastered, sai → reviewing |
| ↻ Ôn tập | `status: reviewing` | Nhập âm HV → đúng → mastered, sai → reviewing |
| ★ Kiểm tra | `status: mastered` | Nhập âm HV → đúng → giữ mastered, sai → reviewing |

Phím tắt: `Enter` kiểm tra · `Del` undo thẻ vừa xong.

**Filter** — lọc theo trạng thái (Tất cả / Mới / Đang ôn / Đã thuộc) + ô tìm kiếm.

---

## Cấu trúc data mỗi chữ

```json
{
  "id": "lyr001",
  "char": "心",
  "hanViet": "Tâm",
  "pinyin": "xīn",
  "jyutping": "sam1",
  "meaning": "Tim; tâm; lòng",
  "compounds": [
    { "word": "真心", "reading": "chân tâm", "meaning": "chân thành" }
  ],
  "radical": "心",
  "notes": "",
  "status": "new",
  "dateAdded": "2026-04-14"
}
```

`status` có 3 giá trị: `new` · `reviewing` · `mastered`

---

## Import JSON

Tạo file `.json` là mảng các object theo cấu trúc trên, rồi dùng nút **↑ Import** trên header.

Logic dedup khi import:
- Chữ chưa có → thêm mới
- Chữ đã có, status trong file ≠ `new` → khôi phục status + notes (dùng khi chuyển máy)
- Chữ đã có, status trong file là `new` → giữ nguyên status hiện tại

Khi chữ có nhiều âm HV (ví dụ `"Vi / Vị"`), flashcard chấp nhận cả hai cách nhập, phân cách bằng `/`.

## Export JSON

Nút **↓ Export** tải về file `hantu-kho-YYYY-MM-DD.json` chứa toàn bộ dữ liệu kèm status. Dùng làm backup hoặc chuyển sang trình duyệt/máy khác.

---

## Nguồn từ vựng đã nhập

| Batch | Nguồn | Số chữ |
|-------|-------|--------|
| VOCAB_300 | 300 chữ thông dụng nhất Mandarin | ~300 |
| VOCAB_LYRICS | 站在樹林內就如沒氧氣... (Quảng Đông) | 89 |
| 盼望 | 盼望你没有为我又再度暗中淌泪... | 35 |
| 痛哭 | 痛哭的你 擁抱著痛苦的我... | 125 |
| 近日離開 | 近日像每樣話題總不適合你... | 124 |

---

## Thêm từ vựng thủ công

Nút **+ Thêm** trên header — điền đầy đủ char / Hán Việt / Pinyin / Jyutping / nghĩa / bộ thủ.
