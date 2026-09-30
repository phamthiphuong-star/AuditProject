# ĐÁNH GIÁ HIỆN TRẠNG ỨNG DỤNG AI TRONG HOẠT ĐỘNG KIỂM THỬ

| | |
|---|---|
| **Dự án** | Cụm HOSHU (ENNEW, BI, DB Renew, Invoice, Synchronize) |
| **Ngày đánh giá** | 30/09/2026 |
| **Người đánh giá** | PhuongPT |

---

## 1. Cách làm việc hiện tại với AI

### 1.1. Công cụ sử dụng

- Toàn cụm **hiện chưa áp dụng AI (Inspector)** để gen testcase, testcase vẫn làm **thủ công**.
- PM **có mong muốn** áp dụng AI để gen testcase, nhưng tester **chưa có thời gian tìm hiểu** Inspector.

### 1.2. Quy trình kiểm thử hiện tại

**Tình hình task của các dự án con:**

| Dự án con | Tình hình task | IT | ST | Auto test |
|---|---|---|---|---|
| **ENNEW** | Có task, chủ yếu task nhỏ, task gấp của KH | TC (Create Manual)<br>Run test: Chưa đẩy lên Inspector | Không | Chưa áp dụng |
| **Invoice** | Gần đây có 2 task | TC (Create Manual)<br>Run test: Đã đẩy lên Inspector | Không | Chưa áp dụng |
| **BI** | CLOSE | – | – | – |
| **DB Renew** | Gần đây không có task | – | – | – |
| **Synchronize** | Gần đây không có task | – | – | – |

> **ENNEW:** chưa điền kết quả lên Inspector để quản lý.  
> *Lý do: từ tháng 9, HaNTT3 không có đủ thời gian để test ENNEW (100% công số đang join dự án khác).*

---

## 2. Spec đầu vào để test

- Không có file spec riêng; spec chủ yếu là **mô tả trong task Jira, viết ngắn gọn**.
- **Q&A:** nếu có thắc mắc, team hỏi đáp **trực tiếp trong comment task Jira**, không có file Q&A riêng.
- **Phạm vi ảnh hưởng:** do **dev note trong task Jira**.

Workflow hiện tại:

1. Task được tạo trên **Jira**, mô tả ngắn gọn.
2. Dev note **phạm vi ảnh hưởng** vào task Jira.
3. Tester đọc task; nếu có thắc mắc thì **hỏi trong comment task Jira**, dev/PM trả lời ngay trong comment.
4. Tester **tạo TC/checklist** dựa trên toàn bộ thông tin trong task Jira.
5. Tester thực hiện test **manual**; kết quả test được điền lên Inspector ở **Invoice**, **ENNEW chưa điền**.

> **Nhận xét:** Thông tin đầu vào ngắn và nằm rải rác trong task Jira. Tester vẫn làm được nhờ hiểu nghiệp vụ, nhưng khi chuyển sang gen bằng AI thì mô tả ngắn gọn trong task sẽ **chưa đủ để AI gen testcase đầy đủ**; khi cần tổng hợp lại (regression, bàn giao) cũng phải lục lại từng task.

---

## 3. Các vấn đề hiện tại

### 3.1. Chưa có nguồn lực và kế hoạch để áp dụng Inspector

- PM **có mong muốn** áp dụng AI, nhưng tester không có thời gian tìm hiểu Inspector.
- Riêng **ENNEW**: từ tháng 9, HaNTT3 không có đủ thời gian để test ENNEW (100% công số đang join dự án khác) → chưa apply Inspector.
- Không có kế hoạch, mốc thời gian cụ thể → việc áp dụng AI **dễ bị trì hoãn kéo dài**.

### 3.2. Spec đầu vào chưa đủ chi tiết để gen testcase bằng AI

- Mô tả task ngắn gọn, phần thông tin chi tiết nằm trong Q&A và dev note → nếu chỉ đưa mô tả task vào AI, testcase gen ra sẽ **thiếu case, chung chung**.
- Đây là **rào cản chính** khiến tester đánh giá **AI gen không hiệu quả**.

### 3.3. Testcase làm thủ công

- Testcase/checklist viết tay → **tốn effort**, nhất là khi số task tăng hoặc task gấp của KH.
- Testcase nằm trong **các file phân tán**, không quản lý tập trung, khó theo dõi lịch sử và tái sử dụng cho regression.

