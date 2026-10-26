# Phần 4. Domain Design — Mô hình nghiệp vụ tối giản

**Trạng thái:** đã chốt ở mức tối giản. Với ứng dụng CRUD đơn giản, có thể gộp đầu ra vào Requirements.

## Mục tiêu

Thống nhất hệ thống quản lý những gì, chúng liên quan thế nào và quy tắc thuộc về đâu. Đối chiếu các chức năng để tránh hiểu nghiệp vụ mâu thuẫn hoặc để AI tự suy đoán khi thiết kế.

## Đầu vào

- Product Planning: phạm vi MVP và nhóm chức năng sắp triển khai.
- Requirements: luồng sử dụng, dữ liệu nghiệp vụ, quy tắc và tiêu chí chấp nhận của nhóm chức năng đó.

## Việc cần làm và câu hỏi cần trả lời

1. **Khái niệm:** xác định các đối tượng nghiệp vụ và ý nghĩa của từng thuật ngữ. Hệ thống quản lý những gì? Có cách hiểu nào dễ gây nhầm lẫn?
2. **Quan hệ:** xác định đối tượng nào liên quan, phụ thuộc hoặc tồn tại độc lập. Khi sửa hay xóa một đối tượng, đối tượng khác bị ảnh hưởng thế nào?
3. **Vòng đời và quy tắc:** làm rõ trạng thái, điều kiện chuyển trạng thái và điều kiện luôn phải đúng. Đối chiếu Requirements, đưa điểm chưa rõ cho người dùng quyết định.
4. **Trách nhiệm:** xác định nhóm chức năng quản lý đối tượng và xử lý quy tắc nào, nếu cần phân nhóm. Đi qua luồng chính để kiểm tra trách nhiệm bị thiếu hoặc trùng.
5. **Kiểm tra mô hình:** AI đi qua một luồng chính và 1–2 tình huống dễ gây mâu thuẫn liên quan đến phạm vi đã chốt, chẳng hạn xóa đối tượng đang có dữ liệu phụ thuộc. Đối chiếu Requirements trước; chỉ hỏi người dùng về quy tắc còn thiếu hoặc mâu thuẫn. Không tự thêm chức năng để xử lý tình huống giả định. Quy tắc được chốt cập nhật tại nguồn yêu cầu; sơ đồ tham chiếu hoặc tóm tắt, tránh tạo nguồn quy tắc thứ hai.

Chỉ mô hình hóa phần phục vụ phạm vi đã chốt. Chưa cần thiết kế chi tiết bảng, class, API hoặc quyết định tách service.

**Ranh giới đã chốt sau phỏng vấn:** nhóm trách nhiệm ở đây là nhóm nghiệp vụ, không phải service kỹ thuật. Đầu ra gồm khái niệm, quan hệ, trạng thái/quy tắc và trách nhiệm nghiệp vụ; đây là đầu vào để Architecture quyết định cách tổ chức hệ thống và chia service. Hai nhóm nghiệp vụ khác nhau không tự động trở thành hai microservice.

## Ví dụ minh họa

Giả sử MVP có tạo dự án, tạo công việc trong dự án và cập nhật trạng thái công việc. Requirements quy định công việc thuộc một dự án, có ba trạng thái chưa làm / đang làm / hoàn thành, và cho phép xóa dự án.

Điểm cần làm rõ: xóa dự án thì xử lý các công việc bên trong thế nào? AI nêu câu hỏi, không tự chọn quy tắc.

Nếu người dùng chọn chỉ xóa dự án rỗng, mô hình ngắn gồm:

- Dự án nhóm các công việc và có thể chưa có công việc nào.
- Công việc thuộc đúng một dự án, có tên và trạng thái.
- Một dự án có nhiều công việc; không xóa dự án còn công việc.
- Phần quản lý dự án kiểm tra điều kiện xóa; phần quản lý công việc xử lý tạo và cập nhật trạng thái.

Quy tắc xóa cần được cập nhật lại vào Requirements cùng tiêu chí kiểm tra. Đây là ví dụ, không phải yêu cầu của một sản phẩm đã chọn.

## Đầu ra

Một mục “Mô hình nghiệp vụ” ngắn chứa khái niệm, quan hệ, trạng thái và quy tắc quan trọng, nhóm trách nhiệm nếu cần, cùng các điểm còn mở. Tham chiếu yêu cầu đã có thay vì sao chép toàn bộ.

**Dạng đầu ra đã chốt sau phỏng vấn:** sơ đồ nghiệp vụ đơn giản kèm ghi chú ngắn. Box biểu diễn khái niệm, đường nối có nhãn biểu diễn quan hệ; ghi chú giải thích thuật ngữ, trạng thái và quy tắc quan trọng. Ghi trách nhiệm nghiệp vụ khi cần. Sơ đồ mô tả hệ thống quản lý gì và quan hệ giữa chúng, không phải flow thứ tự công việc của Product Planning. Chỉ thể hiện phần phục vụ chức năng sắp triển khai, bổ sung dần.

- CRUD đơn giản, ít quan hệ: đặt sơ đồ và ghi chú trong `REQUIREMENTS.md`.
- Nhiều đối tượng, trạng thái hoặc quy tắc chéo: có thể tách tài liệu domain chứa sơ đồ và ghi chú, tham chiếu Requirements.

## Phân công người và AI

- AI đề xuất mô hình dựa trên yêu cầu, giải thích mỗi thành phần phục vụ yêu cầu nào và phát hiện mâu thuẫn.
- Người dùng kiểm tra ý nghĩa nghiệp vụ, quyết định quy tắc còn mở và chốt ranh giới quan trọng.
- Quy tắc được làm rõ phải phản ánh lại vào Requirements; chức năng mới phải quay về Product Planning để chốt phạm vi.

## Điều kiện hoàn thành và checklist

- [ ] Khái niệm chính được hiểu thống nhất.
- [ ] Quan hệ và quy tắc quan trọng của nhóm chức năng sắp làm đã rõ.
- [ ] Luồng chính có trách nhiệm xử lý rõ ràng.
- [ ] Đã kiểm tra mô hình bằng một luồng chính và 1–2 tình huống liên quan; quy tắc mới được chốt đã cập nhật vào nguồn yêu cầu.
- [ ] Không còn mâu thuẫn lớn với Requirements; điểm chưa rõ ảnh hưởng triển khai đã được giải quyết.

**Lỗi thường gặp:** thêm đối tượng phục vụ chức năng chưa có; mặc định mỗi đối tượng là một service; thiết kế dữ liệu quá chi tiết trước khi hiểu nghiệp vụ; giữ quy tắc khác nhau trong nhiều tài liệu.

**Mức độ cần thiết:** giữ một lượt kiểm tra domain; độ sâu tùy bài toán. Không bắt buộc bước hoặc tài liệu riêng cho CRUD đơn giản.

**Bước kế tiếp:** UX/UI Design — màn hình, luồng thao tác và trạng thái giao diện cho chức năng sắp triển khai.
