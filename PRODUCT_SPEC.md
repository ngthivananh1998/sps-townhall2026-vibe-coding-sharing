# Salesman Promotion Tracker — Product Specification
_Last updated: 2026-03-31 (v3)_

---

## Tổng quan

Web app quản lý toàn bộ chu trình nâng/hạ bậc Salesman hàng tháng, thay thế quy trình manual qua email, Google Drive và nhiều file Excel rải rác. Mục tiêu: tập trung dữ liệu, tự động hóa thông báo, tạo audit trail rõ ràng và rút ngắn thời gian xử lý.

**Scale:** 1–40 salesman/cycle | **Auth:** Username & Password | **Email:** Google Workspace

---

## Stakeholders & Roles

| Role | Quyền trong app |
|---|---|
| **Root Admin** | Full access, quản lý user accounts |
| **HRBP** | Full access, quản lý user + BGK list, điều phối cycle, set thứ tự trình bày |
| **SFE** | Upload danh sách đầu vào, xem toàn bộ cycle |
| **RSM** | Xem tất cả salesman, điền nomination form |
| **Sales Manager** | Approve/Reject, nhận escalation khi RSM trễ deadline |
| **BU Head (Head of SPS)** | Final approval, ra quyết định cuối cùng |
| **BGK (Judges)** | Chấm điểm interview — 9 người cố định, thay đổi khi có người nghỉ/mới |
| **Salesman (Candidate)** | **Không đăng nhập app** — chỉ nhận email và confirm qua link trong email |
| **C&B** | Nhận export file kết quả |

---

## Hệ thống Bậc Salesman

| Bậc | Tên đầy đủ | Viết tắt | Grade | Loại HĐ |
|-----|-----------|----------|-------|---------|
| 1 | Salesman 1 | SA1 | 0 | HĐ Lao động |
| 2 | Salesman 2 | SA2 | 1 | HĐ Lao động |
| 3 | Salesman 3 | SA3 | 2 | HĐ Lao động |

**Quy tắc:** Nâng/hạ mỗi lần đúng 1 bậc, không skip.

> **Lưu ý:** SA1 hạ bậc = **Terminated** (không có bậc dưới SA1). SA2 hạ về SA1 cần terminate HĐLĐ cũ và ký HĐ mới.

### Điều kiện Nâng bậc
_(Nguồn: 032026_TB KPI & CST SA_SME longtail.docx — Phần V)_

| Tiêu chí | SA1 → SA2 | SA2 → SA3 |
|----------|-----------|-----------|
| Thâm niên tại bậc hiện tại | ≥ 3 tháng | ≥ 3 tháng |
| KPI 3 tháng liên tiếp | **> 600 điểm**/tháng | **> 1,000 điểm**/tháng |
| Nguyện vọng lên bậc | ✓ Bắt buộc | ✓ Bắt buộc |
| RSM đánh giá | Đạt kỳ vọng | Đạt kỳ vọng |
| Hội đồng đánh giá | Đạt kỳ vọng (avg ≥ 3) | Đạt kỳ vọng (avg ≥ 3) |

> **Đơn vị KPI:** điểm (không phải số loa thô) — tính theo loại hình merchant: 3/5/10 điểm/loa tùy nhóm.

### Điều kiện Hạ bậc
_(Nguồn: 032026_TB KPI & CST SA_SME longtail.docx — Phần V)_

| Bậc hiện tại | Ngưỡng KPI | Chu kỳ xét | Ghi chú thêm |
|-------------|-----------|-----------|-------------|
| SA1 (LV1) | < 200 điểm/tháng | — | → **Terminate HĐ** (không hạ bậc) |
| SA2 (LV2) | < 400 điểm/tháng | 2 tháng liên tiếp | Hoặc nguyện vọng cá nhân |
| SA3 (LV3) | < 600 điểm/tháng | 2 tháng liên tiếp | Hoặc nguyện vọng cá nhân |

**Các trường hợp Terminate SA1 thêm:**
- 5 ngày liên tiếp không chạy số (không xin phép/không thông báo quản lý)
- Phát sinh hành vi gian dối/lừa đảo khách hàng

---

## Quy trình Nâng bậc (Happy Path)

