# Phần 5. UX/UI Design — Luồng sử dụng và giao diện nhất quán

**Trạng thái:** chốt tạm thời. Điều chỉnh khi áp dụng vào dự án thực tế.

## Mục tiêu và phạm vi

Người dùng chủ trì thiết kế, AI và công cụ hỗ trợ tạo phương án, chỉnh sửa và rà soát. Thiết kế cần làm rõ cách hoàn thành luồng chính, nội dung từng màn hình và phản hồi sau thao tác, đồng thời nhất quán về hình thức lẫn hành vi.

Chỉ thiết kế nhóm chức năng sắp triển khai. MVP tự dùng ưu tiên dễ dùng, đủ trạng thái và nhất quán; chưa cần bộ design system lớn.

## Đầu vào

- Product Planning: phạm vi MVP, chức năng và thứ tự triển khai.
- Requirements: luồng, quy tắc, dữ liệu và tiêu chí chấp nhận.
- Domain Design: thuật ngữ, quan hệ và trạng thái nghiệp vụ.
- Thiết bị mục tiêu và hình tham khảo nếu có; chỉ rõ điểm muốn học theo.

## Quy trình thực hiện

1. **Chuẩn bị brief và luồng:** chọn một luồng ưu tiên, ghi người dùng muốn hoàn thành việc gì, bắt đầu ở đâu, thao tác và kết quả từng bước. Liệt kê màn hình cần thiết, chức năng được phép có và phần ngoài phạm vi.
2. **Phác bố cục và chọn hướng UI:** dùng wireframe hoặc yêu cầu AI tạo bản nháp. Xác định vị trí điều hướng, nội dung, form và hành động chính. Nếu chưa rõ phong cách, yêu cầu tối đa hai phương án để lựa chọn.
3. **Tạo và duyệt một màn hình đại diện:** chọn màn hình có các thành phần thường dùng, dùng nội dung gần thực tế. Chỉnh bố cục và thao tác, rồi thống nhất màu, chữ, khoảng cách và component.
4. **Ghi bộ quy ước dùng chung:** rút từ màn hình đã duyệt; ghi cả hình thức, trạng thái và cách tương tác. Dùng tên nhất quán cho giá trị dùng lại (design tokens), không tự xây nhiều component chưa cần.
5. **Mở rộng các màn hình và trạng thái:** yêu cầu AI dùng cùng quy ước, component và màn hình tham chiếu. Bổ sung dữ liệu rỗng, loading, lỗi, thành công, disabled khi phù hợp; nối luồng hoặc ghi rõ phản hồi của mỗi thao tác.
6. **Review và bàn giao:** đi qua nhiệm vụ từ đầu đến cuối, kiểm tra dữ liệu dài, lỗi và thiết bị mục tiêu. Lưu bản được duyệt, quy ước và liên kết tới mã chức năng trong Requirements làm căn cứ triển khai.

Nếu đã có màn hình trong Stitch, bắt đầu bằng review màn hình đó và chốt bộ quy ước, không cần tạo lại từ đầu. Mỗi lượt chỉnh sửa tập trung một màn hình hoặc một vài thay đổi cụ thể.

## Bộ quy ước UI tối thiểu

- **Màu:** hành động chính, nền, chữ, đường viền, thành công, cảnh báo và lỗi.
- **Typography và spacing:** font, cấp tiêu đề/nội dung/chú thích, thang khoảng cách, kích thước và bo góc dùng chung.
- **Layout:** khung trang, điều hướng, chiều rộng nội dung và cách co giãn theo thiết bị mục tiêu.
- **Component:** các button, input, select, danh sách/bảng, thông báo và dialog cần cho phạm vi hiện tại; thống nhất trạng thái normal, hover, focus, disabled, loading và lỗi khi phù hợp.
- **Form:** nhãn rõ, lỗi gần trường liên quan, không mất nội dung khi lưu thất bại.
- **Thông báo:** phân biệt lỗi tại trường, thông báo chung và thông báo ngắn không chặn thao tác; lỗi cần xử lý không biến mất quá nhanh.
- **Dialog:** quy định khi nào dùng, cách đóng/hủy và xử lý dữ liệu chưa lưu; không yêu cầu xác nhận cho mọi thao tác.
- **Khả năng sử dụng:** có focus, thao tác bàn phím và không dùng màu làm dấu hiệu duy nhất.

## Công cụ hỗ trợ

