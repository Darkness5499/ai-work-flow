# Email service — ghi chú phỏng vấn kiến trúc

Ngày: 2026-10-21. Đây là chủ đề riêng ngoài phần xây dựng playbook đang làm. Trạng thái: đang phỏng vấn bằng `grill-me` / `grilling`, mỗi lượt một câu. Nội dung tư vấn bên dưới là đề xuất, chưa phải kiến trúc được duyệt. Chưa triển khai service.

## 1. Thông tin người dùng cung cấp

- Có Open API portal và service onboarding để đối tác như MISA, KiotViet đăng ký.
- Muốn khách hàng đăng ký được dùng thử dịch vụ trên UAT.
- Luồng được người dùng xác nhận: đăng ký trên onboarding → gửi dữ liệu lên VietinBank eFAST → người dùng duyệt tay → eFAST gửi webhook về onboarding. Đã xác nhận chỉ gửi cấu hình sang UAT sau khi onboarding nhận webhook báo duyệt thành công từ eFAST. Chưa xác nhận eFAST ở môi trường nào.
- Onboarding và khách hàng trên live hiện không giao tiếp được với UAT; nguyên nhân kỹ thuật/chính sách chưa rõ.
- Trả lời Q1: người dùng nhận định “khả năng là do chính sách cấm trao đổi dữ liệu”. Đây là giả thuyết, chưa có nội dung chính sách xác nhận phạm vi cấm hoặc ngoại lệ.
- Đề xuất xây service email gửi JSON giữa hai môi trường; số request ít, chưa có số liệu cụ thể.
- Người dùng gọi dịch vụ mail Microsoft là “asml”; chưa xác định tên sản phẩm. Không tự đồng nhất với SMTP, Exchange Online, Microsoft Graph hoặc Azure Communication Services Email.

### Thuật ngữ: VietinBank eFAST

VietinBank eFAST là dịch vụ ngân hàng điện tử dành cho khách hàng doanh nghiệp của VietinBank. Trang eFAST chính thức cung cấp giao diện đăng nhập và hướng dẫn sử dụng; FAQ của VietinBank mô tả việc phê duyệt tại doanh nghiệp đối với giao dịch tài chính và một số yêu cầu dịch vụ. Dùng cách viết `eFAST` thống nhất trong tài liệu.

Trong bài toán này, eFAST là hệ thống tiếp nhận dữ liệu từ onboarding để người dùng duyệt tay và gửi webhook kết quả về onboarding, theo mô tả của người dùng. Không đồng nhất eFAST với Open API portal, onboarding hoặc service email. Chưa xác định người duyệt cụ thể thuộc đối tác, khách hàng doanh nghiệp hay bộ phận khác; không mặc định đó là nhân viên ngân hàng.

Nguồn công khai đã tra cứu xác nhận vai trò ngân hàng điện tử doanh nghiệp và khả năng phê duyệt, chưa xác nhận contract webhook onboarding cụ thể của hệ thống này. Không suy diễn endpoint, payload, chữ ký, retry hay trạng thái callback từ thông tin giới thiệu sản phẩm.

## 2. Hiểu bài toán và phản biện ban đầu

Open API portal thường là nơi đối tác tìm tài liệu API, đăng ký ứng dụng, xin quyền truy cập và theo dõi quá trình tích hợp. Cần phân biệt portal với API gateway và với chuẩn mô tả OpenAPI. Chưa biết sản phẩm portal cụ thể của hệ thống này.

Bài toán đang có vẻ là cấp tài nguyên/quyền dùng thử ở UAT sau đăng ký trên live, không phải chuyển mọi API request qua email. Đây là giả định cần xác nhận. API thử nghiệm của đối tác vẫn cần một đường truy cập UAT được cho phép; cầu nối onboarding không tự giải quyết khả năng truy cập đó.

Hai môi trường tách biệt vẫn có thể giao tiếp qua một điểm tích hợp có kiểm soát. Cần tìm nguyên nhân: chưa có route/firewall, cấm inbound vào UAT, hay chính sách cấm trao đổi dữ liệu live–UAT. Email cũng là cầu nối dữ liệu, không phải ngoại lệ mặc nhiên của chính sách cách ly.

