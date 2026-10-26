# Project Setup — Dựng và kiểm chứng nền tảng dự án

**Trạng thái:** đã chốt khung tám nhóm bước; sẽ breakdown chi tiết từng nhóm khi tiếp tục.

## Vị trí trong playbook

Thuộc `01. PRODUCT LIFECYCLE → Implementation & Testing`, là bước đầu trước khi triển khai chức năng. Không thay thế Architecture hoặc Detailed Design; phần 7 của vòng đời vẫn là Detailed Design.

- Architecture quyết định cấu trúc, trách nhiệm, công nghệ và cách giao tiếp.
- Detailed Design thiết kế dữ liệu, contract và luồng xử lý cho nhóm chức năng sắp làm, bao gồm luồng cần kiểm chứng khi setup.
- Project Setup hiện thực các quyết định thành nền tảng chạy và kiểm tra được.
- Bộ quy tắc dựng service dùng lại thuộc `03. STANDARDS & POLICIES`; checklist nghiệm thu có thể đặt trong `04. TEMPLATES & CHECKLISTS`. Tham chiếu thay vì sao chép nội dung.

## Mục tiêu và nguyên tắc

Tạo nền tảng đủ rõ để người dùng kiểm soát và AI tiếp tục phát triển nhất quán. Tự xây dựng để hiểu từng thành phần; chưa chọn ứng dụng, ngôn ngữ, thư viện, công cụ sinh project hoặc cách chia repository trong playbook này.

Bắt đầu bằng **một service đại diện và một luồng kiểm chứng**, hoàn thiện chuẩn rồi mới nhân rộng. Không dựng tất cả service tương lai ngay từ đầu.

Quy tắc cần có ba lớp: chuẩn chung toàn hệ thống; yêu cầu theo loại service; quy ước theo stack khi công nghệ đã được chọn. Service khác ngôn ngữ có thể khác cấu trúc code và công cụ build, nhưng phải tuân thủ contract và quy ước giao tiếp đã chốt.

## Đầu vào chung

Phạm vi MVP, Requirements, mô hình nghiệp vụ, kiến trúc và thiết kế UI liên quan đã được thống nhất. Khi áp dụng cần làm rõ các quyết định còn thiếu ảnh hưởng trực tiếp đến setup, không tự coi giả định là quyết định được duyệt.

## Tám nhóm bước

### 1. Xác định phạm vi setup

- Xác định service và frontend nào cần khởi tạo trong giai đoạn hiện tại.
- Ghi trách nhiệm, loại giao tiếp và dependency của từng thành phần.
- Phân biệt dựng ngay, để sau và ngoài phạm vi.
- Chọn một luồng tối thiểu để kiểm chứng nền tảng.

**Đầu ra:** danh sách thành phần cần dựng và tiêu chí nghiệm thu. Không tự thêm thành phần ngoài kiến trúc đã chốt.

### 2. Chốt quy ước chung toàn hệ thống

- Đặt tên service, API, sự kiện và cấu hình.
- Biểu diễn ID, ngày giờ, số tiền và giá trị thiếu.
- Định dạng lỗi và cách liên kết log với request.
- Xác thực, phân quyền và quản lý secrets theo yêu cầu.
- Quản lý phiên bản, thay đổi contract và tương thích với bên sử dụng.

**Đầu ra:** bộ quy ước có ví dụ, phân biệt bắt buộc và có điều kiện. Project Setup áp dụng tiêu chuẩn; không tự đặt quy ước riêng mâu thuẫn giữa các service.

### 3. Tổ chức repository và cấu trúc từng thành phần

- Xác định vị trí source code, tài liệu, contract, cấu hình môi trường và script.
- Phân định code nghiệp vụ, giao tiếp, truy cập dữ liệu và tích hợp bên ngoài.
- Xác định phần được dùng chung và phần thuộc riêng từng service.
- Quy định cách build và kiểm tra từng thành phần độc lập.

**Đầu ra:** cấu trúc repository và quy tắc tổ chức code. Mỗi ngôn ngữ có cấu trúc phù hợp, không ép cùng một cây thư mục. Không tạo lớp hoặc thư mục rỗng chỉ để đủ mẫu.

### 4. Thiết lập contract tại các điểm giao tiếp

- HTTP API: endpoint, request, response, status và lỗi; dùng mô tả contract phù hợp như OpenAPI khi áp dụng.
- Sự kiện/message: tên, schema, ý nghĩa, bên phát/nhận và cách xử lý trùng nếu cần.
- RPC: dịch vụ, phương thức, message và lỗi tương ứng.

Contract nghiệp vụ được thiết kế trong Detailed Design. Project Setup thiết lập nơi lưu, cách kiểm tra và cách sử dụng contract, cùng contract tối thiểu đã duyệt cho luồng kiểm chứng.

