# Vibe Coding: Từ Zero Technical đến Deploy Product

> **"Tôi không biết code. Nhưng tôi đã build và deploy một app."**

---

# PHẦN 1: VIBE CODING LÀ GÌ & TẠI SAO BẠN NÊN QUAN TÂM

## Định nghĩa Vibe Coding

Vibe Coding = **Bạn mô tả điều bạn muốn bằng ngôn ngữ tự nhiên, AI viết code cho bạn.**

Bạn không cần:
- Học ngôn ngữ lập trình
- Hiểu cấu trúc dữ liệu
- Biết framework hay library

Bạn CHỈ cần:
- **Biết mình muốn gì**
- **Biết cách diễn đạt**
- **Kiên nhẫn thử và sai**

## Ai có thể vibe code?

**Bất kỳ ai không biết code** — HR, Marketing, Sales, Designer, Founder, Giáo viên, Sinh viên...

Bạn chỉ cần:
- Có một vấn đề muốn giải quyết (hoặc ý tưởng muốn thử)
- Biết dùng máy tính cơ bản
- Kiên nhẫn nói chuyện với AI

> **Ví dụ cá nhân:** Tôi là HR, zero background technical. Và tôi đã build + deploy một app hoàn chỉnh.

## Lợi ích cụ thể

| Lợi ích | Giải thích |
|---------|-----------|
| **Tự chủ hoàn toàn** | Không cần chờ dev, không cần xin budget, không cần viết ticket rồi chờ 2 sprint |
| **Chi phí gần $0** | AI tool ~$20/tháng, hosting miễn phí — rẻ hơn thuê freelancer 100 lần |
| **Tốc độ nhanh** | Từ ý tưởng đến app chạy được trong vài ngày, không phải vài tháng |
| **Validate ý tưởng** | Thay vì nói "tôi có ý tưởng", bạn show "đây là app tôi đã làm" |

---

# PHẦN 2: HÀNH TRÌNH HỌC TẬP — TỪ MÙ CODE ĐẾN SHIP PRODUCT

> **Phần này kể câu chuyện thật của bạn. Càng thật, càng "fail", càng hấp dẫn.**

## Timeline cá nhân

```
Ngày 0: "AI code được hả? Thử xem"
        → Lên ChatGPT / YouTube research
        → "Giờ vibe code ổn nhất tôi nên xài tool gì?"
        → Claude Code
    ↓
Ngày 1: Mở Claude Code lần đầu. Gõ prompt đầu tiên. Wow, nó tạo code thật!
    ↓
Ngày 2: Hào hứng → Gặp lỗi → Hoảng → Copy lỗi paste lại → AI fix → Phấn khởi lại
    ↓
Ngày 3: Bắt đầu hiểu "flow": mô tả → review → chỉnh sửa → repeat
    ↓
Ngày 4: App chạy được trên máy. Nhờ AI deploy Vercel. Có link thật!
    ↓
Bây giờ: Đứng đây sharing cho mọi người 😄
```

## Những cột mốc quan trọng

| Cột mốc | Cảm xúc lúc đó | Bài học |
|---------|----------------|---------|
| Research tool nào xài | "Nhiều quá, chọn gì đây?" | Không cần chọn đúng nhất, chọn cái bắt đầu được ngay |
| Lần đầu thấy AI tạo code | "Ảo thật sự" | AI mạnh hơn mình tưởng |
| Lần đầu gặp lỗi không hiểu | "Chắc mình không làm được" | Bình tĩnh, copy lỗi, paste lại cho AI |
| Lần đầu tự fix được (nhờ AI) | "Mình cũng debug được!" | Kiên nhẫn = skill quan trọng nhất |
| Lần đầu có người khác dùng thử | "Nó thật sự hoạt động!" | Ship sớm, đừng chờ hoàn hảo |
| Lần đầu thấy app trên link thật | "Wow, mình làm được thật" | Deploy không khó như mình tưởng |

