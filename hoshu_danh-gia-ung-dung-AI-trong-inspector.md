# ĐÁNH GIÁ HIỆN TRẠNG ỨNG DỤNG AI TRONG HOẠT ĐỘNG KIỂM THỬ

| | |
|---|---|
| **Dự án** | Cụm HOSHU (ENNEW, BI, DB Renew, Invoice, Synchronize) |
| **Ngày đánh giá** | 30/09/2026 |
| **Người đánh giá** | PhuongPT |

---

## 1. Cách làm việc hiện tại với AI

### 1.1. Công cụ sử dụng

- Toàn cụm **hiện chưa áp dụng AI (Inspector)** để gen testcase.
- Định hướng của PM với từng dự án con **chưa giống nhau**:
  - **ENNEW:** PM để tester tự cân đối: **bận, chưa kịp tìm hiểu thì chưa áp dụng; có thời gian thì có thể thử**. Tester (HaNTT3) đang dành **100% công số cho 2 dự án khác** → chưa có thời gian tìm hiểu Inspector.
  - **BI, DB Renew, Invoice, Synchronize:** PM **có mong muốn** áp dụng AI để gen testcase.
- **Invoice** đã bắt đầu **đẩy testcase lên Inspector và fill kết quả test** với 2 task gần đây.

### 1.2. Quy trình kiểm thử hiện tại

| | ENNEW | BI, DB Renew, Invoice, Synchronize |
|---|---|---|
| **Testcase** | Hầu như không có, verify trực tiếp trên task | 100% task có TC/checklist, viết tay Excel |
| **Evidence cho KH** | Khi KH yêu cầu: làm TC Excel + evidence | Tùy task: note ID data test trên STG, chụp ảnh; PM gửi KH |
| **Dev dùng TC** | – | Không |
| **Auto test** | *(chưa có thông tin)* | Không làm |

### 1.3. Tình trạng các dự án con

| Dự án con | Tình trạng |
|---|---|
| **ENNEW** | Có task (các task nhỏ) → chưa áp dụng AI do tester chưa có thời gian tìm hiểu, hầu như không có testcase. |
| **BI** | Chưa có task. |
| **DB Renew** | Gần đây không có task → chưa làm gì trên Inspector. |
| **Invoice** | Tuần trước mới có 2 task → đã **đẩy testcase lên Inspector và fill kết quả test**. |
| **Synchronize** | Chưa có task. |

> **Nhận xét:** Hiện chỉ **ENNEW** và **Invoice** có task phát sinh, nhưng cách làm hai bên khác nhau. Các dự án con còn lại chưa có task → đây là thời điểm phù hợp để chuẩn bị cách làm với AI trước khi task mới phát sinh.

---

## 2. Spec đầu vào để test

Cách làm **giống nhau trong toàn cụm**:

- Không có file spec riêng; spec chủ yếu là **mô tả trong task Jira, viết ngắn gọn**.
- **Q&A:** nếu có thắc mắc, team hỏi đáp **trực tiếp trong comment task Jira**, không có file Q&A riêng.
- **Phạm vi ảnh hưởng:** do **dev note trong task Jira**.

Workflow hiện tại:

1. Task được tạo trên **Jira**, mô tả ngắn gọn.
2. Dev note **phạm vi ảnh hưởng** vào task Jira.
3. Tester đọc task; nếu có thắc mắc thì **hỏi trong comment task Jira**, dev/PM trả lời ngay trong comment.
4. Tester chuẩn bị test dựa trên toàn bộ thông tin trong task Jira:
   - **BI, DB Renew, Invoice, Synchronize:** viết tay testcase/checklist trên **Excel** (Invoice đã đẩy testcase lên Inspector với 2 task gần đây).
   - **ENNEW:** không viết testcase, **verify trực tiếp** theo case được mô tả trong task; chỉ làm testcase Excel khi KH yêu cầu test result.
5. Tester thực hiện test và ghi nhận kết quả (Excel / Inspector).
6. Với BI, DB Renew, Invoice, Synchronize: tùy task, tester note **ID data test trên STG** / chụp ảnh màn hình làm evidence, **PM gửi evidence cho KH**.

> **Nhận xét:** Thông tin đầu vào ngắn và nằm rải rác trong task Jira. Tester vẫn làm được nhờ hiểu nghiệp vụ, nhưng khi chuyển sang gen bằng AI thì mô tả ngắn gọn trong task sẽ **chưa đủ để AI gen testcase đầy đủ**; khi cần tổng hợp lại (làm testcase cho KH, regression, bàn giao) cũng phải lục lại từng task.

---

## 3. Các vấn đề hiện tại

### 3.1. ENNEW chưa có nguồn lực để áp dụng Inspector

