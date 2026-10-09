# OPERATING DASHBOARD — Trợ lý AI tư vấn tuyển sinh ngoài giờ

**Mô hình:** B2B2C · **Cập nhật:** 09/10/2026 · Nguyễn Ngọc Linh — 2A202602480
**NORTH STAR:** Partner activation rate · hiện tại/mục tiêu: [CHƯA CÓ DỮ LIỆU].
**Trạng thái:** Chưa có pilot/baseline được ghi nhận; mọi đèn hiện là **chưa đo**, không gán màu. Ngưỡng dưới đây là vùng quyết định, không phải trạng thái hiện tại.

### Leading — hằng ngày/tuần

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 · nguồn | Báo trước cho |
|---|---|---|---|
| Partner activation rate | Chưa đo | ≥60% / 30–<60% / <30% [TB; §3.3 starter, baseline sau 2 cohort 30 ngày] | Billable conversations/partner (O) |
| End-user reach trong partner | Chưa đo | ≥B / <B trong 1 tuần / <B trong 2 tuần liền; B = baseline 2 tuần đầu có end-user thật [TB] | Số hội thoại tính phí/partner (O) |

### Operating — tuần/tháng

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 · nguồn | Báo trước cho |
|---|---|---|---|
| Số hội thoại tính phí/partner | Chưa đo | ≥V̄ / <V̄ 1 tuần / <V̄ 2 tuần liền; V̄ = TB 2 tuần đầu có tính phí [TB] | Doanh thu/partner (G) |
| Chi phí inference ÷ doanh thu — theo TỪNG partner | Chưa đo | ≤2,84% / >2,84–9,84% / >9,84% [MH; stress B, cần kiểm chứng bằng giá/chi phí thật] | GM tổng (G) |
| Chất lượng nhìn từ end-user (tỷ lệ hội thoại đạt eval) | Chưa đo | ≥Q̄, không lỗi nghiêm trọng / <Q̄ một chu kỳ / ≥1 lỗi nghiêm trọng hoặc <Q̄ 2 chu kỳ liền [TB; Q̄ = baseline] | Partner NRR (G) |

### Lagging — quý

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 · nguồn |
|---|---|---|
| Doanh thu/partner (đủ quý) | Chưa đo | ≥$5.670 / $4.678,05–<5.670 / <$4.678,05 [MH; stress B, chưa phải doanh thu thực] |
| Partner NRR | Chưa đo | ≥max(100%, Bₙ) / ≥100% và <max(100%, Bₙ) / <100%; Bₙ = baseline 2 quý gia hạn [TB] |
| GM tổng | Chưa đo | ≥67% / 60–<67% / <60% [MH; stress B, chưa gồm overhead/thuế/thanh toán/acquisition/rev-share] |

### 5 luật quyết định (⏹ = dừng)

1. **⏹ NẾU** Partner activation rate <30% trong 2 cohort 30 ngày liền **VÀ** ≥5 partner đủ kỳ quan sát, **THÌ** Partnerships/PartnerOps dừng ký mới, tuần làm việc kế tiếp kích hoạt partner hiện có; **KHÔNG THÌ** không tính chữ ký là tăng trưởng.
2. **NẾU** End-user reach trong partner <B 2 tuần liền **VÀ** cùng mẫu số đủ điều kiện đã ghi nhận, **THÌ** Partner Ops thử CTA trên Facebook Page, đo lại tuần sau; **KHÔNG THÌ** không làm tính năng trước khi thử phân phối.
3. **NẾU** Số hội thoại tính phí/partner <V̄ 2 tuần liền, **THÌ** Product/Data Ops đối soát event theo conversation_id/24h, sửa điểm rơi trước tuần sau; **KHÔNG THÌ** không thêm partner chưa kích hoạt để che volume thấp.
4. **⏹ NẾU** Chi phí inference ÷ doanh thu — theo TỪNG partner >9,84% trong 2 tháng chốt liền **VÀ** cả hai tháng có doanh thu dương, **THÌ** AI Ops/Finance đóng băng mở rộng AI, đặt cap usage/giá trước khi mở lại; **KHÔNG THÌ** không tăng volume để che tỷ lệ đỏ.
5. **⏹ NẾU** ≥1 lỗi nghiêm trọng tuyển sinh/học phí/hạn chót ở bất kỳ eval nào **HOẶC** tỷ lệ hội thoại đạt eval <Q̄ trong 2 chu kỳ với tổng ≥100 ca thật, **THÌ** QA và đầu mối tuyển sinh partner dừng auto-reply nhóm câu hỏi đó, chuyển người thật, sửa KB đã duyệt; **KHÔNG THÌ** không hạ rubric hay giấu handoff.

### Cổng gác 90 ngày

Ngày tính từ D0; **GO nếu đạt**. FIX tối đa một lần cho cùng vấn đề; nếu vấn đề đó trượt lại ở cổng sau thì PIVOT hoặc KILL.

| Cổng | Metric duy nhất | Ngưỡng qua | Bằng chứng vật lý cần lưu | Nếu trượt |
|---|---|---|---|---|
| 30 — học, không đặt doanh thu | Số partner có pilot đã ký và end-user path được xác nhận | ≥1 partner/path; path nêu rõ bước end-user | Thỏa thuận pilot + sơ đồ hành trình/xác nhận walkthrough | FIX quyền truy cập/path một lần; nếu lặp ở D60: PIVOT |
| 60 | Số partner activation | ≥1 partner có tương tác thật của end-user trong 30 ngày | Go-live record + log hội thoại có timestamp, loại test | PIVOT nếu đã FIX cùng lỗi path ở D30; nếu chưa, FIX một lần |
| 90 | GM tổng của partner pilot | ≥60% trong kỳ 90 ngày [MH; stress B, phải tính lại từ số thật] | Đối soát doanh thu, COGS và rev-share theo partner | PIVOT giá/chi phí; KILL nếu cùng giả thuyết unit economics vẫn trượt sau một lần FIX/PIVOT |

**KILL CRITERIA:** Nếu đến D90 số partner activation là **0** (không partner nào có ≥1 hội thoại end-user thật trong 30 ngày từ go-live), dừng hướng B2B2C qua partner; ngày lịch đánh giá = **[CẦN LINH XÁC NHẬN: ngày D0 để chốt ngày D90]**. Chưa có runway để đặt hạn khác.

**CHƯA ĐO ĐƯỢC — 9/9 đèn Trạm 1 đều 🔧:** (1) activation: danh sách partner/go-live + log user thật, sau cohort 30 ngày; (2) reach: mẫu số end-user + log đã khử danh tính, sau 2 tuần hoạt động; (3) TTFE: ngày ký/go-live + timestamp event đầu, sau pilot đầu; (4) volume volatility: volume/partner/tháng, sau nhiều tháng [chưa có lịch]; (5) GM sau rev-share: F/u thực, hợp đồng rev-share, doanh thu/COGS; (6) inference cost/revenue: log cost và doanh thu theo partner; (7) tập trung volume: log theo partner ID, cần ≥2 partner hoạt động; (8) chất lượng end-user: kết quả/nhãn eval và SLA, ≥100 ca thật; (9) doanh thu/partner, NRR, GM tổng: hợp đồng, hóa đơn, COGS; NRR cần 2 quý gia hạn. Pilot/go-live và ngày có số: **[CẦN LINH XÁC NHẬN: ngày bắt đầu pilot]**.