```
[SFE] Upload file Excel danh sách đề xuất tháng đó
        ↓
[App] Parse → tạo Cycle, auto-check knock-out conditions
        ↓
[RSM] Nhận notification → điền Nomination Form trong app
      Deadline: trước ngày 5 hàng tháng
      ↓ (nếu RSM trễ → escalate email đến Sales Manager, cycle không bị block)
[RSM] Upload bài thu hoạch của salesman lên app (on behalf)
      Deadline: ≥ 5 ngày làm việc trước ngày interview
      ↓ (nếu chưa nộp → email nhắc CẢ RSM lẫn salesman; salesman không đăng nhập app)
[Sales Manager (kiet.tran2)] Review tổng hợp → Approve / Reject từng case + comment
        ↓
[BU Head (trang.nguyen12)] Endorse trên quyết định của Sales Manager → Final approve
        ↓
[HRBP] Set thứ tự trình bày, assign lịch interview (tuần 2 hàng tháng)
        App tự động gửi cho ứng viên + BGK:
        - Lịch interview, địa điểm/link
        - Link xem bài thu hoạch đã được RSM nộp
        ↓
[BGK - 9 người] Chấm điểm trực tiếp trong app theo scorecard
        Thời gian: 7 phút trình bày | 5 phút Q&A (SA→SA2) / 10 phút Q&A (SA→SA3)
        RSM của ứng viên vẫn chấm nhưng điểm KHÔNG tính vào average cuối
        ↓ (ứng viên vắng mặt → HRBP đánh dấu → auto fail)
[App] Tổng hợp điểm (loại trừ điểm RSM phụ trách):
        - avg ≥ 3 AND < 50% BGK (non-RSM) cho < 3 → "Đạt yêu cầu"
        - avg < 3 OR ≥ 50% BGK (non-RSM) cho < 3 → "Xem xét" / Fail
        ↓
[BU Head] Final decision:
        - Approve → email thông báo Pass → Salesman (kèm link confirm)
        - Reject → email thông báo Trượt → Salesman (kèm link confirm)
        ↓
[Salesman] Click link trong email để xác nhận đồng thuận (không cần đăng nhập app)
           App track: token, thời điểm confirm, trạng thái pending/confirmed
        ↓
[HRBP] Xuất file Excel cho C&B → xác nhận đóng Cycle
```

---

## Quy trình Hạ bậc / Terminate

```
[SFE] Upload danh sách hạ bậc/terminate (cùng file, proposal_type = demote / terminate)
        ↓
[App] Tách danh sách riêng trong Cycle
        ↓
[RSM] Điền form đánh giá hạ bậc (form mới, thiết kế trong Phase 1)
        ↓
[Sales Manager → BU Head] Approve danh sách
        ↓
[App] Gửi email thông báo:
        TO: Salesman liên quan
        CC: RSM, ASM, all SFE, HRBP, BU Head, Sales Manager
        ↓
[Salesman] Click link trong email để xác nhận đồng thuận (không cần đăng nhập app)
        ↓
[HRBP] Xuất file C&B → đóng phần hạ bậc
```

> **SA1 → Terminate:** email thông báo terminate (không phải hạ bậc). Cần track salesman confirm tương tự.

---

## Người dùng hệ thống (Named)

| Username | Tên | Role |
|----------|-----|------|
| trang.nguyen12 | Trang Nguyễn | BU Head (Head of BU SME) |
| kiet.tran2 | Kiệt Trần | Sales Manager |
| vi.dinh | Vi Đinh | SFE Manager |
| anh.nguyen67 | Anh Nguyễn | HRBP |
| _(các domain còn lại)_ | — | RSM |

---

## Hội đồng Đánh giá (BGK)

| Vị trí | Role trong buổi |
|--------|----------------|
| Head of SPS | Chủ tịch, ra quyết định cuối cùng |
| Senior Manager - SME Sales | Đánh giá năng lực bán hàng thực chiến |
| RSMs | Đánh giá năng lực bán hàng thực chiến |
| Đại diện SFE | Kiểm chứng dữ liệu KPI |
| Đại diện HRBP | Điều phối quy trình |

**Tổng 9 người cố định.** Danh sách được HRBP quản lý trong Admin Panel — cập nhật khi có người nghỉ/mới vào.

> **Quy tắc chấm điểm BGK:**
> - RSM chấm điểm cho salesman của **team mình** như bình thường trong app.
> - Tuy nhiên điểm của RSM **không được tính vào điểm trung bình cuối cùng** của ứng viên đó.
> - Điểm RSM vẫn hiển thị để tham khảo và lưu vào audit log.
> - App tự xác định RSM nào là "RSM phụ trách" của ứng viên nào (từ dữ liệu candidates) và loại trừ khi tính average.

