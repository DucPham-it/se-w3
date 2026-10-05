# BT04 · Mini-SRS — Hệ thống quản lý lịch khám Phòng khám An Tâm

**Nhóm:** 13

| MSSV | Họ Và Tên |
|---|---|
| 24120032 | Nguyễn Phan Khánh Đăng |
| 24120041 | Phạm Võ Đức|
| 24120043 | Nguyễn Công Dũng|
| 24120045 | Nguyễn Văn Hạ|

# 0. Quy ước tài liệu

## 0.1 Quy ước nguồn

| Mã | Nguồn | Ý nghĩa |
|---|---|---|
| `F-CS` | Fact from Case Study | Dữ kiện được cung cấp trực tiếp trong tình huống Phòng khám An Tâm |
| `STK-xx` | Stakeholder | Bên sử dụng dịch vụ |
| `Q-Oxx` | Câu hỏi mở | Câu hỏi dùng trong khảo sát/phỏng vấn |
| `Q-Cxx` | Câu hỏi đóng | Câu hỏi dùng trong khảo sát/phỏng vấn |
| `Q-Xxx` | Câu hỏi ngoại lệ | Câu hỏi làm rõ ngoại lệ và yêu cầu phi chức năng |
| `Q-xx` | Open Issue | Câu hỏi chưa có câu trả lời chính thức từ stakeholder |
| `A-xx` | Assumption | Giả định của nhóm, phải được ghi nhãn và xác nhận sau |
| `FR-xx` | Functional Requirement | Yêu cầu chức năng |
| `NFR-xx` | Non-functional Requirement | Yêu cầu phi chức năng |
| `SC-xx` | Scenario | Tình huống sử dụng |
| `TC-xx` | Test Scenario | Kịch bản kiểm nghiệm yêu cầu |
| `REV-xx` | Review Finding | Vấn đề phát hiện trong peer review |
| `CR-xx` | Change Request | Yêu cầu thay đổi chính thức |


# 1. Problem Statement & Scope

## 1.1 Bối cảnh và hiện trạng đã biết

Phòng khám An Tâm là phòng khám đa khoa quy mô nhỏ. Dữ kiện tình huống cho biết:

- Có **06 bác sĩ** thuộc nhiều chuyên khoa.
- Có khoảng **80–120 lượt bệnh nhân mỗi ngày**.
- Có **02 nhân viên tiếp nhận mỗi ca**.
- Việc đặt lịch hiện được thực hiện qua **điện thoại và ghi vào sổ**.
- Nhân viên tiếp nhận ghi lịch và **gọi điện xác nhận**.
- Bệnh nhân mới **khai thông tin khi đến phòng khám**.
- Bác sĩ nhận **danh sách lịch khám vào đầu mỗi ca**.
- Khi bác sĩ nghỉ đột xuất, nhân viên phải **gọi từng bệnh nhân** để thông báo.


## 1.2 Phát biểu vấn đề

Quy trình hiện tại phụ thuộc nhiều vào điện thoại, sổ giấy và trao đổi thủ công. Điều này làm cho việc cập nhật, tra cứu và phối hợp lịch khó đồng bộ khi lịch thay đổi.

Các vấn đề được xác định từ tình huống:

1. Việc đặt lịch phụ thuộc vào điện thoại và ghi chép thủ công.
2. Khi lịch thay đổi, thông tin trên sổ không tự động được đồng bộ cho các bên liên quan.
3. Khi bác sĩ nghỉ đột xuất, nhân viên phải liên hệ từng bệnh nhân.
4. Bệnh nhân mới chỉ khai thông tin khi đến phòng khám.
5. Bác sĩ phụ thuộc vào danh sách được cung cấp vào đầu ca để chuẩn bị.

## 1.3 Mục tiêu hệ thống

Xây dựng hệ thống hỗ trợ **quản lý lịch khám và tiếp nhận bệnh nhân tập trung**, nhằm:

- Giúp nhân viên tiếp nhận quản lý lịch khám tự động thay thủ công, dễ quan sát thay đổi lịch.
- Giúp bác sĩ xem lịch khám, danh sách bệnh nhân và các thông tin cần thiết được cấp quyền để thuận tiện chuẩn bị trước.
- Đồng bộ hoá thông tin, hạn chế xung đột và sai sót khi sắp lịch.
- Giúp bệnh nhân khai báo thông tin, tự đổi, hủy lịch từ xa, và hệ thống tự cập nhật chỗ trống.
- Giảm các thao tác gọi điện và ghi chép thủ công, tự động hóa thao tác thông báo cho bệnh nhân.


## 1.4 Giá trị mong đợi

| Đối tượng | Giá trị mong đợi |
|---|---|
| Bệnh nhân | Đặt/đổi/hủy lịch thuận tiện hơn; giảm nhu cầu đến trực tiếp chỉ để thay đổi lịch |
| Nhân viên tiếp nhận | Giảm ghi chép và tra cứu thủ công; dễ nhận biết lịch thay đổi |
| Bác sĩ | Có danh sách lịch khám cập nhật để chuẩn bị trước |
| Quản lý phòng khám | Có nguồn thông tin tập trung để theo dõi hoạt động đặt lịch và vận hành |
| Phòng khám | Giảm phụ thuộc vào sổ giấy và trao đổi thủ công |

## 1.5 Stakeholder

| ID | Stakeholder | Vai trò | Nhu cầu | Ảnh hưởng đến hệ thống |
|---|---|---|---|---|
| `STK-01` | Quản lý phòng khám | Quản lý vận hành | Bệnh nhân đặt lịch nhanh, không phải gọi nhiều lần | Quyết định chính sách, nghiệp vụ và ưu tiên |
| `STK-02` | Bác sĩ | Thực hiện khám | Biết bệnh nhân nào đến và thông tin/hồ sơ nào cần thiết | Trực tiếp sử dụng lịch và danh sách khám |
| `STK-03` | Nhân viên tiếp nhận | Quản lý lịch, tiếp nhận bệnh nhân | Cần nhìn thấy thay đổi lịch đồng bộ và xử lý lịch hằng ngày | Người thao tác thường xuyên với lịch |
| `STK-04` | Bệnh nhân | Người sử dụng dịch vụ | Muốn đổi lịch mà không phải đến tận nơi | Người tạo, xem và thay đổi lịch hẹn |

## 1.6 In-Scope

### A. Quản lý lịch hẹn

- Tạo lịch.
- Xem lịch.
- Đổi lịch.
- Hủy lịch.
- Theo dõi trạng thái lịch.

### B. Tra cứu khả năng đặt lịch

- Tra cứu chuyên khoa.
- Tra cứu bác sĩ.
- Tra cứu ngày/ca làm việc.
- Tra cứu khung giờ khả dụng.

### C. Quản lý lịch làm việc của bác sĩ

- Ghi nhận lịch làm việc.
- Ghi nhận nghỉ/vắng.
- Ngăn đặt lịch khi bác sĩ không khả dụng.

### D. Tiếp nhận bệnh nhân

- Tra cứu bệnh nhân.
- Ghi nhận bệnh nhân đến khám.
- Lưu thông tin cơ bản cần thiết cho việc đặt lịch và tiếp nhận.

### E. Bác sĩ theo dõi lịch khám

- Xem lịch theo ngày/ca.
- Xem danh sách bệnh nhân dự kiến.
- Xem các thông tin đã được cấp quyền để chuẩn bị trước.

### F. Xử lý thay đổi lịch

- Ghi nhận lịch thay đổi.
- Xác định các lịch bị ảnh hưởng.
- Thông báo/cập nhật cho các bên theo chính sách được xác nhận.

### G. Quản lý quyền truy cập cơ bản

- Phân quyền theo vai trò.
- Ghi nhận các thao tác thay đổi quan trọng.

## 1.7 Out-Scope (Ngoài phạm vi hệ thống)

