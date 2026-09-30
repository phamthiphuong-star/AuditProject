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

### 4.1. Làm rõ lý do PM không dùng AI *(xử lý 3.1)*

- Tổ chức trao đổi giữa **PM – tester – QA** để xác định cụ thể rào cản.
- Tùy nguyên nhân mà có hướng xử lý:
  - **Bảo mật / hợp đồng KH:** kiểm tra điều khoản, xin phép KH hoặc chỉ dùng AI với dữ liệu đã ẩn thông tin nhạy cảm.
  - **Cho rằng không đáng effort vì task nhỏ:** chứng minh bằng việc dùng thử ở 4.2.
  - **Chưa nắm cách dùng:** hướng dẫn / chia sẻ kinh nghiệm từ các dự án đã áp dụng.
- ⚠️ *Cần xác nhận với PM: lý do cụ thể không áp dụng AI.*

### 4.2. Dùng thử Inspector với các task nhỏ *(xử lý 3.1, 3.2)*

- Chọn một nhóm task trong 2–4 tuần để **gen testcase nhẹ (checklist)** bằng Inspector, với input là **mô tả task + Q&A trong comment + phạm vi ảnh hưởng dev note** trên Jira (thông tin đã có sẵn, không cần viết thêm spec).
- Với task nhỏ, AI giúp tạo testcase gần như tức thì → có testcase **mà không tăng đáng kể effort** so với verify trực tiếp.
- Đo lại effort và số bug phát hiện được so với cách làm hiện tại để PM có số liệu ra quyết định.

### 4.3. Quy định mức testcase tối thiểu cho mỗi task *(xử lý 3.2)*

- Mỗi task tối thiểu có **checklist các case đã verify** (case chính, validation, phạm vi ảnh hưởng), không cần viết chi tiết như testcase đầy đủ.
- Tích lũy dần thành **bộ regression** cho các chức năng hay thay đổi.

### 4.4. Quản lý testcase và kết quả test trên Inspector thay Excel *(xử lý 3.3, 3.4)*

- Quản lý testcase, kết quả và evidence **tập trung trên Inspector**.
- Khi KH cần test result thì **xuất báo cáo từ Inspector** thay vì làm file Excel riêng.
  > **Note:** Inspector có hỗ trợ **export test result**.
- **Khai thác chức năng Report trên Inspector** để PM theo dõi trực tiếp tiến độ và kết quả test.

### 4.5. Áp dụng AI từng bước, không thay đổi cách làm hiện tại *(đề xuất thêm)*

Dự án đã quen vận hành theo cách hiện tại với các task nhỏ, nên thay vì thay đổi quy trình, chỉ đưa AI vào **đúng những điểm đang tốn effort hoặc dễ sót case**:

**Bước 1 – AI hỗ trợ đọc task trước khi verify**
- Tester đưa **mô tả task + Q&A + phạm vi ảnh hưởng dev note** trên Jira vào AI để nhận **gợi ý các case cần verify và điểm có thể bị ảnh hưởng**.
- Không tạo thêm tài liệu, không thay đổi quy trình; chỉ giúp tester verify đầy đủ hơn, giảm sót case.

**Bước 2 – Dùng Inspector khi KH cần test result**
- Đây là điểm đang tốn effort nhất: tester phải làm testcase Excel và gắn evidence thủ công.
- Khi có yêu cầu từ KH, dùng Inspector **gen testcase từ task Jira**, thực hiện test, gắn evidence và **export test result** gửi KH.
- Các task thường ngày vẫn giữ cách verify trực tiếp như hiện tại.

> **Lợi ích:** Hiệu quả thấy được ngay (giảm effort làm test result cho KH) mà không làm xáo trộn cách làm việc của dự án → dễ được PM chấp nhận, làm cơ sở để mở rộng dần sang 4.2–4.4.

---

## 5. Kết luận

Dự án chưa áp dụng AI theo đề nghị của PM, nhưng lý do cụ thể chưa được trao đổi. Song song đó, dự án **hầu như không có testcase**, chỉ làm testcase thủ công bằng Excel khi KH yêu cầu, nên chất lượng test phụ thuộc vào cá nhân và PM không có dữ liệu để đánh giá. Trọng tâm cải thiện là **làm rõ rào cản với PM, bắt đầu áp dụng AI ở những điểm tốn effort mà không thay đổi cách làm hiện tại (đọc task, làm test result cho KH), từ đó mở rộng dần sang quản lý testcase/kết quả test trên Inspector**.
