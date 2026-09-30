# ĐÁNH GIÁ HIỆN TRẠNG ỨNG DỤNG AI TRONG HOẠT ĐỘNG KIỂM THỬ

| | |
|---|---|
| **Dự án** | SCMBD |
| **Ngày đánh giá** | 30/09/2026 |
| **Người đánh giá** | PhuongPT |

---

## 1. Cách làm việc hiện tại với AI

### 1.1. Công cụ sử dụng

Dự án dùng **AI (Inspector)** để gen testcase.

### 1.2. Quy trình làm việc với Inspector

| Giai đoạn | Cách thực hiện hiện tại |
|---|---|
| **Gen testcase** | Dùng hoàn toàn **MCP/CLI** để gen testcase. |
| **Thực hiện test** | • Chỉ có **IT (Integration Test)**, không thực hiện ST (System Test).<br>• Tester test **manual**, điền kết quả lên Inspector để quản lý. |
| **Auto test** | ⚠️ *Cần confirm thêm với PM.* |

---

## 2. Spec đầu vào để gen testcase

Workflow hiện tại:

1. PM gen **Basic Design (BD)**.
2. Gen testcase từ BD.
3. Khi BD thay đổi, **PM báo lại team**:
   - **Thay đổi lớn:** AI đọc BD và **update testcase** → tester review.
   - **Thay đổi nhỏ:** tester **tự update testcase** trên Inspector.

> **Nhận xét:** Dự án có spec đầu vào rõ ràng (BD) và có cách xử lý khi BD thay đổi. Điểm cần chú ý là việc cập nhật testcase phụ thuộc vào **thông báo của PM** và **đánh giá lớn/nhỏ** của từng người.

---

## 3. Các vấn đề hiện tại

### 3.1. Cập nhật testcase phụ thuộc vào thông báo của PM

- Tester chỉ biết BD thay đổi khi PM báo lại.
- Nếu thông báo bị sót hoặc chưa nêu đủ phần thay đổi → testcase **không được cập nhật kịp**, lệch với BD.

### 3.2. Chưa có tiêu chí phân loại thay đổi lớn / nhỏ

- Cách xử lý khác nhau (AI update hay tester tự update) nhưng **chưa có tiêu chí rõ ràng** để phân loại.
- Mỗi người đánh giá một kiểu → cách cập nhật testcase **không đồng nhất**.

### 3.3. Thay đổi nhỏ update tay, khó đối chiếu với BD

- Testcase update tay trên Inspector không qua AI và không qua review → **khó kiểm soát** testcase còn khớp với BD hay không.
- Nhiều thay đổi nhỏ tích lũy dần → testcase và BD **có thể lệch nhau** mà không ai phát hiện.

### 3.4. Chỉ thực hiện IT, không có ST

- Test theo từng chức năng, không test các **luồng nghiệp vụ xuyên nhiều chức năng** → có rủi ro lỗi tích hợp không được phát hiện.

### 3.5. Auto test chưa rõ

- Chưa có thông tin về auto test của dự án. ⚠️ *Cần confirm thêm với PM.*

---

## 4. Định hướng khắc phục và đề xuất cải thiện

### 4.1. Quản lý thay đổi BD rõ ràng *(xử lý 3.1)*

- BD có **version và change log**: mỗi lần thay đổi ghi rõ phần nào thay đổi.
- Tester đối chiếu change log để biết **testcase nào bị ảnh hưởng**, không chỉ dựa vào thông báo.
- Có thể dùng AI **so sánh 2 version BD** để liệt kê điểm thay đổi.

### 4.2. Định nghĩa tiêu chí thay đổi lớn / nhỏ *(xử lý 3.2)*

- Thống nhất tiêu chí trong team, ví dụ:
  - **Nhỏ:** đổi text, label, message, giá trị mặc định.
  - **Lớn:** đổi luồng nghiệp vụ, logic, validation, thêm/bớt màn hình hoặc chức năng.
- Trường hợp không chắc → xử lý theo hướng **thay đổi lớn**.

### 4.3. Định kỳ đối chiếu BD – testcase *(xử lý 3.3)*

- Định kỳ (ví dụ cuối mỗi sprint) dùng AI **đối chiếu BD mới nhất với testcase** trên Inspector để phát hiện case thiếu hoặc lệch.
- Tester review kết quả đối chiếu và cập nhật.

### 4.4. Cân nhắc bổ sung ST cho các luồng chính *(xử lý 3.4)*

- Đánh giá khả năng bổ sung **ST cho các luồng nghiệp vụ chính** xuyên nhiều chức năng.
- Có thể dùng AI gen testcase ST từ BD của các chức năng liên quan.

### 4.5. Làm rõ hiện trạng auto test *(xử lý 3.5)*

- Confirm với PM: dự án có làm auto test không, ai thực hiện, dựa trên testcase nào.

---

## 5. Kết luận

Dự án đã dùng AI (MCP/CLI) để gen testcase từ **Basic Design do PM gen**, có quy trình xử lý khi BD thay đổi. Điểm cần cải thiện là **quản lý thay đổi BD rõ ràng**, **thống nhất tiêu chí thay đổi lớn/nhỏ** và **định kỳ đối chiếu BD – testcase** để testcase luôn khớp với BD; đồng thời cân nhắc bổ sung **ST cho các luồng chính** và làm rõ hiện trạng auto test.