### A. Thanh toán trực tuyến và xử lý hoàn tiền
- Thanh toán viện phí qua ngân hàng hoặc ví điện tử.
- Xử lý giao dịch và hoàn tiền khi hủy lịch (chuyển vào phạm vi qua CR-01).

### B. Bệnh án điện tử lâm sàng đầy đủ
- Chẩn đoán chi tiết và phác đồ điều trị.
- Tiền sử bệnh lý chuyên sâu và dị ứng thuốc.
- Lưu trữ lịch sử khám chữa bệnh lâm sàng (hệ thống chỉ lưu thông tin hành chính cơ bản phục vụ đặt lịch và tiếp nhận).

### C. Khám trực tuyến / Telemedicine
- Phiên khám hoặc video call trực tuyến.
- Cung cấp phòng khám online (chuyển vào phạm vi qua CR-01).

### D. Hệ thống phân bổ bác sĩ / tự chẩn đoán theo triệu chứng
- Tiếp nhận và phân tích triệu chứng từ xa để tự động chỉ định chuyên khoa hoặc bác sĩ trước khi đến phòng khám.


## 1.8 Thuật ngữ viết tắt

| Viết tắt | Giải thích |
|---|---|
| SRS | Software Requirements Specification — Đặc tả yêu cầu phần mềm |
| FR | Functional Requirement — Yêu cầu chức năng |
| NFR | Non-functional Requirement — Yêu cầu phi chức năng |
| STK | Stakeholder |
| SC | Scenario |
| TC | Test Scenario/Test Case |
| CR | Change Request |
| RBAC | Role-Based Access Control — Phân quyền theo vai trò |
| SMS | Short Message Service |
| UI | User Interface — Giao diện người dùng |


# 2. Elicitation Plan — Kế hoạch thu thập yêu cầu

## 2.1 Mục tiêu

- Làm rõ quy trình đặt lịch, xác nhận, đổi/hủy lịch hiện tại.
- Xác định quy tắc phân bổ khung giờ và giới hạn bệnh nhân.
- Xác định cách xử lý đến trễ, vắng mặt, khám gấp và bác sĩ nghỉ.
- Xác định quyền xem/sửa dữ liệu theo từng vai trò.
- Xác định yêu cầu về hiệu năng, bảo mật, lưu trữ và độ ổn định.

## 2.2 Kỹ thuật thu thập yêu cầu

### 2.2.1 Phỏng vấn

- **Mục tiêu:** hiểu quy trình đặt lịch hiện tại, các quy tắc còn thiếu (khung giờ, giới hạn bệnh nhân, đến trễ, vắng mặt, khám gấp, bác sĩ nghỉ), 
nhu cầu của từng vai trò và yêu cầu về tốc độ, bảo mật, lưu trữ.
- **Đối tượng:** quản lý phòng khám, bác sĩ, nhân viên tiếp nhận (mỗi vai trò ít nhất 1 người).
- **Vai trò trong nhóm:** 1 người hỏi, 1 người ghi chép, 1 người theo dõi và ghi câu hỏi phát sinh.
- **Thời lượng dự kiến:** 30–45 phút/người.
- **Cách ghi nhận:** biên bản mỗi buổi kèm mã câu hỏi, ghi âm nếu được đồng ý, gửi lại biên bản cho người được hỏi xác nhận.

### 2.2.2 Bảng câu hỏi

- **Mục tiêu:** biết bệnh nhân đang đặt, đổi, hủy lịch thế nào, khai thông tin ra sao, muốn nhận thông báo qua kênh nào.
- **Đối tượng:** bệnh nhân mới và cũ.
- **Mục tiêu mẫu:** tối thiểu 20 phản hồi.
- **Vai trò trong nhóm:** 1 người thiết kế phiếu, 1 người phát và thu, 1 người tổng hợp.
- **Thời lượng:** dưới 5 phút/phiếu; thu trong 2–3 ngày.
- **Cách ghi nhận:** Google Form ẩn danh hoặc phiếu giấy phát lúc bệnh nhân chờ khám; xuất bảng tổng hợp kết quả.

### 2.2.3 Quan sát

- **Mục tiêu:** xem cách nhân viên ghi lịch vào sổ, gọi xác nhận, tra cứu lịch, thông báo thay đổi và đưa danh sách 
cho bác sĩ; tìm chỗ vướng hoặc dễ nhầm.
- **Đối tượng:** công việc của nhân viên tiếp nhận trong một ca, ưu tiên giờ đông khách.
- **Vai trò trong nhóm:** 2 người quan sát, 1 người tổng hợp.
- **Thời lượng:** 2–3 giờ.
- **Cách ghi nhận:** bảng quan sát gồm giờ, việc nhân viên làm, công cụ dùng (sổ, điện thoại), thời gian, chỗ bị vướng;
ảnh chụp sổ phải che tên và số điện thoại bệnh nhân.

## 2.3 Bộ câu hỏi khảo sát

### 2.3.1 Câu hỏi mở

**Chủ đề: Đặt lịch và xác nhận hiện tại**

- **Q-O1 — Nhân viên tiếp nhận:** Anh/chị hãy kể từng bước từ lúc nhận cuộc gọi đặt lịch đến khi ghi sổ và gọi xác nhận. Bước nào mất nhiều thời gian hoặc dễ nhầm nhất?
- **Q-O2 — Quản lý:** Anh/chị muốn bệnh nhân đặt lịch nhanh, không phải gọi nhiều lần. Hiện bệnh nhân thường phải gọi mấy lần, vì sao, và theo anh/chị thế nào là "nhanh"?
- **Q-O3 — Nhân viên tiếp nhận:** Khi cần tìm một lịch đã ghi trong sổ, anh/chị làm thế nào, mất bao lâu và hay gặp khó khăn gì?

**Chủ đề: Tiếp nhận bệnh nhân**

- **Q-O4 — Bệnh nhân mới:** Khi đến khám lần đầu, anh/chị phải khai những thông tin gì và mất bao lâu? Phần nào anh/chị thấy bất tiện?

**Chủ đề: Bác sĩ theo dõi lịch**

- **Q-O5 — Bác sĩ:** Danh sách đầu ca hiện gồm những thông tin gì, và còn thiếu gì để anh/chị chuẩn bị? "Hồ sơ cần chuẩn bị" cụ thể là những gì, cần biết trước bao lâu?

**Chủ đề: Đổi/hủy lịch**

- **Q-O6 — Nhân viên tiếp nhận:** Hãy kể một lần gần đây phải đổi hoặc hủy lịch. Anh/chị đã làm những thao tác nào, và có ai bị bỏ sót thông tin không?
- **Q-O7 — Bệnh nhân:** Khi cần đổi hoặc hủy lịch, anh/chị đã làm thế nào và gặp khó khăn gì? Anh/chị mong muốn đổi lịch bằng cách nào?
- **Q-O8 — Quản lý:** Khi bác sĩ nghỉ đột xuất, phòng khám xử lý ra sao và điều gì làm việc gọi từng bệnh nhân khó khăn?

### 2.3.2 Câu hỏi đóng

