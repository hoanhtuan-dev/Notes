# 📄 File mới: `KeHoachTrienKhai_MayChuan.md`

Dưới đây là **toàn bộ nội dung** (kế hoạch quảng bá + phân tích dự án + giải thích 4 việc tiếp theo + kế hoạch offline chi tiết). Bạn copy nguyên khối từ dòng dưới vào file là dùng được ngay.

---

# KẾ HOẠCH TRIỂN KHAI QUẢNG BÁ & THU HÚT NGƯỜI DÙNG — MAYCHUAN
**Phiên bản:** 1.0 · **Phạm vi:** 90 ngày · **Đối tượng:** Khách mua · Chủ shop online · Nhà may/Xưởng

---

## 0. TÓM TẮT ĐIỀU HÀNH

| Hạng mục | Nội dung |
|---|---|
| **Mục tiêu 90 ngày** | 150 shop đăng ký · 50 shop trả phí · 300 khách hoạt động · widget ≥25% lượt render · churn <5%/tháng |
| **3 mặt trận** | B2C viral (khách mua) · B2B online (chủ shop) · B2B offline (nhà may/xưởng) |
| **Ngân sách** | 57–80tr/tháng (có thể chi mạnh cho kênh thắng vì LTV/CAC ≈ 48×) |
| **Nút thắt lớn nhất** | Form đăng ký hiện **không phân loại được "nhà may"** và **không thu UTM** → không đo được kênh nào ra shop thật |
| **Việc phải xong trước khi chạy paid** | G1 (thêm `type`) + G2 (UTM/ref_code) |

---

## 1. CHẨN ĐOÁN HIỆN TRẠNG (bám theo code thật)

### 1.1. Đòn bẩy đã có sẵn — dùng ngay, không cần build

| Đòn bẩy | Vị trí trong code | Cách khai thác |
|---|---|---|
| Trial 30 ngày / 50 render, **không cần thẻ** | `backend/config/shop_plans.php` | Đây là mồi mạnh nhất. Dùng làm CTA chính trong mọi bài viết/inbox |
| Watermark ở gói free-ad | `shop_plans.php` (`watermark`) | Cho thấy watermark công khai → mỗi ảnh free lan ra là 1 lần quảng cáo |
| Widget `/embed/tryon` | route embed | Chỉ mở ở Pro → **mồi nâng cấp tự nhiên**, đo được hiệu ứng |
| Hoàn 100% credit khi đặt đơn | logic credit | Rủi ro cho shop ≈ 0 → bán rất dễ |
| Escrow T+7 | logic thanh toán | Tăng niềm tin cho shop mới |

**Kết luận:** sản phẩm đã đủ mạnh để bán. Vấn đề nằm ở **phễu và đo lường**, không nằm ở tính năng.

### 1.2. Khoảng trống chặn tăng trưởng

| Mã | Khoảng trống | Ảnh hưởng | Ưu tiên |
|---|---|---|---|
| **G1** | `MerchantRegisterView.vue` chưa có phân loại "nhà may" | Xưởng đăng ký bị gộp chung với shop → phễu nhà may vô hình | **P0** |
| **G2** | Chưa thu UTM / `ref_code` khi đăng ký | Không biết kênh nào ra shop thật → mọi ngân sách là cảm tính | **P0** |
| **G3** | Chưa có referral 2 chiều | Mất vòng lặp viral rẻ nhất | P1 |
| **G4** | Chưa có landing riêng từng phân khúc | Paid traffic đổ vào 1 trang chung → CVR thấp | P1 |
| **G5** | Chưa có trang công khai `/mau` (thư viện mẫu) | Mất SEO + mất bằng chứng xã hội | P1 |
| **G6** | Paywall chưa thông minh | Chặn nhầm người dùng đang hào hứng | P2 |
| **G7** | Chưa có voucher code | Buổi offline không có đòn chốt | P2 |
| **G8** | Chưa có case study công khai | Bán B2B thiếu dẫn chứng | P2 |

---

