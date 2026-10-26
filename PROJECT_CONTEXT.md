# Ngữ cảnh và trạng thái dự án

## Nguồn thông tin

- [Khung playbook](ref/readme.md).
- [Ngữ cảnh cá nhân và nguyên tắc hướng dẫn](ref/rule.md).
- Yêu cầu khởi tạo kho làm việc để cùng xây dựng workflow cá nhân.

## Thông tin đã biết

- Mục đích cốt lõi được người dùng xác nhận: project này là workflow và checklist dùng chung cho chính người dùng và AI, chỉ rõ cách làm việc, thứ tự các bước trong từng mục lớn và điều kiện hoàn thành dự án.
- Kết quả mong muốn: hệ thống, cấu trúc code và tài liệu rõ ràng, dễ tra cứu; khi thay đổi/chỉnh sửa vẫn giữ nhất quán và biết phần nào bị ảnh hưởng. “Chuẩn chỉ, đẹp đẽ” gồm đúng yêu cầu, cấu trúc hợp lý, UI nhất quán và kiểm chứng được, không chỉ đầy đủ tài liệu.
- Playbook cần dùng được khi tạo mới lẫn chỉnh sửa dự án, không chỉ là tài liệu học lý thuyết. Giữ đủ đơn giản cho một người cùng AI thực hiện.

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
- Mỗi mục cần thể hiện đầu vào, thứ tự thực hiện, đầu ra, phân công người/AI và checklist có bằng chứng hoặc điều kiện hoàn thành; phân biệt bắt buộc, có điều kiện và có thể hoãn.
- Khi sửa dự án, kiểm tra tác động lên yêu cầu, thiết kế, contract, code, test và tài liệu; cập nhật nguồn chính có liên quan, tránh sao chép nội dung rồi để lệch nhau. Ghi trạng thái và bước tiếp theo sau thay đổi.

## Trạng thái hiện tại

**Giai đoạn:** đã chốt [workflow tổng thể](01-product-lifecycle/00-overall-workflow.md) gồm vòng định hướng và vòng triển khai lặp, ba mức xử lý thay đổi, phân quyền người/AI và một nguồn trạng thái chung. Đã chốt phần 1 đến phần 4; chốt tạm thời phần 5, đã chốt lại phần 6 sau phỏng vấn; đã lưu phần 7 giản lược. Đã tạo hướng dẫn và checklist phần 8 — triển khai chức năng với AI theo yêu cầu. Khung Project Setup đã chốt, breakdown chi tiết vẫn để lại sau. Người dùng đã yêu cầu tạm hoãn phần 9 — Release và phần 10 — Operations; phạm vi hiện tại dừng ở phần 8.

Người dùng đã chấp nhận trình tự Discovery sau phỏng vấn, đầu ra và điều kiện mở lại; giữ mức tối giản. Nội dung được lưu tại [phần 1 — Discovery](01-product-lifecycle/01-discovery.md). Đây là việc chốt hướng dẫn dùng lại, không phải hoàn thành Discovery cho một sản phẩm cụ thể.

Phần 2 đã chốt lại sau phỏng vấn tại [Product Planning](01-product-lifecycle/02-product-planning.md). Đầu ra chính là flow các box theo giai đoạn; mỗi box là chức năng hoặc công việc có kết quả rõ, mũi tên thể hiện thứ tự đề xuất. Danh sách chung gồm chức năng, nền tảng, thử nghiệm và sửa lỗi khi có. Làm sau MVP/chưa quyết định/không làm tách khỏi luồng hiện tại. Không chia task kỹ thuật hoặc quản lý trạng thái sẵn sàng/bị chặn ở bước này (người dùng đã bác bỏ vì quá chi tiết). Khi chuẩn bị thực hiện mới làm rõ yêu cầu, thiết kế và chia task. AI đề xuất vị trí box mới cùng tác động tới MVP/thứ tự, người dùng duyệt trước khi cập nhật flow. Đã lưu ví dụ Mermaid quản lý công việc chỉ để minh họa, không phải dự án được chọn. Chưa chốt quy tắc thời hạn/deadline mặc định.

Phần 3 được người dùng chấp nhận và lưu tại [Requirements](01-product-lifecycle/03-requirements.md). Chỉ làm rõ nhóm chức năng sắp triển khai: luồng chính, quy tắc và dữ liệu nghiệp vụ, lỗi quan trọng, tiêu chí chấp nhận và yêu cầu chất lượng cần thiết. AI không tự chốt quy tắc hoặc thêm chức năng ngoài kế hoạch.

Phần 4 đã chốt tại [Domain Design](01-product-lifecycle/04-domain-design.md) ở mức tối giản: khái niệm, quan hệ, vòng đời/quy tắc và trách nhiệm. Giữ một lượt kiểm tra domain; với CRUD đơn giản có thể gộp đầu ra vào Requirements, không bắt buộc tài liệu riêng. Chỉ làm rõ phần phục vụ chức năng sắp triển khai.