### 3.4. Kết quả test chưa được quản lý đồng bộ, PM không có dữ liệu về chất lượng test

- Invoice đã điền kết quả test lên Inspector, nhưng **ENNEW chưa điền** → testcase, kết quả test và evidence chưa được quản lý tập trung cho cả cụm.
- PM muốn biết tình hình test thì phải **mở từng file testcase** để xem, **không có báo cáo tổng hợp** (tiến độ, số case pass/fail).

### 3.5. Dev chưa sử dụng testcase của tester

- Testcase chỉ phục vụ tester, dev không tham khảo → dev không nắm được tester sẽ test những gì, **không tự kiểm tra trước** theo các case đó. Chỗ hiểu khác nhau giữa dev và tester chỉ lộ ra khi tester test, **bug phát hiện muộn** hơn.

### 3.6. Auto test chưa áp dụng được

- Đã có dự định cài đặt Inspector cho auto test, nhưng dự án toàn **task siêu gấp, release trong ngày** → không có công số để cài đặt và chạy thử.
- Cụm HOSHU gồm **nhiều hệ thống khác nhau** nhưng khi trỏ Inspector lên, AI **không phân biệt đúng hệ thống cần test**, gen testcase lẫn spec giữa các hệ thống (VD: test Invoice nhưng lại lấy spec của ENNEW) → kết quả không dùng được.

---

## 4. Định hướng khắc phục và đề xuất cải thiện

Sử dụng Inspector là **bắt buộc**, không thay đổi cách làm việc với Jira.

### 4.1. ENNEW fill kết quả test trên Inspector từ tháng 10 *(xử lý 3.1)*

- Từ tháng 10, **LeNT thay HaNTT3** test ENNEW. LeNT đã biết dùng Inspector.

### 4.2. Dùng MCP để AI đọc đầy đủ task Jira *(xử lý 3.2)*

- Đưa task Jira qua **MCP**, yêu cầu AI **đọc hết nội dung task và tất cả comment**.
- AI chỉ ra điểm còn thiếu/chưa rõ, gợi ý case cần test và câu hỏi Q&A. Câu trả lời vẫn ghi trong comment Jira.

### 4.3. Quản lý testcase và kết quả test trên Inspector *(xử lý 3.3, 3.4)*

- Tất cả dự án con **fill kết quả test và gắn evidence** (ID data test trên STG, ảnh chụp màn hình) trên Inspector.
- PM xem tiến độ, kết quả qua **Report**.
- Có thể **export test result** từ Inspector để gửi KH.
- Chuyển dần testcase đã có lên Inspector làm **bộ regression**.

### 4.4. Chia sẻ testcase cho dev *(xử lý 3.5)*

- Gắn **link testcase trên Inspector vào task Jira**; dev tự kiểm tra các case chính trước khi chuyển cho tester.

### 4.5. Tách riêng từng hệ thống trên Inspector *(xử lý 3.6)*

- Mỗi hệ thống **một project/spec riêng**; khi gen testcase hoặc auto test phải **chỉ định rõ hệ thống**. Thử trước với Invoice.
- Auto test: không làm cho task gấp release trong ngày; bắt đầu với **chức năng ổn định, hay phải regression**.

### 4.6. Dùng chung rule/skill cho cả cụm *(đề xuất thêm)*

- Một bộ **rule/skill chung** cho cụm, kèm **file riêng cho từng hệ thống**; có người phụ trách cập nhật.

---

## 5. Kết luận

**Hiện trạng:**

- Chưa dùng AI gen testcase; testcase làm thủ công, chỉ test IT manual.
- Invoice đã fill kết quả trên Inspector, ENNEW chưa → PM không có báo cáo tổng hợp.
- Auto test chưa làm được: không có công số, AI lẫn spec giữa các hệ thống.

**Trọng tâm cải thiện:**

1. ENNEW fill kết quả trên Inspector từ tháng 10 (LeNT).
2. Dùng MCP để AI đọc đầy đủ task Jira khi gen testcase.
3. Quản lý testcase, kết quả, evidence tập trung trên Inspector.
4. Tách riêng từng hệ thống trên Inspector, trước khi làm auto test.
5. Chia sẻ testcase cho dev, dùng chung rule/skill cho cả cụm.
