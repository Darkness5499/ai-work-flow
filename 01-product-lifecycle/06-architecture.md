# Phần 6. Architecture — Cấu trúc và quyết định kỹ thuật

**Trạng thái:** đã chốt sau phỏng vấn: sơ đồ hệ thống là đầu ra trung tâm, kèm lựa chọn công nghệ, kiểm tra luồng và điều kiện mở lại. Chưa chọn kiến trúc hoặc công nghệ cho sản phẩm cụ thể.

## Mục tiêu

Xác định cấu trúc hệ thống, trách nhiệm các thành phần, công nghệ và phương án triển khai phù hợp. Người dùng hiểu lý do và đánh đổi để giao việc cho AI mà vẫn kiểm soát hệ thống.

Bắt đầu từ yêu cầu, ràng buộc và rủi ro. Playbook không mặc định microservices hoặc hạ tầng phức tạp. Khi người dùng đã chủ động chọn microservices cho một dự án, kể cả để học, AI ghi nhận đó là định hướng đã chốt; tập trung làm rõ ranh giới service, giao tiếp và hạ tầng vừa đủ, không liên tục yêu cầu quay về monolith. Vẫn chỉ ra chi phí và phản biện cách chia service không hợp lý.

## Đầu vào

- Product Planning: phạm vi MVP, thứ tự thực hiện và mục tiêu học tập.
- Requirements: hành vi, quy tắc và yêu cầu chất lượng.
- Domain Design: khái niệm, quan hệ và nhóm trách nhiệm.
- UX/UI: luồng và màn hình đã duyệt.
- Ràng buộc thực tế về thời gian, ngân sách, kỹ năng và môi trường.

## Việc cần làm và câu hỏi cần trả lời

### 1. Xác định yêu cầu chi phối kiến trúc

- Ứng dụng chạy trên máy cá nhân hay trên Internet để dùng từ nhiều thiết bị?
- Có những loại dữ liệu nào? Dữ liệu nào quan trọng hoặc nhạy cảm?
- Luồng nào cần phản hồi ngay, luồng nào có thể xử lý sau?
- Có tích hợp dịch vụ bên ngoài không?
- Có giới hạn thời gian, ngân sách hoặc công nghệ bắt buộc nào?

**Đầu ra:** danh sách ngắn yêu cầu, ràng buộc và rủi ro ảnh hưởng đến thiết kế. Điều chưa biết ghi là giả định, không tự đặt quy mô lớn. Chạy local hay trên Internet được quyết định theo từng dự án, chưa có mặc định được chốt.

### 2. Chia hệ thống và xác định trách nhiệm

- Frontend, backend và nơi lưu dữ liệu chịu trách nhiệm gì?
- Backend cần những module/service nào? Thành phần nào sở hữu dữ liệu nào?
- Các thành phần giao tiếp thế nào? Quy tắc nghiệp vụ được kiểm tra ở đâu?
- Một luồng chính đi qua những thành phần nào?

**Đầu ra:** sơ đồ hệ thống thể hiện frontend, backend/service, nơi lưu dữ liệu và hệ thống bên ngoài liên quan; trách nhiệm, quyền sở hữu dữ liệu và đường giao tiếp có nhãn chỉ cách giao tiếp. Tách rõ thành phần cần cho MVP và phần dự kiến để sau.

Ví dụ minh họa cho ứng dụng quản lý công việc nhỏ: frontend gọi backend; backend có module dự án và công việc; dữ liệu lưu trong một cơ sở dữ liệu. Đây là phương án để đánh giá, không phải kiến trúc mặc định. Mỗi thành phần bổ sung phải giải thích được yêu cầu mà nó phục vụ.

### 3. Chọn giải pháp và giải thích đánh đổi

- Yêu cầu nào khiến chúng ta cần lựa chọn này?
- Có phương án đơn giản hơn vẫn đáp ứng không?
- Chi phí xây dựng, học và vận hành là gì?
- Đây là nhu cầu sản phẩm hay mục tiêu học tập?
- Bằng chứng hoặc điều kiện nào khiến quyết định cần thay đổi?

**Đầu ra:** một phương án ưu tiên, giải thích từng thành phần phục vụ yêu cầu nào và chi phí xây dựng, học, vận hành. Chỉ thêm tối đa hai phương án thay thế khi có đánh đổi đáng cân nhắc. Phân biệt:

- **Cần cho MVP:** thiếu thì không đáp ứng yêu cầu đã chốt.
- **Thêm để học:** phục vụ mục tiêu học tập, có giới hạn phạm vi.
- **Chưa cần:** để sau, không đưa vào base hiện tại.

Người dùng review và chốt trước khi dùng phương án làm căn cứ dựng base.

Với quyết định quan trọng, ghi: Bối cảnh → Phương án → Quyết định → Lý do → Hệ quả → Khi nào xem xét lại. Có thể ghi ngay trong tài liệu kiến trúc; chỉ tách ADR khi cần.

Nếu thiếu bằng chứng, thực hiện thử nghiệm nhỏ với câu hỏi cần kiểm chứng, giới hạn thời gian và tiêu chí kết luận.

### 4. Kiểm tra sơ đồ bằng luồng và tình huống thất bại

AI đi qua một luồng chính và một tình huống thất bại quan trọng trước khi duyệt:

- Trách nhiệm và quyền sở hữu dữ liệu đã rõ chưa?
- Có thành phần hoặc đường giao tiếp bị thiếu không?
- Khi một bên không hoạt động, dữ liệu ở trạng thái nào và người dùng nhận phản hồi gì?