Phần 5 đã chốt tạm thời tại [UX/UI Design](01-product-lifecycle/05-ux-ui-design.md). Người dùng chủ trì thiết kế, cần hướng dẫn cụ thể để giao việc cho AI hoặc dùng công cụ như Google Stitch. Quy trình: brief và luồng → bố cục/hướng UI → duyệt màn hình đại diện → quy ước dùng chung → mở rộng màn hình/trạng thái → review và bàn giao. Giữ nhất quán màu, chữ, spacing, button, form, thông báo và dialog. Đầu ra là brief, quy ước và thiết kế đã duyệt; không tự thêm chức năng. Có thể điều chỉnh khi thực hành.

Phần 6 đã chốt sau phỏng vấn tại [Architecture](01-product-lifecycle/06-architecture.md): yêu cầu/ràng buộc → sơ đồ hệ thống → phương án công nghệ ưu tiên → rà luồng chính và thất bại quan trọng → người dùng review/chốt. Sơ đồ thể hiện trách nhiệm, quyền sở hữu dữ liệu, cách giao tiếp và MVP/để sau. Công nghệ chia cần cho MVP/thêm để học/chưa cần, tối đa hai phương án thay thế khi đáng so sánh. Playbook không mặc định microservices, nhưng AI tôn trọng lựa chọn microservices đã chốt cho từng dự án, vẫn phản biện độ phức tạp. Chỉ mở lại khi đổi cấu trúc, trách nhiệm, dữ liệu, giao tiếp hoặc quyết định nền tảng; AI nêu tác động để người dùng duyệt. Chi tiết endpoint/bảng/config để bước sau. Chưa có stack hay môi trường triển khai cụ thể được chọn.

Người dùng muốn AI chất vấn quyết định kiến trúc từng câu nhưng cần gợi ý, giải thích trước khi tự quyết định. Skill `grill-me` đã đọc chỉ dẫn gọi `Skill("grilling")`; phiên không có công cụ Skill và không tìm thấy skill grilling, nên đã thông báo giới hạn và trực tiếp hỗ trợ thảo luận theo yêu cầu.

Người dùng muốn tự xây base cho hướng microservices, độc lập với ứng dụng, ngôn ngữ và thư viện ở mức playbook. Không yêu cầu khởi tạo service thực tế. Monorepo/multi-repo, stack, thư viện và cấu trúc thư mục cụ thể chưa được chốt; không ép lựa chọn các chi tiết này. Contract là artifact bắt buộc tại điểm giao tiếp phù hợp, cần cơ chế kiểm chứng implementation; service khác ngôn ngữ có thể khác code/build nhưng phải tuân thủ contract chung.

Project Setup đã được xác nhận là bước đầu trong `01. PRODUCT LIFECYCLE → Implementation & Testing`, không thuộc Architecture và không thay thế phần 7 — Detailed Design. Bộ quy tắc dựng service dùng lại thuộc `03. STANDARDS & POLICIES`; checklist có thể đặt trong `04. TEMPLATES & CHECKLISTS`, tránh sao chép nội dung.

Đã lưu [Project Setup](01-product-lifecycle/08-implementation-testing/01-project-setup.md) với tám nhóm: (1) phạm vi; (2) quy ước chung; (3) repository/cấu trúc; (4) contract; (5) service mẫu; (6) frontend nếu có; (7) cách chạy và kiểm tra lặp lại; (8) nghiệm thu và bàn giao. Người dùng đồng ý dựng một service đại diện và một luồng kiểm chứng, hoàn thiện chuẩn rồi mới nhân rộng. Khung đã chốt, chi tiết từng nhóm còn cần thảo luận.

Người dùng rất quan tâm chi tiết Project Setup và muốn AI chủ động tổng hợp đầy đủ, không trả lời chung chung hoặc buộc họ nhắc từng yêu cầu nền tảng. Mỗi nhóm cần đầu vào, quyết định, việc thực hiện, artifact và tiêu chí nghiệm thu; phân biệt bắt buộc và có điều kiện, chuẩn hệ thống / loại service / quy ước theo stack.

## Các thông tin cần làm rõ lần lượt

- Các thông tin dưới đây sẽ được làm rõ khi cần cá nhân hóa hoặc áp dụng vào một dự án; không phải điều kiện chặn việc xây dựng khung workflow chung.
- Mục tiêu ưu tiên: học tập, portfolio, người dùng thật hay kinh doanh.
- Quỹ thời gian và ngân sách.
- Năng lực hoặc công nghệ muốn đào sâu.
- Mức độ AI được hỗ trợ và tự thực hiện.
- Tiêu chí hoàn thành phiên bản đầu tiên.

Danh sách này để theo dõi; không hỏi tất cả trong cùng một lượt.

## Bước tiếp theo

Phỏng vấn Architecture đã kết thúc và được người dùng xác nhận cập nhật tài liệu cùng ngữ cảnh. Đã thực hiện; chưa có mục tiếp theo được chọn.