- **Google Stitch:** dùng để tạo và chỉnh UI bằng mô tả hoặc hình tham khảo. Đưa brief vào project, duyệt một màn hình, sau đó yêu cầu tái sử dụng chuẩn cho các màn hình tiếp theo.
- **Figma:** dùng khi cần trực tiếp chỉnh bố cục, component và prototype. Các kỹ năng bắt đầu gồm Frame, Auto Layout, Component/Variant và nối tương tác.
- **Penpot:** lựa chọn thay thế cho thiết kế, component và prototype.
- **Giấy bút:** đủ để phác luồng và wireframe ban đầu.
- **Thư viện UI như Angular Material:** tham khảo khi chọn hướng triển khai để thiết kế phù hợp với component có sẵn; không thay thế việc thiết kế luồng.

Không bắt buộc dùng nhiều công cụ. Bắt đầu với Stitch nếu muốn AI tạo bản nháp; chỉ dùng thêm công cụ khác khi cần chỉnh sửa. Khả năng xuất hoặc tích hợp cần kiểm tra tại thời điểm sử dụng; code sinh ra vẫn phải review và kiểm chứng trước khi tích hợp.

Nguồn tham khảo đã dùng khi thảo luận:

- [Google giới thiệu Stitch](https://developers.googleblog.com/en/stitch-a-new-way-to-design-uis/).
- [Hướng dẫn prompt Stitch](https://discuss.ai.google.dev/t/stitch-prompt-guide/83844).
- [Figma Auto Layout](https://help.figma.com/hc/en-us/articles/360040451373-Guide-to-auto-layout-in-Figma).
- [Penpot User Guide](https://help.penpot.app/user-guide/).
- [Angular Material theming](https://material.angular.dev/guide/theming).

## Prompt khởi đầu

```text
Thiết kế UI cho [ứng dụng], phục vụ [người dùng].
Mục tiêu luồng: [việc cần hoàn thành].
Thiết bị mục tiêu: [...].

Phạm vi đã chốt: [mã chức năng, danh sách màn hình].
Ngoài phạm vi: [...].

Trước tiên chỉ thiết kế màn hình [tên]:
- Nội dung cần hiển thị: [...].
- Hành động chính/phụ: [...].
- Quy tắc và phản hồi: [...].
- Trạng thái cần thể hiện: [...].

Quy ước UI: [màu, font, spacing, layout, component, thông báo/dialog].
Tham khảo: [hình hoặc bản thiết kế, nêu rõ điểm muốn học theo].
Nếu chưa có quy ước, đề xuất hai hướng để tôi chọn trước khi mở rộng.

Nếu thiếu thông tin ảnh hưởng đến hành vi, hỏi trước.
Không tự thêm chức năng; ghi đề xuất bổ sung riêng.
Sau khi tôi duyệt, dùng màn hình và quy ước này làm chuẩn cho màn hình tiếp theo.
```

## Đầu ra và phân công

Khi áp dụng, giữ brief, bộ quy ước dùng chung và các màn hình/luồng đã duyệt. Có thể lưu liên kết thiết kế và ghi chú trong một file `UI_SPEC.md`; không sao chép tài liệu nghiệp vụ sang nhiều nơi. Ghi rõ bản nào là bản đã duyệt.

- Người dùng quyết định trải nghiệm, phong cách và phạm vi; review và chốt thiết kế.
- AI chuẩn bị prompt, đề xuất màn hình, phát hiện trạng thái thiếu và kiểm tra sự nhất quán. Khi code, bám bản thiết kế và Requirements đã duyệt.
- Nếu thiết kế làm phát sinh chức năng hoặc quy tắc mới, đưa về Product Planning/Requirements để chốt trước.

## Điều kiện hoàn thành và checklist

- [ ] Luồng chính có đủ màn hình, thao tác và phản hồi.
- [ ] Các trạng thái quan trọng đã được thể hiện hoặc mô tả.
- [ ] Màu, chữ, spacing, component và hành vi nhất quán.
- [ ] Đã xem xét thiết bị mục tiêu, nội dung thực tế và khả năng sử dụng.
- [ ] Không có chức năng ngoài kế hoạch bị tự thêm vào bản đã duyệt.
- [ ] Có bản thiết kế và quy ước đủ rõ để bàn giao triển khai.

**Lỗi thường gặp:** yêu cầu “giao diện đẹp” nhưng thiếu ngữ cảnh; tạo mọi màn hình cùng lúc trước khi duyệt chuẩn; chỉ vẽ trạng thái có dữ liệu; coi prototype hoặc code sinh ra là bằng chứng ứng dụng đã hoạt động đúng.

**Mức độ cần thiết:** cần làm rõ UX/UI cho chức năng có giao diện; độ chi tiết tùy mức phức tạp. Prototype tương tác dùng khi cần kiểm tra luồng, không bắt buộc cho mọi màn hình.

**Bước kế tiếp:** Architecture — cấu trúc ứng dụng, lựa chọn công nghệ và cách triển khai phù hợp.