## Tâm lý qua từng giai đoạn

```
Hào hứng → Bối rối → Nản → "Thử thêm 1 lần nữa" → Ồ, được rồi! → Hào hứng lại → Lặp lại...
```

> **Key insight:** Vibe coding không phải đường thẳng lên. Nó là **American rollercoaster**.
> Điều quan trọng là đừng bỏ cuộc ở đáy.

---

# PHẦN 3: CÁC BƯỚC & CÔNG CỤ

## Tổng quan công cụ

| Công cụ | Vai trò | Ghi chú |
|---------|---------|---------|
| **Claude Code** | AI assistant — "developer" của bạn | Dùng để brainstorm, code, fix bug, deploy |
| **VS Code** | Text editor — nơi xem và chỉnh code | Không cần hiểu code, chỉ cần mở file AI tạo |
| **GitHub** | Lưu trữ code | Giống Google Drive nhưng cho code |
| **Vercel** | Deploy frontend | Kéo thả, miễn phí |
| **Railway** | Deploy backend + database | Đơn giản, có free tier |
| **Trình duyệt** | Test app | Chrome, Edge... cái gì cũng được |

> **Bạn không cần thành thạo tất cả.** AI sẽ hướng dẫn bạn dùng từng tool khi cần.

---

## Bước 1: Brainstorming — Từ ý tưởng mơ hồ đến Product Spec

> **Mục tiêu:** Có một file Product Spec (`.md`) rõ ràng, chi tiết — làm "hợp đồng" giữa bạn và AI trước khi bắt tay vào code.

### 1.1 Bắt đầu bằng câu hỏi — Hỏi chính mình

Trước khi mở AI, dành 15-30 phút tự hỏi:

| Câu hỏi | Tại sao quan trọng |
|----------|-------------------|
| Vấn đề tôi đang gặp là gì? | Không có vấn đề = không có app |
| Tôi đang giải quyết cho ai? (mình, team, khách hàng?) | Quyết định mức độ phức tạp |
| Hiện tại người ta giải quyết vấn đề này bằng cách nào? | Biết đối thủ / giải pháp hiện tại |
| Nếu chỉ được 1 tính năng duy nhất, đó là gì? | Tránh lan man, tập trung core value |
| App nào trên thị trường giống ý tưởng của tôi? | Có reference = mô tả dễ hơn 10 lần |

> **Tip:** Lúc này bạn chưa cần biết "app" là gì. Chỉ cần biết **vấn đề** là gì.

### 1.2 Nhờ AI đặt ngược câu hỏi lại cho bạn

Đây là **bí kíp quan trọng nhất**. Thay vì cố gắng mô tả mọi thứ từ đầu, hãy nói với AI:

```
Tôi có ý tưởng muốn làm một app quản lý công việc cho team HR.
Tôi chưa biết cụ thể cần gì. Hãy đặt cho tôi 10-15 câu hỏi
để hiểu rõ hơn về app tôi muốn build, bao gồm: đối tượng người dùng,
tính năng, giao diện, quy mô, và bất kỳ thứ gì cần thiết
để bạn có thể giúp tôi tạo ra nó.
```

AI sẽ hỏi ngược lại những câu như:
- "App này dùng trên web hay mobile?"
- "Bao nhiêu người sẽ dùng cùng lúc?"
- "Có cần đăng nhập / phân quyền không?"
- "Dữ liệu có nhạy cảm không? Cần bảo mật đến mức nào?"
- "Bạn muốn phong cách giao diện như thế nào? Có app nào bạn thích giao diện của nó?"

> **Tại sao cách này hiệu quả?**
> Vì bạn **không biết mình không biết gì**. AI biết những câu hỏi cần hỏi mà bạn chưa nghĩ tới.
> Giống như đi khám bác sĩ — bác sĩ hỏi bạn, không phải bạn tự chẩn đoán.

