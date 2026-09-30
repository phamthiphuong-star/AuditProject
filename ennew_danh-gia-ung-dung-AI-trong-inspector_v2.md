# ĐÁNH GIÁ HIỆN TRẠNG ỨNG DỤNG AI TRONG HOẠT ĐỘNG KIỂM THỬ

| | |
|---|---|
| **Dự án** | ENNEW |
| **Ngày đánh giá** | 30/09/2026 |
| **Người đánh giá** | PhuongPT |

---

## 1. Cách làm việc hiện tại với AI

### 1.1. Công cụ sử dụng

Dự án **hiện không áp dụng AI (Inspector)** trong hoạt động kiểm thử.

- Lý do: **PM đề nghị tạm thời chưa sử dụng**.
- Tester **không hỏi lại PM** lý do không dùng → hiện chưa ai nắm được nguyên nhân cụ thể.

### 1.2. Quy trình kiểm thử hiện tại

| Giai đoạn | Cách thực hiện hiện tại |
|---|---|
| **Testcase** | • Hầu như **không có testcase**.<br>• Các task nhỏ, tester **verify trực tiếp trên task** theo case được mô tả trong task. |
| **Test result cho KH** | • Chỉ làm testcase **khi KH yêu cầu test result**.<br>• Testcase làm bằng **file Excel**, có gắn evidence.<br>• **Không gen từ AI**. |
| **Auto test** | *(chưa có thông tin)* |

---

## 2. Spec đầu vào để test

- Không có file spec riêng; tester dựa vào **nội dung mô tả trong task Jira** để verify.
- **Q&A:** nếu có thắc mắc, team hỏi đáp **trực tiếp trong comment task Jira**, không có file Q&A riêng.
- **Phạm vi ảnh hưởng:** do **dev note trong task Jira**.

> **Nhận xét:** Toàn bộ thông tin đầu vào (mô tả, Q&A, phạm vi ảnh hưởng) nằm rải rác trong task Jira. Với task nhỏ thì cách này đủ dùng, nhưng khi cần tổng hợp lại (làm testcase cho KH, regression, bàn giao) sẽ phải lục lại từng task.

---

## 3. Các vấn đề hiện tại

### 3.1. Chưa áp dụng AI và chưa rõ lý do

- Việc chưa dùng AI xuất phát từ đề nghị của PM nhưng **không có trao đổi** giữa PM và tester → không xác định được rào cản thực sự (bảo mật dữ liệu KH, ràng buộc hợp đồng, đánh giá effort không đáng, hay chưa được hướng dẫn...).
- Không rõ lý do thì cũng **không có hướng để gỡ vướng**, dự án sẽ tiếp tục đứng ngoài lộ trình áp dụng AI chung.

### 3.2. Không có testcase cho các task thường ngày

- Verify trực tiếp theo mô tả task → **không có bằng chứng về độ bao phủ**, không biết những gì đã test và những gì chưa test.
- Chất lượng test **phụ thuộc hoàn toàn vào cá nhân tester**; khó bàn giao khi đổi người.
- Không có tài sản testcase để **tái sử dụng cho regression** khi các task nhỏ tích lũy dần.

### 3.3. Testcase chỉ làm khi KH yêu cầu, bằng Excel

- Testcase làm theo kiểu **bổ sung khi cần nộp**, không phải để dẫn dắt việc test → dễ mang tính hình thức.
- Làm thủ công trên Excel, gắn evidence bằng tay → **tốn effort**, file phân tán, **không quản lý tập trung**, không theo dõi được lịch sử.

### 3.4. PM không có dữ liệu về chất lượng test

- Không có testcase và kết quả test được quản lý → PM **không có cơ sở đánh giá** chất lượng kiểm thử của dự án, ngoài phản hồi từ tester và KH.

---

## 4. Định hướng khắc phục và đề xuất cải thiện

Dự án đã quen vận hành theo cách hiện tại với các task nhỏ, nên đề xuất áp dụng AI **theo lộ trình từng giai đoạn**: bắt đầu từ những điểm không làm thay đổi cách làm việc, chỉ mở rộng khi đã có kết quả và được PM đồng ý.

### 4.1. Làm rõ lý do PM chưa dùng AI *(xử lý 3.1)*

