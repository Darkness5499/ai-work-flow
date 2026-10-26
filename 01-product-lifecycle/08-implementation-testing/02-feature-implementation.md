# Phần 8. Implementation & Testing — Triển khai chức năng với AI

**Trạng thái:** hướng dẫn và checklist được tạo theo yêu cầu; điều chỉnh khi áp dụng thực tế.

## Mục tiêu, đầu vào và phạm vi

Hoàn thành từng chức năng nhỏ, kiểm chứng được và người dùng hiểu các thay đổi quan trọng. Áp dụng vòng lặp này sau khi nền tảng cần thiết đã sẵn sàng; [Project Setup](01-project-setup.md) là bước riêng, chưa đi sâu thêm ở đây.

Đầu vào: nhiệm vụ theo Product Planning, Requirements và tiêu chí chấp nhận, [ghi chú Detailed Design](../07-detailed-design.md), contract, UI và quy ước liên quan, code hiện tại cùng cách chạy/test. Chỉ tham chiếu tài liệu cần cho nhiệm vụ, không sao chép toàn bộ playbook vào prompt.

## Thứ tự thực hiện

### 1. Chọn một nhiệm vụ đủ nhỏ

- Chọn chức năng theo thứ tự đã chốt, kiểm tra các phụ thuộc đã sẵn sàng.
- Ghi mục tiêu, phạm vi làm/không làm và tiêu chí chấp nhận.
- Nếu thay đổi quá lớn để review, chia theo kết quả nhỏ có thể kiểm chứng; vẫn hướng tới luồng hoàn chỉnh qua các phần liên quan.

**Đầu ra:** nhiệm vụ rõ phạm vi, tham chiếu thiết kế và có cách kiểm tra hoàn thành. Người dùng chốt phạm vi; AI hỗ trợ chia nhỏ.

### 2. Giao ngữ cảnh và kiểm tra cách hiểu

- AI đọc tài liệu và code liên quan, kiểm tra thay đổi đang có để không ghi đè công việc khác.
- AI tóm tắt ngắn phần sẽ sửa, thứ tự thực hiện, giả định và cách kiểm chứng.
- Điểm chưa rõ ảnh hưởng nghiệp vụ, dữ liệu, contract hoặc kiến trúc cần được làm rõ trước phần việc phụ thuộc. Không tự coi giả định là yêu cầu.
- Trong phạm vi đã được giao, AI tiếp tục làm mà không hỏi lại từng thay đổi nhỏ. Chỉ đưa quyết định mới có ảnh hưởng ra để người dùng tham gia.

**Đầu ra:** hiểu thống nhất nhiệm vụ; biết thành phần bị tác động và kiểm tra cần chạy.

### 3. Triển khai theo thiết kế

- Chốt/cập nhật contract và migration cần thiết theo thiết kế trước khi triển khai phần phụ thuộc.
- Làm nghiệp vụ, tích hợp và UI theo thứ tự phụ thuộc; tái sử dụng cấu trúc và quy ước hiện có.
- Bổ sung kiểm tra hành vi cùng với thay đổi, không chờ đến cuối mới nghĩ cách kiểm chứng.
- Xử lý trường hợp lỗi quan trọng và trạng thái UI thuộc phạm vi.
- Không tự thêm chức năng, thư viện, service hoặc refactor phần không liên quan. Đề xuất mở rộng được ghi riêng để quyết định.

**Đầu ra:** thay đổi code tập trung, kèm contract/migration/test khi có. Không bắt buộc test-first; lựa chọn cách thực hiện phù hợp nhiệm vụ.

### 4. Kiểm chứng và sửa lỗi

Chạy các kiểm tra phù hợp với thay đổi và các kiểm tra bắt buộc của dự án:

- Build, kiểm tra kiểu, lint hoặc kiểm tra tĩnh tương ứng.
- Quy tắc nghiệp vụ quan trọng: kiểm thử tự động ở mức phù hợp.
- API và dữ liệu thay đổi: kiểm tra contract, validation, lỗi và tích hợp lưu trữ; kiểm tra migration trên môi trường thử nếu có.
- Giao tiếp qua service: kiểm tra tương thích và tình huống dependency lỗi; gửi lặp, retry hoặc đồng thời chỉ kiểm tra khi liên quan.
- UI thay đổi: kiểm tra luồng chính, trạng thái rỗng/loading/lỗi và thiết bị mục tiêu liên quan.
- Kiểm tra luồng xuyên suốt với các thành phần thật khi cần; mock đơn lẻ không chứng minh tích hợp thực tế.

AI sửa lỗi do thay đổi gây ra và chạy lại kiểm tra bị ảnh hưởng. Nếu kiểm tra bị chặn do môi trường hoặc lỗi có sẵn, ghi rõ bằng chứng và phần chưa kiểm chứng; không báo đã pass. Không sửa test chỉ để chiều theo implementation sai yêu cầu.

**Đầu ra:** lệnh/kiểm tra đã chạy, kết quả và giới hạn. Kiểm chứng theo hành vi và rủi ro, không chạy mọi loại test cho mọi thay đổi hoặc chạy lặp vô ích.

### 5. Review thay đổi và thử chức năng