### 1.3 Trả lời và đào sâu — Qua nhiều vòng

Đừng cố trả lời hoàn hảo. Trả lời theo kiểu:
- "Tôi nghĩ là..." (chưa chắc cũng ok)
- "Tôi chưa biết, bạn gợi ý đi" (để AI suggest)
- "Giống như Notion nhưng đơn giản hơn" (tham chiếu app khác)

AI sẽ hỏi tiếp, bạn trả lời tiếp. **Lặp lại 2-3 vòng** cho đến khi cả hai đều rõ.

Ví dụ một vòng hội thoại:

```
AI:  "Bạn muốn quản lý task theo dạng list hay kanban board?"
Bạn: "Kanban board là gì?"
AI:  "Kanban là dạng cột như Trello — ví dụ: To Do | Doing | Done..."
Bạn: "À hay đấy, tôi muốn dạng đó!"
```

> **Không có câu hỏi nào là ngu cả.** Hỏi càng nhiều, spec càng rõ.

### 1.4 Nhờ AI tổng hợp thành Product Spec

Sau khi hỏi-đáp đủ rồi, nói với AI:

```
Dựa trên tất cả thông tin tôi đã cung cấp, hãy tạo cho tôi một
Product Spec hoàn chỉnh dưới dạng file markdown, bao gồm:

1. Tổng quan sản phẩm (product overview)
2. Đối tượng người dùng (target users)
3. Danh sách tính năng chi tiết (features), chia theo MVP và Nice-to-have
4. Mô tả giao diện từng màn hình chính (UI description)
5. Yêu cầu kỹ thuật cơ bản (tech stack gợi ý)
6. Những thứ KHÔNG nằm trong scope (out of scope)
```

AI sẽ tạo ra một file `.md` hoàn chỉnh — đây chính là **bản thiết kế** của app bạn.

### 1.5 Review và chốt spec

Đọc lại Product Spec, hỏi bản thân:
- Có đúng ý mình không?
- Có thiếu gì không?
- Có cái nào quá phức tạp, cần bỏ bớt không?

Chỉnh sửa lần cuối với AI:

```
Sửa lại giúp tôi:
- Bỏ tính năng chat, chưa cần thiết
- Thêm: cho phép export task ra Excel
- MVP chỉ cần 3 tính năng chính thôi, còn lại để phase 2
```

### Kết quả: Product Spec hoàn chỉnh

```markdown
# Product Spec: HR Task Manager

## Tổng quan
App quản lý công việc cho team HR, dạng kanban board...

## Target Users
- HR team 5-10 người
- Không cần kiến thức kỹ thuật để sử dụng

## MVP Features
- [ ] Tạo, sửa, xóa task
- [ ] Kéo thả task giữa các cột (To Do → Doing → Done)
- [ ] Gán task cho thành viên
- [ ] Đặt deadline + cảnh báo quá hạn

## Nice-to-have (Phase 2)
- [ ] Export Excel
- [ ] Dashboard thống kê
- [ ] Tích hợp Google Calendar

## Out of Scope
- Chat / messaging
- Mobile app
- Đa ngôn ngữ
```

> **Tại sao phải làm spec trước?**
>
> Không có spec = bạn sẽ thay đổi ý liên tục = AI code đi code lại = mất thời gian gấp 3-5 lần.
>
> Có spec = bạn chỉ cần nói "code theo spec này" = AI hiểu ngay, làm đúng ngay.

---

## Bước 2: Code — Nói chuyện với AI để build app

### Vòng lặp cơ bản

```
Bạn gửi spec / mô tả yêu cầu
    ↓
AI viết code
    ↓
Bạn chạy app, xem kết quả
    ↓
Chưa ưng? → Mô tả lại / điều chỉnh
    ↓
Ưng rồi? → Chuyển sang tính năng tiếp
```

### Ví dụ hội thoại thật