- PM **không phản đối** dùng AI, nhưng việc áp dụng phụ thuộc vào thời gian rảnh của tester.
- Tester dành **100% công số cho 2 dự án khác** → không có thời gian tìm hiểu Inspector.
- Không có kế hoạch, mốc thời gian cụ thể → việc áp dụng AI ở ENNEW **dễ bị trì hoãn kéo dài**.

### 3.2. Spec đầu vào chưa đủ chi tiết để gen testcase bằng AI

- Mô tả task ngắn gọn, phần thông tin chi tiết nằm trong Q&A và dev note → nếu chỉ đưa mô tả task vào AI, testcase gen ra sẽ **thiếu case, chung chung**.
- Đây là **rào cản chính** khi hiện thực hóa mong muốn gen testcase của PM.

### 3.3. Testcase chưa đồng đều và đang làm thủ công

- **ENNEW:** hầu như không có testcase, verify trực tiếp theo mô tả task:
  - **Không có bằng chứng về độ bao phủ** test.
  - Chất lượng test **phụ thuộc hoàn toàn vào cá nhân tester**.
  - Không có tài sản testcase để **tái sử dụng cho regression**.
  - Testcase chỉ làm **bổ sung khi KH cần nộp** → dễ mang tính hình thức.
- **Các dự án con còn lại:** có testcase cho 100% task nhưng **viết tay trên Excel**:
  - **Tốn effort**, nhất là khi số task tăng.
- Cả hai trường hợp đều dùng **file Excel phân tán**, không quản lý tập trung, khó theo dõi lịch sử và tái sử dụng.

### 3.4. Dev không sử dụng testcase

- Testcase chỉ phục vụ tester, dev không tham khảo → dev không nắm được tester sẽ test những gì, **không tự kiểm tra trước** theo các case đó.
- Chỗ hiểu khác nhau giữa dev và tester chỉ lộ ra khi tester test, **bug phát hiện muộn** hơn.

### 3.5. PM không có dữ liệu về chất lượng test

- Testcase và kết quả test không được quản lý tập trung → PM **không theo dõi trực tiếp** được tình trạng testcase, kết quả test, và **không có cơ sở đánh giá** chất lượng kiểm thử ngoài phản hồi từ tester và KH.

---

## 4. Định hướng khắc phục và đề xuất cải thiện

Các dự án con đang ở **mức sẵn sàng khác nhau**, nên đề xuất áp dụng theo từng nhóm:

- **BI, DB Renew, Invoice, Synchronize:** đã có thói quen viết testcase cho 100% task và PM ủng hộ AI → **chuyển thẳng cách tạo testcase hiện tại sang AI**, không thay đổi quy trình làm việc với Jira.
- **ENNEW:** chưa có testcase thường xuyên, tester hạn chế công số → **áp dụng từng bước, effort thấp**, bắt đầu từ những điểm không làm thay đổi cách làm việc.

### 4.1. Bố trí thời gian cho ENNEW áp dụng Inspector *(xử lý 3.1)*

- Thống nhất với PM **thời gian cụ thể** để tester tìm hiểu Inspector, thay vì chờ khi có thời gian.
- Giảm effort tìm hiểu:
  - Tester Invoice / QA **hướng dẫn ngắn** cách dùng Inspector.
  - Dùng lại **rule/skill chung của cụm** (mục 4.7), không phải tự xây.
- Bắt đầu từ **giai đoạn 1** (mục 4.4) – effort thấp, không đổi cách làm hiện tại.

### 4.2. Gen testcase bằng Inspector từ thông tin trên Jira *(xử lý 3.2, 3.3 – BI, DB Renew, Invoice, Synchronize)*

- Input gen testcase là **toàn bộ thông tin của task trên Jira**: mô tả task + Q&A trong comment + phạm vi ảnh hưởng dev note (không chỉ riêng phần mô tả task).
- Bắt đầu với **Invoice** (dự án con đang có task và đã dùng Inspector); các dự án con còn lại áp dụng ngay khi có task mới.
- Tester **review lại testcase AI gen** trước khi dùng, bổ sung các case nghiệp vụ AI không biết.

### 4.3. Dùng AI đọc task và bổ sung thông tin còn thiếu *(xử lý 3.2 – toàn cụm)*

- Trước khi gen testcase hoặc verify, dùng AI đọc task Jira để **chỉ ra các điểm còn thiếu/chưa rõ** (luồng, điều kiện, validation, dữ liệu bị ảnh hưởng), **gợi ý các case cần verify** và **gợi ý câu hỏi Q&A** cần hỏi dev/PM.
- Câu trả lời vẫn ghi vào comment Jira như hiện nay → không phát sinh thêm tài liệu spec riêng.
- Với ENNEW, đây cũng là bước khởi đầu nhẹ nhất (giai đoạn 1 – mục 4.4).