- **Q-C1 — Bệnh nhân:** Để đặt được lịch khám, anh/chị thường phải gọi mấy lần? 1; 2; 3 lần trở lên
- **Q-C2 — Quản lý:** Lịch do bệnh nhân tự đặt có cần nhân viên duyệt trước khi có hiệu lực không? Cần duyệt; Có hiệu lực ngay
- **Q-C3 — Nhân viên tiếp nhận:** Bệnh nhân cũ có phải khai lại thông tin khi đến khám không? Có; Không
- **Q-C4 — Nhân viên tiếp nhận:** Việc bệnh nhân đến phòng khám hiện có được ghi nhận không? Có, ghi sổ; Có, cách khác: …; Không
- **Q-C5 — Quản lý:** Mỗi lượt khám có độ dài cố định không? Cố định (…) phút; Theo chuyên khoa; Theo bác sĩ
- **Q-C6 — Quản lý:** Có giới hạn số bệnh nhân tối đa mỗi bác sĩ mỗi ca không? Có (…) bệnh nhân; Không
- **Q-C7 — Bác sĩ:** Anh/chị muốn xem danh sách khám vào lúc nào? Đầu ca; Từ hôm trước; Cập nhật liên tục trong ca
- **Q-C8 — Quản lý:** Bệnh nhân được đổi/hủy lịch chậm nhất trước giờ khám bao lâu? Sát giờ; Trước 2 giờ; Trước 24 giờ; Khác: …
- **Q-C9 — Bệnh nhân:** Anh/chị muốn nhận thông báo qua kênh nào? SMS; Zalo; Email; Gọi điện

### 2.3.3 Câu hỏi ngoại lệ và yêu cầu phi chức năng

**Ngoại lệ nghiệp vụ**

- **Q-X1:** Bệnh nhân đến trễ bao nhiêu phút thì phải xếp lại/mất lượt? Ai quyết định?
- **Q-X2:** Bệnh nhân vắng mặt không báo thì xử lý thế nào?
- **Q-X3:** Ca khám gấp hoặc bệnh nhân không hẹn trước do ai quyết định và ảnh hưởng thế nào tới lịch đã đặt?
- **Q-X4:** Khi bác sĩ nghỉ đột xuất, bệnh nhân được thông báo bằng kênh nào và có được chuyển bác sĩ/đổi ngày không?
- **Q-X5:** Nếu hai người cùng chọn một khung giờ gần như đồng thời, hệ thống nên xử lý thế nào?

**Yêu cầu phi chức năng**

- **Q-X6:** Với từng vai trò, ai được xem/sửa thông tin nào? Có cần lưu ai sửa và sửa lúc nào không?
- **Q-X7:** Giờ cao điểm có bao nhiêu người thao tác đồng thời? Thời gian phản hồi bao lâu là chấp nhận được?
- **Q-X8:** Dữ liệu cần lưu bao lâu? Có quy định pháp lý nào? Có cần sao lưu định kỳ không?
- **Q-X9:** Nếu hệ thống ngừng hoạt động trong giờ làm việc, gián đoạn tối đa chấp nhận được là bao lâu?

# 3. Giả định, phụ thuộc và vấn đề mở

## 3.1 Giả định đã ghi nhãn

| ID | Giả định | Cơ sở | Trạng thái |
|---|---|---|---|
| `A-01` | Trong prototype, mỗi khung giờ dùng sức chứa cấu hình; dữ liệu kiểm thử mặc định có thể dùng `N = 2` | Quy tắc sức chứa chưa được xác nhận | Chờ `Q-01` |
| `A-02` | Hệ thống được triển khai dạng web; nhân viên/bác sĩ dùng máy tính, bệnh nhân có thể dùng điện thoại | Phù hợp mục tiêu truy cập từ xa nhưng chưa được stakeholder xác nhận | Chờ STK-01 |
| `A-03` | Giờ mở cửa cụ thể chưa xác định; hệ thống phải cho phép cấu hình ca làm việc thay vì hard-code | Tình huống chỉ nói “mỗi ca” | Chờ STK-01 |
| `A-04` | Prototype dùng chính sách sao lưu mỗi ngày, RPO 24 giờ, RTO 4 giờ | Ngưỡng lưu trữ/khôi phục chưa có | Chờ `Q-09` |
| `A-05` | Bộ trường bệnh nhân tối thiểu của prototype: họ tên, ngày sinh, số điện thoại | Case không liệt kê trường bắt buộc | Chờ `Q-05` |
| `A-06` | Khi bác sĩ nghỉ, prototype cho phép nhân viên chọn một trong các hướng: đổi giờ, đổi bác sĩ phù hợp hoặc hủy | Case chỉ xác nhận hiện tại phải gọi từng bệnh nhân | Chờ `Q-X4` |
| `A-07` | Prototype dùng 4 vai trò: Quản lý, Nhân viên tiếp nhận, Bác sĩ, Bệnh nhân | Có 4 stakeholder chính; quyền chi tiết chưa xác nhận | Chờ `Q-07` |
| `A-08` | Mục tiêu hiệu năng prototype: tác vụ đọc phổ biến ≤ 2 giây ở tải thử nghiệm | Chưa có ngưỡng stakeholder | Chờ `Q-X7` |
| `A-09` | Prototype kiểm thử tối thiểu 10 phiên đồng thời | Số user đồng thời thực tế chưa có | Chờ `Q-X7` |
| `A-10` | Phiên đăng nhập prototype tự hết hạn sau 15 phút không hoạt động | Chưa có chính sách bảo mật cụ thể | Chờ `Q-X8` |
| `A-11` | Mục tiêu usability prototype: bệnh nhân tự đặt lịch ≤ 6 bước, nhân viên đặt hộ ≤ 8 bước | Chưa có ngưỡng usability từ stakeholder | Chờ khảo sát |
| `A-12` | Prototype ghi nhật ký các thao tác thay đổi lịch và dữ liệu quan trọng | Cần hỗ trợ truy vết thao tác nhưng stakeholder chưa xác nhận | Chờ `Q-07` |
| `A-13` | Prototype không lưu mật khẩu dạng plaintext; thông tin xác thực phải được bảo vệ bằng cơ chế phù hợp | Quy tắc kỹ thuật bảo mật của prototype | Chờ xác nhận chính sách bảo mật |

## 3.2 Câu hỏi chưa được stakeholder trả lời

| Mã | Câu hỏi | Hỏi ai | Requirement bị ảnh hưởng |
|---|---|---|---|
| `Q-01` | Khung giờ chuẩn và sức chứa tối đa là bao nhiêu? | STK-01, STK-03 | FR-02, FR-03 |
| `Q-02` | Quy định đổi/hủy: báo trước bao lâu, có cần duyệt không? | STK-01, STK-03, STK-04 | FR-05, FR-06 |
| `Q-03` | Bệnh nhân đặt online xác minh danh tính bằng cách nào? | STK-01, STK-04 | FR-01, FR-02, FR-10 |
| `Q-04` | Quy trình mới có còn gọi điện xác nhận không? | STK-01, STK-03 | FR-04, FR-11 |
| `Q-05` | Trường dữ liệu bệnh nhân tối thiểu gồm những gì? Bệnh nền/dị ứng có thuộc phạm vi hay không? | STK-01, STK-02 | FR-01, FR-08 |
| `Q-06` | Quy tắc đến trễ, vắng mặt, khám gấp là gì? | STK-01, STK-03 | FR-04, FR-09 |
| `Q-07` | Ai được xem/sửa loại dữ liệu nào? | STK-01, STK-03 | FR-10, NFR-04 |
| `Q-08` | Kênh thông báo nào được chấp nhận và ai chịu chi phí? | STK-01, STK-04 | FR-11 |
| `Q-09` | Chính sách lưu trữ, sao lưu, RPO/RTO cụ thể là gì? | STK-01 | NFR-05 |

## 3.3 Phụ thuộc

| ID | Phụ thuộc | Liên quan |
|---|---|---|
| DEP-01 | Hệ thống phụ thuộc kết nối mạng để đồng bộ lịch và dữ liệu | Operating Environment |
| DEP-02 | Chức năng thông báo phụ thuộc kênh được stakeholder lựa chọn | FR-11, Q-08 |
| DEP-03 | Sau CR-01, thanh toán phụ thuộc cổng thanh toán bên thứ ba | FR-12, Q-CR01-01 |
| DEP-04 | Sau CR-01, khám trực tuyến phụ thuộc nền tảng/phương thức phiên khám được lựa chọn | FR-14, Q-CR01-05 |

