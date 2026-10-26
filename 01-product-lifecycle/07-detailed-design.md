# Phần 7. Detailed Design — Thiết kế triển khai tối giản

**Trạng thái:** phiên bản giản lược theo yêu cầu làm dự án một mình; điều chỉnh khi áp dụng.

## Mục tiêu và đầu vào

Làm rõ cách triển khai chức năng sắp làm, đủ để người dùng review và AI không tự đoán quyết định quan trọng. Đầu vào là chức năng trong kế hoạch, Requirements, UI, Architecture và quy ước liên quan. Tham chiếu các nguồn này, không chép lại.

## Cách làm

Chọn một chức năng hoặc luồng nhỏ theo kế hoạch. Viết một ghi chú thiết kế ngay trong nhiệm vụ hoặc tài liệu chức năng, gồm năm mục:

1. **Phạm vi:** làm gì, không làm gì; tham chiếu tiêu chí chấp nhận và xác định frontend/service bị tác động.
2. **Contract:** đầu vào, đầu ra, validation và lỗi tại các điểm giao tiếp. Tham chiếu hoặc cập nhật artifact contract đang dùng; không tạo bản mô tả thứ hai trùng nội dung.
3. **Dữ liệu:** đọc/ghi gì, ràng buộc nào cần giữ, có đổi schema hoặc migration không. Nếu không đổi, ghi rõ hoặc tham chiếu thiết kế hiện có.
4. **Xử lý:** mô tả ngắn luồng chính, lỗi quan trọng và phản hồi UI nếu có. Chỉ rõ bước gọi service khác hoặc xử lý bất đồng bộ khi xuất hiện.
5. **Kiểm chứng:** các trường hợp cần kiểm tra, tối thiểu luồng thành công và lỗi quan trọng, dựa trên tiêu chí chấp nhận.

Review điểm chưa rõ ảnh hưởng đến nghiệp vụ, dữ liệu hoặc contract; chốt trước khi thực hiện phần phụ thuộc. Chia thành nhiệm vụ nhỏ hơn chỉ khi một nhiệm vụ khó review hoặc có phụ thuộc cần tách.

## Độ sâu theo chức năng

- CRUD đơn giản hoặc một API: tài liệu implement API đủ năm mục trên có thể chính là Detailed Design; không cần thêm tài liệu.
- Luồng qua nhiều API/service: thêm mô tả thứ tự tương tác hoặc sơ đồ khi hữu ích, quyền sở hữu dữ liệu và cách xử lý thất bại một phần.
- Có gửi lặp, retry hoặc cập nhật đồng thời ảnh hưởng kết quả: bổ sung cách tránh tác dụng phụ lặp và giữ đúng quy tắc.
- Chỉ thay đổi giao diện: tập trung hành vi UI và kiểm chứng; tham chiếu contract/dữ liệu không đổi.

Không bắt buộc sơ đồ, pseudocode, danh sách class/method hoặc tài liệu riêng cho mỗi API. Thiết kế theo từng chức năng sắp làm, không thiết kế toàn hệ thống trước.

## Mẫu ghi chú

```text
Chức năng: [mã và tên]
Phạm vi và yêu cầu: [tham chiếu; thành phần bị tác động]
Contract: [tham chiếu hoặc thay đổi cần chốt]
Dữ liệu: [đọc/ghi; ràng buộc; migration nếu có]
Xử lý: [luồng chính; lỗi quan trọng; phản hồi UI nếu có]
Kiểm chứng: [thành công; đầu vào sai; lỗi hoặc trường hợp đặc biệt liên quan]
Điểm cần quyết định: [chỉ ghi khi còn vấn đề ảnh hưởng triển khai]
```

## Đầu ra, phân công và điều kiện hoàn thành

**Đầu ra:** một ghi chú thiết kế cho chức năng và các artifact kỹ thuật thực sự cần cập nhật (contract, schema/migration khi có). Không bắt buộc file `DETAILED_DESIGN.md` hoặc bộ tài liệu implement API riêng.

AI chuẩn bị bản nháp, chủ động chỉ ra thiếu sót và giải thích phương án; người dùng review quyết định quan trọng. AI tự thực hiện chi tiết code trong phạm vi đã chốt. Chức năng hoặc cơ chế kiến trúc mới phải quay về kế hoạch/kiến trúc để quyết định.

**Hoàn thành khi:** biết sẽ sửa phần nào, contract và dữ liệu thay đổi thế nào, xử lý lỗi chính ra sao và dùng kiểm tra gì để xác nhận. Không còn giả định chưa chốt có thể làm thay đổi đáng kể hành vi.

**Checklist:** đúng phạm vi; contract rõ; dữ liệu rõ; luồng và lỗi rõ; có cách kiểm chứng.

**Lỗi thường gặp:** lặp lại Requirements, tách quá nhiều file, mô tả từng dòng code, hoặc bỏ qua xử lý thất bại giữa các service để rút ngắn tài liệu.

**Mức độ cần thiết:** bắt buộc làm rõ ở mức vừa đủ; độ dài tùy rủi ro và độ phức tạp.

**Bước kế tiếp:** triển khai và kiểm thử chức năng. Nếu nền tảng chưa có, thực hiện phạm vi Project Setup cần thiết trước.