---

## Rubric Đánh giá

**Thang điểm:** 1–5 | **Ngưỡng đạt:** 3 (Đạt kỳ vọng) | **Kết quả:** Average điểm tất cả BGK

### Section III — Năng lực thực hiện công việc _(SA1→SA2 và SA2→SA3)_

| # | Tiêu chí | Input |
|---|---------|-------|
| 1 | Hiểu sản phẩm & thông điệp bán hàng | Điểm 1–5 + Minh chứng |
| 2 | Kỹ năng tiếp cận & chốt deal | Điểm 1–5 + Minh chứng |
| 3 | Chăm sóc & giữ chân merchant | Điểm 1–5 + Minh chứng |
| 4 | Tinh thần cầu tiến học hỏi | Điểm 1–5 + Minh chứng |
| 5 | Tinh thần vượt qua khó khăn | Điểm 1–5 + Minh chứng |

Tổng hợp: Điểm tổng hợp | Điểm mạnh | Điểm cần cải thiện | Đánh giá chung

### Section IV — Tiềm năng lãnh đạo _(chỉ SA2→SA3)_

| # | Tiêu chí | Input |
|---|---------|-------|
| 1 | Chủ động hỗ trợ/kèm cặp đồng đội | Điểm 1–5 + Minh chứng |
| 2 | Ảnh hưởng tích cực đến nhóm | Điểm 1–5 + Minh chứng |
| 3 | Giải quyết tình huống phức tạp | Điểm 1–5 + Minh chứng |
| 4 | Tinh thần trách nhiệm với kết quả chung | Điểm 1–5 + Minh chứng |

Tổng hợp: Điểm tổng hợp | Điểm mạnh | Điểm cần cải thiện | Đánh giá chung

---

## RSM Nomination Form — Cấu trúc

1. **Header:** Tên RSM, Domain, Chức danh | Tên salesman được đề cử
2. **Section I:** Ngày gia nhập, Chức danh được nâng, Khu vực
3. **Section II:** KPI 3 tháng (T / T+1 / T+2): Target vs Thực đạt _(SFE đã upload sẵn, RSM confirm/bổ sung)_
4. **Section III:** 5 tiêu chí năng lực
5. **Section IV:** 4 tiêu chí tiềm năng _(chỉ hiện khi proposed_level = SA3)_
6. **Section V:** Kế hoạch phát triển sau nâng bậc (năng lực ưu tiên + phương thức đào tạo)

---

## Cấu trúc File Excel Đầu vào (Chuẩn hóa)

> Chi tiết đầy đủ + auto-validation rules + export format: [development_specs/input-file-format.md](development_specs/input-file-format.md)

Đề xuất **1 sheet cố định** tên `INPUT`, thay thế format hiện tại để app parse ổn định:

| Cột | Tên cột | Bắt buộc | Ghi chú |
|-----|---------|----------|---------|
| A | emp_id | ✓ | Mã nhân viên |
| B | full_name | ✓ | Họ tên đầy đủ |
| C | email | ✓ | Email công ty |
| D | current_level | ✓ | SA1 / SA2 / SA3 |
| E | proposal_type | ✓ | promote / demote |
| F | proposed_level | ✓ | SA1 / SA2 / SA3 |
| G | rsm_name | ✓ | Tên RSM |
| H | rsm_email | ✓ | Email RSM |
| I | asm_name | | Tên ASM |
| J | asm_email | | Email ASM |
| K | domain | ✓ | Khu vực/Domain |
| L | onboarding_date | ✓ | Ngày gia nhập (dd/mm/yyyy) |
| M | tenure_months | ✓ | Số tháng tại bậc hiện tại |
| N | kpi_month1_target | ✓ | KPI target tháng T (điểm) |
| O | kpi_month1_actual | ✓ | KPI thực đạt tháng T (điểm) |
| P | kpi_month2_target | ✓ | KPI target tháng T+1 (điểm) |
| Q | kpi_month2_actual | ✓ | KPI thực đạt tháng T+1 (điểm) |
| R | kpi_month3_target | ✓ | KPI target tháng T+2 (điểm) |
| S | kpi_month3_actual | ✓ | KPI thực đạt tháng T+2 (điểm) |
| T | aspiration | ✓ | Nguyện vọng lên bậc: yes / no |