Request ít giúp giảm tải nhưng không loại bỏ gửi trùng, mất phản hồi, xử lý dở dang, dữ liệu giả mạo và nhu cầu đối soát. Email có thể phù hợp làm giải pháp giới hạn nếu đó là kênh được phép, dữ liệu tối thiểu, chấp nhận bất đồng bộ và có người xử lý lỗi. Không ưu tiên email làm nền tảng tích hợp lâu dài chỉ vì lưu lượng thấp.

## 3. Các phương án cần xem xét

1. **API cấp UAT qua gateway có kiểm soát:** phù hợp khi được mở kết nối hẹp. Onboarding gửi lệnh tạo tenant/application UAT bằng danh tính dịch vụ riêng, quyền tối thiểu và idempotency key. API trả operation ID; theo dõi kết quả nếu provisioning chưa hoàn thành. Ít thành phần nếu đã có gateway, nhưng phụ thuộc đường mạng được duyệt.
2. **UAT chủ động pull từ điểm trung gian được phép:** ưu tiên khảo sát khi UAT không nhận inbound nhưng được outbound. Onboarding ghi yêu cầu vào queue hoặc API trung gian lưu yêu cầu bền vững; worker UAT nhận, xử lý rồi gửi kết quả. Hai phía chỉ có quyền cần thiết, không dùng chung tài khoản quản trị. Queue có chi phí cấu hình/vận hành nhưng phù hợp hơn email cho ACK, retry và hàng đợi lỗi. Nếu đã dùng Azure, Service Bus là một ứng viên, chưa phải lựa chọn đã chốt.
3. **Email JSON hoặc thao tác thủ công có kiểm soát:** nếu chỉ email được phép, dùng thiết kế ở phần sau. Với số yêu cầu rất ít và SLA thoải mái, có thể để nhân sự duyệt/cấp UAT thủ công trước khi đầu tư một bridge tự động. Đánh đổi là thời gian chờ và công sức vận hành.

Khuyến nghị hiện tại: tìm đúng ràng buộc kết nối trước; nếu chỉ cấm inbound vào UAT, ưu tiên khảo sát pull. Nếu cấm mọi trao đổi dữ liệu giữa hai môi trường, cần quy trình được phép hoặc onboarding UAT độc lập; không dùng email để lách ràng buộc.

## 4. Nếu buộc phải dùng email: thiết kế tối thiểu đề xuất

### Đầu vào và phạm vi

Chỉ chuyển lệnh nghiệp vụ hẹp, ví dụ `ProvisionSandbox`, và phản hồi kết quả. Chưa xây một nền tảng gửi mọi loại dữ liệu. Chốt tên dịch vụ Microsoft, khả năng gửi/đọc tự động, quyền truy cập mailbox, schema dữ liệu, độ trễ chấp nhận và đường trả kết quả trước khi code.

### Trình tự xử lý

