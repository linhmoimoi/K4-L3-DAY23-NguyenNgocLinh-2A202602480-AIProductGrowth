# Worksheet — Trợ lý AI tư vấn tuyển sinh ngoài giờ

Họ tên: Nguyễn Ngọc Linh · MSSV: 2A202602480 · Ngày làm: 09/10/2026

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
| **Volume volatility** — độ lệch chuẩn volume tháng ÷ volume trung bình | 🔧 | 2.000 hội thoại/tháng trong PDF là workload giả định, không phải lịch sử. Cần log volume theo tháng, tách theo partner; cần ít nhất 3 tháng dữ liệu hoàn chỉnh để có các quan sát tháng đầu tiên và tính volatility. |
| **GM sau rev-share** — (doanh thu − rev-share − COGS) ÷ doanh thu | 🔧 | PDF có COGS giả định A $83,74/B $623,74 mỗi tháng và Cost/Job A $0,0598/B $0,4455; chưa có F/u, doanh thu Hybrid hoặc điều khoản rev-share xác nhận. Cần giá thực, doanh thu/chi phí theo partner và điều khoản chia sẻ để tính. |
| **Chi phí inference ÷ doanh thu — theo TỪNG partner** | 🔧 | Cần API/inference cost log gắn partner và doanh thu được ghi nhận theo partner. PDF mới có API + infra + retry giả định $53,74/tháng, chưa có doanh thu thực để tính tỷ lệ. |
| **Tập trung volume** — % volume từ partner lớn nhất | 🔧 | Chưa có volume thực theo partner hoặc danh sách partner hoạt động. Cần log hội thoại/job gắn partner ID và tổng volume cùng kỳ. |
| **Chất lượng nhìn từ end-user** — tỷ lệ hoàn thành / escalate / khiếu nại, đo trên end-user | 🔧 | PDF đề xuất đo ≥100 ca eval về containment, reopen trong 24 giờ và handoff; containment 70% hiện là giả định. Cần event/log theo từng hội thoại, nhãn kết quả và khiếu nại end-user; đối chiếu với SLA khi chốt. |
| **Doanh thu/partner · partner NRR · GM tổng** — tính riêng từng partner rồi cộng | 🔧 | Chưa có khách trả tiền hoặc doanh thu partner xác nhận; GM tổng cũng chưa tính overhead đầy đủ. Cần hợp đồng/giá thực, billing và COGS theo partner; NRR cần dữ liệu doanh thu qua kỳ gia hạn. |

## Trạm 2 — Thẻ đèn