- Tổ chức trao đổi giữa **PM – tester – QA** để xác định cụ thể rào cản.
- Tùy nguyên nhân mà có hướng xử lý:
  - **Bảo mật / hợp đồng KH:** kiểm tra điều khoản, xin phép KH hoặc chỉ dùng AI với dữ liệu đã ẩn thông tin nhạy cảm.
  - **Cho rằng không đáng effort vì task nhỏ:** chứng minh bằng kết quả của giai đoạn 1 (mục 4.2).
  - **Chưa nắm cách dùng:** hướng dẫn / chia sẻ kinh nghiệm từ các dự án đã áp dụng.
- ⚠️ *Cần xác nhận với PM: lý do cụ thể không áp dụng AI.*

### 4.2. Giai đoạn 1 – Áp dụng AI, không thay đổi cách làm hiện tại *(xử lý 3.2, 3.3)*

Chỉ đưa AI vào **đúng những điểm đang tốn effort hoặc dễ sót case**; các task thường ngày vẫn verify trực tiếp như hiện tại.

**a) AI hỗ trợ đọc task trước khi verify**
- Tester đưa **mô tả task + Q&A + phạm vi ảnh hưởng dev note** trên Jira vào AI để nhận **gợi ý các case cần verify và điểm có thể bị ảnh hưởng**.
- Không tạo thêm tài liệu, không thay đổi quy trình; chỉ giúp tester verify đầy đủ hơn, giảm sót case.

**b) Dùng Inspector khi KH cần test result**
- Đây là điểm đang tốn effort nhất: tester phải làm testcase Excel và gắn evidence thủ công.
- Khi có yêu cầu từ KH, dùng Inspector **gen testcase từ task Jira**, thực hiện test, gắn evidence và **xuất test result từ Inspector** thay vì làm file Excel riêng.
  > **Note:** Inspector có hỗ trợ **export test result**.

**c) Ghi nhận kết quả**
- Ghi lại effort làm test result bằng Inspector so với cách làm Excel trước đây, và các case AI gợi ý mà tester có thể đã bỏ sót.
- Đây là số liệu để PM đánh giá và quyết định có chuyển sang giai đoạn 2 hay không.

### 4.3. Giai đoạn 2 – Mở rộng khi giai đoạn 1 có kết quả *(xử lý 3.2, 3.3, 3.4)*

Chỉ triển khai khi giai đoạn 1 cho thấy hiệu quả rõ ràng và **PM đồng ý**.

**a) Dùng thử Inspector cho các task thường ngày**
- Chọn một nhóm task trong 2–4 tuần để **gen testcase nhẹ (checklist)** bằng Inspector, input là thông tin đã có sẵn trên Jira (không cần viết thêm spec).
- Đo effort và số bug phát hiện được so với verify trực tiếp.

**b) Quy định mức testcase tối thiểu cho mỗi task** *(nếu dùng thử hiệu quả)*
- Mỗi task tối thiểu có **checklist các case đã verify** (case chính, validation, phạm vi ảnh hưởng), không cần viết chi tiết như testcase đầy đủ.
- Tích lũy dần thành **bộ regression** cho các chức năng hay thay đổi.

**c) Quản lý tập trung trên Inspector**
- Quản lý testcase, kết quả và evidence **tập trung trên Inspector**.
- **Khai thác chức năng Report trên Inspector** để PM theo dõi trực tiếp tiến độ và kết quả test.

---

## 5. Kết luận

Dự án chưa áp dụng AI theo đề nghị của PM, nhưng lý do cụ thể chưa được trao đổi. Song song đó, dự án **hầu như không có testcase**, chỉ làm testcase thủ công bằng Excel khi KH yêu cầu, nên chất lượng test phụ thuộc vào cá nhân và PM không có dữ liệu để đánh giá. Đề xuất đi theo lộ trình hai giai đoạn: **trước hết làm rõ rào cản với PM và áp dụng AI ở những điểm tốn effort mà không thay đổi cách làm hiện tại (đọc task, làm test result cho KH)**; khi có kết quả và PM đồng ý thì **mở rộng sang testcase cho task thường ngày và quản lý tập trung trên Inspector**.