1. Chỉ sau khi nhận và xác thực webhook duyệt thành công từ eFAST, onboarding mới tạo yêu cầu chuyển cấu hình UAT. Đề xuất lưu kết quả duyệt và outbox trong một transaction cục bộ, liên kết với đăng ký/phiên bản đã duyệt bằng `requestId`; webhook trùng không tạo thêm yêu cầu nghiệp vụ.
2. Sender lấy outbox, tạo envelope có `schemaVersion`, `messageId`, `requestId`, `type`, `source`, `target`, `issuedAt`, `expiresAt` và payload tối thiểu. Gửi cùng `messageId` khi retry cùng một message; phản hồi dùng ID riêng và liên kết bằng `requestId`.
3. Ký số envelope bằng khóa của phía gửi; phía nhận chỉ giữ public key xác minh. Ký trên bytes chuẩn hóa hoặc định dạng chữ ký chuẩn, không tự ghép JSON rồi giả định thứ tự trường ổn định. Dữ liệu cần bảo mật phải được mã hóa cho bên nhận; TLS của mail không thay thế mã hóa payload khi cần bảo mật đầu cuối. Không gửi production secret, token hoặc bản sao dữ liệu khách hàng live.
4. Gửi tới mailbox chuyên dụng. Nếu là Exchange Online/Microsoft 365 và được cấp quyền, có thể dùng Microsoft Graph với danh tính ứng dụng giới hạn tới mailbox cần thiết. Nếu “asml” chỉ là relay gửi mail, phải xác định thêm cơ chế nhận/đọc; relay gửi không mặc nhiên có Graph mailbox.
5. Worker UAT chủ động đọc mailbox nếu outbound được phép. Với Graph, có thể dùng delta query theo folder, theo hết các trang và lưu checkpoint sau khi đã lưu bền vững message vào inbox nội bộ. Không dùng cờ unread/read làm hàng đợi hoặc bằng chứng xử lý thành công.
6. Receiver giới hạn kích thước, kiểm tra chữ ký, schema, loại lệnh, target UAT, thời hạn, quyền của nguồn gửi và payload. Địa chỉ From/subject/allowlist chỉ là lớp lọc bổ sung, không thay thế xác thực lệnh. Không tải URL tùy ý trong payload hoặc thực thi nội dung nhận được.
7. Lưu inbox với ràng buộc unique trên message ID; đồng thời bảo vệ nghiệp vụ bằng request ID hoặc khóa provisioning. Message trùng không tạo tenant mới. Nếu cùng ID nhưng payload khác thì từ chối và ghi nhận lỗi. Với provisioning gồm nhiều bước hoặc gọi hệ thống ngoài, lưu tiến độ và thiết kế từng bước idempotent để phục hồi sau crash.
8. UAT tạo tài nguyên và credentials riêng. Ghi kết quả cùng outbox phản hồi trong transaction khi khả thi. Gửi `Succeeded` hoặc `Failed` kèm mã lỗi an toàn; không trả secret qua email. Cơ chế đối tác nhận credentials UAT cần được thiết kế riêng.
9. Live xác thực phản hồi và cập nhật đúng request, không để message cũ làm lùi trạng thái. Phân biệt `Pending`, `SubmittedToMail`, `Succeeded`, `Failed`, `NeedsReview`. Hết thời gian chờ chỉ có nghĩa chưa biết kết quả; không kết luận UAT chưa tạo tài nguyên.
10. Retry có backoff, giới hạn số lần và thời gian; lỗi tạm thời mới retry tự động. Payload sai/chữ ký sai đưa vào vùng cách ly để review. Khi mất phản hồi, dùng request ID đối soát hoặc gửi lại lệnh idempotent để nhận lại kết quả đã lưu. Có người chịu trách nhiệm xử lý tồn đọng.

### Các điểm không được hiểu nhầm

- Microsoft Graph `sendMail` trả `202 Accepted` chỉ xác nhận nhận yêu cầu gửi, không xác nhận thư đã tới hay provisioning đã thành công.
- Email có thể bị trì hoãn, lọc hoặc cách ly. Không cam kết exactly-once; bảo vệ tác động nghiệp vụ bằng idempotency, inbox/outbox và đối soát.
- Chữ ký ngăn sửa/giả payload, nhưng chống replay còn cần lưu ID, kiểm tra thời hạn và giới hạn quyền lệnh. Thời gian lưu dấu vết chống trùng phải bao phủ cửa sổ retry/replay được thiết kế.
- Mailbox, log, backup và retention đều là nơi dữ liệu có thể được giữ lại. Chỉ gửi dữ liệu cần cho UAT và xác định thời hạn lưu.
- Queue cũng có thể giao lại message; chọn queue không loại bỏ nhu cầu idempotency nghiệp vụ.

### Phân công và đầu ra

Người dùng xác nhận ràng buộc hạ tầng, chính sách dữ liệu, sản phẩm mail, SLA và nghiệp vụ cấp UAT. AI hỗ trợ so sánh, soạn contract và kịch bản kiểm chứng sau khi đủ thông tin. Đầu ra trước triển khai: quyết định kênh truyền, contract lệnh/kết quả, sơ đồ quyền truy cập, trạng thái xử lý và cách phục hồi lỗi.