## 2. ĐỊNH VỊ & THÔNG ĐIỆP THEO 3 PHÂN KHÚC

| Phân khúc | Nỗi đau | Lời hứa 1 dòng | Kênh chính | CAC mục tiêu |
|---|---|---|---|---|
| 👤 **Khách mua** | "Không biết mặc lên có vừa/đẹp không" | *"Xem bạn mặc bộ đó thế nào — trước khi bấm mua"* | TikTok/Reels, KOC micro, seeding, referral 2 chiều | ~0 (viral) |
| 🏪 **Chủ shop online** | "Flat-lay xấu, thuê mẫu tốn 500k–1tr/look" | *"Flat-lay → ảnh người mặc thật, ~1.000₫/lượt"* | Group seller FB/Zalo, paid test, agency/affiliate, case study | ≤ 250k |
| ✂️ **Nhà may / Xưởng** | "Khách ở xa không tới thử, chốt đơn chậm" | *"Cho khách xem trước bộ đồ trên dáng họ — chốt tại xưởng"* | **Offline-first**: chợ vải/phố may, hội chợ, Zalo xưởng, trường dạy may | ≤ 350k |

---

## 3. PHỄU & CHỈ SỐ

### 3.1. Phễu B2C (khách mua)
```
Video viral → Xem demo thử đồ → Tự thử 1 ảnh (không cần đăng nhập)
→ Đăng ký để lưu ảnh → Giới thiệu bạn bè → Quay lại thử tiếp
```
**Chỉ số:** view → click (≥3%) → thử lần đầu (≥25%) → đăng ký (≥15%) → share (≥8%)

### 3.2. Phễu B2B online (chủ shop)
```
Bài SEO / group → Đọc case study → Đăng ký trial (có UTM)
→ Render ảnh đầu tiên (<24h) → Dùng 10–20 ảnh → Chạm trần 50 render
→ Nâng cấp Pro
```
**Chỉ số:** visit → đăng ký (≥6%) → time-to-first-render <24h (≥80%) → trial→paid (≥33%)

### 3.3. Phễu B2B offline (nhà may)
```
Gặp tại xưởng/chợ → Demo live 3 ảnh trên điện thoại của chủ → In ảnh mini tại chỗ
→ Xin Zalo + voucher → Đăng ký trong 48h → Dùng thử 1 tuần → Chốt gói Xưởng
```
**Chỉ số:** tiếp cận → demo live (≥20%) → đăng ký (≥10%) → trial→paid (≥30%)

---

## 4. KẾ HOẠCH 90 NGÀY — 4 SPRINT

### SPRINT 1 (Ngày 1–14): VÁ NỀN — *không chạy paid*
- [ ] **G1** Thêm `type` (online_shop / workshop / tailor / brand) vào form + DB
- [ ] **G2** Thu `utm_source`, `utm_medium`, `ref_code` ở cả đăng ký shop và đăng ký khách
- [ ] Dựng bảng theo dõi thủ công (Google Sheet) trước khi có dashboard
- [ ] Viết xong 20 bài SEO + 12 kịch bản video
- [ ] Soạn checklist + lịch offline

**Điều kiện ra Sprint 2:** form đăng ký ghi được "nhà may", mọi đăng ký có nguồn.

### SPRINT 2 (Ngày 15–35): BÁN TAY 1-1
- [ ] Mục tiêu: **30 shop online + 10 nhà may** đăng ký
- [ ] Time-to-first-render < 24h cho **mọi** shop mới (tự tay hỗ trợ)
- [ ] Chạy 2 chuyến offline đầu tiên (Ninh Hiệp + 1 điểm phía Nam)
- [ ] Đăng 8 video, 10 bài SEO, seeding 15 group
- [ ] Ghi lại **mọi câu hỏi/phản đối** → làm nguyên liệu nội dung