Phỏng vấn phần 4 — Domain Design bằng `grill-with-docs` đã có ba điểm đồng ý và được ghi vào phần 4: (1) chỉ xác định khái niệm, quan hệ, trạng thái/quy tắc và trách nhiệm nghiệp vụ; Architecture quyết định chia service; (2) đầu ra là sơ đồ nghiệp vụ đơn giản với box khái niệm, đường nối có nhãn quan hệ và ghi chú ngắn, bổ sung dần theo chức năng; CRUD đơn giản đặt trong Requirements; (3) AI kiểm tra một luồng chính và 1–2 tình huống dễ gây mâu thuẫn, đối chiếu Requirements trước, chỉ hỏi quy tắc thiếu/mâu thuẫn và không tự thêm chức năng. Quy tắc mới được chốt cập nhật tại nguồn yêu cầu. Sơ đồ domain khác flow công việc của Product Planning. Người dùng chuyển sang phỏng vấn Architecture trước khi trả lời xác nhận tổng kết phần 4; giữ các điểm đã đồng ý, không tự coi phần tổng kết đã được xác nhận.

Đã lập [danh mục skill](05-ai-workflows/skill-catalog.md) ngày 2026-10-19 từ bộ nguồn có sẵn trong `skills/skills/` (checkout Git riêng `skills/`, remote mattpocock/skills). Có `productivity/grilling/SKILL.md`; nhận định trước đây không tìm thấy grilling đã được thay thế bởi phát hiện này. Đọc skill đích tại đường dẫn đó khi cần; không giả vờ có công cụ Skill. Chưa cài đặt hoặc chạy setup engineering, cấu hình tracker, xuất issue/PR hay thực thi skill triển khai. Danh mục là nguồn chính cho cách chọn và dùng skill, có liên kết từ README và AGENTS.md.

Phỏng vấn Discovery đã kết thúc và được người dùng xác nhận cập nhật. Đã chốt: ý tưởng ngắn → AI tóm tắt và làm rõ từng điểm thiếu bằng 2–3 đề xuất, mỗi lượt một câu → chốt hướng với kết quả mong muốn cụ thể → Product Brief tách đã chốt/giả định/còn mở → người dùng review trước Product Planning. Mô tả rõ là đủ, chưa bắt buộc bằng chứng hoặc KPI; giả định giữ để kiểm chứng sau. Mở lại khi đổi người dùng, vấn đề, giá trị, mục tiêu ưu tiên hoặc ràng buộc lớn; chỉ rà phần bị ảnh hưởng.

Workflow tổng thể đã được người dùng xác nhận và lưu tại [workflow tổng thể](01-product-lifecycle/00-overall-workflow.md): vòng định hướng tạo nền tảng vừa đủ; vòng triển khai lặp theo từng luồng nhỏ; thay đổi được xử lý theo ba mức nhỏ, vừa và lớn; AI tự làm việc nhỏ trong phạm vi đã chốt rồi cung cấp bằng chứng để người dùng review; `PROJECT_CONTEXT.md` là nguồn trạng thái chung.

Đã lưu [Detailed Design tối giản](01-product-lifecycle/07-detailed-design.md) theo yêu cầu mới: một ghi chú theo chức năng gồm phạm vi, contract, dữ liệu, xử lý và kiểm chứng. Tài liệu implement API có thể chính là Detailed Design với chức năng nhỏ; không tạo hai bộ trùng nhau. Chỉ bổ sung tương tác nhiều service, thất bại một phần, xử lý lặp hoặc đồng thời khi liên quan.

Đã tạo [hướng dẫn Implementation & Testing](01-product-lifecycle/08-implementation-testing/02-feature-implementation.md): chọn nhiệm vụ → giao ngữ cảnh → triển khai → kiểm chứng/sửa lỗi → người dùng review → lưu kết quả/bàn giao. Có checklist trước khi code và hoàn thành, prompt giao việc và mẫu trạng thái phiên. Giữ đơn giản cho một người, kiểm chứng theo rủi ro, không bắt buộc mọi loại test hay nhiều file tài liệu. Đây là hướng dẫn được tạo theo yêu cầu, chưa có nghiệm thu chức năng thực tế nào.

Workflow tổng thể đã được chốt và đồng bộ với README. Chưa có mục tiếp theo được người dùng chọn. Không tự chuyển sang phần 9 — Release hoặc phần 10 — Operations vì cả hai đang tạm hoãn. Không tự quay lại breakdown Project Setup. Khi được yêu cầu quay lại setup, bắt đầu từ nhóm 1 — phạm vi; mục đó vẫn cần chi tiết theo yêu cầu đã lưu. Các nội dung được bổ sung sau phải phục vụ workflow/checklist dùng chung cho người và AI, ưu tiên tính rõ ràng và khả năng duy trì khi thay đổi.

## Cách bàn giao sang phiên mới

Đọc các nguồn theo thứ tự trong `README.md`, tiếp tục từ bước tiếp theo ở trên. Sau khi người dùng trả lời, cập nhật thông tin đã biết và bước tiếp theo; phân biệt rõ thông tin được xác nhận với giả định hoặc đề xuất.