**Lần 1 — Khởi động:**

> "Hãy đọc file product-spec.md và code app theo đúng spec đó"

→ AI tạo ra toàn bộ cấu trúc project, code frontend, code backend, database.

**Lần 2 — Thấy giao diện chưa đẹp:**

> "Giao diện chưa đẹp lắm. Tôi muốn nó modern hơn, có màu gradient, có animation khi thêm task"

→ AI cập nhật CSS, thêm animation.

**Lần 3 — Phát hiện lỗi:**

> "Khi tôi thêm task xong, danh sách không tự cập nhật. Phải refresh trang mới thấy"

→ AI fix bug, thêm logic tự động refresh.

**Lần 4 — Muốn thêm tính năng:**

> "Tôi muốn có thể đặt deadline cho mỗi task, và task nào quá hạn thì hiện màu đỏ"

→ AI thêm trường deadline, logic so sánh ngày, styling màu đỏ.

### Những lúc bế tắc & cách xử lý

| Tình huống | Cách xử lý |
|------------|-------------|
| AI tạo code nhưng chạy bị lỗi | Copy **toàn bộ lỗi**, paste lại cho AI: "Tôi gặp lỗi này, fix giúp tôi" |
| Không hiểu AI đang nói gì | "Giải thích cho tôi như tôi 5 tuổi" hoặc "Giải thích không dùng thuật ngữ technical" |
| Kết quả không đúng ý | Mô tả lại cụ thể hơn, hoặc gửi screenshot: "Tôi muốn nó trông giống thế này, không phải thế kia" |
| Loay hoay mãi không fix được | Dừng lại, nghỉ ngơi, quay lại với đầu óc tỉnh táo. Hoặc thử hỏi cách khác |
| AI quên context / làm sai | Copy lại spec, nhắc lại: "Đọc lại spec, phần X bạn làm chưa đúng" |

### Mindset quan trọng

> **Bạn là Product Manager. AI là Developer.**
>
> Việc của bạn KHÔNG phải là code.
> Việc của bạn là: biết mình muốn gì, mô tả rõ ràng, và review kết quả.

---

## Bước 3: Test — Kiểm tra sản phẩm

### Tự mình dùng thử

- Mở app lên, thử TỪNG tính năng
- Thử những trường hợp "lạ": nhập text rất dài, để trống, click liên tục
- Ghi lại những chỗ lỗi hoặc chưa ưng

### Nhờ người khác dùng thử

- Gửi cho bạn bè / đồng nghiệp
- Quan sát họ dùng: họ bối rối ở đâu? Click sai ở đâu?
- Thu thập feedback → quay lại nói chuyện với AI để fix

### Ví dụ feedback thật

> "Ê, tao thêm task mà không thấy nút xóa ở đâu"
> → Bạn nói với AI: "Thêm nút xóa rõ ràng hơn, đặt bên phải mỗi task, icon thùng rác"

---

## Bước 4: Deploy — Đưa app lên internet

### Deploy là gì?

Hiểu đơn giản: **Biến app từ "chạy trên máy mình" thành "ai cũng truy cập được qua link".**

### Các bước (vẫn nhờ AI)

1. **Hỏi AI:** "Giúp tôi deploy app này lên internet"
2. AI sẽ hướng dẫn từng bước:
   - Tạo tài khoản trên platform (Vercel, Railway, Render,...)
   - Push code lên GitHub
   - Kết nối và deploy
3. **Kết quả:** Bạn có một URL thật, gửi cho ai cũng mở được

### Cảm giác lần đầu

> Lần đầu tiên thấy app mình chạy trên một cái link thật, gửi cho bạn bè mở được —
> đó là khoảnh khắc **"wow, mình thật sự làm được"**.

---

## Bước 5: AI Skill — Dạy AI "nhớ" và tái sử dụng