# 4. Môi trường vận hành

- Ứng dụng web.
- Nhân viên tiếp nhận và bác sĩ truy cập bằng trình duyệt trên máy tính.
- Bệnh nhân có thể truy cập bằng trình duyệt trên điện thoại hoặc máy tính.
- Hệ thống cần kết nối mạng để đồng bộ dữ liệu.
- Môi trường triển khai, hệ điều hành, trình duyệt hỗ trợ, cấu hình máy chủ và dịch vụ thông báo **chưa được stakeholder xác nhận**.


# 5. Các hạng mục yêu cầu

## 5.1 Yêu cầu chức năng

| ID | Loại | Nguồn | Ưu tiên | Phiên bản | Mô tả | Lý do | Tiêu chí kiểm chứng |
|---|---|---|---|---|---|---|---|
| **FR-01 — Quản lý thông tin bệnh nhân cơ bản** | Chức năng | `F-CS`; `STK-02`; `STK-04`; `A-05`; `Q-05` | Must | 1.0 | Hệ thống phải cho phép tạo, tra cứu và cập nhật thông tin bệnh nhân phục vụ đặt lịch/tiếp nhận. Bộ trường prototype theo `A-05` cho đến khi `Q-05` được xác nhận. | Bệnh nhân mới hiện chỉ khai thông tin khi đến phòng khám; bác sĩ cần thông tin để chuẩn bị. | Với dữ liệu theo `A-05`, tạo được hồ sơ mới, tra cứu lại được và cập nhật không làm mất dữ liệu cũ ngoài trường được sửa. |
| **FR-02 — Đặt lịch hẹn mới** | Chức năng | `STK-01`; `STK-04`; `F-CS` | Must | 1.0 | Hệ thống phải cho phép chọn chuyên khoa/bác sĩ/ngày và chọn một khung giờ khả dụng để tạo lịch. | Giảm phụ thuộc vào gọi điện và sổ giấy. | Chỉ slot khả dụng mới chọn được; đặt thành công sinh đúng 1 lịch; lịch xuất hiện trong danh sách của nhân viên và bác sĩ liên quan. |
| **FR-03 — Kiểm tra ràng buộc đặt lịch** | Chức năng | `F-CS`; `A-01`; `Q-01`; `Q-X5` | Must | 1.0 | Hệ thống phải từ chối đặt lịch nếu vượt sức chứa cấu hình, bệnh nhân có lịch giao nhau hoặc bác sĩ không làm việc. | Tránh tạo lịch không hợp lệ khi nhiều người thao tác. | Với dataset `A-01`, khi slot đã đủ `N` lịch hợp lệ thì lịch tiếp theo bị từ chối và dữ liệu cũ không thay đổi. |
| **FR-04 — Quản lý trạng thái lịch hẹn** | Chức năng | `F-CS`; `STK-03`; `Q-04`; `Q-06` | Must | 1.0 | Hệ thống phải quản lý vòng đời lịch hẹn. Tập trạng thái chi tiết phải phù hợp quy trình đã xác nhận; prototype hỗ trợ tối thiểu Chờ xác nhận, Đã xác nhận, Đã đến, Hủy. | Giúp nhiều nhân viên cùng thấy một trạng thái thống nhất. | Mọi chuyển trạng thái được ghi thời điểm và người thực hiện; chuyển trạng thái không được cấu hình phải bị từ chối. |
| **FR-05 — Đổi lịch hẹn** | Chức năng | `STK-04`; `STK-03`; `Q-02` | Must | 1.0 | Hệ thống phải cho phép đổi một lịch chưa kết thúc sang slot hợp lệ khác theo chính sách phòng khám. | Bệnh nhân muốn đổi lịch mà không phải đến tận nơi. | Đổi thành công giải phóng slot cũ, chiếm slot mới và giữ mã lịch; nếu slot mới không còn khả dụng thì lịch cũ vẫn giữ nguyên. |
| **FR-06 — Hủy lịch hẹn** | Chức năng | `STK-04`; `STK-03`; `Q-02` | Must | 1.0 | Hệ thống phải cho phép hủy lịch chưa kết thúc theo chính sách phòng khám và giải phóng slot. | Giữ dữ liệu lịch trống chính xác. | Sau hủy, lịch có trạng thái Hủy và slot có thể được đặt lại; lịch hủy vẫn tra cứu được. |
| **FR-07 — Quản lý lịch làm việc và lịch bị ảnh hưởng khi bác sĩ nghỉ** | Chức năng | `STK-02`; `STK-03`; `F-CS`; `A-06`; `Q-X4` | Must | 1.0 | Hệ thống phải cho phép ghi lịch làm việc/nghỉ của bác sĩ và xác định các lịch hẹn bị ảnh hưởng. Hành động xử lý theo chính sách được xác nhận; prototype dùng `A-06`. | Hiện nhân viên phải gọi từng bệnh nhân khi bác sĩ nghỉ. | Đánh dấu bác sĩ nghỉ làm slot tương ứng không thể đặt mới; danh sách lịch bị ảnh hưởng được tạo đầy đủ. |
| **FR-08 — Bác sĩ xem danh sách lịch khám** | Chức năng | `STK-02`; `F-CS`; `Q-O5`; `Q-05` | Must | 1.0 | Hệ thống phải cho phép bác sĩ xem danh sách bệnh nhân theo ngày/ca và các thông tin đã được cấp quyền để chuẩn bị. | Hiện bác sĩ nhận danh sách vào đầu ca. | Chọn ngày/ca trả đúng các lịch của bác sĩ; không hiển thị dữ liệu ngoài quyền được cấu hình. |
| **FR-09 — Tiếp nhận bệnh nhân đến khám** | Chức năng | `F-CS`; `STK-03`; `Q-X1`; `Q-X2`; `Q-X3` | Must | 1.0 | Hệ thống phải cho phép nhân viên ghi nhận bệnh nhân đã đến. Các trạng thái đến trễ/vắng/khám gấp chỉ áp dụng theo business rule đã xác nhận. | Hệ thống được yêu cầu hỗ trợ tiếp nhận bệnh nhân. | Một lịch hợp lệ có thể được đánh dấu Đã đến; hệ thống lưu thời điểm và nhân viên thực hiện. |
| **FR-10 — Quản lý tài khoản, vai trò và nhật ký** | Chức năng | `F-CS`; `STK-01`; `A-07`; `A-12`; `Q-07` | Must | 1.0 | Hệ thống phải hỗ trợ tài khoản theo vai trò, kiểm tra quyền trước khi truy cập chức năng/dữ liệu và lưu nhật ký thao tác quan trọng. | Quyền xem/sửa là nội dung bắt buộc cần làm rõ; hệ thống có nhiều loại người dùng. | Thao tác ngoài quyền bị từ chối; thao tác cập nhật lịch tạo nhật ký gồm người thực hiện, thời điểm và đối tượng. |
| **FR-11 — Thông báo thay đổi lịch** | Chức năng | `STK-01`; `STK-03`; `STK-04`; `Q-08`; `F-CS` | Should | 1.0 | Hệ thống phải tạo thông báo khi lịch được tạo/đổi/hủy hoặc bị ảnh hưởng do bác sĩ nghỉ. Kênh gửi do `Q-08` quyết định. | Giảm nhu cầu gọi điện thủ công và giúp bệnh nhân biết thay đổi. | Mỗi sự kiện tạo đúng thông báo gắn đúng lịch; nội dung ngày/giờ/bác sĩ khớp dữ liệu lịch; trạng thái gửi được ghi lại nếu có tích hợp kênh gửi. |

## 5.2 Yêu cầu phi chức năng

### Nhóm A — Hiệu năng và quy mô

