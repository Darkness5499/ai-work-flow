# Software Product Engineering Playbook

Workflow và checklist dùng chung cho người dùng và AI để xây dựng dự án web full-stack có trình tự, cấu trúc rõ ràng, tài liệu nhất quán và kết quả được kiểm chứng. Khung dài hạn bao phủ vòng đời sản phẩm; phạm vi hiện tại dừng ở Implementation & Testing, tạm hoãn Release và Operations.

## Mục tiêu

- Biết việc tiếp theo cần làm, đầu ra cần tạo và điều kiện hoàn thành.
- Hướng dẫn cả người dùng và AI cách phối hợp, thứ tự các bước trong từng mục lớn và giới hạn công việc.
- Giữ cấu trúc hệ thống, code, contract và tài liệu rõ ràng, dễ tra cứu và đồng bộ khi thay đổi.
- Dùng checklist để hoàn thành dự án chỉn chu: đúng yêu cầu, giao diện nhất quán, code có tổ chức và có bằng chứng kiểm tra.
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

- [Workflow tổng thể — Từ định hướng đến vòng lặp triển khai](01-product-lifecycle/00-overall-workflow.md): hai vòng làm việc, ba mức xử lý thay đổi, ranh giới quyết định giữa người dùng và AI, cùng cách lưu trạng thái để tiếp tục qua phiên.

- [Phần 1. Discovery — Xác định vấn đề, người dùng và mục tiêu](01-product-lifecycle/01-discovery.md): đã chốt trình tự từ ý tưởng đến brief được review, kết quả mong muốn cụ thể và điều kiện mở lại.

- [Phần 2. Product Planning — Flow công việc và giai đoạn](01-product-lifecycle/02-product-planning.md): đầu ra chính là flow các box theo giai đoạn và thứ tự; tách phần ngoài MVP, chưa chia task kỹ thuật.

- [Phần 3. Requirements — Hành vi và tiêu chí chấp nhận](01-product-lifecycle/03-requirements.md): làm rõ luồng, quy tắc, trường hợp lỗi và tiêu chí kiểm tra cho nhóm chức năng sắp triển khai.

- [Phần 4. Domain Design — Mô hình nghiệp vụ tối giản](01-product-lifecycle/04-domain-design.md): khái niệm, quan hệ, quy tắc và trách nhiệm; có thể gộp vào Requirements với CRUD đơn giản.

- [Phần 5. UX/UI Design — Luồng sử dụng và giao diện nhất quán](01-product-lifecycle/05-ux-ui-design.md): chốt tạm thời; người dùng chủ trì, dùng Stitch hoặc công cụ tương đương, duyệt màn hình mẫu và quy ước trước khi mở rộng.

- [Phần 6. Architecture — Cấu trúc và quyết định kỹ thuật](01-product-lifecycle/06-architecture.md): đã chốt; lấy sơ đồ hệ thống làm trung tâm, đề xuất công nghệ có đánh đổi, kiểm tra luồng/thất bại và quy định khi mở lại.

- [Project Setup — thuộc Implementation & Testing](01-product-lifecycle/08-implementation-testing/01-project-setup.md): đã chốt khung tám nhóm bước; dựng một service đại diện và một luồng kiểm chứng trước khi nhân rộng.

- [Phần 7. Detailed Design — Thiết kế triển khai tối giản](01-product-lifecycle/07-detailed-design.md): một ghi chú theo chức năng gồm phạm vi, contract, dữ liệu, xử lý và kiểm chứng; có thể gộp với tài liệu implement API.

- [Phần 8. Implementation & Testing — Triển khai chức năng với AI](01-product-lifecycle/08-implementation-testing/02-feature-implementation.md): hướng dẫn sáu bước, checklist trước/sau khi code, prompt giao việc và ghi chú bàn giao.

Đã có hướng dẫn đến Implementation & Testing. **Phần 9 — Release và phần 10 — Operations tạm hoãn theo yêu cầu người dùng**, chưa cần soạn hoặc đi sâu. Breakdown chi tiết Project Setup cũng được để lại sau. Project Setup thuộc Implementation & Testing, không thay thế Detailed Design và không thuộc Architecture. Bộ quy tắc dựng service dùng lại thuộc Standards & Policies; checklist nghiệm thu thuộc Templates & Checklists khi cần tách riêng.

## Cách dùng workflow và checklist

1. Xác định dự án đang ở giai đoạn nào, đọc ngữ cảnh và các nguồn liên quan.
2. Trong mỗi mục, theo đầu vào → các việc cần làm → đầu ra → checklist và điều kiện hoàn thành. Ghi rõ mục không áp dụng hoặc hoãn cùng lý do.
3. Người dùng chốt phạm vi và quyết định quan trọng; AI chủ động chuẩn bị phương án, thực hiện trong phạm vi và cung cấp bằng chứng kiểm chứng.
4. Khi chỉnh sửa, xác định tác động tới yêu cầu, thiết kế, contract, code, test và tài liệu; cập nhật những nguồn bị ảnh hưởng, kiểm tra lại phần liên quan.
5. Lưu trạng thái đã làm, còn thiếu, quyết định đã chốt và bước tiếp theo để cả người dùng lẫn phiên AI mới tiếp tục được.

Mỗi thông tin có một nguồn chính, các tài liệu khác tham chiếu tới nguồn đó. Checklist phải gắn với kết quả hoặc bằng chứng, không chỉ đánh dấu đã viết tài liệu. Quy trình đủ thực dụng cho một người; không thêm thủ tục hoặc file trùng lặp chỉ để đủ bộ.

## Khung nội dung dự kiến

Bộ skill hỗ trợ đã có trong `skills/skills/`. Xem [danh mục skill và cách sử dụng](05-ai-workflows/skill-catalog.md) để chọn theo nhiệm vụ, kiểm tra điều kiện và tránh nhầm việc có file với việc đã cài đặt công cụ.

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