### SPRINT 3 (Ngày 36–65): VÒNG LẶP VIRAL
- [ ] Bật **referral 2 chiều** (G3)
- [ ] Ra trang `/mau` công khai (G5)
- [ ] Paywall thông minh (G6): nhắc nâng cấp đúng lúc chạm trần, không chặn giữa việc
- [ ] Bắt đầu paid test: **20–40tr** chia 3 nhóm (TikTok B2C / FB group B2B / Google search "thử đồ ảo")
- [ ] Chốt giá 2 gói nhà may **sau khi gặp 5 nhà may đầu tiên**

### SPRINT 4 (Ngày 66–90): SCALE
- [ ] Scale kênh thắng (tắt kênh CAC > 2× mục tiêu)
- [ ] Đẩy widget `/embed/tryon` cho agency/affiliate
- [ ] Ký 3–5 đối tác (agency chụp ảnh, trường dạy may, hội chợ)
- [ ] Công bố 5 case study (G8)

---

## 5. KÊNH & CHIẾN THUẬT CHI TIẾT

### 5A. Khách mua (B2C) — mục tiêu: viral, CAC ≈ 0
1. **TikTok/Reels:** format "thử bộ này trước khi mua" — quay màn hình thao tác 15s, kết bằng ảnh kết quả.
2. **KOC micro (5k–50k follower):** trả 300k–1tr/video hoặc đổi credit. Ưu tiên người bán thời trang.
3. **Seeding:** group "Mua bán đồ si", "Thời trang nữ", comment tự nhiên dưới bài hỏi "có vừa không".
4. **Referral 2 chiều:** người mời + người được mời đều nhận render miễn phí.

### 5B. Chủ shop online (B2B) — mục tiêu: 50 shop trả phí
1. **Group seller FB/Zalo:** không spam link, đăng **trước/sau** bằng ảnh thật của chính shop trong group.
2. **SEO:** 6 bài đúng ý định ("chụp lookbook không cần studio"…).
3. **Paid test:** ngân sách nhỏ 5tr/nhóm, đo CAC từng nhóm trong 7 ngày.
4. **Agency/affiliate:** hoa hồng 20–30% tháng đầu cho người giới thiệu.
5. **Case study:** 1 shop thật + số liệu thật (số ảnh, thời gian tiết kiệm, tiền tiết kiệm).

### 5C. Nhà may / Xưởng (B2B offline) — mục tiêu: 20 xưởng
> **Nguyên tắc:** nhà may **không tìm** sản phẩm công nghệ. Phải đến tận nơi, **cầm điện thoại của chủ xưởng làm 3 ảnh tại chỗ**.

1. **Offline trực tiếp:** chợ vải / phố may / xưởng may (chi tiết ở Mục 15).
2. **Zalo xưởng:** group "xưởng may", "nguồn hàng quảng châu"…
3. **Trường dạy may:** giới thiệu cho học viên sắp mở xưởng.
4. **Hội chợ triển lãm vải & phụ liệu:** thuê gian hàng nhỏ hoặc chỉ đi dạo phát tờ rơi + demo.
5. **Đòn chốt độc quyền:** in ảnh mini tại chỗ — chủ xưởng cầm ảnh "khách mặc mẫu của xưởng" về là chốt.

---

## 6. GÓI GIÁ (bao gồm 2 gói nhà may đề xuất)

| Gói | Giá | Trial | Render | Widget | Watermark | Commission | Analytics |
|---|---|---|---|---|---|---|---|
| Free-ad | 0 | — | giới hạn | ✗ | ✓ | — | — |
| Starter | — | 30 ngày | 50 | ✗ | ✗ | 10% | basic |
| Pro | — | 30 ngày | cao hơn | ✓ | ✗ | 8% | funnel |
| Business | — | 30 ngày | cao nhất | ✓ | ✗ | 5% | funnel |
| **Xưởng Cơ Bản** *(mới)* | 299k | 30 ngày | vừa | **✓** | ✗ | **0%** | basic |
| **Xưởng Pro** *(mới)* | 899k | 30 ngày | cao | ✓ | ✗ | **0%** | funnel |