| ID | Loại | Nguồn | Ưu tiên | Phiên bản | Mô tả | Lý do | Tiêu chí kiểm chứng |
|---|---|---|---|---|---|---|---|
| **NFR-01 — Thời gian phản hồi** | Hiệu năng | `STK-01`; `STK-03`; `A-08`; `Q-X7` | Must | 1.0 | Trong prototype, các màn hình tra cứu lịch phổ biến phải phản hồi theo ngưỡng `A-08`; ngưỡng production phải xác nhận qua khảo sát. | Quy trình đặt lịch cần nhanh và không làm tăng thời gian thao tác. | Với tải thử nghiệm chuẩn, 95% yêu cầu đọc lịch ≤ 2 giây theo `A-08`. |
| **NFR-02 — Người dùng đồng thời** | Hiệu năng | `F-CS`; `A-09`; `Q-X7` | Should | 1.0 | Prototype phải hỗ trợ ít nhất 10 phiên đồng thời mà không phát sinh lỗi chức năng. | Cần kiểm tra hệ thống khi nhiều vai trò thao tác cùng lúc. | Chạy 10 phiên đồng thời thực hiện tra cứu/đặt lịch; không có lỗi 5xx hoặc mất dữ liệu. |

### Nhóm B — Bảo mật và dữ liệu

| ID | Loại | Nguồn | Ưu tiên | Phiên bản | Mô tả | Lý do | Tiêu chí kiểm chứng |
|---|---|---|---|---|---|---|---|
| **NFR-03 — Xác thực và phiên làm việc** | Bảo mật | `F-CS`; `A-10`; `A-13`; `Q-X8` | Must | 1.0 | Các chức năng nội bộ phải yêu cầu đăng nhập; thông tin xác thực không được lưu dạng mật khẩu thuần; prototype hết phiên theo `A-10`. | Hệ thống xử lý dữ liệu cá nhân và lịch khám. | Tài khoản chưa đăng nhập không truy cập được màn hình nội bộ; phiên không hoạt động 15 phút hết hiệu lực theo `A-10`. |
| **NFR-04 — Phân quyền dữ liệu** | Bảo mật | `F-CS`; `A-07`; `Q-07` | Must | 1.0 | Mọi truy cập dữ liệu phải tuân theo ma trận quyền cấu hình theo vai trò. | Quyền xem/chỉnh sửa là nội dung đề bài yêu cầu khảo sát. | Test một thao tác được phép và một thao tác bị cấm cho từng vai trò trong ma trận quyền đã xác nhận. |
| **NFR-05 — Sao lưu và khôi phục** | Dữ liệu/Reliability | `F-CS`; `A-04`; `Q-09` | Should | 1.0 | Prototype sao lưu và khôi phục theo `A-04`; ngưỡng production phải được stakeholder xác nhận. | Mất lịch làm gián đoạn vận hành. | Thực hiện phục hồi từ bản sao lưu thử nghiệm; dữ liệu đối chiếu đúng và thời gian phục hồi không vượt `A-04`. |

### Nhóm C — Khả dụng

| ID | Loại | Nguồn | Ưu tiên | Phiên bản | Mô tả | Lý do | Tiêu chí kiểm chứng |
|---|---|---|---|---|---|---|---|
| **NFR-06 — Số bước đặt lịch** | Usability | `STK-01`; `STK-03`; `STK-04`; `A-11` | Should | 1.0 | Prototype hướng tới bệnh nhân tự đặt lịch không quá 6 bước và nhân viên đặt hộ không quá 8 bước. | Phản ánh mục tiêu đặt lịch nhanh. | Chạy test usability với kịch bản chuẩn; số bước không vượt `A-11`. |

# 6. Bối cảnh yêu cầu

## SC-01 — Bệnh nhân đặt lịch thành công

- **Requirement liên quan:** FR-01, FR-02, FR-03, FR-11
- **Tác nhân chính:** Bệnh nhân
- **Tiền điều kiện:** Có bác sĩ và lịch làm việc khả dụng; bệnh nhân có thể cung cấp thông tin cần thiết.
- **Kích hoạt:** Bệnh nhân chọn chức năng đặt lịch.

### Luồng chính

1. Bệnh nhân chọn chuyên khoa hoặc bác sĩ.
2. Hệ thống hiển thị ngày và khung giờ khả dụng.
3. Bệnh nhân chọn một khung giờ.
4. Hệ thống kiểm tra ràng buộc theo FR-03.
5. Bệnh nhân nhập/xác nhận thông tin cần thiết.
6. Hệ thống tạo lịch hẹn.
7. Hệ thống cập nhật sức chứa khung giờ.
8. Hệ thống hiển thị kết quả đặt lịch.
9. Nếu FR-11 được cấu hình kênh gửi, hệ thống tạo thông báo tương ứng.

### Luồng thay thế/ngoại lệ

- **A1 — Dữ liệu bệnh nhân không hợp lệ:** Hệ thống chỉ rõ trường lỗi và không tạo lịch.
- **A2 — Slot vừa hết chỗ:** Hệ thống từ chối tạo lịch và yêu cầu chọn slot khác.
- **A3 — Bác sĩ vừa được đánh dấu nghỉ:** Hệ thống thông báo slot không còn khả dụng.

### Hậu điều kiện

- **Thành công:** Có đúng một lịch hẹn mới.
- **Thất bại:** Không tạo lịch -> dữ liệu lịch hiện có không bị thay đổi.


## SC-02 — Khung giờ hoặc bác sĩ không còn khả dụng

- **Requirement liên quan:** FR-02, FR-03, FR-07
- **Tác nhân chính:** Bệnh nhân
- **Tiền điều kiện:** Bệnh nhân đang chọn lịch.
- **Kích hoạt:** Bệnh nhân chọn một slot không còn khả dụng.

### Luồng chính

1. Bệnh nhân chọn bác sĩ/ngày.
2. Hệ thống kiểm tra lịch làm việc và sức chứa.
3. Hệ thống phát hiện slot không hợp lệ.
4. Hệ thống từ chối thao tác đặt lịch.
5. Hệ thống hiển thị lý do và tải lại danh sách slot khả dụng.

### Ngoại lệ

- **A1 — Cạnh tranh đồng thời:** Một người khác đặt thành công trước; giao dịch hiện tại bị từ chối và lịch cũ không bị ảnh hưởng.
- **A2 — Bác sĩ nghỉ đột xuất:** Slot của bác sĩ không còn cho phép đặt.

### Hậu điều kiện

Không có lịch không hợp lệ được tạo.


## SC-03 — Bệnh nhân đổi hoặc hủy lịch

- **Requirement liên quan:** FR-05, FR-06, FR-11
- **Tác nhân chính:** Bệnh nhân
- **Tiền điều kiện:** Bệnh nhân có một lịch chưa kết thúc và được phép thay đổi theo chính sách.
- **Kích hoạt:** Bệnh nhân chọn Đổi lịch hoặc Hủy lịch.

### Luồng chính — Đổi lịch

1. Bệnh nhân mở lịch hiện tại.
2. Bệnh nhân chọn Đổi lịch.
3. Hệ thống hiển thị các slot hợp lệ.
4. Bệnh nhân chọn slot mới.
5. Hệ thống kiểm tra FR-03.
6. Hệ thống chuyển lịch sang slot mới và giải phóng slot cũ.
7. Hệ thống ghi lịch sử thay đổi.
8. Hệ thống tạo thông báo theo FR-11 nếu được cấu hình.

### Luồng chính — Hủy lịch

1. Bệnh nhân mở lịch hiện tại.
2. Bệnh nhân chọn Hủy.
3. Hệ thống yêu cầu xác nhận.
4. Hệ thống chuyển lịch sang trạng thái Hủy.
5. Hệ thống giải phóng slot.
6. Hệ thống tạo thông báo nếu được cấu hình.

### Ngoại lệ