**North Star:** Partner activation rate (đèn dẫn đầu của B2B2C, theo dõi hằng tuần) — hiện tại: **chưa có dữ liệu** vì chưa có pilot; mục tiêu khởi điểm đề xuất: **≥60%** partner activation sau hai cohort đủ 30 ngày, cùng ngưỡng xanh tại Trạm 3. Đây là mục tiêu thiết kế để kiểm chứng, không phải kết quả hay benchmark.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **Partner activation rate** ⭐ | Trong mỗi cohort partner đã go-live đủ 30 ngày, tính partner có ít nhất một hội thoại thật của end-user được AI phản hồi trong 30 ngày đầu. Loại partner chưa đủ kỳ, tài khoản/hội thoại thử nội bộ và partner chỉ ký nhưng chưa go-live. | Số partner đủ điều kiện có ≥1 hội thoại end-user thật được AI phản hồi trong 30 ngày đầu ÷ tổng partner go-live đã đủ 30 ngày quan sát × 100% | Tổng hợp theo cohort mỗi tuần; Partner Ops duy trì danh sách partner/go-live, Product/Data Ops đối soát log hội thoại. | **Số hội thoại tính phí/partner (O)** — activation là bước đầu để có volume sử dụng tính phí. |
| 2 | L | **End-user reach trong partner** | Theo từng partner mỗi tuần, tính end-user duy nhất trong tệp đủ điều kiện đã có ít nhất một hội thoại được AI phản hồi. Dùng ID khử danh tính; loại user thử, nhân sự partner và người ngoài tệp đủ điều kiện. | Số end-user duy nhất có hội thoại AI phản hồi ÷ tổng end-user đủ điều kiện của partner × 100% | Partner Ops lấy mẫu số từ partner; Product/Data Ops đối soát log đã khử danh tính hằng tuần. | **Số hội thoại tính phí/partner (O)** — reach trong tệp là tín hiệu sớm cho số hội thoại. |
| 3 | O | **Số hội thoại tính phí/partner** *(đèn bổ sung riêng cho Value Metric Hybrid)* | Theo partner và tuần, đếm `conversation_id` có ít nhất một phản hồi AI, gộp các lượt trong cửa sổ 24 giờ và vẫn tính hội thoại được handoff. Loại hội thoại thử, hội thoại không có phản hồi AI và lượt lặp trong cùng cửa sổ. Đây là Value Metric của mô hình Hybrid: phí nền `F` + `u` nhân số hội thoại tính phí. | Số `conversation_id` duy nhất/partner/tuần sau khử trùng lặp 24 giờ (đơn vị: hội thoại) | Product/Data Ops thiết lập event và kiểm tra log Page theo partner ID, `conversation_id`, thời điểm và cờ phản hồi AI; tổng hợp hằng tuần. | **Doanh thu/partner (G)** — hội thoại tính phí là phần usage của doanh thu Hybrid; không tính pipeline hay báo giá. |
| 4 | O | **Chi phí inference ÷ doanh thu — theo TỪNG partner** | Với từng partner trong cùng kỳ, so chi phí API/inference, hạ tầng và retry gắn trực tiếp với job AI với doanh thu ghi nhận của partner đó. Không lấy trung bình giữa các partner; QA, escalation/HITL và overhead không nằm trong tử số inference mà được tính ở COGS/GM. | Tổng chi phí API/inference + hạ tầng + retry gắn với partner trong kỳ ÷ doanh thu ghi nhận của cùng partner trong cùng kỳ × 100% | Product/Data Ops cung cấp cost log theo partner; Finance đối soát doanh thu theo cùng kỳ và cùng quy ước ghi nhận; rà soát tuần, chốt tháng. | **GM tổng (G)** — inference là COGS biến đổi, tỷ lệ tăng sẽ kéo giảm biên gộp của partner. |
| 5 | O | **Chất lượng nhìn từ end-user (tỷ lệ hội thoại đạt eval)** | Trên mẫu hội thoại thật được reviewer chấm, tính hội thoại trả lời đúng theo nguồn tuyển sinh đã duyệt, không có lỗi nghiêm trọng và không reopen trong 24 giờ. Handoff đạt nếu chuyển đúng câu hỏi đến người phụ trách theo SLA; không tính hội thoại thử/nội bộ. | Số hội thoại end-user được reviewer chấm đạt và không reopen trong 24 giờ ÷ tổng hội thoại end-user đã được reviewer chấm × 100% | QA sở hữu rubric và chọn mẫu; Partner Ops xác nhận SLA handoff; Product/Data Ops lưu log và nhãn. Tổng hợp hằng tuần sau đủ cửa sổ 24 giờ. | **Partner NRR (G)** — chất lượng ổn định có thể báo trước việc partner duy trì hoặc mở rộng chi tiêu khi gia hạn. |
| 6 | G | **Doanh thu/partner** | Theo từng partner/quý, tính doanh thu Hybrid đã ghi nhận từ phí nền và usage hội thoại tính phí. Không cộng pipeline, báo giá, doanh thu giả định hoặc khoản chưa được ghi nhận. | Tổng doanh thu đã ghi nhận của partner trong quý (USD/partner/quý); theo thiết kế là tổng từng tháng của (`F` + `u` × hội thoại tính phí), ghi nhận theo chính sách kế toán đã chọn | Finance sở hữu hợp đồng, billing, đối soát usage và chính sách ghi nhận; chốt theo quý. | Bảng điểm; không báo trước cho đèn tầng dưới. |
| 7 | G | **Partner NRR** | Trên cùng cohort có doanh thu định kỳ đầu kỳ, tính phần doanh thu định kỳ còn lại sau churn, giảm mức dùng/giảm gói và mở rộng. Loại partner mới sau ngày đầu kỳ và khoản thu một lần. | (MRR đầu kỳ − MRR churn − MRR giảm + MRR mở rộng) ÷ MRR đầu kỳ × 100%, tính theo partner/cohort rồi tổng hợp | Finance theo dõi billing, usage và trạng thái gia hạn; rà soát hằng quý và tại mỗi kỳ gia hạn. | Bảng điểm; không báo trước cho đèn tầng dưới. |
| 8 | G | **GM tổng** | Theo từng partner/quý, lấy doanh thu trừ rev-share và COGS thực tế quy thuộc được (API/inference, retry, QA, escalation/HITL và triển khai nếu xếp vào COGS). Không coi overhead bằng 0 trong PDF stress là chi phí thực tế bằng 0, và không dùng stress case làm GM thực tế. Chi phí chung báo riêng, không phân bổ vào GM partner. | (Doanh thu partner − rev-share − COGS partner đầy đủ) ÷ doanh thu partner × 100% | Finance sở hữu đối soát doanh thu, hợp đồng rev-share và sổ COGS; chốt theo quý, báo chi phí chung riêng. | Bảng điểm; không báo trước cho đèn tầng dưới. |