> **Đây là level tiếp theo.** Sau khi vibe code lặp đi lặp lại, bạn sẽ nhận ra: "Mình cứ phải nói đi nói lại cùng một thứ. Có cách nào để AI nhớ không?"
>
> Câu trả lời: **Có. Tạo Skill cho AI.**

### Skill là gì?

Skill = **Một bộ hướng dẫn bạn tạo sẵn, để AI dùng lại mỗi khi cần.**

Hiểu đơn giản:
- Không có skill: Mỗi lần tạo project mới, bạn phải mô tả lại từ đầu — "tôi muốn style giống Momo, dùng màu hồng, bo góc 12px, font là Inter..."
- Có skill: Bạn chỉ cần nói `/momo-frontend` → AI tự biết tất cả

> Giống như bạn tạo một **"bí kíp nấu ăn"** cho AI. Thay vì mỗi lần dặn "cho muối, cho đường, cho nước mắm...", bạn chỉ cần nói "nấu theo công thức số 3".

### Cách tạo Skill — Vẫn nhờ AI!

**Bước 1: Nhờ AI thu thập thông tin**

```
Hãy scan website momo.vn, phân tích toàn bộ thông tin về:
- Bảng màu (color palette)
- Font chữ
- Bo góc, shadow, spacing
- Style các component: button, card, header, footer
- Layout tổng thể

Sau đó tổng hợp thành một bản style guide chi tiết.
```

→ AI sẽ trả về một bản phân tích đầy đủ về design system của Momo.

**Bước 2: Biến thành Skill**

```
Dựa trên style guide trên, hãy tạo một skill (slash command) tên
"momo-frontend". Khi gọi skill này, AI sẽ:
1. Tạo project Next.js với cấu trúc chuẩn
2. Áp dụng toàn bộ style giống Momo (màu sắc, font, component)
3. Tạo sẵn các component cơ bản: Header, Footer, Button, Card
4. Setup responsive cho mobile
```

→ AI tạo file skill với tất cả hướng dẫn bên trong.

**Bước 3: Dùng lại**

Từ giờ, mỗi khi bắt đầu project mới:

```
/momo-frontend
```

→ Một lệnh duy nhất. AI tự tạo project với đầy đủ style giống Momo. Xong.

### Ví dụ các Skill bạn có thể tạo

| Skill | Chức năng |
|-------|----------|
| `/momo-frontend` | Tạo project với style giống Momo web |
| `/landing-page` | Tạo landing page chuẩn với hero section, features, CTA |
| `/crud-api` | Tạo backend API cơ bản: Create, Read, Update, Delete |
| `/deploy-vercel` | Tự động deploy lên Vercel theo đúng quy trình mỗi lần |
| `/fix-bug` | Scan toàn bộ lỗi, liệt kê, và fix từng cái một |

### Tại sao Skill là "game changer"?

```
Không có Skill:
  Project 1: mô tả 30 phút → code 2 giờ
  Project 2: mô tả 30 phút → code 2 giờ  (lặp lại y hệt!)
  Project 3: mô tả 30 phút → code 2 giờ  (lại lặp lại!)

Có Skill:
  Tạo skill: 1 lần, 30 phút
  Project 1: /momo-frontend → code 30 phút
  Project 2: /momo-frontend → code 30 phút
  Project 3: /momo-frontend → code 30 phút
```

> **Bạn đang dạy AI cách làm việc theo ý bạn.** Càng tạo nhiều skill, AI càng hiểu bạn, và bạn càng nhanh.

---

# PHẦN 4: DEMO

> **Phần này bạn show trực tiếp trên sân khấu.**

## Demo 1: Show app hoàn chỉnh (3-5 phút)

- Mở app trên trình duyệt
- Walk through từng tính năng chính
- Nhấn mạnh: "Tất cả những gì các bạn thấy, tôi không viết 1 dòng code nào"

## Demo 2: Live vibe coding (5-7 phút) — Optional nhưng rất ấn tượng