> **Đơn vị KPI:** điểm (merchant type × số loa: 3/5/10 điểm/loa).

App sẽ **auto-validate** khi parse:
- Knock-out tenure: < 3 tháng
- Knock-out KPI (promote): SA1 cần > 600đ/tháng × 3 tháng; SA2 cần > 1,000đ/tháng × 3 tháng
- Knock-out aspiration: aspiration ≠ yes
- Terminate flag: SA1 có KPI < 200đ (flag riêng, không block cycle)

---

## Database Schema (sơ bộ)

> Full schema với RLS policies và computed logic: [development_specs/database-schema.md](development_specs/database-schema.md)

```sql
-- Người dùng hệ thống
users (
  id, name, email, password_hash,
  role,         -- 'admin' | 'hrbp' | 'sfe' | 'rsm' | 'sales_manager' | 'bu_head' | 'judge' | 'candidate'
  is_active, created_at
)

-- Chu kỳ đánh giá hàng tháng
cycles (
  id, month, year,
  status,       -- 'draft' | 'rsm_review' | 'approval' | 'interview' | 'decision' | 'closed'
  rsm_deadline, -- ngày 5 hàng tháng
  interview_date,
  created_by, created_at
)

-- Danh sách ứng viên trong cycle
candidates (
  id, cycle_id, emp_id, full_name, email,
  current_level,   -- 'SA1' | 'SA2' | 'SA3'
  proposal_type,   -- 'promote' | 'demote'
  proposed_level,
  rsm_id, asm_name, asm_email, domain,
  onboarding_date, tenure_months,
  kpi_t1_target, kpi_t1_actual,
  kpi_t2_target, kpi_t2_actual,
  kpi_t3_target, kpi_t3_actual,
  knockout_passed bool,      -- auto-computed on upload
  pool_limit_ok bool,        -- auto-computed on upload
  presentation_order int,    -- HRBP set
  status,                    -- 'pending_nomination' | 'nominated' | 'approved' | 'rejected' | 'interview_pending' | 'submitted' | 'absent' | 'scored' | 'passed' | 'failed' | 'closed'
  is_absent bool default false
)

-- Nomination form của RSM (promote)
rsm_nominations (
  id, candidate_id, rsm_id,
  -- Section III: 5 competency criteria
  comp_1_score smallint, comp_1_evidence text,
  comp_2_score smallint, comp_2_evidence text,
  comp_3_score smallint, comp_3_evidence text,
  comp_4_score smallint, comp_4_evidence text,
  comp_5_score smallint, comp_5_evidence text,
  comp_summary_score decimal, comp_strengths text,
  comp_improvements text, comp_overall text,
  -- Section IV: leadership (nullable, SA2→SA3 only)
  lead_1_score smallint, lead_1_evidence text,
  lead_2_score smallint, lead_2_evidence text,
  lead_3_score smallint, lead_3_evidence text,
  lead_4_score smallint, lead_4_evidence text,
  lead_summary_score decimal, lead_strengths text,
  lead_improvements text, lead_overall text,
  -- Section V: development plan
  training_priority text, training_method text,
  status,         -- 'draft' | 'submitted'
  submitted_at
)

-- Form đánh giá hạ bậc của RSM (demote) — thiết kế mới
rsm_demotion_assessments (
  id, candidate_id, rsm_id,
  reason text,             -- lý do hạ bậc
  evidence text,           -- minh chứng KPI
  rsm_recommendation text, -- đề xuất hướng xử lý
  status,                  -- 'draft' | 'submitted'
  submitted_at
)

-- Approval flow
approvals (
  id, candidate_id, approver_id,
  role,       -- 'sales_manager' | 'bu_head'
  decision,   -- 'approve' | 'reject'
  comment text, decided_at
)

-- Interview sessions
interviews (
  id, cycle_id,
  scheduled_at, location_or_link,
  submission_deadline,
  judge_ids int[],          -- array of user IDs (BGK)
  created_by
)

-- Bài thu hoạch (RSM nộp thay salesman)
submissions (
  id, candidate_id, interview_id,
  file_url, file_name, file_size,
  submitted_by,   -- rsm_id (RSM nộp thay)
  submitted_at
)

-- Chấm điểm của từng BGK
scores (
  id, candidate_id, judge_id,
  -- Section III: 5 criteria (1-5)
  comp_1 smallint, comp_2 smallint, comp_3 smallint,
  comp_4 smallint, comp_5 smallint,
  comp_average decimal,
  -- Section IV: leadership (nullable, SA2→SA3 only)
  lead_1 smallint, lead_2 smallint,
  lead_3 smallint, lead_4 smallint,
  lead_average decimal,
  -- Overall
  total_average decimal,
  vote,       -- 'pass' | 'fail'
  notes text,
  scored_at
)

-- Kết quả tổng hợp
results (
  id, candidate_id,
  avg_score decimal,          -- tính từ non-RSM judges only
  rsm_score decimal,          -- điểm RSM (lưu riêng, không tính vào avg)
  pass_votes int, fail_votes int,
  counted_judges int,         -- tổng BGK được tính (không kể RSM)
  classification,             -- 'dat_yeu_cau' | 'xem_xet' | 'fail'
  bu_head_decision,           -- 'approve' | 'reject'
  effective_date date,
  decided_at
)

-- Xác nhận đồng thuận của Salesman
candidate_confirmations (
  id, candidate_id,
  decision_type,              -- 'promote' | 'demote' | 'terminate'
  outcome,                    -- 'pass' | 'fail'
  email_sent_at,
  confirmed_at,               -- null nếu chưa confirm
  confirmation_token,         -- token trong link email
  status                      -- 'pending' | 'confirmed'
)

-- Email templates (pre-built, editable by Admin/HRBP)
email_templates (
  id, type, subject_template, body_template, updated_at
)
-- types: 'rsm_invite' | 'rsm_escalation' | 'approval_request' | 'interview_invite'
--        | 'submission_reminder' | 'result_pass' | 'result_fail' | 'demotion_notify'
--        | 'cb_handoff'

-- Log thông báo đã gửi
notifications (
  id, recipient_id, template_type,
  subject, body, sent_at, status   -- 'sent' | 'failed'
)
```

