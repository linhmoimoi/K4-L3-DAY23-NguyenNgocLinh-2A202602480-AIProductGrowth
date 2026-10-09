# OPERATING DASHBOARD — Trợ lý AI tư vấn tuyển sinh ngoài giờ

**Mô hình:** B2B2C · **Cập nhật:** 09/10/2026 · Nguyễn Ngọc Linh — 2A202602480
**NORTH STAR:** Partner activation rate · trạng thái hiện tại: **chờ partner pilot go-live để lập baseline** · mục tiêu khởi điểm đề xuất: **≥60%** sau hai cohort đủ 30 ngày; đây là mục tiêu cần kiểm chứng, không phải kết quả pilot.
**Trạng thái:** Pilot đang ở giai đoạn đề xuất; chưa có partner go-live hoặc baseline vận hành. Các đèn đang **chờ dữ liệu pilot**, chưa gán màu. Ngưỡng dưới đây là vùng quyết định, không phải kết quả hiện tại.

### Pilot đề xuất — chưa triển khai

**Phạm vi:** mời 1 trường/trung tâm làm partner pilot trên 1 Facebook Page; giới hạn trả lời tự động trong nhóm câu hỏi tuyển sinh có tài liệu do partner duyệt, câu ngoài phạm vi hoặc không chắc chắn chuyển người phụ trách. Trước khi go-live, xác nhận quyền truy cập Page/Meta, nguồn tri thức, người nhận handoff và cách ghi log đã khử danh tính. Đây là kế hoạch, chưa phải partner hay tích hợp đã xác nhận.

**Đo trong pilot:** ghi partner ID, ngày go-live, `conversation_id`, phản hồi AI, handoff, chi phí inference và trạng thái eval; loại traffic test nội bộ. Rà activation hằng tuần; chốt chất lượng trên các ca thật có reviewer. Chỉ bật auto-reply sau khi partner duyệt nguồn và luồng handoff. D0 12/10/2026 vẫn là ngày kế hoạch; chỉ bắt đầu tính các mốc 30/60/90 ngày từ ngày go-live thực tế.

### Leading — hằng ngày/tuần

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 · nguồn | Báo trước cho |
|---|---|---|---|
| Partner activation rate | Chờ cohort pilot đủ 30 ngày | ≥60% / 30–<60% / <30% [TB; §3.3 starter, baseline sau 2 cohort 30 ngày] | Billable conversations/partner (O) |
| End-user reach trong partner | Chờ 2 tuần hoạt động pilot | ≥B / <B trong 1 tuần / <B trong 2 tuần liền; B = baseline 2 tuần đầu có end-user thật [TB] | Số hội thoại tính phí/partner (O) |

### Operating — tuần/tháng

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 · nguồn | Báo trước cho |
|---|---|---|---|
| Số hội thoại tính phí/partner | Chờ 2 tuần baseline pilot | ≥V̄ / <V̄ 1 tuần / <V̄ 2 tuần liền; V̄ = TB 2 tuần đầu có tính phí [TB] | Doanh thu/partner (G) |
| Chi phí inference ÷ doanh thu — theo TỪNG partner | Chờ log cost và doanh thu pilot | ≤2,84% / >2,84–9,84% / >9,84% [MH; stress B, cần kiểm chứng bằng giá/chi phí thật] | GM tổng (G) |
| Chất lượng nhìn từ end-user (tỷ lệ hội thoại đạt eval) | Chờ eval ca thật trong pilot | ≥Q̄, không lỗi nghiêm trọng / <Q̄ một chu kỳ / ≥1 lỗi nghiêm trọng hoặc <Q̄ 2 chu kỳ liền [TB; Q̄ = baseline] | Partner NRR (G) |

