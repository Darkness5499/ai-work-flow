# Ngữ cảnh và trạng thái dự án

## Nguồn thông tin

- [Khung playbook](ref/readme.md).
- [Ngữ cảnh cá nhân và nguyên tắc hướng dẫn](ref/rule.md).
- Yêu cầu khởi tạo kho làm việc để cùng xây dựng workflow cá nhân.

## Thông tin đã biết

- Người dùng là lập trình viên full-stack khoảng 5 năm kinh nghiệm, chủ yếu Angular và Java backend; đã tiếp xúc với microservices.
- Muốn cải thiện khả năng xác định bài toán, phát triển sản phẩm, tư duy hệ thống, thiết kế kiến trúc, lựa chọn giải pháp và vận hành.
- Thực hiện dự án một mình với AI hỗ trợ; quy trình cần vừa sức và ít thủ tục.
- Muốn hiểu cách quyết định và đánh đổi, không để AI quyết định thay.
- Cần phân biệt mục tiêu hoàn thành sản phẩm với mục tiêu học chuyên sâu.
- Người dùng xác nhận playbook dành chung cho các project web full-stack, không có sản phẩm cụ thể. Không yêu cầu chọn sản phẩm thực hành để tiếp tục xây dựng playbook.
- MVP mặc định là bản tự dùng và kiểm chứng. Bước 2 cần cho ra kế hoạch và thứ tự thực hiện chức năng, kiểm soát việc AI tự mở rộng phạm vi.

## Nguyên tắc làm việc

- Mỗi lượt chỉ hỏi một câu quan trọng nhất, chờ trả lời và không hỏi lại thông tin đã có.
- Chưa xây dựng quy trình dài trước khi hiểu nhu cầu.
- Khi đủ thông tin, trình bày những điểm đã chốt, giả định và vấn đề mở để người dùng kiểm tra.
- Bắt đầu lựa chọn kỹ thuật từ yêu cầu, ràng buộc và rủi ro; không mặc định kiến trúc phức tạp.
- AI thực hiện các nhiệm vụ nhỏ trong phạm vi đã chốt, nêu giả định và kiểm chứng kết quả; người dùng tham gia quyết định quan trọng và review kết quả.
- Đọc `ref/rule.md` để có hướng dẫn đầy đủ; bản tóm tắt này không thay thế nguồn gốc.

## Trạng thái hiện tại

**Giai đoạn:** đã chốt phần 1 đến phần 4; chốt tạm thời phần 5 — UX/UI Design và phần 6 — Architecture. Chưa thảo luận phần 7 — Detailed Design.

Người dùng chấp nhận mục tiêu và các câu hỏi Discovery đã trình bày, chưa cần đi sâu. Nội dung được lưu tại [phần 1 — Discovery](01-product-lifecycle/01-discovery.md). Đây là việc chốt hướng dẫn dùng lại, không phải hoàn thành Discovery cho một sản phẩm cụ thể.

Phần 2 được lưu tại [Product Planning](01-product-lifecycle/02-product-planning.md), theo lựa chọn MVP tự dùng và kiểm chứng. Kế hoạch cần phân rõ chức năng MVP, làm sau, chưa quyết định và không làm, cùng thứ tự và giai đoạn triển khai. AI phải tách đề xuất bổ sung khỏi phạm vi đã được người dùng chốt.

Phần 3 được người dùng chấp nhận và lưu tại [Requirements](01-product-lifecycle/03-requirements.md). Chỉ làm rõ nhóm chức năng sắp triển khai: luồng chính, quy tắc và dữ liệu nghiệp vụ, lỗi quan trọng, tiêu chí chấp nhận và yêu cầu chất lượng cần thiết. AI không tự chốt quy tắc hoặc thêm chức năng ngoài kế hoạch.

Phần 4 đã chốt tại [Domain Design](01-product-lifecycle/04-domain-design.md) ở mức tối giản: khái niệm, quan hệ, vòng đời/quy tắc và trách nhiệm. Giữ một lượt kiểm tra domain; với CRUD đơn giản có thể gộp đầu ra vào Requirements, không bắt buộc tài liệu riêng. Chỉ làm rõ phần phục vụ chức năng sắp triển khai.

Phần 5 đã chốt tạm thời tại [UX/UI Design](01-product-lifecycle/05-ux-ui-design.md). Người dùng chủ trì thiết kế, cần hướng dẫn cụ thể để giao việc cho AI hoặc dùng công cụ như Google Stitch. Quy trình: brief và luồng → bố cục/hướng UI → duyệt màn hình đại diện → quy ước dùng chung → mở rộng màn hình/trạng thái → review và bàn giao. Giữ nhất quán màu, chữ, spacing, button, form, thông báo và dialog. Đầu ra là brief, quy ước và thiết kế đã duyệt; không tự thêm chức năng. Có thể điều chỉnh khi thực hành.

Phần 6 đã chốt tạm thời tại [Architecture](01-product-lifecycle/06-architecture.md). Khung gồm yêu cầu chi phối kiến trúc → thành phần và trách nhiệm → lựa chọn/đánh đổi → triển khai và vận hành. Đầu ra khi áp dụng là `ARCHITECTURE.md`; chưa cần chi tiết toàn bộ bảng, endpoint hoặc class. Người dùng sẽ bổ sung khi thực tế phát hiện thiếu sót. Câu hỏi chạy local hay Internet chưa được trả lời; để quyết định theo dự án, không tự gán lựa chọn.

Người dùng muốn AI chất vấn quyết định kiến trúc từng câu nhưng cần gợi ý, giải thích trước khi tự quyết định. Skill `grill-me` đã đọc chỉ dẫn gọi `Skill("grilling")`; phiên không có công cụ Skill và không tìm thấy skill grilling, nên đã thông báo giới hạn và trực tiếp hỗ trợ thảo luận theo yêu cầu.

## Các thông tin cần làm rõ lần lượt

- Các thông tin dưới đây sẽ được làm rõ khi cần cá nhân hóa hoặc áp dụng vào một dự án; không phải điều kiện chặn việc xây dựng khung workflow chung.
- Mục tiêu ưu tiên: học tập, portfolio, người dùng thật hay kinh doanh.
- Quỹ thời gian và ngân sách.
- Năng lực hoặc công nghệ muốn đào sâu.
- Mức độ AI được hỗ trợ và tự thực hiện.
- Tiêu chí hoàn thành phiên bản đầu tiên.

Danh sách này để theo dõi; không hỏi tất cả trong cùng một lượt.

## Bước tiếp theo

Thảo luận **phần 7 — Detailed Design: thiết kế dữ liệu, API và luồng xử lý cho nhóm chức năng sắp triển khai** khi người dùng tiếp tục. Phần này chưa được chốt.

Giữ mức trình bày ngắn gọn tương tự phần 1; chưa tự mở rộng thành quy trình chi tiết hoặc điền dữ liệu cho sản phẩm chưa tồn tại.

## Cách bàn giao sang phiên mới

Đọc các nguồn theo thứ tự trong `README.md`, tiếp tục từ bước tiếp theo ở trên. Sau khi người dùng trả lời, cập nhật thông tin đã biết và bước tiếp theo; phân biệt rõ thông tin được xác nhận với giả định hoặc đề xuất.