**Lưu ý kỹ thuật khi thêm vào `shop_plans.php`** — phải khớp đủ bộ khoá code đang đọc:
```
id, name, icon, price_vnd, trial_days, render_credits, max_products,
storage_gb, commission_rate, widget, api, priority_queue, watermark,
staff_accounts, human_qa_images, analytics, support, tagline
```
- `commission_rate = 0.0` vì nhà may không bán trên sàn.
- `widget = true` ngay ở bản Cơ Bản — tại xưởng, widget chính là "cho khách xem trước tại chỗ", là khác biệt cạnh tranh, **không nên khoá sau Pro**.
- `watermark = false` cho cả 2: xưởng cần ảnh sạch để in lookbook.
- **Chốt giá chỉ sau khi gặp 5 nhà may đầu tiên.**

---

## 7. NGÂN SÁCH

| Khoản | Tháng 1 | Tháng 2 | Tháng 3 |
|---|---|---|---|
| Paid test (TikTok/FB/Google) | 0 | 20tr | 40tr |
| KOC micro (15–20 video) | 5tr | 10tr | 15tr |
| Offline (đi lại, in ảnh, voucher, quà) | 8tr | 10tr | 8tr |
| Sản xuất nội dung (editor/quay) | 6tr | 6tr | 6tr |
| Công cụ (email, CRM, sheet) | 2tr | 2tr | 2tr |
| Dự phòng | 5tr | 5tr | 5tr |
| **Tổng** | **26tr** | **53tr** | **76tr** |

---

## 8. LỊCH NỘI DUNG + HOOK MẪU

### 8.1. Lịch 4 tuần (lặp lại)

| Thứ | Nội dung chính |
|---|---|
| 2 | 1 bài SEO (B2B) + 1 video B2C |
| 3 | Seeding 3 group (B2C) |
| 4 | 1 bài SEO (nhà may) + 1 video chủ shop |
| 5 | Inbox/Zalo 20 chủ shop |
| 6 | 1 video B2C + story before/after |
| 7 | Offline (đi chợ vải / phố may) |
| CN | Tổng hợp số liệu, chuẩn bị tuần sau |

### 8.2. 5 hook mẫu (dùng ngay cho video 2 giây đầu)
1. *"Bộ này trên mạng 250k, mà mặc lên có đẹp không? Thử luôn."*
2. *"Shop tôi chụp lookbook không cần mẫu, không cần studio."*
3. *"Khách ở Hà Nội vẫn chốt được bộ may ở Sài Gòn — nhờ cái này."*
4. *"Xưởng mà cho khách xem trước bộ đồ trên dáng họ thì chốt nhanh gấp đôi."*
5. *"Tôi trả 1.000₫ cho 1 ảnh người mặc thay vì 1 triệu cho 1 buổi chụp."*

### 8.3. 20 bài SEO — chia nhóm từ khoá
- **6 bài B2C:** thử đồ ảo là gì · cách biết online có vừa không · mặc đẹp không cần đến tiệm · so sánh size online · ảnh AI thử đồ có đáng tin · mẹo mua đồ online không bị hoàn
- **6 bài chủ shop:** chụp lookbook không cần studio · chụp flat-lay bằng điện thoại · giảm tỷ lệ hoàn đơn thời trang · tăng CVR ảnh sản phẩm · chi phí chụp mẫu thực tế · tool AI cho shop thời trang
- **5 bài nhà may/xưởng:** lookbook cho xưởng may · chốt đơn may đo không cần khách tới thử · bán hàng xưởng qua Zalo · ảnh mẫu cho xưởng · cách demo mẫu vải online
- **3 bài địa phương:** Ninh Hiệp · Vạn Phúc · chợ vải Bình Dương

### 8.4. 12 kịch bản video
6 B2C + 4 chủ shop + 2 xưởng. Mỗi kịch bản gồm: hook 2s · timeline 15–25s · cảnh quay · caption + hashtag · **CTA gắn UTM riêng**.

---

## 9. SCRIPT DEMO 15 PHÚT (dùng cho mọi buổi 1-1)

