# Phần 1. Discovery — Xác định vấn đề, người dùng và mục tiêu

**Trạng thái:** đã chốt trình tự, đầu ra và điều kiện mở lại sau phỏng vấn; giữ tối giản cho một người cùng AI.

## Mục tiêu

Làm rõ dự án phục vụ ai, giải quyết vấn đề gì và kết quả nào cho thấy dự án có giá trị. Tách mục tiêu sản phẩm khỏi mục tiêu học tập để lựa chọn phạm vi phù hợp với nguồn lực cá nhân.

## Các câu hỏi cần trả lời

1. **Người dùng:** Ai sẽ sử dụng ứng dụng? Trong tình huống nào?
2. **Vấn đề:** Họ đang gặp khó khăn gì? Hiện họ giải quyết bằng cách nào?
3. **Giá trị:** Sau khi có ứng dụng, việc gì sẽ dễ hơn, nhanh hơn hoặc ít sai sót hơn?
4. **Mục tiêu:** Sản phẩm cần đạt điều gì? Bạn muốn học hoặc rèn năng lực nào? Khi hai mục tiêu xung đột, ưu tiên nào quan trọng hơn?
5. **Ràng buộc và giả định:** Bạn có bao nhiêu thời gian, ngân sách? Điều gì đã biết và điều gì mới chỉ là phỏng đoán cần kiểm chứng?

## Trình tự thực hiện

1. **Mô tả ý tưởng:** người dùng cung cấp vài câu về ý tưởng hoặc vấn đề ban đầu.
2. **Làm rõ:** AI tóm tắt điều đã hiểu, xác định thông tin thiếu trong năm nhóm câu hỏi. Với mỗi điểm thiếu quan trọng, đề xuất 2–3 phương án cùng lý do; mỗi lượt hỏi một câu để người dùng chọn hoặc sửa. Không tự tạo toàn bộ sản phẩm rồi coi đó là yêu cầu.
3. **Chốt hướng:** xác định người dùng, vấn đề, kết quả mong muốn, mục tiêu ưu tiên và ràng buộc. Kết quả phải cụ thể, nhận biết được; chưa cần KPI, danh sách chức năng hoặc tiêu chí kiểm thử chi tiết.
4. **Tổng hợp:** AI viết Product Brief khoảng một trang, phân biệt **đã chốt / giả định / còn mở**. Việc đồng ý dùng một giả định làm hướng đi không biến nó thành sự thật đã kiểm chứng.
5. **Review và chuyển bước:** người dùng kiểm tra, chỉnh sửa và chấp nhận brief trước khi chuyển sang Product Planning. Giữ lại giả định và điểm còn mở để kiểm chứng hoặc làm rõ sau.

Ví dụ kết quả mong muốn: “Khi bắt đầu ngày làm việc, tôi biết những việc cần ưu tiên mà không phải tổng hợp từ nhiều chỗ.” Với mục tiêu học: “Tôi tự giải thích và kiểm chứng được cách hai service phối hợp khi một bên thất bại.” Tránh chỉ ghi “ứng dụng tiện lợi”.

## Đầu vào, đầu ra và điều kiện hoàn thành

- **Đầu vào:** ý tưởng hoặc vấn đề ban đầu; với dự án học tập có thể dùng tình huống giả định và ghi rõ.
- **Người và AI:** bạn cung cấp bối cảnh, quyết định mục tiêu và kiểm tra nội dung; AI đặt câu hỏi, phát hiện điểm thiếu, phản biện và tổng hợp.
- **Đầu ra:** Product Brief ngắn chứa người dùng, vấn đề, cách giải quyết hiện tại, kết quả mong muốn cụ thể, mục tiêu sản phẩm và học tập, ràng buộc; phân biệt đã chốt, giả định và còn mở.
- **Điều kiện hoàn thành:** giải thích được làm cho ai, giải quyết vấn đề gì, kết quả mong muốn là gì và biết giả định quan trọng nào cần kiểm chứng; người dùng đã review và chấp nhận brief.
- **Ngưỡng bằng chứng đã chốt:** mô tả rõ là đủ để chuyển sang Product Planning; chưa bắt buộc nghiên cứu hoặc bằng chứng thực tế ở Discovery. Đánh dấu giả định và giữ lại để kiểm chứng sau, không coi Product Brief là bằng chứng nhu cầu đã được xác nhận.
- **Mức độ cần thiết:** bắt buộc ở mức ngắn gọn; độ sâu tùy dự án.

## Checklist và lỗi thường gặp

- [ ] Người dùng và vấn đề đủ rõ để giải thích ngắn gọn.
- [ ] Mục tiêu sản phẩm và mục tiêu học tập được phân biệt.
- [ ] Có kết quả mong muốn cụ thể, nhận biết được.
- [ ] Ràng buộc được ghi nhận; đã chốt, giả định và còn mở được phân biệt.
- [ ] Người dùng đã review và chấp nhận Product Brief.
- [ ] Tránh chọn công nghệ hoặc kiến trúc trước rồi mới tìm bài toán; chỉ ghi nhận công nghệ nếu là ràng buộc hoặc mục tiêu học tập.

Chưa cần liệt kê đầy đủ tính năng hoặc thiết kế kiến trúc ở bước này.

## Khi nào mở lại Discovery

Rà lại khi thay đổi người dùng mục tiêu, vấn đề chính, giá trị, mục tiêu ưu tiên hoặc ràng buộc lớn khiến hướng hiện tại không còn phù hợp. Chỉ rà phần bị ảnh hưởng và các quyết định liên quan, không phỏng vấn lại từ đầu.

Ví dụ: chuyển từ ứng dụng tự quản lý công việc sang quản lý đội nhóm cần rà Discovery; thêm bộ lọc danh sách thường chỉ cần cập nhật Product Planning và Requirements. Cập nhật brief và trạng thái khi hướng mới được chốt.

**Bước kế tiếp:** Product Planning — chọn phạm vi phiên bản đầu tiên và tiêu chí thành công.
