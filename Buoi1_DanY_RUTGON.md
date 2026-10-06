# BUỔI 1 — TỔNG QUAN THIẾT BỊ & TẬP LỆNH SCPI
## Dàn ý slide giảng dạy — 32 slide / 200 phút *(bản v2 — rút gọn & sắp xếp lại)*

> **GV:** Nguyễn Mạnh Bảo · **Thiết bị:** Keithley Model 2000 · **Lớp:** 3 nhóm ghép (5+2, 1+3, 4), ~15–18 SV
> **Định hướng buổi 1:** **học lệnh SCPI là chính** · thực hành trên **phần mềm giả lập (gõ lệnh trực tiếp, không cần cổng COM)** · Hercules chỉ **giới thiệu ở cuối buổi** để chuẩn bị cho buổi 2
> **Trích dẫn:** `[tr.87]` = trang file PDF manual

---

## ⏱ PHÂN BỔ THỜI GIAN

| Mốc | Khối | Nội dung | Slide | Phút |
|---|---|---|---|---|
| 00:00 | **0** | Mở đầu + An toàn | 1–3 | 10 |
| 00:10 | **A** | Làm quen máy (phần cần cho điều khiển) | 4–7 | 15 |
| 00:25 | **—** | 🎤 3 nhóm báo cáo chuyên đề + GV chuẩn hoá | 8 | 25 |
| 00:50 | **B** | RS‑232 qua USB — **kiến thức nền** | 9–13 | 30 |
| 01:20 | — | ☕ **NGHỈ** | — | 10 |
| 01:30 | **C** | ⭐ **SCPI — 12 lệnh** | 14–20 | 40 |
| 02:10 | **D** | ⭐ **THỰC HÀNH trên giả lập** | 21–26 | 55 |
| 03:05 | **E** | Làm quen Hercules *(chuẩn bị buổi 2)* | 27–28 | 10 |
| 03:15 | **F** | Chốt + giao việc | 29–32 | 5 |
| 03:20 | | **KẾT THÚC** | | **200** |

> **Trục chính của buổi:** 40' học lệnh + 55' gõ lệnh trên giả lập = **95 phút xoay quanh SCPI**.

---

### 🔀 Thay đổi so với bản trước

| Thay đổi | Lý do |
|---|---|
| **Hercules chuyển từ giữa buổi → cuối buổi, còn 10'** | Buổi 1 chưa có máy thật, Hercules không nối được vào đâu. Chỉ giới thiệu giao diện + cho SV tải cài sẵn. |
| **Giả lập KHÔNG dùng COM ảo** | Chỉ là ô nhập lệnh → kiểm tra cú pháp → trả lời. Không cần cài driver, không cần com0com, SV chạy được ngay. |
| **Luật `<CR>`: chỉ dạy lý thuyết** | Giả lập không có cổng nên không mô phỏng được. SV sẽ tự vấp ở buổi 2 với pyserial — lúc đó bài học thấm hơn. |
| **Khối RS‑232: 50' → 30'** | Không thực hành cắm dây thì không nên giảng suông 50'. |
| **Driver CH340/FTDI + Device Manager → đẩy sang buổi 2** | Chỉ có ý nghĩa khi tay cầm cáp thật. |
| **Khối SCPI: 30' → 40'** (thêm slide bài tập tại chỗ) | Đây mới là trọng tâm buổi 1. |
| **Thực hành: 50' → 55'** (thêm Thử thách nhóm) | Tận dụng thời gian dôi ra. |

### 🗑 Đã cắt hẳn khỏi buổi 1
Chuỗi tín hiệu trong DMM · Đo 2‑dây vs 4‑dây · Filter/REL/Autozero · Trigger Model · Buffer `:TRACe` · Thanh ghi trạng thái `*ESE/*ESR/*SRE/*STB` · Luật short‑form chi tiết · Con trỏ `:` `;` · Bảng 10 subsystem · Phụ kiện & card quét · Driver USB‑Serial & Device Manager

---
---

# KHỐI 0 — MỞ ĐẦU (slide 1–3 · 10 phút)

---

### SLIDE 1 — Bìa

**Hiển thị:** BUỔI 1 — TỔNG QUAN THIẾT BỊ & TẬP LỆNH SCPI · Keithley Model 2000 · GV Nguyễn Mạnh Bảo

**🖼 Hình:** **H1** — Ảnh thật Keithley 2000 mặt trước, chiếm 45% bên phải slide.

**🎙 Lời giảng:**
> "Chuỗi ba buổi này, chúng ta học cách điều khiển một thiết bị đo bằng phần mềm. Hôm nay là buổi nền móng: hiểu cái máy, và học **ngôn ngữ** để ra lệnh cho nó."

---

### SLIDE 2 — Buổi 1 làm gì & đạt được gì

**Hiển thị:**
- Lộ trình: **Buổi 1** Học lệnh SCPI → **Buổi 2** Nối máy thật + Python + GUI → **Buổi 3** Vận hành + vấn đáp
- Cuối buổi hôm nay các em phải:
  1. ☐ Biết Keithley 2000 làm được gì và điều khiển được qua đâu
  2. ☐ Hiểu RS‑232 cần cấu hình những gì *(buổi 2 mới cắm dây thật)*
  3. ☐ **Đọc và viết được lệnh SCPI**
  4. ☐ **Dùng thành thạo 12 lệnh cơ bản trên phần mềm giả lập**
  5. ☐ Biết tự tra lỗi bằng `:SYST:ERR?`

**🖼 Hình:**
> **H2.1** — 3 ô chevron ngang (Buổi 1 cam đậm, buổi 2–3 xám), icon: 📖 → 🔌💻 → ⚙️
> **H2.2** — Góc phải: screenshot giả lập đã trả về `KEITHLEY INSTRUMENTS INC.,MODEL 2000,...` — nhãn "đích đến cuối buổi".

**🎙 Lời giảng:**
> "Thầy nói rõ ngay từ đầu để các em khỏi sốt ruột: **hôm nay chúng ta chưa cắm dây vào máy thật**. Buổi 2 mới làm chuyện đó.
> Hôm nay là buổi **học ngôn ngữ**. Giống như học ngoại ngữ — phải thuộc từ vựng và ngữ pháp trước khi sang nước ngoài nói chuyện. Nếu hôm nay các em học tốt, buổi 2 cắm dây vào là chạy luôn. Còn nếu hôm nay lơ là, buổi 2 các em sẽ vừa loay hoay với dây vừa loay hoay với lệnh — gấp đôi khó."

---

### SLIDE 3 — ⚠️ AN TOÀN *(nhắc trước, buổi 2 dùng tới)*

**Hiển thị:** *(nền đỏ/vàng)*
- **1000 V PEAK** trên cọc INPUT — đủ gây tử vong
- **KHÔNG** đo dòng (AMPS) khi đang ở chế độ đo áp → nổ cầu chì
- **KHÔNG** tháo vỏ máy — *"NO INTERNAL OPERATOR SERVICEABLE PARTS"* [tr.17]
- **Quy tắc lớp: chưa được phép thì không cắm, không bật.**

**🖼 Hình:**
> **H3** — Crop vùng cọc đấu mặt trước, khoanh đỏ dòng "1000V PEAK" và "3A 250V". *Nguồn: Figure 2‑1 [tr.14] hoặc ảnh lab.*

**🎙 Lời giảng:**
> "Hai phút, và thầy không nói đùa. Tuy hôm nay chưa đụng máy, thầy vẫn nói trước để các em quen.
> Cọc này chịu 1000 volt — máy đo bình thường, tay các em thì không. Lỗi kinh điển: để máy ở chế độ đo dòng rồi chọc vào nguồn áp — nổ cầu chì, nhóm mất một buổi.
> Quy tắc: **chưa được phép thì không cắm, không bật.**"

---
---

# KHỐI A — LÀM QUEN MÁY (slide 4–7 · 15 phút)

---

### SLIDE 4 — Keithley 2000 là gì

**Hiển thị:**
- DMM để bàn **6½ digit** (hiển thị tới 1.999.999 điểm) — mịn gấp ~1000 lần đồng hồ cầm tay
- Đo được: **DCV · ACV · DCI · ACI · Ω · Tần số · Chu kỳ · Nhiệt độ**
- Dải: 0,1 µV→1000 V · 10 nA→3 A · 100 µΩ→120 MΩ · 3 Hz→500 kHz
- Tốc độ: **50 phép đo/s** (phân giải cao) → **2000 phép đo/s** (phân giải thấp)
- **Điều khiển từ xa qua GPIB hoặc RS‑232** ← lý do nó có mặt trong môn Tự động hoá

**🖼 Hình:**
> **H4.1** — 2 ảnh cạnh nhau: đồng hồ cầm tay rẻ tiền vs Keithley 2000, nhãn "2.000 điểm" vs "2.000.000 điểm".
> **H4.2** — Icon ⚡ + con số "2000 rdg/s" nổi bật.

**🎙 Lời giảng:**
> "Sáu rưỡi chữ số nghĩa là hiển thị tới gần hai triệu điểm phân giải — mịn gấp một nghìn lần đồng hồ cầm tay.
> Con số cần nhớ: **nhanh nhất 2000 phép đo mỗi giây, nhưng khi đó độ chính xác giảm**. Luôn có đánh đổi nhanh ↔ chính xác — lát nữa gặp lại ở lệnh NPLC.
> Và điểm quan trọng nhất: máy này **điều khiển được bằng phần mềm**. Đó là lý do nó nằm trong môn này chứ không phải môn Đo lường."

---

### SLIDE 5 — Mặt trước: chỉ cần nhớ 3 phím

