# BÀI LÀM PHA 2 (ĐỀ LUYỆN TẬP CHỦ ĐỀ TÀI CHÍNH CÁ NHÂN)

- **Họ tên:**
- **Lớp:**
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đăng ký hội thảo ra JSON

**KET QUA AI**

```text
```json
[
  {
    "ma_goi": "DT",
    "ngay_hoi_thao": "2026-12-20",
    "nguoi_lon": 2,
    "tre_em": 1,
    "hang_ve": "thuong",
    "ghi_chu": null
  },
  {
    "ma_goi": "CB",
    "ngay_hoi_thao": "2027-01-10",
    "nguoi_lon": 3,
    "tre_em": 0,
    "hang_ve": null,
    "ghi_chu": "Có một người dùng xe lăn cần lối đi riêng"
  },
  {
    "ma_goi": "VIP",
    "ngay_hoi_thao": null,
    "nguoi_lon": 4,
    "tre_em": 0,
    "hang_ve": "vip",
    "ghi_chu": "ngồi bàn đầu gần màn hình chiếu"
  }
]

```
```

**Link trò chuyện:** https://share.gemini.google/Sgtwa4uKlcW7

## 4.3. Báo giá vé hội thảo bằng Chain-of-Thought

**KET QUA AI**

```text
```python
adult_price = 1500000
num_adults = 4
adult_total = num_adults * adult_price

child_price = 0.5 * adult_price
num_children_6_12 = 2
num_children_under_6 = 1
child_total = num_children_6_12 * child_price + num_children_under_6 * 0

ticket_total = adult_total + child_total
discount = 0.10 * ticket_total if num_adults >= 4 else 0
ticket_after_discount = ticket_total - discount

notebook_price = 200000
num_notebooks = 2
surcharge = num_notebooks * notebook_price

grand_total = ticket_after_discount + surcharge
print(f"adult_total: {adult_total:,.0f}")
print(f"child_total: {child_total:,.0f}")
print(f"ticket_total: {ticket_total:,.0f}")
print(f"discount: {discount:,.0f}")
print(f"surcharge: {surcharge:,.0f}")
print(f"grand_total: {grand_total:,.0f}")


```

```text
adult_total: 6,000,000
child_total: 1,500,000
ticket_total: 7,500,000
discount: 750,000
surcharge: 400,000
grand_total: 7,150,000


```

| Bước | Hạng mục | Diễn giải & Phép tính | Thành tiền (đồng) |
| --- | --- | --- | --- |
| 1 | Tiền người lớn | 4 người lớn × 1.500.000 đồng (Gói DT) | 6.000.000 |
| 2 | Tiền trẻ em | 2 trẻ (8 tuổi, 11 tuổi) × (50% × 1.500.000) + 1 bé (4 tuổi) × 0 đồng = 2 × 750.000 + 0 | 1.500.000 |
| 3 | Tiền vé | 6.000.000 + 1.500.000 | 7.500.000 |
| 4 | Giảm giá nhóm | Nhóm có 4 người lớn (≥ 4) nên giảm 10% tiền vé: 10% × 7.500.000 | -750.000 |
| 5 | Phụ thu sổ tay | 2 bộ × 200.000 đồng (không áp dụng giảm giá) | 400.000 |
| 6 | Tổng tiền | (7.500.000 - 750.000) + 400.000 = 6.750.000 + 400.000 | **7.150.000** |

[RESULT: 7.150.000 đồng]
```

**Link trò chuyện:** https://share.gemini.google/1bT8KJuQc5u5

### b) Kiểm tra kết quả AI

Đúng

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{
  "loai_su_co": "sai_khu_vuc",
  "so_khach": 2,
  "so_hiep_bi_anh_huong": 2,
  "tom_tat": "Khách mua gói DT bị xếp ngồi dãy ghế phụ thiếu bàn viết trong 2 phiên học đầu."
}
```

**Link trò chuyện:** https://share.gemini.google/MrO33YPVplOr

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI** 

```text
| Tiêu chí | Điểm | Minh chứng | Đề xuất sửa |
| --- | --- | --- | --- |
| **Đúng thông tin** (50% - tối đa 5,0đ) | **0,0 / 5,0** | - Báo sai giá vé: *"1.200.000đ/người"* (thông tin chuẩn: 1.500.000 đồng/người lớn).<br>

<br>- Báo sai chính sách huỷ vé: *"huỷ trước 4 ngày thì bên em hoàn lại đủ 100%"* (thông tin chuẩn: huỷ trước từ 3 đến 6 ngày chỉ hoàn 50%). | Điều chỉnh lại đúng thông tin của ban tổ chức:<br>

<br>- Giá vé gói Đầu Tư (DT) là **1.500.000 đồng/người lớn**.<br>

<br>- Nếu huỷ vé trước ngày hội thảo **4 ngày** (nằm trong mốc từ 3 đến 6 ngày), khách hàng sẽ được **hoàn lại 50% tiền vé** (mất 50% phí huỷ). |
| **Đầy đủ** (30% - tối đa 3,0đ) | **1,5 / 3,0** | - Đã đề cập đến cả hai ý hỏi của khách hàng (giá vé và chính sách huỷ vé).<br>

<br>- **Thiếu** lời mời khách hàng cung cấp ngày tham dự hội thảo và số lượng vé muốn đăng ký. | Bổ sung câu kêu gọi hành động ở cuối tin nhắn: *"Anh/chị vui lòng cho em biết ngày hội thảo cụ thể muốn tham dự và số lượng vé đăng ký để bên em hỗ trợ giữ chỗ cho mình nhé."* |
| **Giọng điệu** (20% - tối đa 2,0đ) | **0,5 / 2,0** | - Dùng từ ngữ suồng sã, thiếu chuyên nghiệp: *"nha"*, *"chốt đơn đi ạ"*.<br>

<br>- Hứa hẹn lợi nhuận quá đà: *"đi học về đầu tư chứng khoán lời khủng luôn ạ"*. | Sử dụng ngôn từ chuẩn mực, khách quan:<br>

<br>- Thay *"nha"*, *"chốt đơn"* bằng *"ạ"*, *"đăng ký vé"*.<br>

<br>- Bỏ cam kết *"lời khủng"*, thay bằng giá trị thực tế của khoá học (ví dụ: *"cung cấp kiến thức và phương pháp đầu tư bài bản"*). |
| **TỔNG ĐIỂM** | **2,0 / 10** | Bài làm sai lệch hoàn toàn thông tin giá cả, chính sách hoàn tiền và vi phạm quy chuẩn giao tiếp tư vấn. | Cần viết lại toàn bộ câu trả lời theo đúng dữ liệu chuẩn và giữ thái độ tư vấn chuyên nghiệp. |
```

**Link trò chuyện:** https://share.gemini.google/MQk3MGgQmZSb
