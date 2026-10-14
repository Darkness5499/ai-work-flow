# Software Product Engineering Playbook

Quy trình làm việc cá nhân dành cho một lập trình viên full-stack và AI, từ ý tưởng đến triển khai, vận hành và cải tiến sản phẩm.

## Mục tiêu

- Biết việc tiếp theo cần làm, đầu ra cần tạo và điều kiện hoàn thành.
- Rèn tư duy sản phẩm, hệ thống, kiến trúc và vận hành qua dự án thực tế.
- Hiểu các quyết định và đánh đổi; giữ quyền kiểm soát khi làm việc với AI.
- Cân bằng việc hoàn thành sản phẩm với học chuyên sâu, phù hợp nguồn lực một người.

## Bắt đầu và tiếp tục phiên làm việc

1. Đọc [nguyên tắc hướng dẫn](ref/rule.md).
2. Đọc [khung nội dung gốc](ref/readme.md).
3. Đọc [ngữ cảnh và trạng thái hiện tại](PROJECT_CONTEXT.md).
4. Tiếp tục từ câu hỏi hoặc công việc đang mở; mỗi lượt chỉ hỏi một câu quan trọng nhất và chờ câu trả lời.

Playbook dành chung cho các dự án web full-stack, chưa gắn với sản phẩm cụ thể. Đây là kho tài liệu; chưa có ứng dụng cần cài đặt hoặc chạy.

## Nội dung đã thống nhất

- [Phần 1. Discovery — Xác định vấn đề, người dùng và mục tiêu](01-product-lifecycle/01-discovery.md): chốt ở mức tổng quan, gồm mục tiêu, câu hỏi và cách áp dụng tối thiểu.

- [Phần 2. Product Planning — Phạm vi và thứ tự thực hiện](01-product-lifecycle/02-product-planning.md): MVP để tự dùng và kiểm chứng; chốt chức năng, giai đoạn, thứ tự và giới hạn phạm vi cho AI.

- [Phần 3. Requirements — Hành vi và tiêu chí chấp nhận](01-product-lifecycle/03-requirements.md): làm rõ luồng, quy tắc, trường hợp lỗi và tiêu chí kiểm tra cho nhóm chức năng sắp triển khai.

- [Phần 4. Domain Design — Mô hình nghiệp vụ tối giản](01-product-lifecycle/04-domain-design.md): khái niệm, quan hệ, quy tắc và trách nhiệm; có thể gộp vào Requirements với CRUD đơn giản.

- [Phần 5. UX/UI Design — Luồng sử dụng và giao diện nhất quán](01-product-lifecycle/05-ux-ui-design.md): chốt tạm thời; người dùng chủ trì, dùng Stitch hoặc công cụ tương đương, duyệt màn hình mẫu và quy ước trước khi mở rộng.

- [Phần 6. Architecture — Cấu trúc và quyết định kỹ thuật](01-product-lifecycle/06-architecture.md): chốt tạm thời; bắt đầu từ yêu cầu, xác định thành phần, so sánh giải pháp và kiểm tra khả năng vận hành.

Phần tiếp theo cần thảo luận: Detailed Design — dữ liệu, API và luồng xử lý cho nhóm chức năng sắp triển khai.

## Khung nội dung dự kiến

Giữ năm nhóm trong tài liệu gốc, bổ sung nội dung khi có nhu cầu thực tế:

- **Product Lifecycle:** các bước từ discovery đến operations, đầu ra và điều kiện hoàn thành.
- **Process Library:** cách thực hiện những công việc lặp lại.
- **Standards & Policies:** quy ước kỹ thuật và nguyên tắc phối hợp.
- **Templates & Checklists:** mẫu ngắn để áp dụng ngay.
- **AI Workflows:** cách giao việc, kiểm chứng và review kết quả AI.

Đây là khung phân loại, chưa phải thứ tự thực hiện cố định. Không cần tạo đầy đủ tài liệu cho mọi nhóm ngay từ đầu.

## Duy trì tài liệu

- `README.md`: điểm vào dự án; cập nhật khi cấu trúc hoặc cách sử dụng thay đổi.
- `PROJECT_CONTEXT.md`: thông tin đã biết, điều đã chốt và bước tiếp theo; cập nhật sau mỗi lượt có thông tin hoặc kết quả mới.
- `ref/readme.md` và `ref/rule.md`: nguồn định hướng ban đầu; giữ nguyên khi phát triển nội dung làm việc.

Khi đủ thông tin, tóm tắt các điểm đã chốt, giả định và vấn đề còn mở để người dùng kiểm tra trước khi xây dựng quy trình chi tiết. Chỉ bổ sung template, checklist và bản ghi quyết định khi thực sự cần dùng.