**Hiển thị:**
| Phím | Dùng làm gì |
|---|---|
| `SHIFT` + `RS232` | **Mở menu cấu hình RS‑232** ← cửa ngõ của cả học phần |
| `SHIFT` + `GPIB` | Menu GPIB / chọn ngôn ngữ lập trình |
| `LOCAL` | Thoát chế độ remote khi mặt máy bị khoá |

- Chữ **trắng** trên phím = chức năng chính · chữ **màu** phía trên = phải bấm `SHIFT` trước

**🖼 Hình:**
> **H5.1** — Ảnh mặt trước full‑width, **chỉ khoanh đỏ 3 phím trên**.
> **H5.2** — Zoom cận cảnh phím `SHIFT` và chữ xanh `RS232` / `GPIB`.

**🎙 Lời giảng:**
> "Mặt máy có mấy chục phím, các em đọc manual được. Thầy chỉ bắt nhớ ba.
> **SHIFT rồi RS232** — buổi 2 các em sẽ dùng phím này đầu tiên khi vào lab.
> **LOCAL** — khi gửi lệnh từ máy tính xuống, mặt máy bị khoá, bấm nút không ăn. Đừng hoảng, đừng rút điện: bấm LOCAL."

---

### SLIDE 6 — Màn hình & 4 đèn báo = bộ đồ nghề debug

**Hiển thị:**
| Đèn | Nghĩa | Dùng để chẩn đoán *(buổi 2–3)* |
|---|---|---|
| **REM** | Đang bị PC điều khiển | Mặt máy bị khoá — bình thường |
| **LSTN** | Máy **đang nhận** dữ liệu | **Không sáng = lệnh chưa tới máy** |
| **TALK** | Máy đang gửi dữ liệu về | Máy có trả lời |
| **ERR** | Có lỗi trong hàng đợi | **Sáng = lệnh tới rồi nhưng sai cú pháp** |

**🖼 Hình:**
> **H6.1** — Ảnh cận cảnh màn hình VFD thật, mũi tên chỉ 4 chữ REM / LSTN / TALK / ERR.
> **H6.2** — 2 ảnh so sánh: màn hình bình thường vs màn hình có **REM + ERR** sáng.

**🎙 Lời giảng:**
> "Slide này chưa dùng hôm nay, nhưng sẽ cứu các em ở buổi 2 và 3. Khi chương trình sai, sinh viên nhìn vào màn hình máy tính. Người có nghề nhìn vào **mặt thiết bị**.
> **LSTN không sáng** khi bấm Send ⇒ lệnh chưa hề tới máy ⇒ lỗi dây hoặc cổng COM, không phải lỗi code.
> **ERR sáng** ⇒ lệnh tới rồi nhưng máy không hiểu ⇒ lỗi cú pháp.
> Hai đèn này khoanh vùng được nửa số lỗi. Chụp ảnh lại."

---

### SLIDE 7 — Mặt sau: cổng RS‑232

**Hiển thị:**
- **RS232 — đầu nối DB‑9** ← dùng suốt 3 buổi
- IEEE‑488 (GPIB) — đầu 24 chân, cần card riêng đắt tiền → **không dùng**
- TRIGGER LINK, cọc INPUT/SENSE mặt sau, khe cắm card quét *(tham khảo)*

**🖼 Hình:**
> **H7.1** — Ảnh mặt sau, **khoanh đỏ cổng RS232 DB‑9**, khoanh xám cổng GPIB.
> **H7.2** — Zoom cổng DB‑9, nhãn "← cổng chúng ta dùng từ buổi 2".

**🎙 Lời giảng:**
> "Lật ra sau. Hai cổng truyền thông: cái 24 chân to là GPIB, cái DB‑9 nhỏ là RS‑232. Chúng ta dùng **cái nhỏ**. Lý do thực tế: card GPIB vài trăm đô, cả phòng có một cái; cáp USB‑to‑serial vài chục nghìn, em nào cũng mua được."

---

### SLIDE 8 — 🎤 3 nhóm báo cáo chuyên đề (25 phút)

**Hiển thị:**
- **5 phút trình bày + 3 phút GV nhận xét** × 3 nhóm
- Rubric chiếu trên màn hình:

| Tiêu chí | % |
|---|---|
| Đúng kỹ thuật, số liệu có trích trang manual | 40 |
| Bảng lệnh SCPI: đủ, có nhóm, có ví dụ | 30 |
| Trình bày rõ, đúng giờ | 20 |
| Trả lời chất vấn | 10 |

- **GV sẽ hỏi:** *"Thông tin này ở trang bao nhiêu trong manual?"*

**🖼 Hình:**
> **H8.1** — Đồng hồ đếm ngược 5:00 lớn (GIF/animation).
> **H8.2** — Bảng rubric font lớn, đọc được từ cuối lớp.

**🎙 Lời giảng:**
> "Mời ba nhóm. 5 phút, thầy bấm giờ, hết giờ là dừng — đó cũng là kỹ năng đề cương yêu cầu.
> Thầy báo trước câu sẽ hỏi: **'thông tin này ở trang bao nhiêu?'** Nếu không trả lời được, nghĩa là slide đó chép trên mạng chứ không đọc manual. Thầy phân biệt được."

---
---

# KHỐI B — RS‑232 QUA USB: KIẾN THỨC NỀN (slide 9–13 · 30 phút)

> ⚠️ **Lưu ý cho GV:** khối này **chỉ giảng, không thực hành** (buổi 2 mới cắm dây).
> Giảng nhanh, nhiều hình, để SV *nhận diện* chứ chưa cần làm. Xen 1 bài tập miệng ở slide 11.

---

### SLIDE 9 — Vì sao dùng RS‑232, và vì sao bắt buộc SCPI

**Hiển thị:**
- Keithley 2000 có 2 giao diện: **GPIB** (nhanh, đắt, cần card) · **RS‑232** (chậm hơn, rẻ, phổ cập) → **ta chọn RS‑232**
- Máy nói được 3 ngôn ngữ, nhưng [tr.83]:

| Ngôn ngữ | GPIB | RS‑232 |
|---|---|---|
| **SCPI** | Yes | **Yes** |
| Keithley 196/199 | Yes | **No** |
| Fluke 8840A/8842A | Yes | **No** |

- 👉 **Dùng RS‑232 ⇒ bắt buộc SCPI. Không có lựa chọn nào khác.**
- 🎁 Tin tốt: học SCPI một lần, điều khiển được **Keysight, Rigol, Tektronix…**

**🖼 Hình:**
> **H9.1** — Bảng trên, ô "No" tô đỏ, ô SCPI/RS‑232 tô xanh có viền nhấp nháy.
> **H9.2** — 2 ảnh cạnh nhau: card GPIB (kèm giá ~vài trăm $) vs cáp USB‑RS232 (kèm giá ~vài chục nghìn đ).

**🎙 Lời giảng:**
> "Vì sao chọn RS‑232? Tiền và tính phổ cập. Card GPIB vài trăm đô, cả phòng có một cái; cáp USB‑to‑serial thì ai cũng mua được.
> Nhưng quan trọng hơn: nhìn bảng này. Máy nói được ba thứ tiếng, nhưng **hai thứ tiếng kia chỉ chạy trên GPIB**. Nghĩa là khi chọn RS‑232, các em **không còn lựa chọn nào ngoài SCPI**.
> Và đó là tin tốt — chỉ phải học một ngôn ngữ. Hơn nữa SCPI là chuẩn chung: ra đi làm gặp máy Keysight hay Rigol, gõ cùng câu lệnh, nó vẫn chạy. Khoản đầu tư rất lời."

---

### SLIDE 10 — Đường đi của một lệnh (tổng quan)

**Hiển thị:**
```
[Laptop] → [Cáp USB-RS232] → [Cổng COMx] → [Cáp DB9 thẳng] → [Keithley: RS232 ON]
```
- **5 mắt xích — hỏng bất kỳ mắt nào, triệu chứng đều giống nhau: IM LẶNG**
- Buổi 2 các em sẽ đi qua từng mắt xích này bằng tay
- Hôm nay chỉ cần **nhớ là có 5 mắt xích**, để buổi 2 không hoảng

**🖼 Hình:**
> **H10.1** — **Hình chủ đạo khối B.** Sơ đồ 5 ô nối mũi tên, mỗi ô 1 ảnh thật nhỏ (laptop · cáp USB‑serial · icon cổng COM · đầu DB9 · mặt sau Keithley). Dưới mỗi ô ghi 1 dòng "hỏng ở đây → triệu chứng gì".

**🎙 Lời giảng:**
> "Bức tranh tổng thể. Một lệnh từ máy tính xuống thiết bị phải qua **năm mắt xích**. Hỏng bất kỳ mắt nào thì kết quả **giống hệt nhau: im lặng**.
> Đó là lý do sinh viên hay bế tắc — triệu chứng chỉ có một, nguyên nhân có năm.
> Hôm nay các em chỉ cần **nhớ sơ đồ này**. Buổi 2 cắm dây thật, thầy sẽ đi qua từng mắt xích và đưa flowchart chẩn đoán."

---

### SLIDE 11 — ⚠️ Cáp: straight‑through, KHÔNG null‑modem

**Hiển thị:**
- Keithley chỉ dùng **3 chân: TXD · RXD · GND** [tr.87]
- **Cáp đúng = straight‑through:** 2↔2, 3↔3, 5↔5
- **Cáp sai = null‑modem:** tráo chéo 2↔3 → **KHÔNG BAO GIỜ CHẠY**
- Manual ghi nguyên văn: *"Do not use a null modem cable."*

**❓ Câu hỏi miệng cho lớp:** *"Nếu dùng nhầm cáp null‑modem, máy có cháy không? Triệu chứng sẽ là gì?"*