- **A1 — Quá hạn thay đổi:** Hệ thống xử lý theo business rule được xác nhận từ `Q-02`, không tự áp dụng ngưỡng thời gian chưa được xác nhận.
- **A2 — Slot mới vừa hết chỗ:** Hệ thống giữ nguyên lịch cũ.

### Hậu điều kiện

- Đổi thành công: lịch nằm ở slot mới.
- Hủy thành công: lịch có trạng thái Hủy và slot được giải phóng.
- Thất bại: lịch cũ giữ nguyên.


## SC-04 — Bác sĩ xem danh sách lịch khám

- **Requirement liên quan:** FR-08, FR-10, NFR-04
- **Tác nhân chính:** Bác sĩ
- **Tiền điều kiện:** Bác sĩ đã đăng nhập và có quyền xem lịch của mình.
- **Kích hoạt:** Bác sĩ mở danh sách lịch khám theo ngày/ca.

### Luồng chính

1. Bác sĩ chọn ngày hoặc ca.
2. Hệ thống kiểm tra quyền.
3. Hệ thống hiển thị các lịch thuộc bác sĩ.
4. Bác sĩ chọn một lịch.
5. Hệ thống hiển thị thông tin bệnh nhân trong phạm vi được cấp quyền.

### Ngoại lệ

- Truy cập lịch không thuộc quyền: hệ thống từ chối và ghi nhật ký.

### Hậu điều kiện

Không thay đổi dữ liệu lịch; thao tác truy cập được kiểm soát theo quyền.


## SC-05 — Bác sĩ nghỉ đột xuất

- **Requirement liên quan:** FR-07, FR-11
- **Tác nhân chính:** Nhân viên tiếp nhận/Quản lý
- **Tiền điều kiện:** Bác sĩ có lịch làm việc và có lịch hẹn trong thời gian bị ảnh hưởng.
- **Kích hoạt:** Người có quyền ghi nhận bác sĩ nghỉ.

### Luồng chính

1. Người dùng chọn bác sĩ và thời gian nghỉ.
2. Hệ thống xác định các lịch hẹn bị ảnh hưởng.
3. Hệ thống ngăn đặt lịch mới vào thời gian nghỉ.
4. Hệ thống hiển thị danh sách lịch cần xử lý.
5. Nhân viên áp dụng phương án được chính sách cho phép; prototype theo `A-06`.
6. Hệ thống cập nhật các lịch tương ứng.
7. Hệ thống tạo thông báo cho bệnh nhân theo FR-11 nếu có kênh gửi.

### Ngoại lệ

- Không có lịch bị ảnh hưởng: hệ thống chỉ cập nhật lịch nghỉ.
- Không có slot/bác sĩ thay thế: nhân viên giữ lịch ở trạng thái cần xử lý hoặc hủy theo chính sách.

### Hậu điều kiện

Không còn slot mới cho bác sĩ trong thời gian nghỉ; các lịch bị ảnh hưởng được nhận diện và có trạng thái xử lý rõ ràng.

## SC-06 — Tiếp nhận bệnh nhân đến khám

- **Requirement liên quan:** FR-09
- **Tác nhân chính:** Nhân viên tiếp nhận
- **Tiền điều kiện:** Bệnh nhân có lịch hợp lệ.
- **Kích hoạt:** Bệnh nhân đến phòng khám.

### Luồng chính
1. Nhân viên tìm lịch của bệnh nhân.
2. Hệ thống hiển thị lịch phù hợp.
3. Nhân viên chọn Ghi nhận đã đến.
4. Hệ thống cập nhật trạng thái Đã đến.
5. Hệ thống lưu thời điểm và nhân viên thực hiện.

### Ngoại lệ
- Không tìm thấy lịch: hệ thống không tự tạo lượt mới; xử lý theo quy trình được stakeholder xác nhận.
- Bệnh nhân đến trễ: xử lý theo Q-06.

### Hậu điều kiện
Lịch được ghi nhận Đã đến hoặc giữ nguyên nếu thao tác thất bại.


# 7. Validation Report

## 7.1 Phương pháp peer review

Peer review chéo kiểm tra các thuộc tính:

- Tính đúng đắn.
- Tính đầy đủ.
- Tính nhất quán.
- Tính khả thi.
- Tính rõ ràng.
- Tính đo lường/kiểm chứng được.
- Khả năng truy vết nguồn.

## 7.2 Vấn đề phát hiện và quyết định xử lý

| ID | Vấn đề phát hiện | Tiêu chí bị ảnh hưởng | Quyết định | Trạng thái |
|---|---|---|---|---|
| `REV-01` | Bản cũ đưa doanh thu/chấm công vào “giá trị mong đợi” nhưng case không cung cấp nhu cầu này | Đúng đắn, phạm vi | Loại khỏi baseline | Đã sửa |
| `REV-02` | Bản cũ coi bệnh nền/dị ứng/CCCD là trường bắt buộc dù case chưa xác nhận | Đúng đắn, truy vết | Chuyển thành `A-05`/`Q-05`; FR-01 chỉ yêu cầu thông tin cơ bản | Đã sửa |
| `REV-03` | Bản cũ dùng sức chứa cố định 2 như sự thật | Đúng đắn, đo lường | Chuyển thành dataset prototype `A-01`; production chờ `Q-01` | Đã sửa |
| `REV-04` | FR cũ mô tả khám gấp và giới thiệu chi tiết dù đề yêu cầu khảo sát thêm | Đúng đắn, phạm vi | FR-09 đổi thành “tiếp nhận”; quy tắc trễ/vắng/khám gấp để `Q-06` | Đã sửa |
| `REV-05` | Bản cũ có NFR 2 giây, 10 user, 3 năm, 15 phút session nhưng không ghi rõ là giả định | Truy vết, đo lường | Đưa các ngưỡng vào `A-04`, `A-08`, `A-09`, `A-10` | Đã sửa |
| `REV-06` | Scenario cũ dùng mũi tên một dòng, chưa đánh số tương tác | Rõ ràng, kiểm chứng | Viết lại SC-01…SC-05 theo mẫu tác nhân/tiền điều kiện/kích hoạt/luồng | Đã sửa |
| `REV-07` | Scenario đổi lịch cũ tự thêm “bên thứ 3 được ủy quyền” không có nguồn | Đúng đắn | Loại bỏ; chính sách quá hạn chuyển về `Q-02` | Đã sửa |
| `REV-08` | Thiếu bảng thuật ngữ và viết tắt | Đầy đủ | Bổ sung mục 1.8 Thuật ngữ viết tắt | Đã sửa |
| `REV-09` | Bảng yêu cầu cũ thiếu cột phiên bản theo biểu mẫu | Đầy đủ, cấu trúc | Bổ sung cột Phiên bản cho FR/NFR | Đã sửa |
| `REV-10` | Bản cũ chưa có Validation Report, test scenarios, traceability matrix và CR-01 | Đầy đủ | Bổ sung các mục 7, 8, 9, 10 | Đã sửa |
| `REV-11` | Ngoại lệ cũ có thanh toán nhưng chưa nêu khám trực tuyến, trong khi CR-01 cố tình thêm hai nội dung này sau baseline | Nhất quán | Ghi rõ telemedicine và payment ngoài baseline 1.0 | Đã sửa |
| `REV-12` | Bản cũ mâu thuẫn giữa “hồ sơ bệnh nhân ngoài phạm vi” và FR bác sĩ mở hồ sơ | Nhất quán | Phân biệt thông tin hành chính cơ bản (in scope) với bệnh án lâm sàng đầy đủ (out of scope) | Đã sửa |

## 7.3 Kết luận kiểm nghiệm