| Phút | Hành động |
|---|---|
| 0–2 | Hỏi: hiện chụp ảnh sản phẩm thế nào? Tốn bao nhiêu? Mất bao lâu? |
| 2–4 | Mở điện thoại, lấy **ảnh sản phẩm của chính họ** (không dùng ảnh mẫu) |
| 4–8 | Chạy thử 3 ảnh ngay trước mặt họ |
| 8–10 | Cho họ tự bấm 1 lần — để họ sở hữu kết quả |
| 10–12 | Nói con số: ~1.000₫/lượt vs 500k–1tr/buổi chụp |
| 12–14 | Đăng ký trial 30 ngày/50 render, **không cần thẻ** |
| 14–15 | Xin Zalo, hẹn follow-up 48h, tặng voucher |
| Sau | Ghi `utm_source=offline_<địa điểm>` vào form đăng ký |

---

## 10. XỬ LÝ PHẢN ĐỐI

| Phản đối | Trả lời |
|---|---|
| "Ảnh AI trông giả lắm" | Mở ngay 3 ảnh thật của shop họ, để họ tự đánh giá |
| "Tôi không rành công nghệ" | "Anh/chị chỉ cần gửi ảnh qua Zalo, em làm giúp" — bán dịch vụ kèm |
| "Đắt quá" | Quy đổi: 1 buổi chụp = 1 năm dùng tool |
| "Để tôi suy nghĩ" | Hẹn follow-up 48h + tặng voucher có hạn 7 ngày |
| "Sợ khách phát hiện" | Giải thích: đây là ảnh mô phỏng dáng, nhiều shop đang dùng làm lookbook |
| "Xưởng tôi chỉ bán sỉ" | "Đúng rồi, nhưng khách sỉ cũng cần xem mẫu trên dáng người" |

---

## 11. DASHBOARD & ĐO LƯỜNG

**3 phễu theo dõi hằng tuần:**

| Phễu | Chỉ số chính | Ngưỡng tốt |
|---|---|---|
| B2C | view → thử → đăng ký → share | ≥3% → ≥25% → ≥15% → ≥8% |
| Shop online | visit → đăng ký → render đầu → nâng cấp | ≥6% → <24h → ≥33% |
| Nhà may | tiếp cận → demo → đăng ký → trả phí | ≥20% → ≥10% → ≥30% |

**Cột bắt buộc có trong mọi báo cáo:** `utm_source`, `utm_medium`, `ref_code`, `type`, CAC, LTV, thời gian tới ảnh đầu tiên.

---

## 12. RỦI RO & GIẢM THIỂU

| Rủi ro | Mức | Giảm thiểu |
|---|---|---|
| Nhà may đăng ký xong bị gộp chung shop | Cao | **G1 phải xong trước Sprint 2** |
| Chạy paid khi chưa đo được nguồn | Cao | **G2 phải xong trước mọi đồng paid** |
| Ảnh AI bị coi là giả | TB | Luôn demo bằng ảnh thật của khách, không dùng ảnh mẫu |
| Offline tốn thời gian, ROI chậm | TB | KPI cứng mỗi ngày: 15 tiếp cận · 3 demo · 1–2 đăng ký |
| Churn cao sau trial | TB | Time-to-first-render <24h + follow-up 48h |
| Bán sai giá gói Xưởng | TB | **Không chốt giá trước khi gặp 5 nhà may đầu** |

---

## 13. CHECKLIST KỸ THUẬT P0 → P2

### P0 — Bắt buộc trước Sprint 2
- [ ] **G1** `MerchantRegisterView.vue`: thêm dropdown "Bạn là?" (`online_shop / workshop / tailor / brand`)
- [ ] **G1** `stores/merchant.js`: thêm `type` vào payload `registerShop`
- [ ] **G1** Backend: migration thêm cột `type` vào bảng `shops` + validation `in_array` + trả về API + filter/hiển thị ở Admin
- [ ] **G2** Form đọc UTM từ URL + hidden field `ref_code`
- [ ] **G2** Backend: migration `utm_source`, `utm_medium`, `ref_code` + lưu ở `AuthController` (khách mua đi cùng nguồn)