### Checklist trước khi coi thiết kế khả thi

- [ ] Xác nhận kênh trao đổi dữ liệu được phép và UAT có đường truy cập cho đối tác.
- [ ] Xác định chính xác dịch vụ Microsoft và khả năng đọc/gửi tự động ở cả hai phía.
- [ ] Chốt payload tối thiểu, danh tính dịch vụ và cơ chế cấp credentials UAT.
- [ ] Kiểm chứng một request gửi trùng chỉ tạo một tài nguyên nghiệp vụ.
- [ ] Kiểm chứng crash sau provisioning nhưng trước phản hồi có thể phục hồi.
- [ ] Kiểm chứng thư trễ/mất phản hồi, UAT downtime, lỗi xác thực mail và throttling.
- [ ] Từ chối payload sửa đổi, sai target, quá hạn hoặc ngoài quyền.
- [ ] Có correlation ID, đối soát request quá hạn và người xử lý lỗi.

Chưa thực hiện các kiểm chứng hệ thống trên; đây là tiêu chí đề xuất.

## 5. Cây quyết định và câu hỏi đang chờ

Ràng buộc mạng/chính sách → kênh truyền được phép → nghiệp vụ và dữ liệu cần chuyển → độ trễ/độ tin cậy → sản phẩm Microsoft và contract → thử nghiệm → chốt thiết kế.

**Q1:** Live/onboarding không giao tiếp được với UAT vì chưa mở kết nối mạng, vì UAT chỉ được outbound, hay vì chính sách cấm trao đổi dữ liệu giữa hai môi trường?

**Trả lời Q1:** “khả năng là do chính sách cấm trao đổi dữ liệu”. Chưa xác nhận chính sách cấm kết nối trực tiếp, cấm dữ liệu production hay cấm mọi trao đổi. Không mặc định email, queue, mã hóa hoặc chuyển thủ công là ngoại lệ được phép.

**Hướng đánh giá cập nhật:** nếu cấm mọi trao đổi, đề xuất onboarding UAT độc lập, tài khoản và dữ liệu thử nghiệm riêng, không đồng bộ từ live. Có thể đặt đường dẫn tĩnh từ portal tới trang đăng ký UAT nếu được phép; không đính kèm thông tin khách hàng, token live hoặc tự giả định được dùng chung SSO. Nếu chỉ cấm dữ liệu nghiệp vụ production, có thể đánh giá lệnh cấp sandbox với dữ liệu tối thiểu theo phạm vi được cho phép. Hai nhánh này đều chưa được chốt.

**Trả lời Q2:** dữ liệu dự kiến là một bộ object JSON chứa thông tin cấu hình. Người dùng xác nhận dữ liệu sẽ không nhạy cảm; chưa có JSON mẫu/schema vì chưa chốt phương án. Không yêu cầu schema chi tiết ở giai đoạn lựa chọn kiến trúc.

**Điều chỉnh cách phỏng vấn:** AI đã hỏi JSON mẫu quá sớm. Tiếp tục ở mức yêu cầu và đánh đổi của phương án; phần triển khai email ở trên chỉ là tham khảo có điều kiện, không phải quyết định được duyệt. Dữ liệu không nhạy cảm giúp giảm yêu cầu bảo mật nội dung, nhưng vẫn cần bảo vệ tính xác thực/toàn vẹn của lệnh cấu hình và xử lý trùng/lỗi. Phạm vi chính sách trao đổi giữa môi trường vẫn chưa được xác minh.

**Thông tin bổ sung cho Q3:** onboarding phải gửi dữ liệu lên eFAST, người dùng duyệt tay, sau đó eFAST gửi webhook về onboarding. Như vậy toàn bộ luồng có bước chờ phê duyệt và callback; đây là cơ sở đề xuất mô hình bất đồng bộ. Chưa thể suy ra thời gian chờ được phép sau phê duyệt hoặc kết luận email đáp ứng SLA.