- **Đúng đắn:** các yêu cầu không còn tự coi dữ liệu chưa xác nhận là sự thật; các ngưỡng chưa xác nhận được gắn `A-xx`.
- **Đầy đủ:** đã có ≥10 FR, ≥6 NFR thuộc ≥3 nhóm, ≥4 scenario, ≥8 review issue và ≥6 test scenario.
- **Nhất quán:** scope baseline phân biệt rõ thông tin bệnh nhân cơ bản với bệnh án lâm sàng; telemedicine/payment nằm ngoài 1.0 và chỉ vào hệ thống qua CR-01.
- **Khả thi:** core scope tập trung vào booking/reception/schedule; các tính năng mở rộng được tách khỏi baseline.
- **Rõ ràng:** scenario dùng bước đánh số; thuật ngữ được định nghĩa.
- **Đo lường được:** mỗi FR/NFR có tiêu chí kiểm chứng; các ngưỡng chưa được stakeholder xác nhận được ghi là giả định.


# 8. Trường hợp kiểm thử

## TC-01 — Đặt lịch thành công

- **Requirement:** FR-02, FR-03
- **Tiền điều kiện:** Có bác sĩ và slot khả dụng.
- **Bước chính:** Chọn bác sĩ → chọn slot → nhập thông tin hợp lệ → xác nhận.
- **Kết quả mong đợi:** Sinh đúng 1 lịch; slot giảm sức chứa; lịch xuất hiện trong danh sách liên quan.

## TC-02 — Từ chối khi slot đã đủ sức chứa

- **Requirement:** FR-03
- **Tiền điều kiện:** Slot đã có `N` lịch hợp lệ theo cấu hình.
- **Bước chính:** Thử tạo thêm lịch tại cùng slot.
- **Kết quả mong đợi:** Hệ thống từ chối; dữ liệu lịch hiện có không thay đổi; hiển thị lý do.

## TC-03 — Đổi lịch thành công

- **Requirement:** FR-05
- **Tiền điều kiện:** Có lịch cũ và slot mới hợp lệ.
- **Bước chính:** Mở lịch → Đổi → chọn slot mới → xác nhận.
- **Kết quả mong đợi:** Giữ mã lịch; slot cũ được giải phóng; slot mới được chiếm.

## TC-04 — Đổi lịch thất bại do cạnh tranh đồng thời

- **Requirement:** FR-03, FR-05
- **Tiền điều kiện:** Slot mới vừa bị người khác đặt đủ sức chứa.
- **Bước chính:** Người dùng xác nhận đổi sang slot vừa hết chỗ.
- **Kết quả mong đợi:** Đổi bị từ chối; lịch cũ vẫn giữ nguyên.

## TC-05 — Hủy lịch và giải phóng slot

- **Requirement:** FR-06
- **Tiền điều kiện:** Có lịch chưa kết thúc.
- **Bước chính:** Mở lịch → Hủy → xác nhận.
- **Kết quả mong đợi:** Lịch chuyển Hủy; slot được giải phóng; lịch vẫn tra cứu được.

## TC-06 — Ghi nhận bác sĩ nghỉ

- **Requirement:** FR-07
- **Tiền điều kiện:** Bác sĩ có lịch hẹn trong thời gian được chọn.
- **Bước chính:** Ghi nhận khoảng nghỉ.
- **Kết quả mong đợi:** Không cho đặt lịch mới; tạo đúng danh sách lịch bị ảnh hưởng.

## TC-07 — Bác sĩ chỉ xem dữ liệu trong quyền

- **Requirement:** FR-08, FR-10, NFR-04
- **Tiền điều kiện:** Có tài khoản bác sĩ và dữ liệu của nhiều bác sĩ.
- **Bước chính:** Bác sĩ mở danh sách của mình và thử truy cập dữ liệu ngoài quyền.
- **Kết quả mong đợi:** Dữ liệu được phép hiển thị; dữ liệu ngoài quyền bị từ chối.

## TC-08 — Kiểm tra thời gian phản hồi prototype

- **Requirement:** NFR-01
- **Tiền điều kiện:** Môi trường test và dataset chuẩn.
- **Bước chính:** Thực hiện nhiều lần thao tác đọc lịch.
- **Kết quả mong đợi:** Đạt ngưỡng `A-08`; nếu stakeholder thay đổi ngưỡng thì cập nhật test.

## TC-09 — Thanh toán trước thành công cho lịch trực tuyến

- **Requirement:** FR-12
- **Tiền điều kiện:** Bệnh nhân đặt lịch trực tuyến, slot hợp lệ.
- **Bước chính:** Chọn slot trực tuyến → thực hiện thanh toán thành công → hệ thống nhận phản hồi từ cổng thanh toán.
- **Kết quả mong đợi:** Lịch chuyển trạng thái Đã xác nhận; lưu mã giao dịch hợp lệ; slot được giữ thành công.

## TC-10 — Thanh toán trước thất bại hoặc hết hạn (timeout)

- **Requirement:** FR-12
- **Tiền điều kiện:** Bệnh nhân chọn lịch khám trực tuyến và chuyển đến cổng thanh toán.
- **Bước chính:** Bệnh nhân hủy giao dịch hoặc cổng thanh toán báo timeout quá thời gian giữ slot.
- **Kết quả mong đợi:** Lịch không được xác nhận; slot được giải phóng; thông báo lý do thanh toán thất bại.

## TC-11 — Hoàn tiền tự động khi bác sĩ hủy lịch trực tuyến

- **Requirement:** FR-13, FR-11 v1.1
- **Tiền điều kiện:** Lịch khám trực tuyến đã thanh toán thành công. Bác sĩ báo nghỉ đột xuất hoặc hủy ca khám.
- **Bước chính:** Hệ thống hoặc nhân viên ghi nhận hủy ca khám trực tuyến của bác sĩ.
- **Kết quả mong đợi:** Hệ thống tự động tạo yêu cầu hoàn tiền; cập nhật trạng thái hoàn tiền; gửi thông báo hoàn tiền cho bệnh nhân; không phát sinh hoàn tiền trùng lặp.

## TC-12 — Kiểm soát quyền truy cập phiên khám trực tuyến

- **Requirement:** FR-14, NFR-07
- **Tiền điều kiện:** Phiên khám trực tuyến đã được tạo sau khi thanh toán thành công.
- **Bước chính:** Bệnh nhân và bác sĩ liên quan đăng nhập mở phiên khám; tài khoản không liên quan thử mở đường dẫn phiên khám.
- **Kết quả mong đợi:** Đúng bệnh nhân và bác sĩ của ca khám được cấp quyền truy cập; tài khoản ngoài quyền hoặc lịch chưa thanh toán bị từ chối truy cập.


# 9. Yêu cầu thay đổi

## CR-01 — Khám trực tuyến và thanh toán trước

## 9.1 Nội dung thay đổi

Phòng khám bắt đầu cung cấp **khám trực tuyến**. Bệnh nhân phải **thanh toán trước để xác nhận lịch**; nếu bác sĩ hủy lịch, hệ thống phải **hoàn tiền và thông báo cho bệnh nhân**.


## 9.2 Phân tích tác động

| Thành phần | Mức ảnh hưởng | Thay đổi cần thực hiện |
|---|---|---|
| Phạm vi hệ thống | Cao | Telemedicine và thanh toán chuyển từ Out of Scope sang In Scope |
| FR-02 Đặt lịch | Cao | Bổ sung loại lịch: trực tiếp/trực tuyến |
| FR-04 Trạng thái lịch | Cao | Lịch trực tuyến chỉ được xác nhận khi thanh toán thành công |
| FR-06 Hủy lịch | Cao | Phân biệt hủy bởi bệnh nhân và hủy bởi bác sĩ để quyết định hoàn tiền |
| FR-07 Bác sĩ nghỉ | Cao | Nếu bác sĩ hủy lịch trực tuyến đã thanh toán, kích hoạt hoàn tiền |
| FR-11 Thông báo | Cao | Bổ sung thông báo thanh toán, hoàn tiền, thông tin phiên khám trực tuyến |
| Dữ liệu | Cao | Thêm loại lịch, mã giao dịch, trạng thái thanh toán, số tiền, trạng thái hoàn tiền, tham chiếu phiên khám trực tuyến |
| Scenario | Cao | SC-01, SC-03, SC-05 bị ảnh hưởng; cần thêm SC-07 |
| Test | Cao | Bổ sung test thanh toán, thất bại thanh toán, hoàn tiền và truy cập phiên online |
| Bảo mật/NFR | Cao | Phát sinh yêu cầu về dữ liệu thanh toán và bảo vệ phiên khám trực tuyến |

