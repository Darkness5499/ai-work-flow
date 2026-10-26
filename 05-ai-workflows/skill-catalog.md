# Danh mục và cách sử dụng skill

## Nguồn và trạng thái

Đã kiểm tra ngày 2026-10-19. Bộ nguồn nằm tại `skills/skills/`, bên trong checkout Git riêng `skills/`, có remote `https://github.com/mattpocock/skills.git`. Giữ nguyên bộ nguồn; tài liệu này là điểm tra cứu, không sao chép hoặc thay thế hướng dẫn trong từng `SKILL.md`.

Có file trên đĩa không đồng nghĩa skill đã được đăng ký thành slash command hoặc có đủ công cụ để thực thi. Phiên mới phải kiểm tra khả năng hiện có. Không tự cài đặt, cập nhật bộ nguồn hoặc chạy toàn bộ chuỗi skill chỉ vì có danh mục này.

## Skill theo công việc

- **Phỏng vấn Discovery và các quyết định:** [grill-me](../skills/skills/productivity/grill-me/SKILL.md) chuyển tới [grilling](../skills/skills/productivity/grilling/SKILL.md). Đọc cả hai khi được yêu cầu. `grilling` hiện có trong repository; thông tin cũ “không tìm thấy” không còn đúng với bộ nguồn hiện tại.
- **Làm rõ thuật ngữ và domain:** [grill-with-docs](../skills/skills/engineering/grill-with-docs/SKILL.md), [domain-modeling](../skills/skills/engineering/domain-modeling/SKILL.md).
- **Tổng hợp đặc tả:** [to-spec](../skills/skills/engineering/to-spec/SKILL.md).
- **Chia công việc theo luồng hoàn chỉnh và phụ thuộc:** [to-tickets](../skills/skills/engineering/to-tickets/SKILL.md).
- **Kiểm chứng phương án thiết kế:** [prototype](../skills/skills/engineering/prototype/SKILL.md), [codebase-design](../skills/skills/engineering/codebase-design/SKILL.md), [research](../skills/skills/engineering/research/SKILL.md).
- **Triển khai:** [implement](../skills/skills/engineering/implement/SKILL.md); [implement-spec](../skills/skills/engineering/implement-spec/SKILL.md) dành cho luồng triển khai cả spec bằng nhiều agent, không phải mặc định của playbook.
- **Kiểm thử, tìm lỗi và review:** [tdd](../skills/skills/engineering/tdd/SKILL.md), [diagnosing-bugs](../skills/skills/engineering/diagnosing-bugs/SKILL.md), [code-review](../skills/skills/engineering/code-review/SKILL.md).
- **Bàn giao và cải tiến:** [handoff](../skills/skills/productivity/handoff/SKILL.md), [retro](../skills/skills/engineering/retro/SKILL.md).
- **Viết tài liệu cho AI:** [writing-for-agents](../skills/skills/productivity/writing-for-agents/SKILL.md).

Tra cứu đầy đủ theo nhóm: [Productivity](../skills/skills/productivity/README.md), [Engineering](../skills/skills/engineering/README.md), [Misc](../skills/skills/misc/README.md), [In progress](../skills/skills/in-progress/README.md). Không mặc định áp dụng skill thử nghiệm hoặc deprecated.

## Cách dùng trong playbook

1. Xác định nhiệm vụ, giai đoạn hiện tại và phạm vi người dùng đã giao.
2. Chọn skill phù hợp; tôn trọng skill chỉ được gọi khi người dùng yêu cầu. Ví dụ: “Dùng grill-me phỏng vấn phần Discovery” hoặc “Dùng to-tickets chia spec đã chốt”.
3. Đọc file `SKILL.md`, các tài liệu được tham chiếu cần thiết và kiểm tra dependency trước khi thực hiện. Ưu tiên đường dẫn rõ ràng để tránh nhầm skill cùng tên ở thư mục cá nhân.
4. Nếu không có công cụ `Skill`, nói rõ và đọc hướng dẫn skill đích tại chỗ khi phù hợp; không tuyên bố đã gọi công cụ không tồn tại. Các công cụ khác mà skill cần cũng phải được kiểm tra.
5. Giữ quyền quyết định của người dùng và phạm vi playbook: mỗi lượt phỏng vấn một câu theo quy ước đã chốt, dù `grilling` gốc đề xuất hỏi nhiều câu trong một vòng. Không tự mở rộng chức năng hoặc biến giả định thành quyết định.
6. Lưu kết quả vào tài liệu chính của bước đang làm, cập nhật trạng thái và câu hỏi còn mở. Không tạo thêm bản spec/checklist trùng nguồn hiện có.

## Điều kiện trước khi dùng luồng engineering

[setup-matt-pocock-skills](../skills/skills/engineering/setup-matt-pocock-skills/SKILL.md) mô tả cấu hình issue tracker, nhãn triage và vị trí glossary/ADR. Việc cấu hình này chưa được thực hiện trong tác vụ lập danh mục.

`to-spec` và `to-tickets` có hành vi xuất lên tracker; `implement` có commit; `implement-spec` có branch, PR và nhiều agent. Chỉ thực hiện khi skill được áp dụng trong phạm vi được giao và các điều kiện cần thiết đã rõ. Danh mục này không phải yêu cầu tạo issue, PR, commit, chạy agent hoặc dựng ứng dụng.

Khi áp dụng, ưu tiên yêu cầu cụ thể của người dùng hơn các mặc định trong skill; giữ tài liệu vừa đủ cho một người. Release, Operations và breakdown Project Setup vẫn đang hoãn.

## Duy trì danh mục

Cập nhật khi nguồn, đường dẫn hoặc cách dùng thay đổi. `skills/` là repository lồng nhau, chưa được danh mục này biến thành submodule hoặc bản sao vendored: khi chuyển máy/clone playbook, kiểm tra bộ nguồn có hiện diện trước khi theo liên kết. Không tự thay đổi cách lưu trữ Git của bộ nguồn.