**Q4 đã trả lời:** có phải chỉ sau khi onboarding nhận kết quả phê duyệt thành công từ eFAST mới được gửi cấu hình sang UAT? Người dùng xác nhận “đúng”: chỉ sau khi onboarding nhận webhook báo duyệt thành công từ eFAST mới gửi cấu hình sang UAT. Đây là thứ tự đã chốt; chưa chốt kênh truyền.

**Hệ quả thiết kế đề xuất:** phân biệt “đã được duyệt” với “UAT đã sẵn sàng”; webhook phê duyệt không tự chứng minh đã cấu hình UAT. Theo thứ tự đã chốt ở Q4, đề xuất onboarding lưu kết quả phê duyệt hợp lệ và yêu cầu cấp UAT bền vững trước khi worker chuyển cấu hình. Webhook trùng không được tạo thêm yêu cầu cấp UAT cho cùng đăng ký/phiên bản đã duyệt. Trường hợp từ chối, thay đổi đăng ký hoặc callback cũ sẽ được làm rõ sau, chưa tự đặt quy tắc nghiệp vụ.

**Q5 đã trả lời:** người dùng xác nhận “thời gian thoải mái, còn do con người làm nữa”. Ghi nhận thời gian xử lý linh hoạt, không yêu cầu realtime; không chốt mốc 5 phút hay SLA định lượng. Đã biết có bước con người duyệt trên eFAST; chưa suy ra có bước thủ công nào khác ở UAT.

**Đánh giá cập nhật:** cấu hình không nhạy cảm, ít request và thời gian linh hoạt khiến email là phương án có thể cân nhắc nếu được phép. Độ trễ không còn là tiêu chí chính để loại email; cần ưu tiên khả năng xác định kết quả, tránh xử lý trùng và phục hồi lỗi. Chưa chốt email vì phạm vi chính sách và dịch vụ Microsoft cụ thể vẫn chưa rõ.

**Điều chỉnh theo yêu cầu người dùng:** ưu tiên tranh luận các phương án truyền dữ liệu giữa hai môi trường; tạm hoãn câu hỏi tự động/thủ công ở UAT. Không tiếp tục đào sâu email trước khi so sánh lựa chọn kiến trúc.

### So sánh các cách truyền dữ liệu

Tất cả phương án dưới đây là đề xuất có điều kiện, không phải hạ tầng hiện có hoặc kênh đã được phép. Khác môi trường không tự đồng nghĩa không thể kết nối; nếu chính sách cấm chính việc trao đổi dữ liệu thì đổi giao thức không giải quyết được.

- **API HTTPS trực tiếp qua gateway:** onboarding gọi endpoint nhận cấu hình UAT sau duyệt. Phù hợp nếu mở được kết nối giới hạn, có danh tính dịch vụ và quyền hẹp. Ít thành phần nếu đã có gateway/API, nhưng cần timeout, retry và idempotency; UAT ngừng hoạt động thì phía gửi phải giữ yêu cầu để thử lại. Không đồng nghĩa mở toàn bộ mạng giữa hai môi trường.
- **UAT pull từ API trung gian:** onboarding ghi yêu cầu đã duyệt vào vùng tích hợp được phép; worker UAT chủ động lấy, lưu/xử lý rồi gửi kết quả về. Phù hợp khi không cho inbound vào UAT nhưng cho outbound HTTPS. Cần claim/lease, ACK, retry và lưu trạng thái bền vững nếu có nhiều worker; không chỉ GET rồi xóa ngay. Không nên để UAT đọc thẳng database live.
- **Queue/message broker trung gian:** onboarding publish, UAT consume rồi ACK sau xử lý; kết quả gửi về luồng phản hồi riêng. Phù hợp khi tổ chức đã có broker và cho phép hai bên kết nối tới vùng tích hợp. Giảm phần tự viết cơ chế giao nhận so với API polling, nhưng vẫn cần idempotency nghiệp vụ và vận hành broker. Không đề xuất dựng Kafka chỉ vì vài request.
- **File JSON qua SFTP hoặc object storage trung gian:** live xuất file theo request ID; UAT quét định kỳ, lấy file hoàn chỉnh và xử lý; kết quả ghi ở vùng riêng. Phù hợp dữ liệu cấu hình ít, thời gian linh hoạt và tổ chức đã có kênh chuyển file. Cần cơ chế công bố file hoàn chỉnh phù hợp nền tảng, xác thực nguồn/toàn vẹn, chống trùng và đối soát; không dùng việc xóa file làm bằng chứng duy nhất rằng đã xử lý. Đơn giản hay không phụ thuộc hạ tầng sẵn có.
- **Email JSON:** một dạng chuyển file/message qua hệ thống thư. Có thể tận dụng mail sẵn có nhưng phải bổ sung tracking, xác thực payload, chống trùng, retry và đối soát; còn phụ thuộc lọc/quarantine và quyền đọc mailbox. Phù hợp khi mail là kênh trao đổi đã được phép, không tự động tốt hơn vì request ít.
- **Export/import có người vận hành:** xuất cấu hình đã duyệt và nhập qua công cụ UAT. Ít tích hợp tự động nhưng có chi phí thao tác và nguy cơ nhầm môi trường/phiên bản. Phù hợp nếu số yêu cầu rất ít, việc nhập có kiểm tra và quy trình chuyển dữ liệu được phép. Đây vẫn là trao đổi dữ liệu, không phải ngoại lệ chính sách mặc nhiên.

