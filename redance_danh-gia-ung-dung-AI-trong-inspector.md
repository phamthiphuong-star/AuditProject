# ĐÁNH GIÁ HIỆN TRẠNG ỨNG DỤNG AI TRONG HOẠT ĐỘNG KIỂM THỬ

| | |
|---|---|
| **Dự án** | REDANCE |
| **Ngày đánh giá** | 25/09/2026 |
| **Người đánh giá** | LucTV |

---

## 1. Cách làm việc hiện tại với AI

### 1.1. Công cụ sử dụng

Dự án dùng **hoàn toàn AI (Inspector)** để gen testcase, không còn viết testcase bằng tay như trước.

### 1.2. Quy trình làm việc với Inspector

| Giai đoạn | Cách thực hiện hiện tại |
|---|---|
| **Gen testcase** | Dùng hoàn toàn **MCP/CLI** để gen testcase. |
| **Thực hiện test** | • Hiện chỉ có **IT (Integration Test)**, không thực hiện ST (System Test).<br>• Tester chỉ test **manual** và điền kết quả lên Inspector để quản lý. |
| **Auto test** | Do **phía dev** thực hiện. |

---

## 2. Spec đầu vào để gen testcase

Workflow hiện tại:

1. Dev điều tra phạm vi ảnh hưởng / logic của task cần làm.
2. Dev gửi output cho tester.
3. Tester thao tác trên màn hình theo nội dung dev note.
4. Tester confirm spec nếu thấy nội dung dev note thiếu hoặc chưa đúng.
5. Dev check lại và phản hồi.
6. Toàn bộ thông tin được note vào **comment task Jira**.
7. Tester tự collect thông tin trong task Jira và **tạo một file spec** làm input đầu vào.
8. Gen testcase từ file spec đó.

> **Nhận xét:** Spec chỉ được hình thành ở bước cuối, do tester tự tổng hợp từ comment Jira, và không quay lại cho dev hay dự án review trước khi gen testcase.

---

## 3. Các vấn đề hiện tại

### 3.1. Dự án không có file spec cho từng task phát triển

- Xảy ra tình trạng **dev hiểu một kiểu, tester hiểu một kiểu**. Vấn đề chỉ được phát hiện **sau khi dev code xong**, tester mất effort update lại testcase → chất lượng testcase chưa thực sự tốt và ổn định.
- File spec do tester tự định nghĩa để gen testcase **không được team dự án review**, quản lý cũng không nắm được tình trạng/chất lượng → không kiểm soát được chất lượng input đầu vào để gen testcase.

### 3.2. PM không kiểm soát được chất lượng testcase của dự án

- PM báo cáo hàng tuần là dự án dùng AI vào quá trình test **"OK"**.
- Sau khi đánh giá, "OK" ở đây được PM hiểu theo hướng tester **đã dùng được AI** để gen testcase, thực hiện test và quản lý kết quả test.
- Còn **chất lượng testcase thì PM không nắm được**, phụ thuộc hoàn toàn vào feedback của tester.

### 3.3. Auto test

- Tester gửi testcase cho dev, dev gen auto test **hoàn toàn dựa trên testcase của tester**.
- Testcase lại dựa hoàn toàn trên spec tester tự tổng hợp, không qua review → **nguy cơ thiếu/sai input đầu vào lan sang cả auto test**.
- Phía tester đã chạy thử auto test trên môi trường dev với các task đơn giản (CRUD).

### 3.4. Phạm vi ảnh hưởng trong các task

Phạm vi ảnh hưởng note trong task dùng **ngôn từ khó hiểu, thuần technical**, gây khó khăn cho tester khi tìm hiểu task và **tốn effort confirm qua lại**.

### 3.5. Rule/Skill gen testcase

- Tester tự tạo một file rule/skill riêng của dự án; khi gen testcase sẽ input file spec tự mô tả.
- PM hiện **không kiểm soát được rule/skill** phía tester.
- Chất lượng file rule/skill chưa tốt:
  - Nội dung **trùng lặp** khá nhiều, có các nội dung **mâu thuẫn** lẫn nhau.
  - **Thiếu** một số case validation đặc biệt.
  - **Trộn lẫn** rule chung của dự án với nội dung riêng của một màn hình.

---

## 4. Định hướng khắc phục và đề xuất cải thiện

### 4.1. Xây dựng spec cho từng task và review trước khi code *(xử lý 3.1)*