### Lagging — quý

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 · nguồn |
|---|---|---|
| Doanh thu/partner (đủ quý) | Chờ kỳ billing pilot đủ quý | ≥$5.670 / $4.678,05–<5.670 / <$4.678,05 [MH; stress B, chưa phải doanh thu thực] |
| Partner NRR | Chờ dữ liệu gia hạn qua 2 quý | ≥max(100%, Bₙ) / ≥100% và <max(100%, Bₙ) / <100%; Bₙ = baseline 2 quý gia hạn [TB] |
| GM tổng | Chờ đối soát doanh thu và COGS pilot | ≥67% / 60–<67% / <60% [MH; stress B, chưa gồm overhead/thuế/thanh toán/acquisition/rev-share] |

### 5 luật quyết định (⏹ = dừng)

1. **⏹ NẾU** activation <30% ở từng cohort trong hai cohort go-live 30 ngày liên tiếp và có tổng ≥5 partner đủ kỳ, **THÌ** ngừng ký mới, ưu tiên kích hoạt partner hiện tại trong tuần kế; **KHÔNG THÌ** không xem hợp đồng là tăng trưởng end-user.
2. **NẾU** reach <B% trong hai tuần liên tiếp trên cùng tệp đủ điều kiện, **THÌ** thử CTA tư vấn trên Facebook Page và đo lại tuần sau; **KHÔNG THÌ** chưa làm tính năng mới trước khi thử phân phối.
3. **NẾU** hội thoại tính phí/partner <V̄ trong hai tuần liền, **THÌ** Product/Data Ops đối soát `conversation_id`/24 giờ và sửa điểm rơi trước tuần sau; **KHÔNG THÌ** không thêm partner chưa kích hoạt để bù volume.
4. **⏹ NẾU** inference cost/revenue của partner >9,84% trong hai tháng đã đối soát, mỗi tháng có doanh thu dương, **THÌ** ngừng mở rộng AI cho partner đó, tính lại cost và đặt giới hạn usage/giá; **KHÔNG THÌ** không tăng volume để che tỷ lệ đỏ.
5. **⏹ NẾU** có ít nhất một lỗi nghiêm trọng về tuyển sinh/học phí/hạn chót hoặc tỷ lệ eval <Q̄ trong hai chu kỳ với ≥100 ca thật, **THÌ** dừng auto-reply nhóm câu hỏi có lỗi, chuyển người thật và sửa KB đã duyệt; **KHÔNG THÌ** không hạ chuẩn eval hay giấu handoff.

### Cổng gác 90 ngày

Lịch kế hoạch từ D0 đề xuất **12/10/2026** (ngày làm việc kế tiếp từ ngày lập hồ sơ; chưa có nghĩa pilot đã go-live): D30 = 11/11/2026, D60 = 11/12/2026, D90 = 10/01/2027 (D0 + 90 ngày). Nếu go-live thực tế khác, dời các mốc theo ngày bắt đầu thật. **GO nếu đạt**; FIX tối đa một lần cho cùng vấn đề, nếu lỗi lặp ở cổng sau thì PIVOT hoặc KILL.

| Cổng | Metric duy nhất | Ngưỡng qua | Bằng chứng vật lý cần lưu | Nếu trượt |
|---|---|---|---|---|
| 30 — cổng học, chưa đặt mục tiêu doanh thu | Số partner có pilot ký kết | ≥1 partner | Thỏa thuận pilot đã ký; sơ đồ hành trình end-user hoặc biên bản walkthrough là bằng chứng hỗ trợ, không phải metric thứ hai | FIX quyền truy cập/đường đi một lần; nếu cùng lỗi lặp lại ở D60 thì PIVOT |
| 60 | Số partner đã activation | ≥1 partner có tương tác end-user thật trong 30 ngày | Bản ghi go-live và log hội thoại có timestamp, phân biệt traffic thử nghiệm | Nếu lỗi đường đi đã FIX ở D30 mà lặp lại thì PIVOT; nếu chưa thì FIX một lần |
| 90 | GM tổng của partner pilot | ≥60% trong kỳ 90 ngày [MH; stress B, phải tính lại từ số thật] | Đối soát doanh thu, COGS và rev-share theo partner | Điều chỉnh giá/chi phí bằng PIVOT; KILL nếu unit economics vẫn trượt sau một lần FIX/PIVOT |