VPN, private link và firewall rule là phương án tạo/giới hạn đường mạng, không thay thế giao thức truyền dữ liệu hoặc quyết định cho phép trao đổi. Webhook cũng là một dạng HTTP push, không tự vượt qua rào cản kết nối. Shared database hoặc replication live–UAT tạo phạm vi truy cập và coupling lớn hơn nhu cầu chuyển vài cấu hình, nên không ưu tiên trong bài toán này.

### Khuyến nghị sơ bộ cho trường hợp hiện tại

1. Nếu đã có broker hoặc kênh chuyển file được duyệt, ưu tiên tận dụng và so sánh chi phí tích hợp thực tế; không thêm hạ tầng chỉ vì tên công nghệ.
2. Nếu chỉ cấm inbound vào UAT nhưng được outbound HTTPS tới vùng tích hợp, ưu tiên khảo sát UAT pull qua API trung gian. Nếu được mở endpoint UAT hẹp và đã có gateway, API push trực tiếp có thể ít thành phần hơn.
3. Nếu chỉ mail được phép, email là phương án hợp lý trong các ràng buộc đã nêu. Nếu cấm mọi trao đổi dữ liệu, cần onboarding UAT độc lập hoặc ngoại lệ cụ thể được phép; đổi sang queue/SFTP cũng không giải quyết được.

Kết luận đang thảo luận: email không phải lựa chọn duy nhất. Quyết định phụ thuộc kênh được phép và hạ tầng sẵn có nhiều hơn thông lượng/độ trễ. Chưa chọn công nghệ và chưa triển khai. Chính sách và tên dịch vụ Microsoft “asml” vẫn chưa được xác minh.

## 6. Nguồn kỹ thuật đã tra cứu

Các nguồn chỉ xác nhận khả năng sản phẩm; không chứng minh hạ tầng của người dùng có các quyền/kết nối này.

- [Microsoft Graph — quy trình gửi mail và 202 Accepted](https://learn.microsoft.com/en-us/graph/outlook-things-to-know-about-send-mail).
- [Microsoft Graph — theo dõi thay đổi message theo folder bằng delta query](https://learn.microsoft.com/en-us/graph/delta-query-messages).
- [Azure Service Bus — khóa message và settlement](https://learn.microsoft.com/en-us/azure/service-bus-messaging/message-transfers-locks-settlement).
- [Azure Service Bus — mất message và xử lý trùng](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-message-loss-and-duplicates).

- [VietinBank eFAST — cổng ngân hàng điện tử doanh nghiệp](https://efast.vietinbank.vn/).
- [VietinBank — FAQ về phê duyệt và xác thực trên eFAST](https://contact.vietinbank.vn/blog/obj_faq_42767083/fld_faqid_63024046/FAQ10).