---

## Màn hình & Tính năng

### 1. Dashboard
- Cycle hiện tại + status bar timeline (% hoàn thành từng bước)
- Thẻ tóm tắt: tổng đề xuất / promote / demote / pending / done
- **My Actions**: việc cần làm của user đang đăng nhập (role-aware)
- Recent activity feed

### 2. Cycle Management

**Upload & Parse (SFE)**
- Upload `.xlsx` (sheet `INPUT`), preview bảng parsed data
- Auto-validate: highlight knock-out failures + nomination pool violations
- Confirm → tạo Cycle, gửi notification cho RSM

**RSM Nomination Form**
- Danh sách tất cả salesman trong cycle (promote + demote)
- Tab promote: form đầy đủ Section I–V
  - Section IV chỉ hiển thị khi `proposed_level = SA3`
  - KPI data từ file upload hiện sẵn, RSM confirm + điền điểm/minh chứng
- Tab demote: form đánh giá hạ bậc
- Save draft / Submit | Deadline countdown

**Approval Flow**
- Sales Manager: list + summary nomination, approve/reject + comment từng case
- BU Head: list đã qua Manager, batch approve hoặc từng case
- Audit timeline per case (ai làm gì lúc nào)

### 3. Interview Module (HRBP)

- Tạo interview session: ngày giờ, địa điểm/link, assign BGK (từ danh sách 9 người)
- Set thứ tự trình bày (drag & drop hoặc số thứ tự)
- Gửi invitation tự động (in-app + email) đến ứng viên + BGK
- **RSM upload bài thu hoạch** thay mặt salesman (PDF/PPTX, max 50MB)
- Deadline: **≥ 5 ngày làm việc trước ngày interview**
- Email reminder -48h tự động → gửi đến RSM + salesman (email only)
- HRBP đánh dấu vắng mặt → auto fail (không cần BGK chấm)

**Scorecard (BGK)**
- Mỗi BGK thấy danh sách ứng viên của mình
- Form chấm: Section III (tất cả) + Section IV (nếu SA2→SA3)
- Điểm RSM phụ trách được hiển thị riêng, có label "RSM score (not counted)"
- Điểm tính tự động từ non-RSM judges; classification hiện sau khi đủ BGK submit

### 4. Notifications & Emails

