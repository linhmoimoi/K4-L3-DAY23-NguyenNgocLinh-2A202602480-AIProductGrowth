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

**North Star:** Partner activation rate (đèn bật trước của B2B2C, xem hằng tuần) — hiện tại **[CHƯA CÓ DỮ LIỆU]** — mục tiêu **[CHƯA CÓ DỮ LIỆU]**. Day 22 ghi rõ chưa có pilot/khách trả tiền được xác nhận; workload và containment trong mô hình là giả định, không dùng làm số hiện tại hay mục tiêu.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **Partner activation rate** ⭐ | Trong cohort partner đã go-live đủ 30 ngày, đếm partner có ít nhất một hội thoại tư vấn của end-user thật được AI phản hồi trong 30 ngày đầu. Không tính partner chưa đủ 30 ngày quan sát, tài khoản/hội thoại test nội bộ hoặc chỉ ký hợp đồng nhưng chưa go-live. | Số partner đủ điều kiện có ≥1 hội thoại end-user thật được AI phản hồi trong 30 ngày đầu ÷ tổng partner go-live đã đủ 30 ngày quan sát × 100% | Hằng tuần theo cohort; cần danh sách partner/go-live và log hội thoại. **[CẦN LINH XÁC NHẬN: ai sở hữu partner ops/data?]** | **Số hội thoại tính phí/partner (O)** — activation tạo hoạt động end-user đầu tiên, báo trước partner có volume sử dụng tính phí. |
| 2 | L | **End-user reach trong partner** | Theo từng partner và kỳ tuần, đếm end-user duy nhất trong tập khách hàng đủ điều kiện của partner đã có ít nhất một hội thoại được AI phản hồi. Dùng ID đã khử danh tính; không tính tài khoản test, nhân sự partner hoặc người ngoài tập khách hàng đủ điều kiện. | Số end-user duy nhất có hội thoại AI phản hồi ÷ tổng end-user đủ điều kiện của partner × 100% | Hằng tuần; cần log hội thoại và mẫu số/tập khách hàng đủ điều kiện do partner cung cấp. **[CẦN LINH XÁC NHẬN: ai lấy dữ liệu partner và bảo đảm chỉ dùng dữ liệu đã khử danh tính?]** | **Số hội thoại tính phí/partner (O)** — reach rộng hơn trong cùng tệp là tín hiệu sớm cho volume hội thoại. |
| 3 | O | **Số hội thoại tính phí/partner** *(đèn bổ sung riêng cho Value Metric Hybrid)* | Theo partner và tuần, đếm hội thoại có ít nhất một phản hồi AI, gộp trùng `conversation_id` trong cửa sổ 24 giờ; bao gồm hội thoại handoff. Không tính hội thoại test, hội thoại không có phản hồi AI hoặc lượt tin nhắn lặp trong cùng cửa sổ 24 giờ. Đây là Value Metric theo thiết kế Day 22, cần theo dõi vì doanh thu Hybrid dự kiến gồm phí nền `F` + `u` × số hội thoại tính phí. | Số `conversation_id` duy nhất/partner/tuần sau khử trùng lặp 24 giờ (đơn vị: hội thoại) | Tổng hợp hằng tuần từ event/log Page có partner ID, `conversation_id`, thời điểm và cờ phản hồi AI. **[CẦN LINH XÁC NHẬN: ai phụ trách instrument và kiểm tra log?]** | **Doanh thu/partner (G)** — volume tính phí là thành phần usage trong doanh thu Hybrid; không bao gồm pipeline hoặc báo giá chưa ghi nhận. |
| 4 | O | **Chi phí inference ÷ doanh thu — theo TỪNG partner** | Theo từng partner và cùng kỳ, tính chi phí API/inference, hạ tầng và retry trực tiếp gắn với job AI của partner so với doanh thu của chính partner đó. Không gộp partner để lấy trung bình; không tính QA thủ công, escalation/HITL hoặc overhead vào tử số inference (các khoản đó thuộc COGS/GM). | Tổng chi phí API/inference + hạ tầng + retry được gắn với partner trong kỳ ÷ doanh thu ghi nhận của cùng partner trong cùng kỳ × 100% | Theo dõi tuần để phát hiện sớm, đối soát tháng; cần cost log gắn partner ID và doanh thu theo partner. **[CẦN LINH XÁC NHẬN: ai phụ trách dữ liệu chi phí/doanh thu và quy ước ghi nhận doanh thu?]** | **GM tổng (G)** — inference là phần COGS biến đổi; tỷ lệ cao làm giảm biên gộp của chính partner đó. |
| 5 | O | **Chất lượng nhìn từ end-user (tỷ lệ hội thoại đạt eval)** | Trong mẫu hội thoại thật được đánh giá theo rubric đã thống nhất, đếm hội thoại trả lời đúng nhu cầu tuyển sinh và không bị reopen trong 24 giờ. Không tính hội thoại test/nội bộ; handoff không tự động bị coi là đạt hoặc trượt nếu rubric chưa quy định. **[CẦN LINH XÁC NHẬN: rubric “đạt eval” và cách xử lý handoff.]** | Số hội thoại end-user được reviewer chấm đạt và không reopen trong 24 giờ ÷ tổng hội thoại end-user đã được reviewer chấm × 100% | Hằng tuần sau khi đủ cửa sổ reopen 24 giờ; cần log, nhãn kết quả và reviewer. **[CẦN LINH XÁC NHẬN: ai xây rubric và review mẫu?]** | **Partner NRR (G)** — chất lượng tư vấn bền vững có thể báo trước việc partner duy trì/mở rộng chi tiêu qua kỳ gia hạn. |
| 6 | G | **Doanh thu/partner** | Theo từng partner và quý, chỉ tính doanh thu Hybrid đã ghi nhận từ phí nền và usage theo hội thoại tính phí; không tính pipeline, báo giá, doanh thu giả định hoặc khoản chưa được ghi nhận theo quy ước kế toán. | Tổng doanh thu đã ghi nhận của partner trong quý (USD/partner/quý); theo thiết kế: tổng từng tháng của (`F` + `u` × hội thoại tính phí trong tháng), theo kỳ ghi nhận thực tế | Hằng quý; cần hợp đồng/billing, log usage đối soát và quy ước ghi nhận. **[CẦN LINH XÁC NHẬN: ai phụ trách finance/billing và chính sách ghi nhận?]** | Bảng điểm; không báo trước cho đèn tầng dưới. |
| 7 | G | **Partner NRR** | Với cùng tập partner có doanh thu định kỳ đầu kỳ, đo phần doanh thu định kỳ còn lại sau churn, giảm mức dùng/giảm gói và mở rộng trong kỳ. Không tính partner mới ký sau ngày đầu kỳ hoặc khoản doanh thu một lần không định kỳ. | (MRR đầu kỳ − MRR churn − MRR giảm + MRR mở rộng) ÷ MRR đầu kỳ × 100%, tính riêng từng partner/cohort rồi tổng hợp | Hằng quý và sau kỳ gia hạn; cần lịch sử billing/usage và trạng thái gia hạn. **[CẦN LINH XÁC NHẬN: ai phụ trách finance/retention?]** | Bảng điểm; không báo trước cho đèn tầng dưới. |
| 8 | G | **GM tổng** | Theo từng partner và quý, đo phần doanh thu còn lại sau rev-share và toàn bộ COGS thực tế có thể quy thuộc cho partner (API/inference, retry, QA, escalation/HITL và chi phí triển khai nếu được phân loại là COGS). Không coi overhead bằng 0 trong PDF là chi phí thực tế bằng 0; không dùng số stress làm GM thực tế. **[CẦN LINH XÁC NHẬN: quy tắc phân bổ overhead/chi phí chung.]** | (Doanh thu partner − rev-share − COGS partner đầy đủ) ÷ doanh thu partner × 100% | Hằng tháng để vận hành, chốt theo quý; cần billing, hợp đồng rev-share và sổ chi phí thực tế. **[CẦN LINH XÁC NHẬN: ai phụ trách finance/cost allocation?]** | Bảng điểm; không báo trước cho đèn tầng dưới. |

Đèn chi phí AI là đèn số **4: Chi phí inference ÷ doanh thu — theo TỪNG partner**. Đo riêng từng partner để tránh partner lỗ bị che bởi partner có biên tốt. PDF Day 22 chỉ có API + infra + retry giả định $53,74/tháng và Cost/Job stress A/B; chưa có log theo partner hay doanh thu Hybrid thực nên không điền số hiện tại. Các đèn G số 6–8 là kết quả quan sát sau khi có doanh thu và đủ kỳ dữ liệu, không phải số hiện tại.

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