Đèn chi phí AI là đèn số **4: Chi phí inference ÷ doanh thu — theo TỪNG partner**. Đo riêng từng partner để tránh partner lỗ bị che bởi partner có biên tốt. PDF Day 22 chỉ có API + infra + retry giả định $53,74/tháng và Cost/Job stress A/B; chưa có log theo partner hay doanh thu Hybrid thực nên không điền số hiện tại. Các đèn G số 6–8 là kết quả quan sát sau khi có doanh thu và đủ kỳ dữ liệu, không phải số hiện tại.

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | **Partner activation rate** | ≥60% partner trong cohort go-live đủ 30 ngày có ≥1 end-user thật được AI phản hồi | 30%–<60% | <30% | [TB] Dải khởi điểm trong HANDBOOK §3.3 cho B2B2C, không phải benchmark; lập baseline sau hai cohort 30 ngày kể từ go-live pilot đầu tiên. | Dải này báo hiệu partner đã go-live nhưng chưa đưa được end-user thật vào dùng; chỉ xem là baseline sau khi có đủ hai cohort đo. |
| 2 | **End-user reach trong partner** | ≥B% (B = reach gộp của 2 tuần baseline đầu tiên có hoạt động end-user thật) | <B% trong 1 tuần đo | <B% trong 2 tuần liên tiếp | [TB] Chưa có chuẩn phù hợp; lấy B từ hai tuần hoạt động thật đầu tiên sau go-live, với cùng cách tính mẫu số cho từng partner. | So với baseline của chính partner giúp phát hiện reach giảm; một tuần là cảnh báo, hai tuần liên tiếp là tín hiệu rõ hơn, còn tuần thiếu dữ liệu không tính xanh. |
| 3 | **Số hội thoại tính phí/partner** | ≥V̄ (V̄ = số hội thoại/partner/tuần trung bình của 2 tuần baseline đầu tiên có hội thoại tính phí) | <V̄ trong 1 tuần đo | <V̄ trong 2 tuần liên tiếp | [TB] Chưa có chuẩn phù hợp; sau go-live lấy trung bình hai tuần đầu có hội thoại tính phí theo định nghĩa `conversation_id`/24 giờ tại Trạm 2. | So với baseline cùng partner để nhận ra volume hụt; đây là tín hiệu usage, chưa chứng minh unit economics khi F/u chưa chốt. |
| 4 | **Chi phí inference ÷ doanh thu — theo TỪNG partner** | ≤2,84% doanh thu partner/kỳ (mốc mô hình stress B) | >2,84% đến ≤9,84% | >9,84% | [MH] Dùng stress B Day 22; mốc đỏ suy từ GM sàn thiết kế 60%. Phép tính tại Phụ lục [MH] 1. | 2,84% là tỷ lệ inference trong stress B; 9,84% là trần khi giữ nguyên COGS khác và GM 60%. Vì stress B tính theo job hoàn thành còn metric đếm hội thoại có thể gồm handoff, đây chỉ là guardrail tạm đến khi có dữ liệu cùng partner/kỳ. |
| 5 | **Chất lượng nhìn từ end-user (tỷ lệ hội thoại đạt eval)** | ≥Q̄ và không có lỗi nghiêm trọng (Q̄ = tỷ lệ đạt gộp của 2 chu kỳ eval đầu) | <Q̄ trong 1 chu kỳ, không có lỗi nghiêm trọng | Có ≥1 lỗi nghiêm trọng về thông tin tuyển sinh/học phí/hạn chót; hoặc <Q̄ trong 2 chu kỳ liên tiếp | [TB] Lập Q̄ từ hai chu kỳ eval đầu trên hội thoại thật, tối thiểu 100 ca theo kế hoạch Day 22. | Q̄ phản ánh kết quả QA của chính sản phẩm; một chu kỳ giảm là cảnh báo, còn một lỗi tuyển sinh nghiêm trọng cũng đủ bật đỏ để tránh phát tán thông tin sai. |
| 6 | **Doanh thu/partner** | ≥$5.670/partner/quý đủ kỳ (stress B giữ nguyên 3 tháng) | $4.678,05 đến <$5.670/partner/quý | <$4.678,05/partner/quý | [MH] Stress B Day 22; sàn đỏ suy từ COGS $623,74/tháng và GM tối thiểu 60%, xanh neo theo doanh thu stress. Phép tính tại Phụ lục [MH] 2. | Với workload không đổi đủ quý, $4.678,05 là mức để đạt GM 60%, còn $5.670 là stress B ba tháng; cần tính lại khi COGS, giá hoặc rev-share thực khác. |
| 7 | **Partner NRR** | ≥max(100%, Bₙ) (Bₙ = NRR baseline gộp của 2 quý gia hạn đầu) | ≥100% và <max(100%, Bₙ) | <100% | [TB] Không có chuẩn ngoài phù hợp; xác định Bₙ qua hai quý gia hạn đầu có doanh thu định kỳ. | NRR dưới 100% nghĩa cohort mất doanh thu định kỳ; xanh yêu cầu giữ tối thiểu doanh thu đầu kỳ và đạt baseline riêng nếu baseline cao hơn. |
| 8 | **GM tổng** | ≥67,00% | ≥60,00% đến <67,00% | <60,00% | [MH] GM stress B Day 22 là 67,00%, sàn thiết kế là 60%. Phép tính tại Phụ lục [MH] 3. | 67% giữ mức stress B, 60% là sàn thiết kế; phải so trên cùng phạm vi COGS vì stress chưa tính overhead, thuế, phí thanh toán, acquisition hay rev-share. |

