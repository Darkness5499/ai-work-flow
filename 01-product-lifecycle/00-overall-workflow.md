# Workflow tổng thể — Từ định hướng đến vòng lặp triển khai

**Trạng thái:** đã chốt cấu trúc tổng thể; phạm vi hiện tại dừng ở Implementation & Testing. Release và Operations đang tạm hoãn.

## Mục tiêu

Giữ một đường đi rõ từ ý tưởng đến kết quả có thể kiểm chứng mà không phải thiết kế toàn bộ hệ thống trước khi code. Workflow có hai vòng: vòng định hướng tạo nền tảng chung và vòng triển khai lặp hoàn thành từng luồng nhỏ.

## Vòng 1 — Định hướng vừa đủ

Đi theo thứ tự sau, nhưng chỉ làm sâu phần cần cho phạm vi sắp triển khai:

1. **Discovery:** xác định người dùng, vấn đề, giá trị, mục tiêu và ràng buộc.
2. **Product Planning:** chọn phạm vi MVP và sắp thứ tự các luồng hoặc kết quả cần hoàn thành.
3. **Requirements:** làm rõ hành vi, quy tắc, dữ liệu, lỗi quan trọng và tiêu chí chấp nhận của nhóm chức năng sắp làm.
4. **Domain Design:** xác định khái niệm, quan hệ, vòng đời và trách nhiệm nghiệp vụ khi bài toán cần.
5. **UX/UI Design:** chốt luồng sử dụng, màn hình đại diện, trạng thái và quy ước giao diện khi có frontend.
6. **Architecture:** chốt cấu trúc hệ thống, trách nhiệm, quyền sở hữu dữ liệu, cách giao tiếp và quyết định kỹ thuật chi phối triển khai.

Không cần hoàn thiện mọi chi tiết của từng bước trước khi chuyển sang triển khai. Điều kiện để kết thúc vòng định hướng là phạm vi sắp làm đã rõ, các quyết định nền tảng đủ dùng và các giả định hoặc điểm còn mở đã được ghi nhận.

## Vòng 2 — Triển khai lặp theo luồng nhỏ

Với mỗi luồng hoặc chức năng theo Product Planning:

1. Chọn một nhiệm vụ đủ nhỏ, có kết quả và cách kiểm chứng rõ.
2. Bổ sung Requirements, Domain, UX/UI hoặc Architecture cho đúng phần bị thiếu.
3. Viết Detailed Design vừa đủ: phạm vi, contract, dữ liệu, xử lý và cách kiểm chứng.
4. Thực hiện Project Setup nếu nhiệm vụ còn thiếu nền tảng, quy ước hoặc một thành phần đại diện.
5. Triển khai và kiểm thử; AI cung cấp bằng chứng, người dùng review và chấp nhận kết quả.
6. Cập nhật nguồn tài liệu bị ảnh hưởng, trạng thái hiện tại và bước tiếp theo.

Sau đó chọn luồng tiếp theo và lặp lại. Project Setup không bắt buộc lặp lại nếu nền tảng cần thiết đã sẵn sàng.

## Xử lý thay đổi

Trước khi sửa, xác định tác động đến yêu cầu, domain, UI, kiến trúc, contract, code, test và tài liệu. Chỉ mở lại bước có quyết định bị ảnh hưởng.

- **Thay đổi nhỏ:** hành vi và thiết kế nền tảng không đổi; sửa trực tiếp, kiểm tra phần liên quan và cập nhật trạng thái nếu cần.
- **Thay đổi vừa:** ảnh hưởng một chức năng, contract, dữ liệu hoặc nhiều thành phần; rà lại yêu cầu, thiết kế và phạm vi kiểm chứng trước khi sửa.
- **Thay đổi lớn:** đổi người dùng, vấn đề, phạm vi chính, cấu trúc hệ thống hoặc quyết định nền tảng; quay lại bước Product Lifecycle phù hợp, chốt hướng mới rồi mới triển khai.

Không phỏng vấn hoặc viết lại toàn bộ tài liệu từ đầu khi chỉ một phần bị ảnh hưởng.

## Phân công người và AI

Người dùng chốt phạm vi, quy tắc nghiệp vụ, kiến trúc, đánh đổi quan trọng và chấp nhận kết quả. AI đọc nguồn liên quan, phát hiện điểm thiếu, đề xuất phương án, thực hiện việc nhỏ trong phạm vi đã chốt, kiểm chứng và báo cáo giới hạn.

AI có thể tiếp tục mà không hỏi lại từng chỉnh sửa nhỏ nếu mục tiêu, phạm vi và tiêu chí chấp nhận đã rõ. AI phải dừng phần việc phụ thuộc khi còn quyết định chưa chốt có thể làm đổi hành vi, dữ liệu, contract, kiến trúc hoặc phạm vi. Đề xuất ngoài phạm vi được ghi riêng, không tự đưa vào implementation.

## Trạng thái và nguồn chính

`PROJECT_CONTEXT.md` là nguồn trạng thái chung cho phiên hiện tại và phiên AI tiếp theo. Sau thay đổi có ý nghĩa, cập nhật tối thiểu:

- điều đã chốt và giả định còn dùng;
- việc đã hoàn thành cùng bằng chứng kiểm chứng;
- phần chưa hoàn thành, điểm bị chặn hoặc quyết định còn mở;
- bước tiếp theo cụ thể.

Yêu cầu, thiết kế, contract và quyết định được cập nhật tại nguồn chính tương ứng; `PROJECT_CONTEXT.md` chỉ tóm tắt và liên kết, không sao chép toàn bộ nội dung.

## Điều kiện workflow đang được vận hành đúng

- [ ] Biết dự án đang ở vòng nào, bước nào và kết quả tiếp theo cần tạo.
- [ ] Chỉ làm sâu phần phục vụ phạm vi sắp triển khai.
- [ ] Mỗi nhiệm vụ có phạm vi, tiêu chí chấp nhận và bằng chứng kiểm chứng.
- [ ] Người dùng tham gia các quyết định quan trọng và review kết quả.
- [ ] Thay đổi được rà theo tác động; không mở lại các bước không liên quan.
- [ ] Nguồn chính và `PROJECT_CONTEXT.md` đủ để phiên mới tiếp tục.

**Bước kế tiếp:** chọn phần còn mở cần hoàn thiện hoặc áp dụng vòng lặp vào một dự án cụ thể. Không tự chuyển sang Release, Operations hoặc breakdown Project Setup khi các phần này còn đang hoãn.