**🖼 Hình:**
> **H11.1** — **Sơ đồ 2 panel tự vẽ:**
> - (a) ✅ **STRAIGHT‑THROUGH**: hai đầu DB‑9, 3 đường song song 2–2, 3–3, 5–5. Viền xanh, dấu ✔.
> - (b) ❌ **NULL‑MODEM**: đường 2–3 bắt chéo. Viền đỏ, dấu ✘ to, kèm câu trích nguyên văn manual.
> **H11.2** — Ảnh thật đầu DB9 có đánh số chân.

**🎙 Lời giảng:**
> "Manual viết đúng một câu, in đậm: *đừng dùng cáp null‑modem*.
> *(đặt câu hỏi, chờ SV trả lời)*
> Đáp án: **không cháy gì cả — chỉ im lặng tuyệt đối.** Và đó mới là cái nguy hiểm. Cáp null‑modem tráo chéo chân truyền và chân nhận, nó dùng để nối hai máy tính. Ở đây các em nối máy tính với thiết bị, mà thiết bị đã thiết kế để nối thẳng. Dùng nhầm cáp chéo thì chân truyền đâm vào chân truyền — hai thằng cùng nói, không thằng nào nghe.
> Tin vui: phần lớn cáp USB‑to‑RS232 bán sẵn là loại thẳng, nên các em an toàn. Chỉ cẩn thận khi nối thêm cáp DB9 rời để kéo dài."

---

### SLIDE 12 — ⭐ Thông số RS‑232 của Keithley 2000 *(SLIDE PHẢI THUỘC)*

**Hiển thị:** *(khung đậm, nền nổi bật)* [tr.85–87]

| Tham số | Giá trị |
|---|---|
| **Data bits** | **8** |
| **Stop bits** | **1** |
| **Parity** | **None** |
| Baud | 300 … 19.2k · mặc định xuất xưởng **4800** · **lớp dùng 9600** |
| **Hardware handshake (RTS/CTS)** | ❌ **KHÔNG hỗ trợ** |
| Flow control | `NONE` hoặc `XonXoFF` → **lớp dùng NONE** |
| TX TERM (ký tự máy gửi về) | `LF` / `CR` / `LFCR` → **lớp dùng CR** |

### → **Cấu hình chuẩn của lớp: `9600 · 8 · N · 1 · no handshake · CR`**

**🖼 Hình:**
> **H12.1** — Bảng trên, các ô **8‑N‑1** và **không handshake** tô nền vàng.
> **H12.2** — Dòng **`9600 · 8 · N · 1 · CR`** thiết kế như biển hiệu cỡ lớn ở đáy slide, để SV chụp ảnh.

**🎙 Lời giảng:**
> "Chụp ảnh slide này. Thầy sẽ hỏi lại ở buổi 2 và buổi 3, không báo trước.
> Tám bit dữ liệu, một bit stop, không parity — dân trong nghề gọi tắt là '**tám‑en‑một**'. Baud mặc định xuất xưởng là 4800, nhưng cả lớp thống nhất dùng 9600.
> Dòng gạch chân: **máy này không hỗ trợ handshake phần cứng**. Hai sợi RTS và CTS vô dụng ở đây. Buổi 2, nếu em nào viết Python mà bật `rtscts=True`, chương trình sẽ treo vĩnh viễn chờ một tín hiệu không bao giờ tới. Thầy nói trước để khỏi mất buổi."

---

### SLIDE 13 — Bật RS‑232 trên mặt máy + luật `<CR>`

**Hiển thị:**

**Phần 1 — 5 bước bật RS‑232 *(buổi 2 làm tay)*:**
| # | Bấm | Màn hình hiện |
|---|---|---|
| 1 | `SHIFT` → `RS232` | `RS232: OFF` |
| 2 | `▶` rồi `▲/▼` chọn ON → `ENTER` | `RS232: ON` |
| 3 | chọn **9600** → `ENTER` | `BAUD: 9600` |
| 4 | chọn **NONE** → `ENTER` | `FLOW: NONE` |
| 5 | chọn **CR** → `ENTER` | `TX TERM: CR` |

- ⚠️ Bật RS‑232 ON ⇒ **GPIB tự tắt**
- ⚠️ Lưu trong bộ nhớ không bay hơi — **`*RST` không đổi được, chỉ bấm tay**

**Phần 2 — Luật `<CR>` *(lý thuyết, buổi 2 sẽ gặp)*:**
> Manual [tr.86]: *"Incoming commands are processed after the `<CR>` character is received."*
> ⇒ **Lệnh gửi xuống máy thật phải kết thúc bằng `<CR>` (0x0D = `\r`)**, nếu không máy nằm im.
> - Trong Hercules: gõ `$0D` ở cuối
> - Trong Python (buổi 2): `ser.write(b'*IDN?\r')`
>
> 📌 **Phần mềm giả lập hôm nay KHÔNG yêu cầu `<CR>`** — nhưng đây là luật của máy thật, ghi vào vở.

**🖼 Hình:**
> **H13.1** — Storyboard **5 ảnh chụp thật màn hình VFD**: `RS232: OFF` → `ON` → `BAUD: 9600` → `FLOW: NONE` → `TX TERM: CR`. *Chụp tại lab trước buổi dạy.*
> **H13.2** — Hộp cảnh báo riêng cho luật CR: sơ đồ 2 mũi tên PC ⇄ Keithley, mũi tên đi xuống có ô đỏ `\r` nhãn "BẮT BUỘC ở máy thật".

**🎙 Lời giảng:**
> "Phần trên là năm bước bật RS‑232 trên mặt máy. Buổi 2 các em làm tay, hôm nay chỉ cần biết **nó nằm ở đâu**. Nhớ cái bẫy: lựa chọn này **lưu khi tắt nguồn, và lệnh `*RST` không đổi được**. Nếu nhóm trước để máy ở GPIB, nhóm sau cắm cáp vào sẽ không có gì xảy ra. Vào lab, việc đầu tiên: nhìn xem RS232 đã ON chưa.
>
> Phần dưới là một luật thầy muốn các em **ghi vào vở ngay bây giờ**, dù hôm nay chưa gặp. Manual viết: máy chỉ xử lý lệnh **sau khi nhận được ký tự CR**. Nghĩa là gõ `*IDN?` mà không có CR phía sau thì máy nằm im như khúc gỗ — nó không hỏng, nó đang chờ các em nói hết câu.
>
> Thầy nói rõ: **phần mềm giả lập hôm nay không bắt buộc CR**, vì nó không có cổng thật. Nên các em sẽ không vấp phải hôm nay. Nhưng buổi 2 cắm máy thật thì đây là lỗi số một. Ghi lại: **máy thật — lệnh phải kết thúc bằng `\\r`.**"

---
---
> ## ☕ NGHỈ — 10 PHÚT
> *GV phát: cheat sheet 12 lệnh (slide 17) + 3 phiếu thực hành. Mở sẵn phần mềm giả lập trên máy chiếu.*
---
---

# KHỐI C — ⭐ SCPI: 12 LỆNH (slide 14–20 · 40 phút)
> **Đây là trọng tâm buổi 1. Giảng kỹ, cho ví dụ nhiều, có bài tập tại chỗ.**

---

### SLIDE 14 — SCPI là gì

**Hiển thị:**
- **SCPI** = Standard Commands for Programmable Instruments (đọc "**skippy**")
- Ra đời 1990 — trước đó mỗi hãng một bộ lệnh riêng, đổi máy là học lại từ đầu
- **2 họ lệnh sống chung trong một thiết bị:**

| Họ | Dấu hiệu | Ví dụ | Đặc điểm |
|---|---|---|---|
| **Common commands** | bắt đầu bằng **`*`**, luôn 3 chữ cái | `*IDN?` `*RST` `*CLS` | Chuẩn IEEE‑488.2 — **giống hệt trên MỌI thiết bị** |
| **SCPI commands** | bắt đầu bằng **`:`**, cấu trúc cây | `:SENS:VOLT:DC:NPLC` | Phần lớn giống nhau, có mở rộng riêng hãng |

**🖼 Hình:**
> **H14.1** — 4 ảnh thiết bị khác hãng (Keithley 2000, Keysight 34461A, Rigol DM3058, Tektronix DMM4050) xếp hàng, cùng một bong bóng thoại `:MEAS:VOLT:DC?` chĩa vào cả 4.
> **H14.2** — Sơ đồ 2 nhánh: lệnh `*` vs lệnh `:`, mỗi nhánh 3 ví dụ.

**🎙 Lời giảng:**
> "SCPI đọc là 'skippy'. Trước 1990, mỗi hãng máy đo tự nghĩ bộ lệnh riêng — kỹ sư đổi máy là phải học lại. Rồi cả ngành ngồi lại thoả thuận: từ nay điện áp một chiều gọi là `VOLTage:DC` trên mọi thiết bị.
> Các em để ý có **hai họ lệnh**. Họ bắt đầu bằng **dấu sao** là lệnh chuẩn IEEE‑488.2 — luôn ba chữ cái, và **giống hệt nhau trên mọi máy đo trên đời**. Họ bắt đầu bằng **dấu hai chấm** là cây lệnh SCPI.
> Nhớ phân biệt hai họ này, vì cách đọc chúng khác nhau."

---

### SLIDE 15 — Đọc lệnh SCPI = đọc đường dẫn thư mục