- Mở Claude Code trên sân khấu
- Thêm 1 tính năng nhỏ ngay trước mắt khán giả. Ví dụ:
  - "Đổi màu nền app sang xanh lá"
  - "Thêm 1 nút dark mode"
  - "Thêm dòng chữ 'Hello [tên event]' ở header"
- Cho khán giả thấy quy trình: bạn nói → AI code → app thay đổi

> **Tip:** Chọn tính năng ĐƠN GIẢN để demo. Đừng chọn thứ phức tạp có thể fail trên sân khấu.
> Nếu không tự tin live demo, quay video trước cũng được.

## Chuẩn bị cho demo

- [ ] Test app hoạt động ổn trước buổi sharing
- [ ] Chuẩn bị wifi backup (hotspot điện thoại)
- [ ] Phóng to font size để khán giả thấy rõ
- [ ] Có plan B nếu demo fail (video backup)

---

# PHẦN 5: LESSONS LEARNED

## Điều tôi ước mình biết sớm hơn

### 1. Viết spec TRƯỚC khi code
> Tôi đã mất X ngày vì thay đổi ý liên tục. Nếu có spec từ đầu, chỉ mất 1/3 thời gian.

### 2. Đừng cầu toàn
> Version 1 xấu? Không sao. Ship trước, đẹp sau. Có app xấu mà chạy vẫn hơn ý tưởng đẹp mà không tồn tại.

### 3. Copy lỗi, paste lại — đừng cố hiểu
> Bạn không cần hiểu lỗi. AI hiểu. Việc của bạn là copy chính xác lỗi và paste lại.

### 4. Chia nhỏ yêu cầu
> Đừng nói "Tạo cho tôi toàn bộ app". Hãy nói "Tạo trang đăng nhập trước". Rồi "Tạo trang dashboard". Từng phần một.

### 5. Lưu lại những gì hoạt động
> Khi có 1 tính năng chạy ổn, nhờ AI commit (lưu lại). Để lỡ có hỏng thì quay lại được.

## Nếu làm lại từ đầu, tôi sẽ...

- [ ] Dành nhiều thời gian hơn cho brainstorming (2-3 ngày thay vì 2-3 giờ)
- [ ] Làm spec chi tiết hơn, đặc biệt phần giao diện
- [ ] Test với người dùng thật SỚM hơn (không đợi "xong" mới cho xài)
- [ ] Không cố thêm tính năng lung tung — giữ đúng MVP
- [ ] Nhờ AI giải thích từng phần, để hiểu cơ bản app hoạt động thế nào

## Giới hạn — Phải thành thật

### Vibe code KHÔNG thay thế developer

- App đơn giản → Vibe code rất ok
- App phức tạp (ngân hàng, y tế, hàng triệu người dùng) → Cần developer thật
- **Bảo mật:** Bạn không biết code an toàn hay không — đây là rủi ro thật
- **Bảo trì:** Khi app lớn dần, sửa lỗi sẽ khó hơn

### Điều tôi vẫn không hiểu

- Tôi vẫn không hiểu code bên trong hoạt động thế nào
- Tôi không thể tự fix nếu AI cũng bế tắc
- Tôi phụ thuộc hoàn toàn vào AI tool

> **Và điều đó không sao cả** — miễn bạn biết giới hạn của mình.

## Thông điệp cuối

> **Bạn không cần phải là developer để tạo ra thứ gì đó.**
>
> Thời đại AI đã hạ thấp rào cản. Ý tưởng + Kiên nhẫn + AI = Sản phẩm thật.
>
> Nếu một người HR như tôi làm được, bạn cũng làm được.
>
> **Hãy bắt đầu. Ngay hôm nay.**

---

# PHẦN 6: PHỤ LỤC

## Q&A — Câu hỏi thường gặp

**Q: Tôi có cần học code không?**
A: Không bắt buộc. Nhưng nếu hiểu cơ bản, bạn sẽ mô tả tốt hơn và debug nhanh hơn.