**Đầu ra:** artifact contract và cơ chế kiểm tra implementation tuân thủ. Không bắt service không cung cấp HTTP API phải có HTTP contract. Ngôn ngữ khác nhau không phải lý do thay đổi kiểu dữ liệu hoặc hành vi trong contract.

### 5. Dựng một service mẫu làm chuẩn

- Khởi động, đọc và kiểm tra cấu hình.
- Nhận đầu vào, validation và trả lỗi.
- Logging và kiểm tra tình trạng hoạt động.
- Kết nối, migration và giao dịch dữ liệu nếu có lưu trữ.
- Gọi dependency với timeout và xử lý thất bại nếu có; chỉ retry khi an toàn.
- Kiểm thử, build và đóng gói.

**Đầu ra:** service mẫu hoạt động, có giải thích từng phần. Chỉ nhân rộng sau khi kiểm chứng; service mới chỉ nhận những khả năng cần thiết. Nếu có dữ liệu, xác định quyền sở hữu; service khác không tự đọc/ghi dữ liệu nội bộ của nó.

### 6. Dựng frontend base khi dự án có frontend

- Khung trang, routing và tổ chức feature.
- Component và quy ước UI đã duyệt.
- Lớp giao tiếp API theo contract.
- Xử lý loading, lỗi, trạng thái rỗng và xác thực nếu cần.
- Cấu hình môi trường và kiểm thử nền tảng.

**Đầu ra:** frontend chạy được, thống nhất quy ước giao tiếp và UI, gọi được service mẫu. Backend microservices không mặc định yêu cầu microfrontend.

### 7. Thiết lập cách chạy và kiểm tra lặp lại

- Cấu hình mẫu không chứa secrets và hướng dẫn chuẩn bị môi trường.
- Lệnh chạy, dừng, build và test.
- Cách khởi động dependency cần thiết.
- Kiểm tra tự động khi thay đổi code.
- Cách tạo dữ liệu thử và reset môi trường phát triển khi cần.

**Đầu ra:** bản checkout mới chạy được theo tài liệu, không phụ thuộc vào các bước cấu hình ngầm trên máy người tạo.

### 8. Nghiệm thu nền tảng và bàn giao cho AI

- Kiểm chứng một luồng xuyên suốt thành công.
- Kiểm tra đầu vào sai và dependency thất bại khi áp dụng.
- Kiểm tra contract khớp implementation.
- Xác minh có thể tìm nguyên nhân lỗi từ log.
- Chạy build và các kiểm tra cần thiết.
- Kiểm tra hướng dẫn đủ để phiên AI mới tiếp tục đúng cấu trúc và phạm vi.

**Đầu ra:** checklist nghiệm thu, kết quả kiểm chứng và danh sách giới hạn còn lại. Không coi việc từng project khởi động riêng lẻ là đủ bằng chứng tích hợp.

## Cách breakdown chi tiết tiếp theo

Mỗi nhóm dùng cùng cấu trúc: **đầu vào → quyết định cần chốt → việc thực hiện → artifact → tiêu chí nghiệm thu**. Mỗi quy tắc chỉ rõ áp dụng khi nào, đầu ra bắt buộc và cách kiểm chứng. Dùng tài liệu hoặc file kỹ thuật làm nguồn chính và tham chiếu nhau, tránh trùng lặp.

Người dùng chốt phạm vi và các quyết định quan trọng, review bằng chứng. AI chủ động đề xuất đầy đủ các hạng mục, phát hiện thiếu sót và thực hiện trong phạm vi đã duyệt; không bắt người dùng nhắc từng yêu cầu nền tảng hoặc tự mở rộng chức năng.

## Điều kiện hoàn thành chung

- [ ] Phạm vi và quy ước đã rõ, các điểm chưa chốt được ghi riêng.
- [ ] Có service mẫu và contract phù hợp, cùng frontend nếu thuộc phạm vi.
- [ ] Build, chạy, kiểm tra và luồng tích hợp có bằng chứng đạt.
- [ ] Tài liệu và cấu hình mẫu đủ để tái lập môi trường.
- [ ] Có checklist, giới hạn còn lại và căn cứ để nhân rộng hoặc triển khai chức năng tiếp theo.

**Mức độ cần thiết:** bắt buộc với dự án mới; khi thêm service vào hệ thống có sẵn, tái sử dụng chuẩn hiện hành và kiểm chứng phần mới. Các khả năng như database, messaging hoặc frontend chỉ dựng khi cần.

**Bước thảo luận tiếp theo:** breakdown nhóm 1 — phạm vi setup. Chưa tạo service thực tế hoặc chọn stack trong kho playbook này.