### 4.4. Lộ trình từng bước cho ENNEW *(xử lý 3.1, 3.3)*

**Giai đoạn 1 – Áp dụng AI, không thay đổi cách làm hiện tại**

Các task thường ngày vẫn verify trực tiếp như hiện tại; chỉ đưa AI vào **đúng những điểm đang tốn effort hoặc dễ sót case**:

- **AI hỗ trợ đọc task trước khi verify** (theo mục 4.3) → verify đầy đủ hơn, giảm sót case.
- **Dùng Inspector khi KH cần test result:** gen testcase từ task Jira, thực hiện test, gắn evidence và **xuất test result từ Inspector** thay vì làm file Excel riêng.
  > **Note:** Inspector có hỗ trợ **export test result**.
- **Ghi nhận kết quả:** effort làm test result bằng Inspector so với Excel trước đây, và các case AI gợi ý mà tester có thể đã bỏ sót → số liệu để PM quyết định có chuyển sang giai đoạn 2 hay không.

**Giai đoạn 2 – Mở rộng khi giai đoạn 1 có kết quả và PM đồng ý**

- **Dùng thử Inspector cho các task thường ngày:** chọn một nhóm task trong 2–4 tuần để **gen testcase nhẹ (checklist)**, input là thông tin đã có trên Jira; đo effort và số bug phát hiện được so với verify trực tiếp.
- **Quy định mức testcase tối thiểu cho mỗi task** *(nếu dùng thử hiệu quả)*: mỗi task có **checklist các case đã verify** (case chính, validation, phạm vi ảnh hưởng), tích lũy dần thành **bộ regression**.

### 4.5. Quản lý testcase và kết quả test tập trung trên Inspector *(xử lý 3.3, 3.5)*

- Quản lý testcase, kết quả test và evidence **tập trung trên Inspector** thay cho file Excel. Invoice đã bắt đầu làm với 2 task gần đây → duy trì cho các task tiếp theo và áp dụng tương tự cho các dự án con khác (ENNEW theo lộ trình mục 4.4).
- **Khai thác chức năng Report trên Inspector** để PM theo dõi trực tiếp tiến độ và kết quả test; khi cần gửi KH thì **export test result** từ Inspector.
- Gắn evidence (**ID data test trên STG**, ảnh chụp màn hình) **trực tiếp vào từng testcase trên Inspector** → PM lấy evidence gửi KH ngay từ Inspector, không phải tổng hợp riêng.
- Với testcase Excel đã có, cân nhắc chuyển dần các chức năng hay thay đổi lên Inspector để làm **bộ regression**.

### 4.6. Chia sẻ testcase cho dev *(xử lý 3.4)*

- Đính kèm **link testcase trên Inspector vào task Jira**, để dev xem ngay trong task thay vì phải lấy file Excel riêng.
- Khuyến khích dev **tự kiểm tra theo các case chính** trước khi chuyển task cho tester.

### 4.7. Dùng chung rule/skill gen testcase cho cả cụm HOSHU *(đề xuất thêm)*

- Các dự án con có cách làm spec/Jira giống nhau → xây **một bộ rule/skill chung cho cụm** (nghiệp vụ chung, validation chung), cộng thêm phần riêng cho từng dự án con nếu cần.
- Lưu tập trung, có người phụ trách cập nhật, để chất lượng testcase AI gen đồng đều giữa các dự án con; ENNEW dùng lại bộ rule này khi bắt đầu áp dụng.

---

## 5. Kết luận

Cụm HOSHU chưa áp dụng AI để gen testcase. Spec đầu vào của toàn cụm chỉ là mô tả ngắn trên Jira, testcase làm thủ công bằng Excel, dev chưa sử dụng testcase và PM chưa có dữ liệu để đánh giá chất lượng test. Mức sẵn sàng giữa các dự án con khác nhau: **BI, DB Renew, Invoice, Synchronize** đã có testcase cho 100% task và PM mong muốn dùng AI, Invoice đã bắt đầu dùng Inspector; còn **ENNEW** hầu như không có testcase và chưa áp dụng AI do tester chưa có thời gian tìm hiểu.

Trọng tâm cải thiện là **bố trí thời gian cụ thể để ENNEW bắt đầu áp dụng**; với nhóm đã sẵn sàng thì **gen testcase bằng Inspector từ đầy đủ thông tin trên Jira, bắt đầu từ Invoice**; với ENNEW thì **áp dụng từng bước, không thay đổi cách làm hiện tại**; đồng thời **quản lý testcase tập trung trên Inspector, chia sẻ cho dev và dùng chung rule/skill cho cả cụm**.