### Phụ lục [MH] — phép tính (≥2)

**[MH] 1 — Chi phí inference ÷ doanh thu — theo TỪNG partner**

```
Input stress B Day 22 cho một tháng: API + hạ tầng + retry $53,74; QA + escalation $30 + $540 = $570; tổng COGS $623,74; doanh thu $1,35/job × 1.400 job hoàn thành = $1.890; GM sàn thiết kế 60%.
Tỷ lệ inference stress hiện tại = $53,74 ÷ $1.890 = 2,8434% ≈ 2,84%.
Nếu giữ các COGS khác không đổi, inference tối đa để GM còn 60% = (1 − 60%) × $1.890 − $570 = $186; tỷ lệ trần = $186 ÷ $1.890 = 9,8413% ≈ 9,84%.
Vùng quyết định có điều kiện: 🟢 ≤2,84% · 🟡 >2,84% đến ≤9,84% · 🔴 >9,84%.
Giới hạn: $1.890 được tính theo 1.400 job hoàn thành, trong khi Value Metric Trạm 2 là hội thoại có phản hồi AI và gồm handoff; F/u chưa chốt. Đây là guardrail stress B. Khi có pilot, tính lại với doanh thu, cost log, rev-share và overhead của cùng partner/kỳ, không trộn hai mẫu số.
```

**[MH] 2 — Doanh thu/partner**