**Hiển thị:**
```
:SENS : VOLT : DC : NPLC   1
  │       │      │     │    └─ giá trị cần đặt
  │       │      │     └────── đặt tốc độ đo
  │       │      └──────────── loại một chiều
  │       └─────────────────── đại lượng điện áp
  └─────────────────────────── khối đo (Sense)
```
- Dấu `:` = dấu `\` trong đường dẫn file → `C:\Sense\Voltage\DC\NPLC`
- **Có `?` ở cuối = câu hỏi, máy trả lời**
- **Không có `?` = mệnh lệnh, máy làm xong rồi im** → *không phản hồi là ĐÚNG, đừng ngồi chờ*
- Manual in chữ **IN HOA** = phần viết tắt hợp lệ (`SYSTem` → `SYST`)
  → 💡 **Lời khuyên: cứ gõ đầy đủ cho dễ đọc**

**Ví dụ đọc thử — gọi SV trả lời:**
| Lệnh | Đọc ra nghĩa là gì? |
|---|---|
| `:SENS:FUNC?` | "Khối đo, chức năng — đang đo cái gì vậy?" |
| `:SENS:VOLT:DC:RANG 10` | "Khối đo, điện áp, một chiều, thang đo — đặt thành 10 V" |
| `:FORM:ELEM READ` | "Định dạng, thành phần — chỉ trả về số đọc thôi" |

**🖼 Hình:**
> **H15.1** — Chuỗi lệnh ở trên với mũi tên chú giải từng phần, font monospace lớn.
> **H15.2** — Hình ẩn dụ: cây thư mục Windows Explorer `C:\Sense\Voltage\DC\` đặt cạnh cây SCPI.

**🎙 Lời giảng:**
> "Đừng sợ SCPI. Nó chính là **đường dẫn thư mục**. Dấu hai chấm chính là dấu gạch chéo.
> Đọc `:SENS:VOLT:DC:NPLC 1` theo nghĩa đen: vào khối đo, vào điện áp, vào loại một chiều, đặt tốc độ bằng một. Nó là tiếng Anh viết tắt, không phải mật mã.
> *(chỉ bảng ví dụ, gọi 2–3 em đọc thành lời)*
> Một luật duy nhất cần nhớ: **có dấu hỏi thì máy mới trả lời**. Gửi `*RST` mà ngồi chờ phản hồi thì chờ cả ngày.
> Về viết tắt — manual in chữ nửa hoa nửa thường, phần hoa là dạng viết tắt hợp lệ. Nhưng thầy khuyên **cứ gõ đầy đủ**: dài hơn vài ký tự, nhưng người đọc code — chính là thầy ở buổi vấn đáp — hiểu ngay."

---

### SLIDE 16 — 3 luật gõ lệnh (chỉ 3 luật, đủ dùng)

**Hiển thị:**

| # | Luật | ❌ Sai | ✅ Đúng |
|---|---|---|---|
| **1** | Tham số của `:FUNC` phải trong **dấu nháy đơn** | `:SENS:FUNC VOLT:DC` | `:SENS:FUNC 'VOLT:DC'` |
| **2** | **Không gõ dấu `< >` `[ ]`** của manual | `:HOLD:STAT <ON>` | `:HOLD:STAT ON` |
| **3** | Phải có **ít nhất 1 dấu cách** giữa lệnh và tham số | `:SENS:VOLT:DC:NPLC1` | `:SENS:VOLT:DC:NPLC 1` |

- 💡 **Thói quen an toàn: gửi từng lệnh một**, đừng gộp nhiều lệnh bằng `;`
  → vì nếu lệnh thứ 3 sai, các lệnh sau **bị bỏ qua trong im lặng**, rất khó debug
- 📌 *(nhắc lại)* Ở **máy thật** còn luật thứ 4: kết thúc bằng `<CR>` — hôm nay giả lập không cần

**🖼 Hình:**
> **H16.1** — Bảng 3 luật, cột Sai nền hồng gạch đỏ, cột Đúng nền xanh dấu ✔. Font monospace lớn.
> **H16.2** — Screenshot một dòng thật trong manual `:NPLCycles <n>` [tr.142], khoanh `<n>` ghi "chỗ này điền số — KHÔNG gõ ngoặc".

**🎙 Lời giảng:**
> "Thầy rút toàn bộ luật cú pháp SCPI xuống còn **ba luật** cho hôm nay. Nhớ ba cái này là gõ đúng 95% trường hợp.
> Luật 1 là chỗ sinh viên sai nhiều nhất: khi chọn hàm đo, tham số phải nằm trong **dấu nháy đơn**. Có nháy thì chạy, không nháy thì lỗi.
> Luật 2: mở manual ra đầy dấu ngoặc vuông và ngoặc nhọn — **những dấu đó không phải lệnh, đừng gõ vào**. Ngoặc nhọn nghĩa là 'chỗ này bạn điền giá trị'.
> Và thói quen: **gửi từng lệnh một**. SCPI cho gộp nhiều lệnh bằng dấu chấm phẩy, nhưng nếu lệnh thứ ba sai thì các lệnh sau bị bỏ qua **trong im lặng** — thiết bị rơi vào trạng thái cấu hình dở dang, vẫn trả số, số trông vẫn hợp lý, nhưng sai. Đó là loại lỗi nguy hiểm nhất: lỗi không hiện ra."

---

### SLIDE 17 — ⭐ 12 LỆNH CẦN DÙNG *(cheat sheet — in phát mỗi SV)*

**Hiển thị:**
```
── BẮT TAY & RESET ──────────────────────────────────
*IDN?                        Kiểm tra kết nối         ⭐
*RST                         Reset về mặc định
*CLS                         Xoá lỗi + trạng thái

── CẤU HÌNH PHÉP ĐO ─────────────────────────────────
:SENS:FUNC 'VOLT:DC'         Chọn hàm đo (nhớ nháy!)
:SENS:FUNC?                  Hỏi: đang đo hàm gì?
:SENS:VOLT:DC:NPLC 1         Tốc độ ↔ độ chính xác
:SENS:VOLT:DC:RANG 10        Cố định thang 10 V
:FORM:ELEM READ              Chỉ trả số, bỏ đơn vị

── LẤY SỐ LIỆU ──────────────────────────────────────
:READ?                       Đo mới + lấy kết quả     ⭐
:FETC?                       Lấy lại số gần nhất
:MEAS:VOLT:DC?               Đo nhanh một phát

── KHI BẾ TẮC ───────────────────────────────────────
:SYST:ERR?                   Hỏi máy: lỗi gì?         ⭐
```

**📌 Hộp phụ 1 — NPLC là gì:**
> NPLC = số chu kỳ điện lưới máy lấy tích phân cho **một** phép đo. Lưới VN 50 Hz ⇒ 1 NPLC = 20 ms. Dải cho phép **0,01 → 10**.
> **NPLC nhỏ → đo nhanh, số nhảy nhiều · NPLC lớn → đo chậm, số đứng yên.**
> Đồ án: bắt đầu `NPLC 1`, cần nhanh thì giảm, cần ổn định thì tăng.

**📌 Hộp phụ 2 — tên các hàm đo khác (dùng với `:SENS:FUNC`):**
> `'VOLT:DC'` · `'VOLT:AC'` · `'CURR:DC'` · `'CURR:AC'` · `'RES'` (Ω 2 dây) · `'FRES'` (Ω 4 dây) · `'FREQ'` · `'PER'` · `'TEMP'`

**🖼 Hình:**
> **H17.1** — Thiết kế **cheat sheet khổ A4 dọc**: nền sáng, font monospace, 4 nhóm màu viền khác nhau, 2 hộp phụ ở dưới. **Xuất file riêng để in phát mỗi SV.**

**🎙 Lời giảng:**
> "Section 5 của manual có hàng trăm lệnh. Thầy rút xuống **mười hai**. Mười hai lệnh này đủ hoàn thành đồ án ở mức đạt yêu cầu; mọi thứ còn lại là để nâng điểm và sẽ học ở buổi 2.
> Ba lệnh thầy đánh sao: `*IDN?` để kiểm tra kết nối, `:READ?` vì dùng nhiều nhất, `:SYST:ERR?` vì nó cứu các em mỗi khi bế tắc.
> Hộp NPLC: nó là thời gian máy 'ngắm' tín hiệu cho mỗi phép đo. Ngắm lâu thì chính xác nhưng chậm — đúng cái đánh đổi thầy nói ở đầu buổi. Đồ án cứ bắt đầu NPLC bằng 1 rồi tinh chỉnh sau.
> Và `:FORM:ELEM READ` — lệnh nhỏ nhưng quan trọng: nó bảo máy chỉ trả về con số, bỏ chữ 'VDC'. Nếu không đặt, buổi 2 hàm `float()` trong Python của các em sẽ báo lỗi. Năm nào cũng có nhóm mắc."

---

### SLIDE 18 — ⭐ `:MEAS?` vs `:READ?` vs `:FETC?`

**Hiển thị:**

| | `:MEAS:VOLT:DC?` | `:READ?` | `:FETC?` |
|---|---|---|---|
| Cấu hình lại máy? | **Có — xoá cấu hình cũ** | Không | Không |
| Kích phép đo mới? | Có | **Có** | **Không** |
| Trả về | Số mới | Số mới | **Số cũ, lặp lại** |
| Dùng khi | Test nhanh 1 phát | **Vòng lặp thu thập dữ liệu** | Đọc lại kết quả vừa có |

```
❌ CÁCH DỞ                      ✅ CÁCH ĐÚNG
lặp 1000 lần:                   *RST
    :MEAS:VOLT:DC?              :SENS:FUNC 'VOLT:DC'
                                :SENS:VOLT:DC:NPLC 1
(mỗi vòng máy cấu hình lại       :SENS:VOLT:DC:RANG 10
 → chậm, mất hết thiết lập)      :FORM:ELEM READ
                                lặp 1000 lần:
                                    :READ?