| Trigger | Gửi đến | Kênh |
|---------|---------|------|
| Cycle tạo | RSM | In-app + Email |
| RSM sắp trễ deadline nomination (T-2 ngày) | RSM | Email |
| RSM trễ deadline nomination (ngày 5) | Sales Manager | Email (escalation) |
| Đến lượt approve | Sales Manager / BU Head | In-app + Email |
| Interview được tạo | BGK | In-app + Email |
| Deadline nộp bài thu hoạch -48h _(≥5 ngày làm việc trước interview)_ | RSM + Salesman (email only) | Email |
| Chưa nộp bài sau deadline | RSM + Salesman (email only) | Email (nhắc lần 2) |
| Kết quả pass | Salesman (email only) | Email + link confirm đồng thuận |
| Kết quả fail (BU Head reject) | Salesman (email only) | Email + link confirm đồng thuận |
| Hạ bậc / Terminate approved | TO: Salesman / CC: RSM, ASM, all SFE, HRBP, BU Head, Sales Manager | Email + link confirm đồng thuận |
| Salesman chưa confirm sau X ngày | HRBP | In-app reminder |
| File C&B sẵn sàng | HRBP | In-app |

**Email:** Templates có sẵn, lưu trong DB, HRBP/Admin chỉnh sửa được.

### 5. Export

- **File C&B (promote):** Excel — Mã NV, Họ tên, Bậc cũ, Bậc mới, Ngày hiệu lực
- **File C&B (demote):** Excel — Mã NV, Họ tên, Bậc cũ, Bậc mới, Lý do, Ngày hiệu lực
- **Nomination form PDF:** Export từng form RSM ra PDF để lưu hồ sơ
- **Báo cáo cycle:** Tổng hợp kết quả toàn bộ (Excel)

### 6. Admin Panel (Root Admin + HRBP)

- Quản lý user: tạo / deactivate / đổi role
- Quản lý danh sách BGK (9 người, cập nhật khi có thay đổi)
- Cấu hình deadline mặc định (ngày RSM nộp, tuần assessment)
- Quản lý email templates (xem/sửa subject + body)

---

## Tech Stack

| Layer | Công nghệ |
|---|---|
| Frontend | Next.js 14 (App Router), Tailwind CSS, shadcn/ui |
| Forms | React Hook Form + Zod |
| Backend | Next.js API Routes |
| Database | Supabase (PostgreSQL + Row Level Security) |
| Auth | Supabase Auth — email/password, JWT, RLS tích hợp DB |
| File storage | Supabase Storage |
| File parsing | SheetJS (xlsx) |
| Email | Gmail API (Google Workspace) |
| Deployment | Vercel + Supabase |

**Frontend brand:** MoMo Brand Guidelines — internal tool variant. Primary color `#A50064` (Hồng +2), font MoMo Trust Sans/Display.

→ Chi tiết: [development_specs/tech-stack.md](development_specs/tech-stack.md)
→ Frontend guide + MoMo brand tokens: [development_specs/frontend-guide.md](development_specs/frontend-guide.md)
→ Database schema đầy đủ: [development_specs/database-schema.md](development_specs/database-schema.md)
→ Input file format: [development_specs/input-file-format.md](development_specs/input-file-format.md)

---

## Phân kỳ phát triển

### Phase 1 — Core Cycle (4–6 tuần)
- [ ] Auth (login, role-based routing)
- [ ] Upload & parse Excel, validate knock-out + nomination pool
- [ ] RSM Nomination Form — promote (Section I–V)
- [ ] RSM Demotion Assessment Form — thiết kế mới
- [ ] Approval flow: Sales Manager → BU Head
- [ ] Interview module: tạo session, set thứ tự, upload bài, đánh dấu vắng mặt
- [ ] BGK Scorecard, tổng hợp điểm tự động
- [ ] BU Head final decision
- [ ] Email notifications (templates sẵn có) + in-app
- [ ] Export file C&B (promote + demote)
- [ ] Admin: quản lý user + BGK list + email templates

### Phase 2 — Polish & Automation (3–4 tuần)
- [ ] Dashboard analytics (trend, pass/fail rate, thời gian xử lý)
- [ ] Export báo cáo cycle (Excel full + PDF nomination form)
- [ ] Lịch sử nhiều cycle
- [ ] Notification center in-app (inbox)
- [ ] Nomination pool warning khi SFE upload vượt giới hạn

### Phase 3 — Optimization (2–3 tuần)
- [ ] Mobile-responsive cho BGK chấm điểm tại buổi interview
- [ ] Bulk actions (approve all, export all)
- [ ] Audit log export

---

_Không còn câu hỏi mở. Spec đã đủ để bắt đầu build._
