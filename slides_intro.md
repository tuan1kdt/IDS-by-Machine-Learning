---
marp: true
theme: gaia
size: 16:9
paginate: true
backgroundColor: #1a1a2e
color: #eaeaea
style: |
  section {
    font-family: 'Helvetica Neue', 'Segoe UI', sans-serif;
    padding: 60px 80px;
  }
  h1 {
    color: #4fc3f7;
    border-bottom: 3px solid #4fc3f7;
    padding-bottom: 12px;
    font-size: 1.8em;
  }
  h2 {
    color: #81d4fa;
    font-size: 1.3em;
    margin-top: 0;
  }
  ul {
    font-size: 0.85em;
    line-height: 1.7;
  }
  li::marker {
    color: #4fc3f7;
  }
  strong {
    color: #ffd54f;
  }
  section.title {
    background: linear-gradient(135deg, #0f3460 0%, #16213e 100%);
    text-align: center;
  }
  section.title h1 {
    border: none;
    font-size: 2.2em;
    color: #4fc3f7;
  }
  section.title h2 {
    color: #b0bec5;
    font-weight: 300;
  }
  footer {
    color: #78909c;
    font-size: 0.6em;
  }
  /* Two-column layout */
  section.split {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto 1fr;
    gap: 0 30px;
    align-content: start;
  }
  section.split h1 {
    grid-column: 1 / span 2;
  }
  section.split .col {
    padding: 18px 22px;
    border-radius: 8px;
  }
  section.split .pros {
    background: rgba(76, 175, 80, 0.10);
    border-left: 4px solid #66bb6a;
  }
  section.split .cons {
    background: rgba(244, 67, 54, 0.10);
    border-left: 4px solid #ef5350;
  }
  section.split .col h2 {
    margin-bottom: 8px;
  }
  section.split .pros h2 {
    color: #81c784;
  }
  section.split .cons h2 {
    color: #e57373;
  }
  section.split ul {
    font-size: 0.78em;
    margin-top: 6px;
    padding-left: 22px;
  }
  section.split p {
    font-size: 0.78em;
    margin: 6px 0;
  }
  /* Section divider */
  section.divider {
    background: linear-gradient(135deg, #0f3460 0%, #1a1a2e 100%);
    text-align: center;
    justify-content: center;
  }
  section.divider h1 {
    border: none;
    font-size: 2.4em;
    color: #4fc3f7;
  }
  section.divider h2 {
    color: #b0bec5;
    font-weight: 300;
    font-size: 1.1em;
  }
  /* Two-column with image / structured content */
  section.cols2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto 1fr;
    gap: 0 30px;
    align-content: start;
  }
  section.cols2 h1 {
    grid-column: 1 / span 2;
  }
  section.cols2 .col {
    padding: 14px 20px;
  }
  section.cols2 ul {
    font-size: 0.78em;
  }
  section.cols2 .col img {
    max-width: 100%;
    max-height: 480px;
    object-fit: contain;
    border-radius: 6px;
  }
  /* Code-like block for packet structure */
  .packet-stack {
    font-family: 'Menlo', 'Consolas', monospace;
    font-size: 0.65em;
    line-height: 1.3;
    background: rgba(255,255,255,0.04);
    border-radius: 6px;
    padding: 12px;
    margin-top: 10px;
  }
  .packet-stack .layer {
    padding: 6px 10px;
    margin: 3px 0;
    border-radius: 4px;
    color: #1a1a2e;
    font-weight: 600;
  }
  .layer-eth   { background: #b39ddb; }
  .layer-ip    { background: #81d4fa; }
  .layer-tcp   { background: #80cbc4; }
  .layer-data  { background: #ffcc80; }
  /* 5-tuple highlight box */
  .tuple-box {
    background: rgba(79, 195, 247, 0.10);
    border: 1px solid #4fc3f7;
    border-radius: 8px;
    padding: 12px 18px;
    font-family: 'Menlo', monospace;
    font-size: 0.72em;
    margin-top: 10px;
  }
  .tuple-box .label {
    color: #4fc3f7;
    font-weight: 600;
  }
header: '🛡️ AI-Powered IDS using Machine Learning'
footer: 'TDTU — Master Thesis 2026'
---

<!-- _class: title -->
<!-- _paginate: false -->
<!-- _header: '' -->

# AI-Powered Intrusion Detection System

## Real-Time Detection of Network Attacks using Machine Learning

**Le Anh Tuan · To Hoang Dao · Nguyen Tu Thanh Duy**
Ton Duc Thang University — 2026

---

# IDS là gì?

- **Intrusion Detection System (IDS)** là hệ thống giám sát liên tục lưu lượng mạng, phát hiện các hành vi bất thường hoặc vi phạm chính sách bảo mật.

- IDS là lớp phòng thủ trong chiến lược **Defense-in-Depth** — không thay thế Firewall mà bổ sung khả năng phát hiện sau khi traffic đã đi qua.

- Khi phát hiện tấn công, IDS gửi cảnh báo đến **Security Operations Center (SOC)** để phân tích và phản ứng kịp thời.

- Phân biệt: **IDS** (phát hiện & cảnh báo) vs **IPS** (phát hiện & chặn tự động).

---

# Các loại IDS truyền thống

- **Signature-based IDS** — so sánh traffic với cơ sở dữ liệu các mẫu tấn công đã biết (chữ ký - signature).

- **Anomaly-based IDS** — xây dựng mô hình hành vi *bình thường* và cảnh báo khi có độ lệch thống kê.

- **Stateful Protocol Analysis** — theo dõi trạng thái kết nối và so sánh với hành vi giao thức chuẩn (RFC).

- Phổ biến nhất là **Signature-based**, là nền tảng cho *Snort*, *Suricata* — hai công cụ IDS mã nguồn mở hàng đầu.

---

<!-- _class: split -->

# Signature-based IDS

<div class="col pros">

## ✅ Ưu điểm

- **Độ chính xác cao** với tấn công đã biết — false positive rất thấp.
- **Dễ giải thích** — rule dạng văn bản, SOC audit và chỉnh sửa trực tiếp.
- **Nhẹ về tài nguyên** — chỉ so khớp chuỗi, phù hợp inline tốc độ cao.
- Ví dụ: *Snort*, *Suricata* — hàng triệu rule do cộng đồng chia sẻ.

</div>

<div class="col cons">

## ❌ Hạn chế

- **Mù với zero-day** — chỉ bắt được tấn công đã có trong database.
- **Biến thể nhỏ** của tấn công cũ → bỏ sót hoàn toàn.
- **Bảo trì tốn kém** — cần chuyên gia cập nhật hàng ngàn rule liên tục.
- **Bất lực với TLS** — payload mã hóa, signature gần như vô dụng.

</div>

---

<!-- _class: split -->

# Anomaly-based IDS

<div class="col pros">

## ✅ Ưu điểm

- **Phát hiện zero-day** — không cần signature cho tấn công chưa từng thấy.
- **Phát hiện insider threat** — tấn công nội bộ luôn tạo bất thường thống kê.
- **Tự thích nghi** — baseline cập nhật theo thời gian khi mạng thay đổi.
- Ví dụ: máy tính gửi 5GB dữ liệu lúc 3h sáng → *data exfiltration*.

</div>

<div class="col cons">

## ❌ Hạn chế

- **False positive quá nhiều** — backup, cập nhật phần mềm cũng kích hoạt cảnh báo.
- **Alert fatigue** — SOC mệt mỏi, dễ bỏ qua cảnh báo thật.
- **Khó giải thích** — chỉ báo *bất thường*, không nói rõ loại tấn công.
- **Calibrate ngưỡng khó** — môi trường mạng đa dạng, baseline không ổn định.

</div>

---

# IDS bằng Machine Learning — Giải pháp

- 🧠 **Học từ dữ liệu, không viết rule thủ công** — model tự học đặc trưng từ hàng triệu flow có nhãn → không cần security expert viết signature.

- 🎯 **Tổng quát hóa tốt** — phân loại dựa trên thống kê flow (IAT, byte count, TCP flag) → bắt được biến thể mới của tấn công đã biết.

- 🔀 **Phân loại đa lớp đồng thời** — nhận diện DDoS, PortScan, Brute Force, Bot, Web Attack... trong một lần inference.

- ⚖️ **False positive kiểm soát được** — training với *class_weight* + *SMOTE* cân bằng recall/precision theo yêu cầu SOC.

- ⚡ **Tốc độ thực tế** — LightGBM **>30,000 flows/giây** trên CPU thông thường — đáp ứng inline detection.

---

<!-- _class: divider -->
<!-- _paginate: false -->
<!-- _header: '' -->

# Phần 2

## Cơ sở lý thuyết — Network Traffic & Dataset

---

# Network Traffic là gì?

- **Network traffic** (lưu lượng mạng) là toàn bộ dữ liệu di chuyển qua mạng máy tính trong một khoảng thời gian — mỗi khi mở web, gửi email, video call, dữ liệu đều được chia nhỏ và truyền đi.

- Để IDS phân tích được, traffic phải được biểu diễn dưới một định dạng có cấu trúc. Có **2 cấp độ** quan trọng:

  - 📦 **Packet** — đơn vị nhỏ nhất, thô và chi tiết
  - 🌊 **Flow** — đơn vị tổng hợp, phù hợp cho phân tích thống kê

- Định dạng lưu trữ phổ biến: **PCAP** (Packet CAPture) — giữ nguyên từng byte của traffic.

- IDS dựa trên ML thường làm việc ở mức **flow** vì gọn hơn và ít nhiễu hơn so với packet thô.

---

<!-- _class: cols2 -->

# Packet — đơn vị nhỏ nhất

<div class="col">

- Một **packet** là một gói tin có cấu trúc gồm nhiều **header** xếp chồng (encapsulation) và **payload** (dữ liệu thực).

- Mỗi tầng (layer) của mô hình OSI/TCP-IP thêm header riêng: Ethernet → IP → TCP/UDP → Application.

- Phân tích ở mức packet cho biết **chính xác từng byte** — phù hợp cho deep packet inspection (DPI).

- **Hạn chế:** số lượng quá lớn, kích thước biến đổi, khó tổng quát thành đặc trưng thống kê cho ML.

</div>

<div class="col" style="text-align: center;">

![OSI model](assets/osi-model.jpeg)

<p style="font-size: 0.65em; margin-top: 6px; color: #b0bec5;">
Mô hình OSI 7 tầng — mỗi tầng đóng gói thêm header riêng cho packet.
<br><em>Nguồn: ByteByteGo</em>
</p>

</div>

---

# Flow — đơn vị phân tích cho ML

- Một **flow** là một chuỗi packet **2 chiều** giữa hai endpoint trong một khoảng thời gian, được nhóm theo **5-tuple**:

<div class="tuple-box">
<span class="label">5-tuple = </span>(Source IP, Destination IP, Source Port, Destination Port, Protocol)
</div>

- Một kết nối TCP từ máy A:54321 → server B:443 với toàn bộ packet trao đổi (request + response) → được gom thành **một flow**.

- Flow được tổng hợp thành các **đặc trưng thống kê**: thời lượng, tổng bytes, số packet, IAT, phân bố flag TCP...

- 🎯 **Tại sao dùng flow thay vì packet?**
  - Gọn hơn: 1 flow ≈ 100 packet → 1 dòng số liệu
  - Ổn định: ít nhiễu hơn, đặc trưng rõ ràng hơn
  - Mã hóa-friendly: TLS không cản trở thống kê metadata
  - Tiêu chuẩn ngành: NetFlow, IPFIX, CICFlowMeter đều dùng flow

---

<!-- _class: cols2 -->

# PCAP — định dạng lưu trữ traffic

<div class="col">

## 📁 PCAP là gì?

- **Packet CAPture** — định dạng nhị phân lưu trữ packet **byte-for-byte** kèm timestamp.

- Tạo ra bởi *libpcap* / *WinPcap* — thư viện chuẩn để bắt traffic trên hầu hết hệ điều hành.

- File `.pcap` có thể chứa từ vài MB đến hàng chục GB traffic.

- Là định dạng đầu vào của hầu hết công cụ phân tích mạng.

</div>

<div class="col">

## 🔧 Công cụ liên quan

- **tcpdump / Wireshark** — bắt và xem packet trực tiếp.

- **CICFlowMeter** — đọc PCAP, gom packet thành flow, **xuất 78 đặc trưng** thống kê mỗi flow → CSV.

- **Zeek (Bro)** — phân tích PCAP, sinh log có cấu trúc cho SOC.

- 🔄 **Pipeline điển hình:**

  `PCAP → CICFlowMeter → CSV (flow features) → ML model`

</div>

---

# Tóm tắt: Packet vs Flow

|  | 📦 **Packet** | 🌊 **Flow** |
|---|---|---|
| **Đơn vị** | 1 gói tin riêng lẻ | Chuỗi packet 2 chiều theo 5-tuple |
| **Kích thước** | Vài chục byte → ~1500 byte | Tổng hợp từ hàng chục → hàng nghìn packet |
| **Đặc trưng** | Header fields, payload bytes | Statistics: duration, IAT, byte count, flag count |
| **Số lượng** | Hàng tỷ trên 1Gbps link | Ít hơn ~100 lần |
| **Phù hợp với** | DPI, signature matching | ML, anomaly detection, **dataset CIC-IDS2017** |
| **Bị ảnh hưởng bởi TLS?** | ✅ Có (payload mã hóa) | ❌ Không (chỉ dùng metadata) |

→ Project này phân loại tấn công **ở mức flow**, dùng dataset **CIC-IDS2017** chứa 78 đặc trưng/flow.