```

**🖼 Hình:**
> **H18.1** — 2 khối code cạnh nhau: trái viền đỏ nền hồng ❌, phải viền xanh nền xanh ✅.
> **H18.2** — 3 hộp lồng nhau: hộp cam `:MEAS?` bao hộp xanh `:READ?` bao hộp vàng `:FETC?`.

**🎙 Lời giảng:**
> "Ba lệnh cùng để lấy một con số, nhưng khác nhau rất lớn, và nó **quyết định điểm đồ án**.
> `:FETC?` — 'cho xem con số gần nhất'. **Nó không đo lại.** Gọi mười lần có thể nhận đúng một con số lặp mười lần.
> `:READ?` — kích một phép đo mới rồi lấy kết quả.
> `:MEAS?` — còn **cấu hình lại máy từ đầu** trước khi đo.
> Vậy dùng cái nào? `:MEAS?` tiện khi test nhanh một phát. Nhưng trong đồ án nó là lựa chọn tồi, vì **nó xoá hết cấu hình các em vừa đặt** — đặt NPLC, đặt thang đo xong, gọi `:MEAS?` là bay sạch, mỗi vòng lặp.
> Cách đúng nhìn khối bên phải: **cấu hình một lần ở ngoài, trong vòng lặp chỉ gọi `:READ?`**.
> Thầy nói thẳng tiêu chí chấm: buổi 3, nhóm nào nộp code kiểu bên trái thì phần 'tối ưu chương trình' không thể điểm cao. Các em đã được cảnh báo từ hôm nay. Và lát nữa các em sẽ **tự tay chứng minh** điều này trên giả lập."

---

### SLIDE 19 — Khi lỗi: hỏi máy, đừng đoán

**Hiển thị:**
- Gửi **`:SYST:ERR?`** → máy trả `<mã>,"<mô tả>"`. Hết lỗi thì trả `0,"No error"`
- 5 mã hay gặp [tr.209]:

| Mã | Nghĩa | Nguyên nhân thường gặp |
|---|---|---|
| `-113` | Undefined header | Gõ sai tên lệnh (`:MEASU:...`) |
| `-224` | Illegal parameter value | Quên dấu nháy đơn ở `:SENS:FUNC` |
| `-222` | Parameter data out of range | `NPLC 50` (quá 10) |
| `-109` | Missing parameter | Thiếu tham số |
| `0` | No error | Không còn lỗi ✅ |

**🖼 Hình:**
> **H19.1** — Khung terminal nền đen chữ xanh:
> ```
> >>> :MEASU:VOLT:DC?
> (không có gì)
> >>> :SYST:ERR?
> -113,"Undefined header"
> ```
> **H19.2** — Ảnh màn hình máy có chữ **ERR** sáng, khoanh đỏ *(nhắc lại slide 6)*.

**🎙 Lời giảng:**
> "Thiết bị đo không hét vào mặt các em khi có lỗi. Nó lặng lẽ ghi vào hàng đợi và bật chữ ERR bé xíu. Muốn biết lỗi gì, **phải hỏi**.
> Thói quen này phân biệt sinh viên khá và giỏi. Khá thì đọc lại code. Giỏi thì **hỏi thiết bị xem nó không hài lòng chỗ nào**.
> Tập phản xạ ngay hôm nay: cái gì không chạy → gửi `:SYST:ERR?` **trước khi** giơ tay hỏi thầy. Thầy hứa sẽ hỏi lại các em câu đó trước khi trả lời."

---

### SLIDE 20 — 🧩 BÀI TẬP TẠI CHỖ: tìm lỗi trong 5 câu lệnh (6 phút)

**Hiển thị:** *(chiếu cột lệnh trước, cột đáp án hiện sau)*

| # | Câu lệnh | Sai ở đâu? |
|---|---|---|
| 1 | `:SENS:FUNC VOLT:DC` | Thiếu **dấu nháy đơn** → `'VOLT:DC'` · lỗi `-224` |
| 2 | `:HOLD:STAT <ON>` | Gõ cả **dấu ngoặc nhọn** → chỉ `ON` |
| 3 | `:SENS:VOLT:DC:NPLC 50` | NPLC vượt dải 0,01–10 → lỗi `-222` |
| 4 | `:MEASU:VOLT:DC?` | **Sai chính tả** tên lệnh → `:MEAS` · lỗi `-113` |
| 5 | `*RST?` | `*RST` là **mệnh lệnh**, không có dạng truy vấn — bỏ dấu `?` |

**🖼 Hình:**
> **H20.1** — Animation: hiện cột câu lệnh trước, cột "Sai ở đâu" xuất hiện sau khi SV trả lời.
> **H20.2** — Đồng hồ đếm ngược 4:00 + icon 🔍.

**🎙 Lời giảng:**
> "Dừng giảng. Bốn phút, thảo luận theo nhóm. Năm câu lệnh trên màn hình, **cả năm đều sai**. Tìm ra sai ở đâu và sửa thế nào. Nhóm nào tìm đủ năm, thầy ghi nhận vào điểm chuyên cần.
> *(sau 4 phút, chữa từng câu, gọi ngẫu nhiên)*
> Câu số 5 là câu thầy thích nhất: `*RST?`. Lệnh `*RST` là **mệnh lệnh** — bảo máy reset. Thêm dấu hỏi vào là các em đang hỏi máy 'mày reset đi?' — vô nghĩa. Nhớ lại luật ở slide 15: **dấu hỏi chỉ dùng khi hỏi, không dùng khi ra lệnh.**"

---
---

# KHỐI D — ⭐ THỰC HÀNH TRÊN GIẢ LẬP (slide 21–26 · 55 phút)

---

### SLIDE 21 — Phần mềm giả lập Keithley 2000

**Hiển thị:**
- Chương trình Python: **gõ lệnh vào ô nhập → Enter → nhận phản hồi** như máy thật
- **Không cần cổng COM, không cần driver, không cần cáp** → mở ra là chạy
- Nó làm gì:
  - Kiểm tra **cấu trúc lệnh SCPI** có đúng không
  - Đúng → trả về dữ liệu giống máy thật
  - Sai → trả về **đúng mã lỗi** (`-113`, `-222`, `-224`…)
- Mỗi nhóm một bản trên laptop riêng — không phải xếp hàng

**📌 Khác biệt với máy thật *(ghi nhớ)*:**
| | Giả lập hôm nay | Máy thật buổi 2–3 |
|---|---|---|
| Cần cổng COM? | Không | **Có** |
| Cần `<CR>` cuối lệnh? | Không | **Có** |
| Báo lỗi cú pháp? | **Rõ ràng, ngay lập tức** | Phải tự hỏi `:SYST:ERR?` |

**🖼 Hình:**
> **H21.1** — **Screenshot giao diện giả lập** *(chụp trước buổi dạy)*: ô nhập lệnh, khung hiển thị phản hồi, lịch sử lệnh.
> **H21.2** — Sơ đồ đơn giản: `[Ô nhập lệnh] → [Bộ kiểm tra cú pháp SCPI] → [Phản hồi]`. Bên cạnh vẽ mờ sơ đồ buổi 2: `[Python] → [USB-Serial] → [Keithley thật]`, nhãn "câu lệnh giống hệt nhau".

**🎙 Lời giảng:**
> "Hôm nay chúng ta luyện lệnh trên phần mềm giả lập. Nó rất đơn giản: **gõ lệnh vào ô, bấm Enter, xem phản hồi**. Không cần cổng COM, không cần driver, không cần cáp — mở ra là chạy.
> Vì sao dùng giả lập thay vì máy thật? Vì máy thật khi gõ sai thì **im lặng**, người mới học không biết sai ở đâu. Giả lập thì nói thẳng: 'lệnh này sai tên', 'tham số này ngoài dải'. Học nhanh hơn rất nhiều.
> Nhưng các em phải ghi nhớ bảng khác biệt ở dưới: **giả lập dễ tính hơn máy thật**. Nó không bắt các em thêm CR. Buổi 2 thì máy thật sẽ bắt. Thầy nói trước để các em không bị bất ngờ."

---

### SLIDE 22 — 🔬 Thực hành 1: Bắt tay & khám phá (12 phút)

**Hiển thị:** *(phiếu điền tay)*

| # | Gõ lệnh | Ghi kết quả |
|---|---|---|
| 1 | `*IDN?` | ................................... |
| 2 | `*RST` | ................................... |
| 3 | `*CLS` | ................................... |
| 4 | `:SENS:FUNC?` | ................................... |
| 5 | `:SENS:VOLT:DC:NPLC?` | ................................... |
| 6 | `:SENS:VOLT:DC:RANG?` | ................................... |
| 7 | `:SYST:ERR?` | ................................... |

**Câu hỏi ghi vào vở:**
- Lệnh 2 và 3 không trả về gì — đó là **lỗi hay là đúng**? Vì sao?
- Lệnh 4 cho biết gì về trạng thái máy **sau `*RST`**?
- Đối chiếu kết quả lệnh 5 với manual [tr.142]: có khớp không?

**🖼 Hình:**
> **H22.1** — Bảng trên in dạng **phiếu thực hành A4**, phát mỗi nhóm.
> **H22.2** — Góc mờ: kết quả mong đợi của lệnh 1 và 4 *(để GV đối chiếu nhanh khi đi từng bàn)*.

**🎙 Lời giảng:**
> "Mười hai phút. Mở phần mềm, gõ bảy lệnh theo đúng thứ tự, điền vào phiếu. Thầy đi từng bàn.
> Lệnh 2 và 3 không trả về gì — **đó là đúng**, vì chúng không có dấu hỏi. Đây là chỗ thầy muốn các em tự xác nhận lại luật ở slide 15, chứ không phải nghe rồi quên.
> Lệnh 4 rất thú vị: sau khi `*RST`, các em hỏi máy đang đo hàm gì. Kết quả sẽ cho các em biết **mặc định của máy là gì** — và đó là thông tin cực hữu dụng khi viết chương trình, vì nó cho biết cái gì các em không cần gõ.
> Lệnh 5 thì đối chiếu với manual. Đây là cách **kiểm chứng tài liệu bằng thực nghiệm** — một thói quen rất đáng giá."

---

### SLIDE 23 — 🔬 Thực hành 2: Cấu hình & đo (18 phút)

**Hiển thị:**

**Phần A — chạy đúng quy trình cấu hình chuẩn:**
```
*RST
*CLS
:SENS:FUNC 'VOLT:DC'
:SENS:VOLT:DC:NPLC 1
:SENS:VOLT:DC:RANG 10
:FORM:ELEM READ
:READ?
```

**Phần B — thí nghiệm so sánh, ghi lại số:**
| Thao tác | Kết quả |
|---|---|
| Gõ `:FETC?` **3 lần liên tiếp** | ........ / ........ / ........ |
| Gõ `:READ?` **3 lần liên tiếp** | ........ / ........ / ........ |
| **Nhận xét:** hai nhóm số khác nhau ở điểm gì? Vì sao? | |

**Phần C — chứng minh tác hại của `:MEAS?`:**
| Bước | Lệnh | Ghi kết quả |
|---|---|---|
| 1 | `:SENS:VOLT:DC:NPLC 10` | (đặt NPLC = 10) |
| 2 | `:SENS:VOLT:DC:NPLC?` | ........ *(phải là 10)* |
| 3 | `:MEAS:VOLT:DC?` | ........ |
| 4 | `:SENS:VOLT:DC:NPLC?` | ........ ← **NPLC còn là 10 không?** |

**🖼 Hình:**
> **H23.1** — Code block phần A, nền tối, đánh số dòng.
> **H23.2** — Bảng phần B và C với ô trống to để SV viết tay, phần C có icon 💡 "tự chứng minh slide 18".

**🎙 Lời giảng:**
> "Mười tám phút, ba phần.
> Phần A là quy trình cấu hình chuẩn — chính là **khung xương đồ án** của các em. Gõ cho quen tay.
> Phần B là thí nghiệm thầy muốn các em **tự chứng minh**: gõ `:FETC?` ba lần, rồi `:READ?` ba lần. Các em sẽ thấy `:FETC?` trả về **cùng một con số ba lần**, còn `:READ?` trả về **ba số khác nhau**. Đó là bằng chứng thực nghiệm cho slide 18.
> Phần C là phần thầy tâm đắc nhất. Các em đặt NPLC bằng 10, kiểm tra lại thấy đúng là 10. Rồi gọi `:MEAS:VOLT:DC?`. Rồi kiểm tra NPLC lần nữa. **Các em sẽ thấy nó không còn là 10 nữa.**
> Đó chính xác là điều thầy cảnh báo ở slide 18 — `:MEAS?` xoá sạch cấu hình. Và bây giờ các em không phải tin lời thầy nữa, các em **tự chứng minh được**. Nhóm nào làm xong phần C và giải thích được, thầy coi như đã nắm bài quan trọng nhất của buổi."

---

### SLIDE 24 — 💥 Thực hành 3: Phá hoại có chủ đích (10 phút)

**Hiển thị:** *(bắt buộc, không phải tuỳ chọn)*

| # | Cố tình gõ sai | Mã lỗi nhận được | Sửa thế nào |
|---|---|---|---|
| 1 | `:SENS:FUNC VOLT:DC` | ............ | ............ |
| 2 | `:SENS:VOLT:DC:NPLC 50` | ............ | ............ |
| 3 | `:MEASU:VOLT:DC?` | ............ | ............ |
| 4 | `:HOLD:STAT <ON>` | ............ | ............ |
| 5 | `*RST?` | ............ | ............ |

*(sau mỗi lệnh sai, gõ `:SYST:ERR?` để đọc mã lỗi)*

**🖼 Hình:**
> **H24.1** — Bảng trên, icon 💥, viền cam cảnh báo, ô trống to.
> **H24.2** — Thu nhỏ bảng 5 mã lỗi ở slide 19, đặt góc phải để SV đối chiếu.

**🎙 Lời giảng:**
> "Mười phút, và phần này **bắt buộc**, không phải cho vui.
> Các em sẽ cố tình gõ sai năm kiểu — chính là năm câu ở bài tập slide 20 — rồi hỏi `:SYST:ERR?` xem máy phàn nàn gì, ghi lại mã lỗi.
> Vì sao bắt làm? Vì **trong đồ án các em sẽ gõ sai, chắc chắn**. Nếu đã từng nhìn thấy mã `-113` và biết nó nghĩa là 'sai tên lệnh', các em sửa trong ba mươi giây. Chưa từng thấy thì ngồi đoán nửa tiếng.
> **Hôm nay chúng ta gây lỗi trong môi trường an toàn, để buổi 3 không hoảng loạn.**"

---

### SLIDE 25 — 🏆 Thử thách nhóm: tự viết chuỗi lệnh (10 phút)

**Hiển thị:**
> **Đề bài:** Khách hàng yêu cầu đo **điện trở 2 dây**, cần **số liệu rất ổn định** (ưu tiên chính xác hơn tốc độ), và chương trình phải **lấy 5 số đo liên tiếp**.
>
> **Yêu cầu:** Viết chuỗi lệnh SCPI hoàn chỉnh, gõ thử trên giả lập, ghi lại kết quả.

**Gợi ý khung *(hiện sau 4 phút nếu lớp bí)*:**
```
*RST
*CLS
:SENS:FUNC '____'          ← hàm đo nào?
:SENS:RES:NPLC ____        ← ổn định ⇒ NPLC lớn hay nhỏ?
:FORM:ELEM READ
:READ?   (× 5 lần)
```

**Nhóm nào xong trước, trả lời thêm:**
- Nếu khách đổi ý, muốn **đo thật nhanh** thay vì chính xác — sửa dòng nào?
- Nếu đo **điện trở 4 dây** — đổi tham số thành gì?

**🖼 Hình:**
> **H25.1** — Slide dạng "đề bài" nền vàng nhạt, icon 🏆, đồng hồ đếm ngược 10:00.
> **H25.2** — Khung gợi ý thiết kế dạng "điền vào chỗ trống", các ô `____` nổi bật.

**🎙 Lời giảng:**
> "Mười phút, thử thách cuối. Thầy không đưa lệnh sẵn nữa — các em **tự ghép**.
> Đề bài có ba manh mối. 'Điện trở 2 dây' — tra hộp phụ trên cheat sheet xem tên hàm là gì. 'Số liệu rất ổn định, ưu tiên chính xác' — nhớ lại NPLC lớn hay nhỏ? 'Lấy 5 số đo liên tiếp' — dùng `:READ?` hay `:FETC?`, và vì sao?
> Đây chính là dạng bài các em sẽ gặp ở đồ án: **khách hàng nói bằng tiếng Việt, các em dịch sang SCPI.** Đó mới là kỹ năng thật, chứ không phải thuộc lòng lệnh.
> Nhóm nào xong sớm thì làm hai câu hỏi phụ."

---

### SLIDE 26 — Chữa bài & 5 điều chốt lại (5 phút)

**Hiển thị:** *(GV điền trực tiếp khi dạy)*
- Lỗi phổ biến nhất của lớp hôm nay: .......................................
- Đáp án Thử thách nhóm: `'RES'` · NPLC **10** (lớn = ổn định) · `:READ?` × 5
  - Đo nhanh ⇒ đổi `NPLC 0.01` · Đo 4 dây ⇒ `'FRES'`

**5 điều bắt buộc nhớ:**
1. Lệnh **không có `?`** thì **không có phản hồi** — đừng ngồi chờ
2. `:SENS:FUNC` phải có **dấu nháy đơn**
3. `:FETC?` lấy số **cũ** · `:READ?` đo **mới** · `:MEAS?` **xoá cấu hình**
4. **NPLC lớn = chính xác & chậm · NPLC nhỏ = nhanh & nhiễu**
5. Lỗi không tự hiện ra — phải hỏi **`:SYST:ERR?`**

**🖼 Hình:**
> **H26.1** — Slide dạng bảng trắng, có khung trống để GV gõ/viết trực tiếp.
> **H26.2** — 5 điểm chốt dạng icon lớn, đọc được từ cuối lớp.

**🎙 Lời giảng:**
> "Dừng tay, thầy tổng hợp. *(chữa Thử thách nhóm, điền lỗi phổ biến nhất quan sát được)*
> Năm điều trên màn hình. Em nào ghi được cả năm vào vở thì buổi hôm nay coi như thành công.
> Và thầy nhắc lại điều số 3 — đó là điều thầy sẽ hỏi ở buổi 3, và là điều các em vừa **tự tay chứng minh** chứ không phải nghe thầy nói."

---
---

# KHỐI E — LÀM QUEN HERCULES *(chuẩn bị buổi 2)* (slide 27–28 · 10 phút)

> ⚠️ **Lưu ý GV:** chỉ **giới thiệu giao diện**, không nối vào đâu cả (chưa có máy thật, giả lập không dùng COM).
> Mục tiêu duy nhất: SV **tải về, cài sẵn, biết các ô cần điền** để buổi 2 vào là chạy ngay.

---

### SLIDE 27 — Hercules: công cụ của buổi 2

**Hiển thị:**
- **Hercules SETUP Utility** (HW‑group) — miễn phí, **portable, không cần cài**
- Là "bộ đàm" để nói chuyện trực tiếp với thiết bị **mà không cần viết code**
- Buổi 2 dùng tab **Serial**, 6 ô phải điền:

| Ô | Điền |
|---|---|
| Name | `COMx` *(buổi 2 mới biết số)* |
| Baud | `9600` |
| Data size | `8` |
| Parity | `none` |
| **Handshake** | **`OFF`** ← vì Keithley không hỗ trợ |
| Mode | `Free` |

- Bấm **Open** → chữ chuyển xanh = cổng đã mở
- ⚠️ Hercules **không tự thêm `<CR>`** → phải gõ **`$0D`** ở cuối mỗi lệnh
  → `*IDN?$0D`

**🖼 Hình:**
> **H27.1** — **Screenshot toàn cửa sổ Hercules tab Serial**, khoanh đỏ đánh số 1→6 đúng các ô cần chỉnh.
> **H27.2** — Zoom ô Send với chuỗi `*IDN?$0D`, khoanh đỏ phần `$0D`, ghi chú "= ký tự CR, bắt buộc với máy thật".

**🎙 Lời giảng:**
> "Mười phút cuối, thầy giới thiệu công cụ các em sẽ dùng ở buổi 2. Hôm nay **chưa dùng được**, vì chưa có máy thật và phần mềm giả lập của chúng ta không qua cổng COM. Nên các em chỉ cần **nhìn và nhớ mặt**.
> Hercules là phần mềm miễn phí, tải về chạy luôn không cần cài. Nó cho phép nói chuyện với thiết bị **mà không cần viết một dòng code nào** — đây là công cụ kỹ sư thật sự dùng, không phải đồ chơi dạy học.
> Sáu ô thầy khoanh đỏ. Chú ý ô **Handshake để OFF** — nhớ lại slide 12: Keithley không hỗ trợ handshake phần cứng.
> Và cái quan trọng nhất, nối lại với luật CR ở slide 13: **Hercules không tự thêm ký tự xuống dòng**. Các em phải gõ `$0D` ở cuối mỗi lệnh — đó là cú pháp của Hercules nghĩa là 'chèn byte hex 0D vào đây'. Buổi 2, nếu nhóm nào gõ `*IDN?` mà máy im lặng, thì chín mươi phần trăm là quên `$0D`. Thầy nói trước để tiết kiệm cho các em hai mươi phút."

---

### SLIDE 28 — Việc cần làm trước buổi 2 + cầu nối sang Python

**Hiển thị:**

**Trước buổi 2, mỗi SV phải:**
- ☐ Tải Hercules về, giải nén, **mở thử xem giao diện**
- ☐ Cài **Python 3.x** + chạy `pip install pyserial`
- ☐ *(khuyến khích)* Mượn/mua **cáp USB‑RS232**, cắm thử xem máy có nhận cổng COM không

**Và đây là thứ các em sẽ viết ở buổi 2 — chỉ 4 dòng:**

| Thao tác trong Hercules | Dòng Python tương đương |
|---|---|
| Chọn COM + Baud, bấm Open | `ser = serial.Serial('COM3', 9600, timeout=1)` |
| Gõ `*IDN?$0D` rồi Send | `ser.write(b'*IDN?\r')` |
| Đọc khung nhận | `resp = ser.read_until(b'\r').decode()` |
| Bấm Close | `ser.close()` |

> **Python không làm gì khác Hercules. Nó chỉ làm việc đó nhanh hơn và lặp lại được.**

**🖼 Hình:**
> **H28.1** — **Split‑screen:** trái screenshot Hercules, phải 4 dòng Python. Vẽ 4 mũi tên cong nối từng ô sang từng dòng code.
> **H28.2** — Mockup phác thảo GUI sẽ xây ở buổi 2 (combobox chọn COM, nút Connect, ô nhập lệnh, bảng dữ liệu, đồ thị) — tạo động lực.

**🎙 Lời giảng:**
> "Và đây là lý do thầy cho các em xem Hercules dù hôm nay chưa dùng. Nhìn bảng đối chiếu: **mỗi thao tác tay trong Hercules tương ứng với đúng một dòng Python.**
> Nghĩa là buổi 2, khi các em viết chương trình, các em **không học thêm khái niệm mới nào về truyền thông** — chỉ tự động hoá cái tay mình làm.
> Hình bên phải là thứ các em sẽ xây: một giao diện thật, chọn cổng, đồ thị thời gian thực, xuất CSV. Về nhà cài sẵn Python và pyserial để buổi sau vào là code luôn, đừng mất giờ cài đặt."

---
---

# KHỐI F — CHỐT & GIAO VIỆC (slide 29–32 · 5 phút)

---

### SLIDE 29 — 8 điều mang về

**Hiển thị:**
1. Keithley 2000 điều khiển được qua **GPIB** hoặc **RS‑232** — ta dùng RS‑232
2. Dùng RS‑232 ⇒ **bắt buộc SCPI**
3. Cấu hình chuẩn: **`9600 · 8 · N · 1 · no handshake · CR`**
4. SCPI đọc như **đường dẫn thư mục** · **có `?` mới có trả lời**
5. `:SENS:FUNC` phải có **dấu nháy đơn**
6. `:FETC?` số cũ · `:READ?` số mới · **`:MEAS?` xoá cấu hình**
7. Đồ án: **cấu hình 1 lần + `:READ?` trong vòng lặp**
8. Bế tắc ⇒ **`:SYST:ERR?`**

**🖼 Hình:** **H29.1** — 8 dòng đánh số lớn, mỗi dòng 1 icon. Dòng 6 và 7 tô nền nổi bật.

**🎙 Lời giảng:**
> "Tám điều, chụp ảnh. Nếu chỉ nhớ được hai, thầy mong là điều 6 và 7 — vì đó là ranh giới giữa đồ án chạy được và đồ án làm tốt."

---

### SLIDE 30 — Giao việc trước buổi 2

**Hiển thị:**

**Cá nhân — bắt buộc:**
- ☐ **Thuộc 12 lệnh** trong cheat sheet
- ☐ Đọc **Section 4 phần RS‑232 [tr.85–87]** — chỉ 3 trang
- ☐ Cài **Python 3.x** + `pip install pyserial` + tải **Hercules**
- ☐ *(khuyến khích mạnh)* Kiếm **cáp USB‑RS232**, cắm thử ở nhà

**Nhóm — bắt buộc (sản phẩm chấm điểm buổi 1):**
- ☐ **Bảng tổng hợp lệnh SCPI** — tối thiểu **20 lệnh**, mỗi lệnh có:
  cú pháp · tham số & dải hợp lệ · **giá trị mặc định** · **ví dụ đã chạy thật trên giả lập** · **số trang manual**
- ☐ **Slide báo cáo** (bản chỉnh sửa sau nhận xét hôm nay)
- ☐ **File phân công nhiệm vụ** có tên nhóm trưởng

**Cộng điểm:**
- ☐ Nộp kèm **log phiên thực hành** trên giả lập (ảnh chụp hoặc file xuất)

**🖼 Hình:**
> **H30.1** — Checklist 3 khối màu (đỏ = cá nhân, cam = nhóm, xanh = cộng điểm).
> **H30.2** — Icon 📅 + deadline cụ thể ngày/giờ.

**🎙 Lời giảng:**
> "Việc về nhà. Về **Bảng lệnh SCPI** — thầy chỉ yêu cầu **hai mươi lệnh**, nhưng đổi lại thầy đòi chất lượng.
> Thầy **không** nhận bảng chép lại mục lục manual. Thầy muốn thấy cột **dải giá trị hợp lệ** và **giá trị mặc định** — hai cột đó chứng minh các em đã đọc bảng trong manual chứ không chỉ chép tên lệnh. Và mỗi lệnh phải có **một ví dụ các em đã thật sự gõ trên giả lập** — thầy sẽ kiểm tra bằng cách hỏi 'kết quả trả về là gì'."

---

### SLIDE 31 — Cách tính điểm (nhắc lại theo đề cương)

**Hiển thị:**
- GV cho **01 điểm chung** cho sản phẩm cả nhóm (Slide + Cuốn báo cáo + Mã nguồn + Chạy phần cứng)
- **Quỹ điểm cá nhân = Điểm_Nhóm × Số thành viên**
- Nhóm trưởng họp cả nhóm **tự chia quỹ** theo đóng góp thực tế
- ⚠️ File chia điểm phải có **đồng thuận của TẤT CẢ thành viên**

> **Ví dụ:** nhóm 5 người, Điểm_Nhóm 8,0 → quỹ 40 → chia 9 / 8,5 / 8 / 7,5 / 7 *(tổng = 40 ✔)*

**🖼 Hình:**
> **H31.1** — Sơ đồ phễu: [Sản phẩm nhóm] → [Điểm_Nhóm 8,0] → [× 5 = quỹ 40] → [5 ô điểm cá nhân].
> **H31.2** — Icon ✍️ × 5 cạnh dòng "cần đồng thuận tất cả".

**🎙 Lời giảng:**
> "Thầy chấm một điểm chung cho nhóm, nhân số thành viên ra quỹ, rồi **chính các em tự chia**.
> Có chủ đích: nó buộc nhóm trưởng phải thực sự quản lý, và khiến bạn nào định 'đi nhờ xe' phải suy nghĩ — vì người quyết định điểm của em không phải thầy, mà là bốn người bạn biết rõ em đã làm gì.
> Điều kiện: file chia điểm phải có **đồng thuận của tất cả**. Một người không đồng ý là thầy không nhận. Nên **phân công rõ ràng ngay từ hôm nay** và ghi lại ai làm gì."

---

### SLIDE 32 — Kết & Hỏi đáp

**Hiển thị:**
> **Câu hỏi suy nghĩ trước buổi 2:**
> *"Hôm nay trên giả lập, gõ `*IDN?` là có trả lời ngay. Buổi 2 trên máy thật, gõ y hệt vậy mà không có gì. Theo các em, có bao nhiêu nguyên nhân có thể xảy ra?"*

- Kênh nộp bài / deadline / liên hệ

**🖼 Hình:**
> **H32.1** — Nền tối, câu hỏi cỡ chữ lớn giữa slide, icon 🤔.
> **H32.2** — Góc dưới: thông tin nộp bài + QR code.

**🎙 Lời giảng:**
> "Một câu hỏi để các em suy nghĩ tới buổi sau. Hôm nay gõ `*IDN?` là có trả lời ngay, vì giả lập rất dễ tính. Buổi 2 trên máy thật, gõ y hệt mà im lặng — **có bao nhiêu nguyên nhân có thể?**
> Gợi ý: nhìn lại slide 10, cái sơ đồ năm mắt xích. Cộng thêm luật CR ở slide 13. Các em sẽ ra được một danh sách.
> Nhóm nào về nhà liệt kê được danh sách đó, buổi 2 các em sẽ debug nhanh gấp ba lần cả lớp. Hẹn gặp lại. Ai còn thắc mắc thì ở lại hỏi thầy."

---
---

# PHỤ LỤC A — HÌNH ẢNH CẦN CHUẨN BỊ

### ⭐ Phải chụp thật (ưu tiên cao nhất)
| Mã | Nội dung | Slide |
|---|---|---|
| **H21.1** | **Giao diện phần mềm giả lập** *(quan trọng nhất — dùng cả khối D)* | 21 |
| **H13.1** | Storyboard 5 ảnh màn hình VFD: RS232 OFF→ON→BAUD→FLOW→TX TERM | 13 |
| **H27.1** | Hercules tab Serial, khoanh 6 ô cần điền | 27 |
| H6.1 / H6.2 | Màn hình VFD + 4 đèn; ảnh REM+ERR sáng | 6, 19 |
| H5.1 | Mặt trước, khoanh 3 phím | 5 |
| H7.1 | Mặt sau, khoanh cổng RS232 | 7 |

### Crop / vẽ lại từ PDF manual
| Mã | Nguồn | Slide |
|---|---|---|
| H3 | Figure 2‑1 [tr.14] — vùng cọc đấu + cảnh báo điện áp | 3 |
| H9.1 | Table 4‑1 [tr.83] — bảng ngôn ngữ × giao diện | 9 |
| H11.1 | Figure 4‑1 + Table 4‑2 [tr.87] — sơ đồ chân DB‑9 | 11 |
| H16.2 | Table 5‑6 [tr.142] — dòng `:NPLCycles <n>` | 16 |
| H19.x | Table B‑1 [tr.209] — bảng mã lỗi | 19 |

### Sơ đồ tự vẽ (xếp theo độ quan trọng)
| Mã | Slide | Mô tả | ƯT |
|---|---|---|---|
| **H17.1** | 17 | **Cheat sheet 12 lệnh khổ A4 — in phát mỗi SV** | ★★★ |
| **H18.1** | 18 | **2 khối code ❌/✅ + 3 hộp lồng nhau** | ★★★ |
| **H15.1** | 15 | **Lệnh SCPI = đường dẫn thư mục** | ★★★ |
| **H11.1** | 11 | **Straight‑through ✅ vs Null‑modem ❌** | ★★ |
| H10.1 | 10 | Chuỗi 5 mắt xích laptop → Keithley | ★★ |
| H12.2 | 12 | Biển hiệu `9600 · 8 · N · 1 · CR` | ★★ |
| H28.1 | 28 | Split‑screen Hercules ↔ Python | ★★ |
| H14.x | 14 | 4 thiết bị khác hãng cùng nói SCPI | ★ |
| H2.1 | 2 | 3 ô chevron lộ trình 3 buổi | ★ |
| H31.1 | 31 | Phễu chia điểm | ★ |

---

# PHỤ LỤC B — TÀI LIỆU IN PHÁT

| # | Tài liệu | Số bản | Nguồn |
|---|---|---|---|
| 1 | **Cheat sheet 12 lệnh SCPI** (A4) | **1/SV** | Slide 17 |
| 2 | Phiếu thực hành 1 — Bắt tay (7 lệnh) | 1/nhóm | Slide 22 |
| 3 | Phiếu thực hành 2 — Cấu hình & đo (3 phần) | 1/nhóm | Slide 23 |
| 4 | Phiếu thực hành 3 — 5 lỗi cố ý | 1/nhóm | Slide 24 |
| 5 | Phiếu Thử thách nhóm | 1/nhóm | Slide 25 |
| 6 | Rubric báo cáo + yêu cầu Bảng lệnh SCPI | 1/nhóm | Slide 8, 30 |

---

# PHỤ LỤC C — ĐẶC TẢ PHẦN MỀM GIẢ LẬP

> **Kiến trúc:** KHÔNG dùng cổng COM / COM ảo. Chỉ là **ô nhập lệnh → bộ kiểm tra cú pháp SCPI → ô hiển thị phản hồi**, kèm lịch sử lệnh.

### Phải trả lời đúng 12 lệnh ở slide 17
| Lệnh | Phản hồi |
|---|---|
| `*IDN?` | `KEITHLEY INSTRUMENTS INC.,MODEL 2000,1234567,A20 /A02` |
| `*RST` | *(không phản hồi)* — reset trạng thái nội bộ về: FUNC=`VOLT:DC`, NPLC=1, RANG=auto, FORM:ELEM=có đơn vị |
| `*CLS` | *(không phản hồi)* — xoá hàng đợi lỗi |
| `:SENS:FUNC?` | `"VOLT:DC"` |
| `:SENS:FUNC 'VOLT:DC'` | *(không phản hồi)* |
| `:SENS:VOLT:DC:NPLC?` | `+1.00000000E+00` · `? MAX` → `+1.00000000E+01` · `? MIN` → `+1.00000000E-02` |
| `:SENS:VOLT:DC:RANG?` | giá trị thang hiện tại |
| `:FORM:ELEM READ` | *(không phản hồi)* — bỏ hậu tố `VDC` ở các lần đọc sau |
| **`:READ?`** | **số ngẫu nhiên quanh một giá trị, ĐỔI MỖI LẦN GỌI** |
| **`:FETC?`** | **LẶP LẠI đúng số của `:READ?` gần nhất** ← bắt buộc, phục vụ Thực hành 2B |
| **`:MEAS:VOLT:DC?`** | **đo mới VÀ reset cấu hình về mặc định** ← bắt buộc, phục vụ Thực hành 2C |
| `:SYST:ERR?` | lỗi trong hàng đợi; hết thì `0,"No error"` |

### Phải bắt đúng 5 lỗi của Thực hành 3
| Tình huống | Mã lỗi |
|---|---|
| `:SENS:FUNC VOLT:DC` *(thiếu nháy)* | `-224,"Illegal parameter value"` |
| `:SENS:VOLT:DC:NPLC 50` *(quá dải 0,01–10)* | `-222,"Parameter data out of range"` |
| `:MEASU:VOLT:DC?` *(sai tên lệnh)* | `-113,"Undefined header"` |
| `:HOLD:STAT <ON>` *(gõ cả ngoặc)* | `-224,"Illegal parameter value"` |
| `*RST?` *(mệnh lệnh mà thêm `?`)* | `-113,"Undefined header"` |
| Lệnh không có `?` | **Không trả gì** *(phải đúng — bài học slide 15)* |

### Phải hỗ trợ Thử thách nhóm (slide 25)
- Các hàm: `'RES'` · `'FRES'` · `'VOLT:AC'` · `'CURR:DC'` · `'FREQ'` …
- `:SENS:RES:NPLC <n>` và các nhánh tương ứng cho từng hàm
- `:READ?` trả về giá trị **hợp lý theo hàm đang chọn** (Ω trả số ohm, V trả số volt…)

### Nên có
- **Nút xuất log** phiên làm việc → SV nộp kèm báo cáo *(gắn với mục cộng điểm slide 30)*
- Hiển thị **trạng thái nội bộ hiện tại** (FUNC / NPLC / RANGE) ở góc màn hình → giúp SV *nhìn thấy* `:MEAS?` xoá cấu hình ở Thực hành 2C
- Lịch sử lệnh cuộn được, mũi tên ↑ gọi lại lệnh trước

### KHÔNG cần làm
- ❌ Cổng COM ảo / com0com / socket
- ❌ Bắt buộc `<CR>` cuối lệnh *(để buổi 2 dạy cùng pyserial)*
- ❌ Mô phỏng baud rate, độ trễ truyền

---

# PHỤ LỤC D — DỰ PHÒNG

| Rủi ro | Xử lý |
|---|---|
| Cháy giờ ở phần SV báo cáo | Cắt slide 4 và 10; dời 1 nhóm sang đầu buổi 2 |
| Giả lập không chạy trên máy SV | Bản `.exe` đóng gói sẵn + bản web (nếu làm được) + 2 laptop GV cho mượn |
| Lớp ngộp ở khối SCPI | Bỏ slide 14, vào thẳng slide 15 (đường dẫn thư mục) → 16 → 17 |
| Lớp đi nhanh hơn dự kiến | Thử thách nhóm thêm đề: *"đo tần số, lấy 10 mẫu, ưu tiên tốc độ"* |
| Không kịp khối E (Hercules) | Chuyển thành video 3 phút gửi SV xem ở nhà — **không ảnh hưởng buổi 1** |

---

*Bản đầy đủ 55 slide vẫn lưu ở `Buoi1_DanY_Slide_GiangDay.md` — dùng làm kho tham khảo cho buổi 2.*