### P1 — Trong Sprint 3
- [ ] **G3** Referral 2 chiều (mã mời cho cả shop và khách)
- [ ] **G4** Landing riêng cho từng phân khúc
- [ ] **G5** Trang công khai `/mau`

### P2 — Sprint 3–4
- [ ] **G6** Paywall thông minh (nhắc đúng lúc chạm trần)
- [ ] **G7** Voucher code
- [ ] **G8** Case study công khai

---

## 14. GIẢI THÍCH CHI TIẾT 4 VIỆC TIẾP THEO

4 việc này không rời rạc — chúng là **4 nhánh của cùng Sprint 1–2**, chia làm 2 loại:
- **Nội dung** (việc 1 & 4): làm ngay được, không cần dev.
- **Kỹ thuật** (việc 2 & 3): là điều kiện *đo được* và *bán được*.

### 14.1. Viết 20 bài SEO + 12 kịch bản video
- **Mục đích:** lấp G5, tạo "đạn" cho 3 kênh organic.
- **Đầu ra:** `NoiDung/SEO-20-bai.md` + `NoiDung/Video-12-kich-ban.md`
- **Công:** 2–3 ngày · **Chi phí:** 0₫
- **Đo bằng:** UTM `utm_source=blog_tiktok` → biết bài nào ra shop thật
- **Phụ thuộc:** không — làm hôm nay được

### 14.2. Code G1 + G2 (phân loại + đo nguồn) — **ƯU TIÊN SỐ 1**
- **Mục đích:** P0 khoá. Kế hoạch nói thẳng: *không chạy paid cho tới khi đo được nguồn*.
- **Công:** 2–3 ngày · **Rủi ro thấp** (chỉ thêm cột, không đổi luồng)
- **Vì sao bắt buộc trước:** không có nó thì chuyến offline nhà may khiến xưởng đăng ký xong **bị gộp chung với shop** → phễu nhà may vô hình, không biết kênh nào thắng để scale.

### 14.3. Thêm 2 gói nhà may vào `shop_plans.php`
- **Mục đích:** mở dòng doanh thu thứ 4 + là thứ để bán ở buổi offline.
- **Công:** 0,5–1 ngày + test hiển thị bảng giá
- **Thứ tự khuyến nghị:** viết **nháp trước**, **chốt giá sau khi gặp 5 nhà may đầu tiên**. Nếu không, rất dễ bán sai giá và khó lùi.

### 14.4. Kế hoạch chi tiết cho lần offline đầu tiên
- **Mục đích:** đây là kênh khác biệt nhất — nhà may không tìm sản phẩm công nghệ, phải **cầm điện thoại của chủ xưởng làm 3 ảnh tại chỗ**.
- **Công:** 1 ngày soạn + 5–10tr chi phí chuyến
- **Phụ thuộc:** cần **G1 xong** + có voucher (G7). Nếu chưa có voucher thì ghi tay, nhập sau.

### 14.5. Thứ tự đề xuất

| Thứ tự | Việc | Khi nào | Vì sao |
|---|---|---|---|
| 1 | **G1 + G2 (14.2)** | Ngay, 2–3 ngày | Không đo được thì mọi thứ phía sau là cảm tính |
| 2 | **Nội dung (14.1)** | Song song | Cần đạn trước khi inbox/đăng group tuần 3 |
| 3 | **Offline (14.4)** | Soạn ngay, chạy tuần 3–4 | Chỉ cần sau khi G1 xong |
| 4 | **2 gói nhà may (14.3)** | Nháp ngay, chốt giá sau 5 nhà may | Giá phải do thị trường xác nhận |

> **Nếu chỉ được chọn một việc: chọn 14.2 (G1 + G2).** Đây là nút thắt duy nhất mà cả 3 kênh đều cần, và hiện form đăng ký **không có chỗ để ghi "tôi là nhà may"**.

---

## 15. KẾ HOẠCH OFFLINE LẦN ĐẦU — CHI TIẾT

### 15.1. Điểm đến & thời điểm

