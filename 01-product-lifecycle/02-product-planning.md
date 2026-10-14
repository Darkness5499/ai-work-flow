# Phần 2. Product Planning — Phạm vi và thứ tự thực hiện

## Mục tiêu

Chốt danh sách chức năng, phạm vi MVP, các giai đoạn và thứ tự thực hiện: làm trước, làm sau, chưa quyết định và không làm. Kế hoạch là căn cứ giao việc cho AI và kiểm soát việc mở rộng phạm vi.

**MVP mặc định:** bản tự dùng và kiểm chứng luồng cốt lõi. Chưa mặc định phát hành cho người dùng bên ngoài. Tự dùng giúp kiểm chứng hoạt động và mức hữu ích với bản thân, chưa chứng minh nhu cầu của người dùng khác.

## Đầu vào

Product Brief từ Discovery: người dùng, vấn đề, giá trị mong muốn, mục tiêu sản phẩm và học tập, ràng buộc và giả định. Khi áp dụng cần biết quỹ thời gian để giới hạn phạm vi; không tự đặt lịch khi chưa có thông tin.

## Việc cần làm

1. **Xác định luồng chính:** người dùng bắt đầu từ đâu, thực hiện những việc gì và đạt kết quả nào.
2. **Liệt kê chức năng theo luồng:** mỗi chức năng có mã, mục đích, mức tối thiểu dùng được, phụ thuộc và tiêu chí chấp nhận ngắn. Ghi điểm chưa rõ thay vì tự suy đoán thêm chức năng.
3. **Chia phạm vi:** MVP; làm sau MVP; chưa quyết định; không làm. Ghi lý do ngắn cho mỗi lựa chọn. Chức năng phục vụ học tập cần được đánh dấu riêng để cân nhắc chi phí.
4. **Sắp thứ tự:** xét phụ thuộc, rủi ro cần kiểm chứng sớm, giá trị và công sức tương đối. Ưu tiên từng luồng hoàn chỉnh xuyên suốt giao diện, backend và dữ liệu.
5. **Chia giai đoạn:** luồng cốt lõi chạy được → đủ phạm vi MVP → tự dùng và đánh giá. Mỗi giai đoạn chỉ rõ chức năng, kết quả cần đạt và điều kiện hoàn thành. Ước lượng theo quỹ thời gian thực tế; phần sau MVP chỉ là dự kiến.
6. **Review và chốt:** người dùng kiểm tra phạm vi, thứ tự, khả năng cắt giảm và chấp nhận kế hoạch trước khi dùng làm căn cứ triển khai.

## Câu hỏi cần trả lời

- Luồng nào cần chạy trọn vẹn để tự dùng và kiểm chứng ý tưởng?
- Chức năng nào bắt buộc cho luồng đó? Bỏ chức năng nào vẫn đạt mục tiêu?
- Chức năng nào làm sau, chưa đủ cơ sở quyết định hoặc không làm? Vì sao?
- Việc nào phụ thuộc việc nào? Rủi ro nào cần thử nghiệm sớm?
- Giai đoạn đầu làm được gì, tiếp theo làm gì và khi nào coi là xong?
- Nếu thiếu thời gian, cắt phần nào trước mà vẫn giữ được luồng cốt lõi?

## Đầu ra tối thiểu

Khi áp dụng vào một dự án, dùng một file `PRODUCT_PLAN.md` gồm:

- Mục tiêu MVP và luồng cốt lõi cần kiểm chứng.
- Danh sách chức năng có mã, phạm vi tối thiểu, nhóm ưu tiên và lý do.
- Thứ tự thực hiện, phụ thuộc và các giai đoạn; mỗi giai đoạn có điều kiện hoàn thành.
- Các điểm chưa rõ và đề xuất chưa được duyệt, tách khỏi phạm vi đã chốt.
- Ghi nhận ngắn những thay đổi phạm vi đã được người dùng chấp nhận.

Đây là hướng dẫn đầu ra; chưa tạo kế hoạch chức năng giả khi chưa có dự án cụ thể. Chưa cần đặc tả đầy đủ mọi chức năng ở bước này.

## Phân công và giới hạn cho AI

- **Người dùng:** chọn phạm vi MVP, chốt ưu tiên, quyết định thêm/bớt chức năng và review kết quả.
- **AI:** tổ chức thông tin, phân rã chức năng trong phạm vi, phát hiện phụ thuộc hoặc thiếu sót, đề xuất thứ tự và cách thu nhỏ.
- Khi triển khai, nhiệm vụ phải gắn với chức năng đã chốt và tiêu chí chấp nhận. AI có thể tự thực hiện chi tiết kỹ thuật cần thiết trong phạm vi đó.
- AI không tự thêm chức năng, nâng nhóm “làm sau” vào MVP hoặc mở rộng tiêu chí chấp nhận. Các ý tưởng bổ sung phải ghi riêng là đề xuất, kèm lý do và tác động, để người dùng quyết định.
- Nếu phát hiện phần thiếu khiến chức năng không thể hoàn thành, AI nêu điểm vướng và phương án tối thiểu; làm rõ phần ảnh hưởng trước khi mở rộng phạm vi, tiếp tục công việc độc lập nếu có.
- Cập nhật kế hoạch khi thay đổi đã được chấp nhận để phiên AI sau dùng đúng phạm vi hiện tại.

## Điều kiện hoàn thành và checklist

- [ ] Biết MVP tự dùng để kiểm chứng điều gì.
- [ ] Có danh sách chức năng phân rõ MVP, làm sau, chưa quyết định và không làm.
- [ ] Có thứ tự triển khai và kết quả cần đạt cho từng giai đoạn.
- [ ] Chức năng MVP có phạm vi tối thiểu và tiêu chí chấp nhận đủ để đi tiếp sang làm rõ yêu cầu.
- [ ] Người dùng đã review và chốt kế hoạch; đề xuất của AI không bị lẫn vào phạm vi đã duyệt.

**Lỗi thường gặp:** gom mọi ý tưởng vào MVP; triển khai toàn bộ frontend rồi mới backend; tự thêm đăng nhập, phân quyền hoặc dashboard khi luồng chính chưa yêu cầu; coi tự dùng là lý do bỏ qua bảo vệ dữ liệu hoặc kiểm thử cần thiết.

**Mức độ cần thiết:** bắt buộc ở mức gọn, cập nhật khi có bằng chứng hoặc thay đổi phạm vi được chấp nhận.

**Bước kế tiếp:** Requirements — làm rõ hành vi và tiêu chí chấp nhận của các chức năng sắp triển khai.