- AI tự đọc diff: phạm vi, code thừa, xử lý lỗi, contract, dữ liệu và thông tin nhạy cảm.
- AI báo ngắn: đã đổi gì, vì sao, kiểm chứng thế nào và còn hạn chế gì.
- Người dùng xem diff ở các quyết định quan trọng, thử luồng theo tiêu chí chấp nhận và yêu cầu giải thích phần chưa hiểu.
- Nếu chưa đạt, quay lại triển khai/kiểm chứng. Nếu thay đổi mục tiêu hoặc phạm vi, cập nhật kế hoạch/thiết kế trước.

**Đầu ra:** phản hồi review được xử lý và người dùng chấp nhận kết quả. AI tự review không thay thế sự chấp nhận của người dùng.

### 6. Lưu kết quả và bàn giao

- Cập nhật contract, hướng dẫn hoặc quyết định bị ảnh hưởng tại nguồn chính; không viết thêm tài liệu nếu không có thay đổi cần lưu.
- Ghi trạng thái nhiệm vụ: đang làm, chờ review, bị chặn hoặc hoàn thành.
- Lưu thay đổi thành commit theo quy ước dự án khi được giao; ghi mã commit nếu đã có. Phân biệt code còn ở working tree với code đã lưu trong Git.
- Cập nhật trạng thái phiên: việc đã làm, kiểm tra, phần chưa xong và bước tiếp theo cụ thể.

**Đầu ra:** code và ngữ cảnh đủ để tiếp tục ở phiên mới. Hoàn thành chức năng không đồng nghĩa đã merge hoặc triển khai production; Release là bước riêng.

## Checklist trước khi code

- [ ] Chỉ rõ nhiệm vụ và phạm vi, không lấy toàn bộ backlog làm một lần giao việc.
- [ ] Có tiêu chí chấp nhận và ghi chú thiết kế đủ dùng.
- [ ] Có contract/UI/quy ước liên quan hoặc ghi rõ không áp dụng.
- [ ] Các phụ thuộc cần thiết sẵn sàng; biết cách chạy và kiểm tra.
- [ ] Không còn điểm chưa chốt ảnh hưởng lớn đến hành vi hoặc phạm vi.

## Checklist hoàn thành

- [ ] Chức năng đáp ứng tiêu chí chấp nhận và đúng thiết kế đã chốt.
- [ ] Contract, dữ liệu và UI nhất quán với implementation khi có liên quan.
- [ ] Luồng chính và lỗi quan trọng được kiểm chứng bằng bằng chứng phù hợp.
- [ ] Các kiểm tra bắt buộc đã đạt; phần chưa kiểm chứng/giới hạn được nêu rõ. Nếu thiếu bằng chứng cho tiêu chí bắt buộc thì chưa đánh dấu hoàn thành.
- [ ] Diff không chứa thay đổi ngoài phạm vi hoặc secrets.
- [ ] Người dùng đã review, hiểu thay đổi quan trọng và chấp nhận kết quả.
- [ ] Tài liệu bị ảnh hưởng, trạng thái nhiệm vụ và điểm tiếp tục đã cập nhật.

## Prompt giao việc ngắn

```text
Triển khai nhiệm vụ [mã/tên] theo kế hoạch đã chốt.
Nguồn: [yêu cầu, ghi chú thiết kế, contract, UI, quy ước liên quan].
Mục tiêu và tiêu chí chấp nhận: [...].
Ngoài phạm vi: [...].

Đọc code hiện tại, tóm tắt phần sẽ sửa và cách kiểm chứng.
Làm rõ giả định ảnh hưởng nghiệp vụ, dữ liệu hoặc contract trước phần việc phụ thuộc.
Tự triển khai và sửa lỗi trong phạm vi đã giao; đề xuất mở rộng ghi riêng.
Chạy các kiểm tra phù hợp, không tự nhận pass khi chưa chạy hoặc bị chặn.
Kết thúc bằng: thay đổi chính, bằng chứng kiểm tra, giới hạn và cách tôi thử chức năng.
Cập nhật trạng thái để phiên sau tiếp tục, không đánh dấu được người dùng chấp nhận thay tôi.
```

## Ghi chú bàn giao tối thiểu

Ghi ngay trong nhiệm vụ hoặc file trạng thái đang dùng, không bắt buộc tạo file riêng:

```text
Nhiệm vụ / trạng thái:
Đã làm / vị trí code hoặc commit nếu có:
Kiểm tra đã chạy và kết quả:
Chưa kiểm chứng / điểm vướng / quyết định cần chốt:
Bước tiếp theo:
```

**Mức độ cần thiết:** vòng lặp bắt buộc cho chức năng; chọn độ sâu kiểm chứng theo thay đổi và rủi ro. Không yêu cầu nhiều tài liệu hoặc mọi loại test cho việc nhỏ.

**Lỗi thường gặp:** giao cả hệ thống trong một prompt; để AI thêm tính năng; chỉ xem code mà không chạy; coi mock test là tích hợp; chấp nhận báo cáo pass không có bằng chứng; bỏ cập nhật trạng thái khi chuyển phiên.

**Bước kế tiếp:** lặp lại cho chức năng tiếp theo; khi đủ phạm vi phiên bản, chuyển sang Release — chuẩn bị và kiểm chứng phát hành.