| Khu vực | Điểm cụ thể | Giờ đông | Ghi chú |
|---|---|---|---|
| Hà Nội | Chợ Ninh Hiệp (Gia Lâm) | 8–11h | Chủ yếu vải + hàng sẵn |
| Hà Nội | Phố Vạn Phúc (Hà Đông) | 9–11h, 14–16h | Nhiều xưởng may đo |
| TP.HCM | Chợ vải Soái Kình Lâm / Bình Tây | 7–10h | Sỉ vải lớn nhất phía Nam |
| Bình Dương | Chợ vải Bình Dương | 8–11h | Xưởng may công nghiệp |
| Đà Nẵng | Chợ Hàn / phố may | 8–11h | Thị trường miền Trung |

### 15.2. Checklist vật tư
- [ ] Điện thoại (2 cái) + laptop cài sẵn app, đã đăng nhập
- [ ] 4G dự phòng + sạc dự phòng + cáp
- [ ] **Máy in ảnh mini + giấy ảnh** ← đòn chốt quan trọng nhất
- [ ] Namecard + QR Zalo (in sẵn, khổ lớn để quét nhanh)
- [ ] Tờ rơi 1 mặt (1 lợi ích + 1 QR + 1 con số giá)
- [ ] Voucher code giấy (có hạn 7 ngày)
- [ ] Nước / quà nhỏ
- [ ] Sổ ghi chép + biểu mẫu đăng ký giấy
- [ ] Pin dự phòng cho máy in ảnh

### 15.3. Lịch 8 ngày (2 người × 4 ngày)

| Ngày | Buổi sáng | Buổi chiều | KPI ngày |
|---|---|---|---|
| 1 | Ninh Hiệp: dãy vải chính | Ninh Hiệp: khu xưởng sau chợ | 15 tiếp cận · 3 demo · 1–2 ĐK · 25 Zalo |
| 2 | Vạn Phúc: phố may đo | Vạn Phúc: ngõ xưởng nhỏ | nt |
| 3 | Nghỉ / follow-up Zalo | Chuẩn bị chuyến Nam | — |
| 4 | Bay vào TP.HCM | Soái Kình Lâm | nt |
| 5 | Bình Tây | Bình Tây khu xưởng | nt |
| 6 | Bình Dương | Bình Dương | nt |
| 7 | Bay ra / nghỉ | Follow-up toàn bộ | — |
| 8 | Đà Nẵng (nếu ngân sách) | Đà Nẵng | nt |

### 15.4. KPI cứng mỗi ngày
**15 tiếp cận · 3 demo live · 1–2 đăng ký · 25 số Zalo**

### 15.5. Sau chuyến
- [ ] Nhập toàn bộ biểu mẫu giấy vào hệ thống với `utm_source=offline_<địa điểm>`
- [ ] Follow-up Zalo trong 48h
- [ ] Tổng hợp: tỷ lệ demo→đăng ký, phản đối phổ biến, giá nhà may chấp nhận
- [ ] **Chốt giá 2 gói Xưởng dựa trên dữ liệu thật**

---

## 16. VIỆC CẦN QUYẾT NGAY

| # | Việc | Người làm | Deadline |
|---|---|---|---|
| 1 | Bắt đầu G1 + G2 | Dev | 3 ngày |
| 2 | Viết 20 bài SEO + 12 video | Content | 3 ngày |
| 3 | Soạn kế hoạch offline + vật tư | Growth | 1 ngày |
| 4 | Nháp 2 gói nhà may (chưa chốt giá) | Product | 1 ngày |
| 5 | **Xác nhận khu vực địa lý ưu tiên** | Founder | Ngay |

---

*Hết file.*

---

Bạn xác nhận giúp mình **khu vực địa lý ưu tiên** (Bắc / Nam / cả hai) để mình chốt danh sách điểm đến ở Mục 15.1 thành bản chạy được — hoặc nếu muốn, mình làm tiếp **file `NoiDung/SEO-20-bai.md`** với đề bài + dàn ý chi tiết từng bài.