```
Input stress B Day 22: COGS $623,74/tháng ở workload giả định, GM tối thiểu 60%, doanh thu stress $1.890/tháng; chưa gồm overhead/rev-share và giả định workload giữ nguyên.
Từ GM = (doanh thu − COGS) ÷ doanh thu, doanh thu tháng để đạt GM 60% là COGS ÷ (1 − 60%) = $623,74 ÷ 0,40 = $1.559,35/tháng.
Quy đổi cùng workload cho đủ quý: sàn đỏ = $1.559,35 × 3 = $4.678,05/partner/quý; stress B = $1.890 × 3 = $5.670/partner/quý.
Vùng quyết định có điều kiện: 🟢 ≥$5.670/quý · 🟡 $4.678,05 đến <$5.670/quý · 🔴 <$4.678,05/quý.
Giới hạn: phép tính giả định COGS $623,74/tháng thuộc cùng partner và workload suốt quý; giá Hybrid F/u, rev-share, overhead và cách ghi nhận chưa được kiểm chứng bằng pilot. Khi có dữ liệu, dùng doanh thu/COGS thật của partner; nếu COGS đổi theo volume thì tính lại sàn.
```

**[MH] 3 — GM tổng**

```
Đầu vào stress B Day 22: doanh thu $1.890/tháng; COGS $623,74/tháng; GM sàn thiết kế 60%.
GM stress B = ($1.890 − $623,74) ÷ $1.890 × 100% = 66,9979% ≈ 67,00%.
Dải theo hai mốc: 🟢 ≥67,00% (đạt stress B) · 🟡 ≥60,00% và <67,00% (trên sàn nhưng dưới stress) · 🔴 <60,00% (dưới GM sàn thiết kế).
Giới hạn: đây là GM stress trước overhead, thuế, phí thanh toán, acquisition và rev-share, không phải số vận hành. Khi tính GM thực tế, đưa đủ chi phí cung cấp trực tiếp và rev-share vào phép tính; báo chi phí bán hàng/acquisition riêng.
```

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (cần ≥2).

1. ⏹ **NẾU** Partner activation rate **<30% ở từng cohort** **TRONG** hai cohort go-live 30 ngày liên tiếp **VÀ** tổng cộng có **≥5 partner** đủ kỳ quan sát **THÌ** dừng nhận partner mới sau khi chốt cohort thứ hai; Partnerships/Partner Ops dành tuần kế tiếp để kích hoạt partner hiện có. **KHÔNG THÌ** không xem hợp đồng đã ký là bằng chứng end-user hoạt động.
2. **NẾU** End-user reach **<B%** **TRONG** hai tuần liên tục **VÀ** cả hai tuần dùng cùng tệp end-user đủ điều kiện **THÌ** Partner Ops đề nghị thử CTA tư vấn trên Facebook Page hiện hữu và đo reach tuần kế tiếp. **KHÔNG THÌ** chưa phát triển tính năng mới trước khi thử kênh phân phối này.
3. **NẾU** hội thoại tính phí/partner **<V̄** **TRONG** hai tuần liên tục **THÌ** Product/Data Ops rà event `conversation_id`/24 giờ, tìm điểm rơi giữa end-user, phản hồi AI và billing, rồi thống nhất một sửa đổi trước tuần sau. **KHÔNG THÌ** không ký partner chưa kích hoạt để bù volume.
4. ⏹ **NẾU** inference cost/revenue của một partner **>9,84%** **TRONG** hai kỳ tháng đối soát liên tiếp **VÀ** doanh thu dương ở cả hai kỳ **THÌ** dừng tăng lưu lượng AI cho partner đó; Finance và AI Ops tính lại cost theo hội thoại tính phí, đặt giới hạn usage/giá rồi mới mở rộng. **KHÔNG THÌ** không chuyển inference không tạo doanh thu sang công ty hoặc tăng volume để che tỷ lệ đỏ.
5. ⏹ **NẾU** xuất hiện **≥1 lỗi nghiêm trọng** về tuyển sinh/học phí/hạn chót trong eval thật **HOẶC** tỷ lệ eval **<Q̄** **TRONG** hai chu kỳ liên tiếp có tổng **≥100 ca thật** **THÌ** dừng auto-reply nhóm câu hỏi có lỗi ngay (hoặc sau chu kỳ đỏ thứ hai ở nhánh tỷ lệ), chuyển người thật và sửa nguồn tri thức đã duyệt trước khi bật lại. **KHÔNG THÌ** không hạ rubric, bỏ nhãn reopen/handoff hay tính containment là đạt để giữ màu xanh.
