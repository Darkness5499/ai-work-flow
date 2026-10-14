# Phần 3. Requirements — Hành vi và tiêu chí chấp nhận

**Trạng thái:** đã chốt ở mức tổng quan.

## Mục tiêu

Thống nhất chức năng phải hoạt động thế nào và khi nào được coi là đúng, làm căn cứ cho thiết kế, triển khai và kiểm thử. Chỉ làm rõ nhóm chức năng sắp triển khai; các phần làm sau giữ mô tả ngắn trong kế hoạch.

## Đầu vào

Danh sách chức năng, phạm vi MVP và thứ tự thực hiện đã chốt trong Product Planning.

## Việc cần làm và câu hỏi cần trả lời

1. **Mô tả hành vi và luồng sử dụng:** ai sử dụng, điều kiện bắt đầu, thao tác hoặc dữ liệu đầu vào, phản hồi của hệ thống và kết quả cuối cùng là gì?
2. **Làm rõ quy tắc và dữ liệu:** thông tin nào bắt buộc, thế nào là hợp lệ, có quy tắc về trạng thái, quyền truy cập hoặc trùng lặp không? Khi nào được sửa, xóa hoặc thực hiện lại? Mô tả ở mức nghiệp vụ, chưa thiết kế bảng và API.
3. **Chọn trường hợp ngoài luồng chính:** dữ liệu sai hoặc thiếu, danh sách rỗng, dữ liệu không tồn tại, thao tác không được phép, lưu thất bại hoặc gửi nhiều lần. Chỉ chọn tình huống thực sự ảnh hưởng đến chức năng.
4. **Viết tiêu chí chấp nhận:** thể hiện điều kiện hoặc thao tác và kết quả mong đợi có thể kiểm tra. Làm rõ quy tắc cần thiết thay vì để AI tự coi giả định là yêu cầu.
5. **Ghi yêu cầu chất lượng cần thiết:** chọn yêu cầu phù hợp MVP tự dùng, ví dụ lưu dữ liệu bền vững, bảo vệ thông tin nhạy cảm hoặc hỗ trợ thiết bị sử dụng. Diễn đạt cụ thể, kiểm chứng được, tránh chỉ ghi “nhanh” hoặc “bảo mật tốt”.

Ví dụ minh họa tiêu chí cho chức năng tạo công việc, không phải yêu cầu của một dự án đã chọn:

- Nhập tiêu đề hợp lệ và lưu: công việc xuất hiện trong danh sách.
- Tiêu đề trống: hiển thị lỗi, không tạo công việc.
- Tải lại trang sau khi tạo thành công: công việc vẫn tồn tại.

Giới hạn độ dài, trạng thái mặc định hoặc cách xử lý trùng phải được làm rõ nếu cần.

## Đầu ra

Khi áp dụng, dùng một file `REQUIREMENTS.md`, chia theo mã chức năng trong kế hoạch. Mỗi chức năng gồm:

- Mục đích và phạm vi.
- Luồng chính.
- Quy tắc nghiệp vụ và dữ liệu.
- Trường hợp lỗi quan trọng.
- Tiêu chí chấp nhận.
- Điểm chưa rõ cần quyết định.

Yêu cầu chất lượng dùng chung ghi một lần trong tài liệu và tham chiếu khi cần. Không tạo dữ liệu yêu cầu giả cho sản phẩm chưa tồn tại.

## Phân công người và AI

- Người dùng quyết định hành vi mong muốn, quy tắc nghiệp vụ và review yêu cầu.
- AI đặt câu hỏi, tìm thiếu sót hoặc mâu thuẫn, tổng hợp thành yêu cầu có thể kiểm tra.
- AI không tự quyết định quy tắc chưa rõ hoặc thêm chức năng để bao phủ mọi tình huống tưởng tượng.
- Nếu phát sinh chức năng mới, đưa về Product Planning để cân nhắc và chốt phạm vi trước khi triển khai.

## Điều kiện hoàn thành và checklist

- [ ] Nhóm chức năng sắp làm có luồng chính, quy tắc và trường hợp lỗi quan trọng.
- [ ] Tiêu chí chấp nhận có thể dùng để kiểm tra kết quả.
- [ ] Yêu cầu chất lượng cần thiết được diễn đạt cụ thể.
- [ ] Không còn điểm mơ hồ có thể làm thay đổi đáng kể hành vi hoặc phạm vi của nhóm chức năng sắp triển khai.
- [ ] Yêu cầu phù hợp phạm vi đã chốt và được người dùng kiểm tra.

**Lỗi thường gặp:** đặc tả toàn bộ chức năng tương lai quá sớm; viết tiêu chí không kiểm chứng được; để AI biến giả định thành quy tắc; thêm chức năng ngoài kế hoạch trong lúc làm rõ yêu cầu.

**Mức độ cần thiết:** bắt buộc cho nhóm chức năng sắp triển khai; bổ sung dần khi chuyển sang nhóm tiếp theo.

**Bước kế tiếp:** Domain Design — làm rõ các khái niệm nghiệp vụ, quan hệ và trách nhiệm của từng nhóm chức năng.