Ví dụ: lưu dữ liệu thành công nhưng lần gọi service tiếp theo thất bại. Chốt hướng xử lý ở mức kiến trúc; chi tiết timeout, retry, transaction và contract để Detailed Design làm khi liên quan. Nếu rủi ro có thể làm đổi kiến trúc, đề xuất thử nghiệm nhỏ trước phần triển khai phụ thuộc.

Đồng thời kiểm tra khả năng triển khai và vận hành tối thiểu:

- Các thành phần triển khai ở đâu?
- Quản lý cấu hình và thông tin bí mật thế nào?
- Khi thao tác thất bại, người dùng nhận phản hồi gì và tìm lỗi ở đâu?
- Nếu mất dữ liệu, có cách phục hồi phù hợp không?
- Có phần nào quá phức tạp để một người tự duy trì không?

**Đầu ra:** phương án triển khai và vận hành tối thiểu cùng rủi ro cần xử lý. Chưa cần viết toàn bộ cấu hình hạ tầng ở bước này.

### 5. Người dùng review và chốt

AI trình bày sơ đồ, phương án ưu tiên, lý do và rủi ro còn lại. Người dùng review, chấp nhận đánh đổi và chốt trước khi dùng làm căn cứ cho Detailed Design và Project Setup. Đánh dấu các giả định và quyết định còn mở, không trình bày chúng như nội dung đã được duyệt.

## Đầu ra tối thiểu khi áp dụng

Một file `ARCHITECTURE.md` gồm:

- Yêu cầu và ràng buộc chi phối thiết kế.
- Sơ đồ hệ thống là trung tâm: thành phần, trách nhiệm, quyền sở hữu dữ liệu, giao tiếp và phần MVP/để sau.
- Kết quả rà một luồng chính và một tình huống thất bại quan trọng.
- Công nghệ được chọn, lý do và đánh đổi; phân biệt cần cho MVP, thêm để học và chưa cần.
- Cách triển khai, bảo vệ dữ liệu và theo dõi lỗi.
- Giả định, rủi ro, thử nghiệm cần thiết và điều kiện xem xét lại quyết định.

Chưa cần thiết kế toàn bộ bảng, endpoint, class hoặc cấu hình triển khai. Làm dần các chi tiết này cho nhóm chức năng sắp triển khai. Việc nêu hướng vận hành tối thiểu không mở lại phần Release và Operations đang hoãn.

## Khi nào mở lại Architecture

- Thêm, tách, gộp service hoặc chuyển trách nhiệm giữa các service.
- Đổi quyền sở hữu dữ liệu hoặc cách các thành phần giao tiếp.
- Thêm công nghệ nền tảng, tích hợp bên ngoài hoặc đổi môi trường triển khai.
- Phát hiện yêu cầu/rủi ro khiến phương án đã chọn không còn phù hợp.

AI trình bày phần sơ đồ bị ảnh hưởng, lý do và đánh đổi; người dùng chốt rồi mới cập nhật. Chỉ rà phần liên quan. Thay đổi endpoint, trường dữ liệu hoặc xử lý nội bộ không ảnh hưởng các quyết định trên được giải quyết ở Detailed Design.

## Phân công người và AI

- Người dùng chốt các quyết định quan trọng và chấp nhận đánh đổi.
- AI làm rõ yêu cầu, đề xuất phương án, giải thích hệ quả và chỉ ra giả định; không tự mở rộng phạm vi hay chốt công nghệ chưa được thống nhất.
- Khi người dùng chưa biết bắt đầu, AI giải thích lựa chọn trước, sau đó hỏi từng câu để hỗ trợ quyết định.
- Chất vấn theo từng đề xuất: “Nó giải quyết yêu cầu nào?”, “Nếu bỏ nó thì điều gì không làm được?”, “Bạn chấp nhận chi phí gì để giữ nó?”. Mỗi lượt một câu, đào sâu theo câu trả lời.
- Cập nhật tài liệu khi quyết định thay đổi; phân biệt rõ lựa chọn đã chốt và phương án đang xem xét.

## Điều kiện hoàn thành và checklist

- [ ] Các yêu cầu và ràng buộc quan trọng đã rõ; giả định được ghi riêng.
- [ ] Sơ đồ rõ thành phần, trách nhiệm, quyền sở hữu dữ liệu, giao tiếp và phần MVP/để sau.
- [ ] Đã rà một luồng chính và một tình huống thất bại quan trọng.
- [ ] Các lựa chọn quan trọng có lý do, đánh đổi và được người dùng chấp nhận.
- [ ] Có phương án triển khai, quản lý cấu hình, theo dõi lỗi và phục hồi phù hợp.
- [ ] Rủi ro có thể làm thay đổi cấu trúc đã được kiểm chứng hoặc có kế hoạch xử lý rõ trước phần triển khai phụ thuộc.
- [ ] Người dùng đã review, chốt phương án và đủ cơ sở cho Detailed Design/Project Setup.

**Lỗi thường gặp:** chọn công nghệ trước bài toán; thêm thành phần chỉ để học mà không giới hạn thời gian; giả định tải lớn; bỏ qua chi phí vận hành; thiết kế mọi chi tiết trước khi code.

**Mức độ cần thiết:** bắt buộc ở mức vừa đủ; điều chỉnh theo bằng chứng trong quá trình làm, không coi bản đầu là bất biến.

**Bước kế tiếp:** Detailed Design — thiết kế dữ liệu, API và luồng xử lý cho nhóm chức năng sắp triển khai.