## 9.3 Yêu cầu mới/sửa đổi 

| ID | Loại | Nguồn | Ưu tiên | Phiên bản | Mô tả | Tiêu chí kiểm chứng |
|---|---|---|---|---|---|---|
| **FR-02 (sửa)** | Chức năng | `CR-01`; `STK-04` | Must | 1.1 | Khi đặt lịch, hệ thống cho phép chọn hình thức khám Trực tiếp hoặc Trực tuyến nếu bác sĩ/dịch vụ hỗ trợ. | Lịch lưu đúng loại khám; các slot không hỗ trợ online không thể chọn loại online. |
| **FR-12 — Thanh toán trước cho lịch trực tuyến** | Chức năng | `CR-01` | Must | 1.1 | Lịch trực tuyến phải có trạng thái thanh toán thành công trước khi chuyển sang Đã xác nhận. | Thanh toán thất bại không xác nhận lịch; thanh toán thành công gắn đúng mã giao dịch với lịch. |
| **FR-13 — Hoàn tiền khi bác sĩ hủy** | Chức năng | `CR-01` | Must | 1.1 | Khi bác sĩ/phòng khám hủy lịch trực tuyến đã thanh toán, hệ thống phải tạo yêu cầu hoàn tiền và ghi trạng thái hoàn tiền. | Một lịch đã thanh toán bị bác sĩ hủy sinh đúng một yêu cầu hoàn tiền; không hoàn tiền trùng. |
| **FR-14 — Phiên khám trực tuyến** | Chức năng | `CR-01` | Must | 1.1 | Hệ thống phải lưu/tham chiếu thông tin truy cập phiên khám trực tuyến cho lịch đã xác nhận. | Chỉ bệnh nhân và bác sĩ liên quan truy cập được thông tin phiên; lịch chưa thanh toán không nhận quyền truy cập. |
| **FR-11 (sửa)** | Chức năng | `CR-01`; `STK-04` | Must | 1.1 | Bổ sung thông báo thanh toán thành công/thất bại, hoàn tiền và thông tin phiên khám online. | Mỗi sự kiện phát sinh đúng thông báo gắn với lịch/giao dịch tương ứng. |
| **NFR-07 — Bảo vệ giao dịch và phiên khám online** | Phi chức năng — Bảo mật | `CR-01` | Must | 1.1 | Không lưu dữ liệu bí mật của phương thức thanh toán ngoài phạm vi cần thiết; dữ liệu phiên khám trực tuyến phải được kiểm soát truy cập. | Tài khoản không liên quan không truy cập được thông tin giao dịch/phiên; log không chứa dữ liệu nhạy cảm bị cấm lưu. |

## 9.4 Scenario mới

### SC-07 — Đặt lịch khám trực tuyến và thanh toán trước

- **Requirement liên quan:** FR-02 v1.1, FR-12, FR-14, FR-11 v1.1
- **Tác nhân chính:** Bệnh nhân
- **Tiền điều kiện:** Có slot hỗ trợ khám trực tuyến.
- **Kích hoạt:** Bệnh nhân chọn hình thức khám trực tuyến.

#### Luồng chính

1. Bệnh nhân chọn bác sĩ và slot hỗ trợ online.
2. Hệ thống tạo lịch ở trạng thái Chờ thanh toán.
3. Bệnh nhân thực hiện thanh toán qua phương thức được cấu hình.
4. Hệ thống nhận kết quả thanh toán thành công.
5. Hệ thống cập nhật trạng thái thanh toán.
6. Hệ thống xác nhận lịch.
7. Hệ thống tạo/tham chiếu thông tin phiên khám trực tuyến.
8. Hệ thống gửi thông báo xác nhận và thông tin cần thiết.

#### Ngoại lệ

- Thanh toán thất bại: lịch không được xác nhận.
- Kết quả thanh toán không rõ do timeout: hệ thống không tự coi là thành công; cần cơ chế đối soát.
- Slot hết chỗ trước khi thanh toán hoàn tất: cần quy tắc giữ slot, là câu hỏi mở `Q-CR01-04`.

#### Hậu điều kiện

- Thành công: lịch online đã xác nhận và có giao dịch hợp lệ.
- Thất bại: lịch không được xác nhận và không phát sinh trạng thái thanh toán sai.


## 9.5 Câu hỏi/rủi ro mới cần làm rõ

| ID | Câu hỏi/rủi ro |
|---|---|
| `Q-CR01-01` | Sử dụng cổng thanh toán nào? Phương thức nào được hỗ trợ? |
| `Q-CR01-02` | Thời hạn hoàn tiền tối đa là bao lâu? Có phí hoàn tiền không? |
| `Q-CR01-03` | Nếu bệnh nhân tự hủy lịch online thì chính sách hoàn tiền thế nào? |
| `Q-CR01-04` | Khi bệnh nhân đang thanh toán, slot được giữ trong bao lâu để tránh người khác chiếm? |
| `Q-CR01-05` | Khám trực tuyến dùng nền tảng tích hợp nào và yêu cầu bảo mật/ghi hình ra sao? |
| `Q-CR01-06` | Nếu cổng thanh toán báo timeout nhưng tiền đã trừ, cơ chế đối soát xử lý thế nào? |

# 10. Traceability Matrix

| Nhu cầu | Stakeholder/Nguồn | Requirement | Scenario | Test Scenario | Change Request |
|---|---|---|---|---|---|
| `N-01` Đặt lịch nhanh, giảm gọi nhiều lần | STK-01, STK-04 | FR-02, FR-03, NFR-01, NFR-06 | SC-01, SC-02 | TC-01, TC-02, TC-08 | — |
| `N-02` Bác sĩ biết lịch và chuẩn bị trước | STK-02 | FR-08, NFR-04 | SC-04 | TC-07 | — |
| `N-03` Lịch thay đổi phải đồng bộ | STK-03 | FR-04, FR-05, FR-06, FR-11 | SC-03 | TC-03, TC-04, TC-05 | — |
| `N-04` Bệnh nhân đổi lịch từ xa | STK-04 | FR-05 | SC-03 | TC-03, TC-04 | — |
| `N-05` Xử lý bác sĩ nghỉ | F-CS, STK-03 | FR-07, FR-11 | SC-05 | TC-06 | — |
| `N-06` Tiếp nhận bệnh nhân | F-CS, STK-03 | FR-01, FR-09 | SC-06 | TC-01 | — |
| `N-07` Kiểm soát quyền và truy vết | F-CS, STK-01 | FR-10, NFR-03, NFR-04 | SC-04 | TC-07 | — |
| `N-08` Khám trực tuyến | CR-01 | FR-02 v1.1, FR-14 | SC-07 | TC-12 | CR-01 |
| `N-09` Thanh toán trước để xác nhận lịch online | CR-01 | FR-12 | SC-07 | TC-09, TC-10 | CR-01 |
| `N-10` Hoàn tiền khi bác sĩ hủy | CR-01 | FR-13, FR-11 v1.1 | SC-05, SC-07 | TC-11 | CR-01 |
| `N-11` Bảo vệ dữ liệu giao dịch/phiên online | CR-01 | NFR-07 | SC-07 | TC-12 | CR-01 |