**KILL CRITERIA:** Nếu đến D90 = **10/01/2027 theo D0 đề xuất 12/10/2026** số partner activation vẫn là **0** (không partner nào có ≥1 hội thoại end-user thật trong 30 ngày từ go-live), dừng hướng B2B2C qua partner. Đây là lịch kế hoạch, không khẳng định pilot đã bắt đầu; nếu ngày go-live thực tế đổi thì cập nhật D0/D90 tương ứng. Chưa có runway để đặt hạn khác.

**DỮ LIỆU CẦN THU THẬP TRONG PILOT — 9/9 đèn Trạm 1 đang chờ baseline:** (1) activation: danh sách partner/go-live và log end-user thật sau cohort 30 ngày; (2) reach: mẫu số end-user và log khử danh tính sau 2 tuần hoạt động; (3) TTFE: ngày ký/go-live cùng timestamp event đầu; (4) volume volatility: volume/partner/tháng sau ít nhất 3 tháng dữ liệu hoàn chỉnh; (5) GM sau rev-share: F/u thực, hợp đồng rev-share, doanh thu/COGS; (6) inference cost/revenue: cost log và doanh thu theo partner; (7) tập trung volume: log theo partner ID, cần ≥2 partner hoạt động; (8) chất lượng end-user: kết quả/nhãn eval và SLA, ≥100 ca thật; (9) doanh thu/partner, NRR, GM tổng: hợp đồng, hóa đơn, COGS; NRR cần 2 quý gia hạn. D0 kế hoạch là **12/10/2026**; bắt đầu tính các mốc từ go-live thực tế.

<div style="page-break-before: always;"></div>

## Phụ lục — phép tính ngưỡng [MH]

Các số dưới đây lấy từ stress B Day 22, không phải kết quả pilot. Quy đổi dùng cùng workload giả định; phải tính lại bằng doanh thu, COGS và rev-share thực tế theo từng partner.

### 1. Chi phí inference ÷ doanh thu — theo từng partner

Đầu vào tháng stress B: doanh thu **$1.890** (1.400 job × $1,35/job); API + hạ tầng + retry **$53,74**; QA + escalation **$570**; tổng COGS **$623,74**. GM sàn thiết kế **60%**.

- Tỷ lệ inference tại stress B: $53,74 ÷ $1.890 = **2,84%** → mốc xanh.
- Inference tối đa để GM còn 60%, giữ nguyên COGS khác: (1 − 60%) × $1.890 − $570 = **$186**.
- Tỷ lệ trần: $186 ÷ $1.890 = **9,84%** → trên mức này GM xuống dưới sàn 60%.

**Ngưỡng:** 🟢 ≤2,84% · 🟡 >2,84% đến ≤9,84% · 🔴 >9,84%. Stress B tính trên job hoàn thành, còn metric vận hành tính trên hội thoại tính phí; F/u chưa chốt nên đây là guardrail tạm.

### 2. Doanh thu/partner đủ quý

Stress B có COGS **$623,74/tháng**. Tại GM sàn 60%, doanh thu tháng tối thiểu = $623,74 ÷ (1 − 60%) = **$1.559,35**. Giữ workload và COGS đó trong 3 tháng: sàn quý = $1.559,35 × 3 = **$4.678,05**; doanh thu stress B = $1.890 × 3 = **$5.670**.

**Ngưỡng:** 🟢 ≥$5.670/quý · 🟡 $4.678,05 đến <$5.670 · 🔴 <$4.678,05. Giả định COGS thuộc cùng partner, workload ổn định và chưa gồm overhead/rev-share; tính lại khi có số thực.

### 3. GM tổng

GM stress B = ($1.890 − $623,74) ÷ $1.890 × 100% = **67,00%** (làm tròn). Vì vậy 🟢 ≥67% · 🟡 ≥60% đến <67% · 🔴 <60% (sàn thiết kế). Stress chưa gồm overhead, thuế, phí thanh toán, acquisition và rev-share; khi đo thực tế phải tính đủ COGS trực tiếp và rev-share.