- Chuyển output điều tra của dev thành **file spec chính thức của task** theo một **template chuẩn** (mục tiêu, luồng nghiệp vụ, business rule, validation, phạm vi ảnh hưởng, Q&A đã chốt), thay vì để thông tin rải rác trong comment Jira.
- Tổ chức **buổi thống nhất spec giữa dev và tester trước khi dev code** (có thể ngắn 15–30 phút cho mỗi task), để phát hiện sớm chỗ hiểu khác nhau thay vì phát hiện sau khi code xong.
- Có thể dùng AI **tổng hợp nháp spec từ dev note và comment Jira**, sau đó dev và tester cùng review, chốt bản final.
- Lưu spec tại **một nơi tập trung có version control** (Git repo / Writer...), có lịch sử thay đổi. Chỉ gen testcase từ spec đã được chốt.
- ⚠️ *Cần xác nhận với dự án: ai là người chịu trách nhiệm chính viết và chốt spec (dev, BA hay tester)?*

### 4.2. Kiểm soát chất lượng testcase và báo cáo cho PM *(xử lý 3.2)*

- Phía dự án cần định nghĩa **tiêu chí review testcase thống nhất** cho các task, đẩy các tiêu chí này thành **rule/skill để AI review trước**, sau đó con người (test lead/dev) review lại.
- Làm rõ định nghĩa **"OK" trong báo cáo tuần**: tách riêng hai ý *"đã áp dụng AI"* và *"chất lượng testcase"*; bổ sung trạng thái spec/testcase của từng task đã được review hay chưa.
- **Khai thác chức năng Report trên Inspector** để PM theo dõi trực tiếp tiến độ và kết quả test, không chỉ dựa vào feedback của tester.

### 4.3. Auto test *(xử lý 3.3)*

- Chỉ chuyển cho dev gen auto test từ **testcase đã được review**, dựa trên spec đã chốt.
- Tester **review lại độ bao phủ của script auto** so với testcase, đảm bảo auto test không bỏ sót case quan trọng.
- Đánh dấu trên Inspector các testcase **phù hợp / không phù hợp automation** để dev và tester cùng nắm.
- Từ kết quả chạy thử với task CRUD, mở rộng dần sang các cụm chức năng có logic ổn định, lặp lại nhiều.

### 4.4. Mô tả phạm vi ảnh hưởng dễ hiểu hơn *(xử lý 3.4)*

- Thống nhất **template ghi phạm vi ảnh hưởng** gồm hai phần: phần **nghiệp vụ** (màn hình, chức năng, luồng, dữ liệu bị ảnh hưởng) cho tester, và phần **technical** (API, bảng DB, module) cho dev.
- Dùng AI để **chuyển nội dung technical sang mô tả nghiệp vụ**, sau đó dev xác nhận lại.
- Cấp quyền **read-only vào code** và hướng dẫn tester cơ bản để có thể tự đối chiếu Code – Spec – Testcase khi cần, giảm confirm qua lại.

### 4.5. Chuẩn hóa Rule/Skill gen testcase *(xử lý 3.5)*

- **Tái cấu trúc file rule/skill**: tách **rule chung của dự án** và **rule riêng theo từng màn hình/module** thành các file riêng biệt.
- Rà soát để **loại bỏ nội dung trùng lặp, mâu thuẫn** (có thể dùng AI rà soát trước, người review sau).
- Bổ sung **checklist các case validation đặc biệt** của dự án vào rule chung.
- Lưu rule/skill trong **repository chung**, mọi thay đổi đi qua review; chỉ định **owner** duy trì, có versioning và changelog để PM/test lead kiểm soát được.
- Xây dựng **bộ task mẫu kèm testcase chuẩn (golden set)** để kiểm tra chất lượng mỗi khi rule/skill thay đổi.

### 4.6. Cân nhắc bổ sung ST cho các luồng chính *(đề xuất thêm)*

Hiện dự án chỉ thực hiện IT. Nên đánh giá khả năng bổ sung **ST cho các luồng nghiệp vụ chính** xuyên nhiều chức năng, để giảm rủi ro lỗi tích hợp mà test theo từng task không phát hiện được.

---

## 5. Kết luận

Dự án đã chuyển hoàn toàn sang dùng AI để gen testcase, tuy nhiên chất lượng đầu ra phụ thuộc vào **spec do tester tự tổng hợp** và **file rule/skill chưa được chuẩn hóa**, cả hai đều chưa qua review. Rủi ro này còn lan sang auto test do dev gen từ chính testcase đó, trong khi PM chưa có cơ sở để đánh giá chất lượng. Trọng tâm cải thiện là **có spec chính thức cho từng task và thống nhất trước khi code, chuẩn hóa rule/skill, và đưa AI review cùng con người review vào quy trình kiểm soát chất lượng testcase**.
