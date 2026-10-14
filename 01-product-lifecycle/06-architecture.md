# Phần 6. Architecture — Cấu trúc và quyết định kỹ thuật

**Trạng thái:** chốt tạm thời khung hướng dẫn; bổ sung khi áp dụng thực tế. Chưa chọn kiến trúc hoặc công nghệ cho sản phẩm cụ thể.

## Mục tiêu

Xác định cấu trúc hệ thống, trách nhiệm các thành phần, công nghệ và phương án triển khai phù hợp. Người dùng hiểu lý do và đánh đổi để giao việc cho AI mà vẫn kiểm soát hệ thống.

Bắt đầu từ yêu cầu, ràng buộc và rủi ro. Không mặc định microservices, message broker hoặc thành phần phức tạp khi chưa có nhu cầu rõ ràng.

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
- Backend cần những module nghiệp vụ nào?
- Các thành phần giao tiếp thế nào? Quy tắc nghiệp vụ được kiểm tra ở đâu?
- Một luồng chính đi qua những thành phần nào?

**Đầu ra:** sơ đồ cấu trúc tổng thể, trách nhiệm từng phần và một luồng tương tác chính.

Ví dụ minh họa cho ứng dụng quản lý công việc nhỏ: frontend gọi backend; backend có module dự án và công việc; dữ liệu lưu trong một cơ sở dữ liệu. Đây là phương án để đánh giá, không phải kiến trúc mặc định. Mỗi thành phần bổ sung phải giải thích được yêu cầu mà nó phục vụ.

### 3. Chọn giải pháp và giải thích đánh đổi

- Yêu cầu nào khiến chúng ta cần lựa chọn này?
- Có phương án đơn giản hơn vẫn đáp ứng không?
- Chi phí xây dựng, học và vận hành là gì?
- Đây là nhu cầu sản phẩm hay mục tiêu học tập?
- Bằng chứng hoặc điều kiện nào khiến quyết định cần thay đổi?

**Đầu ra:** lựa chọn công nghệ và cách tổ chức hệ thống kèm lý do ngắn. Chỉ so sánh tối đa 2–3 phương án thực sự phù hợp khi có đánh đổi đáng cân nhắc.

Với quyết định quan trọng, ghi: Bối cảnh → Phương án → Quyết định → Lý do → Hệ quả → Khi nào xem xét lại. Có thể ghi ngay trong tài liệu kiến trúc; chỉ tách ADR khi cần.

Nếu thiếu bằng chứng, thực hiện thử nghiệm nhỏ với câu hỏi cần kiểm chứng, giới hạn thời gian và tiêu chí kết luận.

### 4. Kiểm tra khả năng triển khai và vận hành

- Các thành phần triển khai ở đâu?
- Quản lý cấu hình và thông tin bí mật thế nào?
- Khi thao tác thất bại, người dùng nhận phản hồi gì và tìm lỗi ở đâu?
- Nếu mất dữ liệu, có cách phục hồi phù hợp không?
- Có phần nào quá phức tạp để một người tự duy trì không?

**Đầu ra:** phương án triển khai và vận hành tối thiểu cùng rủi ro cần xử lý. Chưa cần viết toàn bộ cấu hình hạ tầng ở bước này.

## Đầu ra tối thiểu khi áp dụng

Một file `ARCHITECTURE.md` gồm:

- Yêu cầu và ràng buộc chi phối thiết kế.
- Sơ đồ thành phần, trách nhiệm và một luồng tương tác chính.
- Công nghệ được chọn, lý do và đánh đổi quan trọng.
- Cách triển khai, bảo vệ dữ liệu và theo dõi lỗi.
- Giả định, rủi ro, thử nghiệm cần thiết và điều kiện xem xét lại quyết định.

Chưa cần thiết kế toàn bộ bảng, endpoint hoặc class. Làm dần các chi tiết này cho nhóm chức năng sắp triển khai.

## Phân công người và AI

- Người dùng chốt các quyết định quan trọng và chấp nhận đánh đổi.
- AI làm rõ yêu cầu, đề xuất phương án, giải thích hệ quả và chỉ ra giả định; không tự mở rộng phạm vi hay chốt công nghệ chưa được thống nhất.
- Khi người dùng chưa biết bắt đầu, AI giải thích lựa chọn trước, sau đó hỏi từng câu để hỗ trợ quyết định.
- Chất vấn theo từng đề xuất: “Nó giải quyết yêu cầu nào?”, “Nếu bỏ nó thì điều gì không làm được?”, “Bạn chấp nhận chi phí gì để giữ nó?”. Mỗi lượt một câu, đào sâu theo câu trả lời.
- Cập nhật tài liệu khi quyết định thay đổi; phân biệt rõ lựa chọn đã chốt và phương án đang xem xét.

## Điều kiện hoàn thành và checklist

- [ ] Các yêu cầu và ràng buộc quan trọng đã rõ; giả định được ghi riêng.
- [ ] Biết các thành phần, trách nhiệm và cách luồng chính đi qua hệ thống.
- [ ] Các lựa chọn quan trọng có lý do, đánh đổi và được người dùng chấp nhận.
- [ ] Có phương án triển khai, quản lý cấu hình, theo dõi lỗi và phục hồi phù hợp.
- [ ] Rủi ro có thể làm thay đổi cấu trúc đã được kiểm chứng hoặc có kế hoạch xử lý rõ trước phần triển khai phụ thuộc.
- [ ] Đủ cơ sở đi vào thiết kế chi tiết nhóm chức năng tiếp theo.

**Lỗi thường gặp:** chọn công nghệ trước bài toán; thêm thành phần chỉ để học mà không giới hạn thời gian; giả định tải lớn; bỏ qua chi phí vận hành; thiết kế mọi chi tiết trước khi code.

**Mức độ cần thiết:** bắt buộc ở mức vừa đủ; điều chỉnh theo bằng chứng trong quá trình làm, không coi bản đầu là bất biến.

**Bước kế tiếp:** Detailed Design — thiết kế dữ liệu, API và luồng xử lý cho nhóm chức năng sắp triển khai.