**Q: Mất bao lâu để ra được app đầu tiên?**
A: Có thể trong 1 ngày nếu app đơn giản. Thường 1-2 tuần nếu tranh thủ ngoài giờ làm.

**Q: AI nào tốt nhất cho vibe code?**
A: Claude Code, Cursor, GitHub Copilot, v0.dev — mỗi tool có điểm mạnh riêng. Thử và chọn cái hợp với mình.

**Q: App có thể kiếm tiền không?**
A: Được. Nhưng trước khi nghĩ đến tiền, hãy nghĩ đến giá trị app mang lại cho người dùng.

**Q: Tôi 40 tuổi, có muộn không?**
A: Không. Vibe code không có tuổi. Chỉ cần bạn có ý tưởng và sự kiên nhẫn.

**Q: Nếu AI tool đóng cửa / tăng giá thì sao?**
A: Code vẫn là của bạn. Bạn có thể chuyển sang tool khác. AI tools đang cạnh tranh rất mạnh — giá sẽ chỉ rẻ hơn.

## Glossary — Thuật ngữ cho người mới

| Thuật ngữ | Nghĩa đơn giản |
|-----------|----------------|
| **Frontend** | Phần người dùng nhìn thấy (giao diện, nút bấm, màu sắc) |
| **Backend** | Phần chạy ngầm phía sau (xử lý dữ liệu, lưu trữ) |
| **Database** | Nơi lưu dữ liệu (giống bảng Excel nhưng cho app) |
| **Deploy** | Đưa app lên internet để ai cũng truy cập được |
| **API** | Cách frontend và backend "nói chuyện" với nhau |
| **Bug** | Lỗi trong app |
| **Debug** | Quá trình tìm và sửa lỗi |
| **Commit** | Lưu lại 1 phiên bản code (như "Save game") |
| **Repository (Repo)** | Thư mục chứa toàn bộ code của project |
| **MVP** | Minimum Viable Product — phiên bản tối giản nhưng đủ dùng |
| **Prompt** | Câu/đoạn văn bạn gõ để yêu cầu AI làm gì đó |
| **Framework** | Bộ công cụ có sẵn để xây app nhanh hơn (ví dụ: Next.js) |

## Tài nguyên tham khảo

| Tài nguyên | Link | Mô tả |
|-----------|------|-------|
| Claude Code | claude.ai/code | AI assistant hỗ trợ coding |
| Cursor | cursor.com | Code editor có AI tích hợp |
| v0.dev | v0.dev | Tạo giao diện bằng mô tả |
| Vercel | vercel.com | Deploy frontend miễn phí |
| Railway | railway.app | Deploy backend đơn giản |
| GitHub | github.com | Lưu trữ và quản lý code |

## Prompt Templates — Copy & dùng luôn

### Prompt brainstorm:
```
Tôi có ý tưởng về [mô tả ngắn]. Tôi không có kiến thức technical.
Hãy đặt cho tôi 15 câu hỏi chi tiết để hiểu rõ app tôi muốn build.
```

### Prompt tạo spec:
```
Dựa trên thông tin trên, tạo Product Spec hoàn chỉnh dạng markdown,
gồm: overview, target users, MVP features, nice-to-have, UI description,
tech stack, và out of scope.
```

### Prompt bắt đầu code:
```
Đọc file product-spec.md và build app theo đúng spec.
Bắt đầu với MVP features trước.
```

### Prompt fix lỗi:
```
Tôi gặp lỗi sau: [paste lỗi]. Hãy fix giúp tôi và giải thích
ngắn gọn lỗi này là gì (giải thích cho người không biết code).
```

### Prompt deploy:
```
Giúp tôi deploy app này lên internet. Hướng dẫn từng bước một,
giải thích đơn giản vì tôi không có kiến thức technical.
```
