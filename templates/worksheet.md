# Worksheet — [Tên sản phẩm]

Họ tên: … · MSSV: … · Ngày làm: …

## Trạm 1 — Loại mô hình

**Câu chốt loại:** Chúng tôi đang thiết kế mô hình **B2B2C** vì bên trả tiền dự kiến là trường/trung tâm tuyển sinh mua quyền kết nối Facebook Page và dịch vụ; người dùng cuối là người cần tư vấn tuyển sinh nhắn tin trên Page của đơn vị đó; sản phẩm xử lý hội thoại AI theo `conversation_id`, nên có bề mặt tiếp xúc và dữ liệu end-user. Chọn B2B2C thay vì B2B vì hệ thống dự kiến trực tiếp phục vụ hội thoại của khách hàng đơn vị mua, không chỉ được trung gian giới thiệu hoặc phân phối. **Giới hạn bằng chứng:** PDF Day 22 ghi đây là kịch bản giả định, chưa có pilot hoặc khách hàng trả tiền được xác nhận; vì vậy đây là loại của mô hình đang thiết kế, chưa phải doanh thu/vận hành đã kiểm chứng hôm nay.

**Đối chiếu ba câu hỏi theo thông tin hiện có:**
- Ai trả tiền: theo thiết kế giá Hybrid, trường/trung tâm tuyển sinh trả phí nền `F` và phí `u` theo hội thoại tính phí; `F`, `u` còn để trống và chưa có khách trả tiền xác nhận.
- Ai dùng: người hỏi tư vấn tuyển sinh qua hội thoại trên Facebook Page; đây là người dùng cuối của dịch vụ, khác với đơn vị mua.
- Có chạm end-user không: theo thiết kế, có — AI phản hồi trực tiếp trong hội thoại của Page và hệ thống dự kiến ghi nhận `conversation_id`, phản hồi AI, handoff và cửa sổ khử trùng lặp 24 giờ. Quyền Meta/Page vẫn cần xác minh; chưa có log pilot chứng minh luồng này đã chạy.

**Bảng đèn §3.3 — B2B2C** (🔧 = cần thiết lập nguồn đo cho pilot; không có đèn nào được xác nhận đo bằng dữ liệu vận hành hôm nay. Số trong PDF là giả định/mục tiêu, không phải baseline thực tế.)

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| **Partner activation rate** ⭐ — % partner đã go-live có ≥1 end-user thật trong 30 ngày; loại tài khoản test nội bộ | 🔧 | Chưa có partner/pilot go-live được xác nhận. Cần danh sách partner và log hội thoại Page có end-user thật, loại test nội bộ; có thể thiết lập event tracking trong pilot. |
| **End-user reach trong partner** — % cơ sở khách hàng của partner đã chạm sản phẩm | 🔧 | Chưa có mẫu số là tổng cơ sở khách hàng của partner hoặc log reach. Cần partner cung cấp mẫu số phù hợp và đối chiếu với log người dùng/hội thoại đã khử trùng lặp. |
| **Time-to-first-end-user** — số ngày từ ký đến end-user thật đầu tiên | 🔧 | Chưa có ngày ký/go-live và event end-user đầu tiên. Cần lưu mốc ký cho từng partner và timestamp của hội thoại thật đầu tiên; bắt đầu tính khi có partner pilot. |
| **Volume volatility** — độ lệch chuẩn volume tháng ÷ volume trung bình | 🔧 | 2.000 hội thoại/tháng trong PDF là workload giả định, không phải lịch sử. Cần log volume theo tháng, tách theo partner; cần tích lũy nhiều tháng mới có volatility quan sát được. |
| **GM sau rev-share** — (doanh thu − rev-share − COGS) ÷ doanh thu | 🔧 | PDF có COGS giả định A $83,74/B $623,74 mỗi tháng và Cost/Job A $0,0598/B $0,4455; chưa có F/u, doanh thu Hybrid hoặc điều khoản rev-share xác nhận. Cần giá thực, doanh thu/chi phí theo partner và điều khoản chia sẻ để tính. |
| **Chi phí inference ÷ doanh thu — theo TỪNG partner** | 🔧 | Cần API/inference cost log gắn partner và doanh thu được ghi nhận theo partner. PDF mới có API + infra + retry giả định $53,74/tháng, chưa có doanh thu thực để tính tỷ lệ. |
| **Tập trung volume** — % volume từ partner lớn nhất | 🔧 | Chưa có volume thực theo partner hoặc danh sách partner hoạt động. Cần log hội thoại/job gắn partner ID và tổng volume cùng kỳ. |
| **Chất lượng nhìn từ end-user** — tỷ lệ hoàn thành / escalate / khiếu nại, đo trên end-user | 🔧 | PDF đề xuất đo ≥100 ca eval về containment, reopen trong 24 giờ và handoff; containment 70% hiện là giả định. Cần event/log theo từng hội thoại, nhãn kết quả và khiếu nại end-user; đối chiếu với SLA khi chốt. |
| **Doanh thu/partner · partner NRR · GM tổng** — tính riêng từng partner rồi cộng | 🔧 | Chưa có khách trả tiền hoặc doanh thu partner xác nhận; GM tổng cũng chưa tính overhead đầy đủ. Cần hợp đồng/giá thực, billing và COGS theo partner; NRR cần dữ liệu doanh thu qua kỳ gia hạn. |

## Trạm 2 — Thẻ đèn

**North Star:** … — hiện tại … — mục tiêu …

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | | | | | |
| 2 | L | | | | | |
| 3 | O | | | | | |
| 4 | O | | | | | |
| 5 | O | | | | | |
| 6 | G | | | | | |

Đèn chi phí AI là đèn số: …

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | | | | | | |

### Phụ lục [MH] — phép tính (≥2)

**[MH] 1 — <tên đèn>**

```
Đầu vào (từ mô hình tài chính / Cost/Job của tôi): …
Phép tính: …
Kết quả → 🟢 … · 🟡 … · 🔴 …
```

**[MH] 2 — <tên đèn>**

```
Đầu vào: …
Phép tính: …
Kết quả → 🟢 … · 🟡 … · 🔴 …
```

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (cần ≥2).

1. **NẾU** … **TRONG/TRÊN** … **VÀ** … **THÌ** … **KHÔNG THÌ** …
2. …
3. …
4. …
5. …
