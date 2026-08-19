# BÁO CÁO LỖI (BUG REPORTS)

Dưới đây là danh sách các lỗi (bugs) được phát hiện trong quá trình tự động hóa kiểm thử (Automation Testing) bằng Postman.

---

## 1. BUG-LOGIN-001: Lỗi không tự động giải phóng Lockout sau 30 giây

**Thông tin chung:**
- **API:** `POST /api/login`
- **Mức độ nghiêm trọng (Severity):** High
- **Mức độ ưu tiên (Priority):** High
- **Ngày phát hiện:** 19/08/2026
- **Người báo cáo:** Hồ Gia Huy

**Mô tả:**
Theo đặc tả nghiệp vụ (FR-02), nếu người dùng đăng nhập sai từ 3 lần trở lên liên tiếp, hệ thống sẽ tạm khóa tài khoản trong 30 giây. Tuy nhiên, sau khi tài khoản bị khóa và đợi hơn 30 giây, tài khoản vẫn bị khóa vĩnh viễn và không thể đăng nhập lại kể cả khi nhập đúng mật khẩu.

**Các bước tái hiện (Steps to Reproduce):**
1. Mở Postman, gửi 3 request `POST /api/login` liên tiếp với payload mật khẩu sai (`{"email": "test@eshop.com", "password": "Sai"}`).
2. Hệ thống trả về lỗi (Trigger lockout).
3. Ngừng gửi request và đợi quá 30 giây.
4. Gửi lại request `POST /api/login` với mật khẩu đúng (`{"email": "test@eshop.com", "password": "Test1234!"}`).

**Kết quả mong đợi (Expected Result):**
Hệ thống trả về `200 OK` và cho phép đăng nhập thành công vì đã hết thời gian phạt 30 giây.

**Kết quả thực tế (Actual Result):**
Hệ thống vẫn trả về `401 Unauthorized` (hoặc thông báo tài khoản đang bị khóa). Lỗi này chỉ biến mất khi khởi động lại backend server (restart) và seed lại dữ liệu (State Leakage vĩnh viễn trên DB).

**Test Case liên quan:** 
- TC_LOGIN_021 (Đăng nhập thành công SAU KHI đợi 30s) - FAIL.

**Link GitHub Issue:** 
👉 *[Sinh viên copy nội dung này tạo Issue trên GitHub và dán link vào đây]*


## 2. BUG-CHECKOUT-001: Thiếu hoàn toàn Validation tại API Checkout

**Thông tin chung:**
- **API:** POST /api/checkout
- **Mức độ nghiêm trọng (Severity):** Critical (Nghiêm trọng nhất)
- **Ngày phát hiện:** 19/08/2026
- **Người báo cáo:** Hồ Gia Huy

**Mô tả:**
API POST /api/checkout không hề có bất kỳ lớp Validation (kiểm tra dữ liệu đầu vào) nào. Backend ngây thơ chấp nhận tất cả các payload không hợp lệ và vẫn trả về \200 OK\ kèm theo việc tạo đơn hàng thành công trong Database. Cụ thể, API chấp nhận số tiền âm, số tiền bằng 0, địa chỉ trống, sai kiểu dữ liệu (NaN, chuỗi chữ), thiếu trường bắt buộc, và thậm chí cả mã độc XSS/SQL Injection. Điều này gây thất thoát tài chính và hổng bảo mật nghiêm trọng.

**Các bước tái hiện (Steps to Reproduce):**
1. Đăng nhập thành công và lấy Bearer Token hợp lệ.
2. Gửi request \POST /api/checkout\ với Body: \{\
total_amount\: -50000, \shipping_address\: \\}\.
3. Quan sát kết quả.

**Kết quả mong đợi (Expected Result):**
Hệ thống phải trả về \400 Bad Request\ và từ chối tạo đơn hàng do số tiền không hợp lệ và thiếu địa chỉ.

**Kết quả thực tế (Actual Result):**
Hệ thống trả về \200 OK\ với nội dung \{\message\:\Checkout
successful\,\orderId\: X}\. Đơn hàng với tổng tiền âm được tạo thành công trong DB.

**Test Case liên quan:** 
- Gần 24 Test case Validation (VD: TC_CHK_002, TC_CHK_003, TC_CHK_020...) - Đều bị FAIL do server trả về 200.

**Link GitHub Issue:** 
👉 *[Sinh viên copy nội dung này tạo Issue trên GitHub và dán link vào đây]*


## 3. BUG-ORDER-001: Lỗi State Machine cho phép chuyển đơn hàng từ Canceled sang Delivered

**Thông tin chung:**
- **API:** \PUT /api/admin/orders/:id/status\
- **Mức độ nghiêm trọng (Severity):** High (Cao)
- **Ngày phát hiện:** 19/08/2026
- **Người báo cáo:** Hồ Gia Huy

**Mô tả:**
Hệ thống State Machine quản lý trạng thái đơn hàng bị lỗi nghiêm trọng trong việc kiểm tra tính hợp lệ của luồng đi (Workflow). Mặc dù hệ thống có chặn một số luồng ngược (ví dụ từ \delivered\ về \confirmed\ bị chặn trả về 400), nhưng nó lại **cho phép đơn hàng đã bị hủy (canceled) chuyển thẳng sang trạng thái đã giao (delivered)**. Điều này là vô lý về mặt quy trình nghiệp vụ vì đơn hàng đã hủy thì không thể đem đi giao thành công được.

Đồng thời, lỗi rò rỉ trạng thái (State Leakage) này đã khiến cho toàn bộ các test case Happy Path phía sau (TC_ORD_001, 002, 003, 004) bị đánh rớt oan uổng do đơn hàng đã bị kẹt vĩnh viễn ở trạng thái \delivered\.

**Các bước tái hiện (Steps to Reproduce):**
1. Đăng nhập bằng tài khoản Admin để lấy Token hợp lệ.
2. Cập nhật trạng thái một đơn hàng thành \canceled\ (VD gọi \PUT /api/admin/orders/1/status\ với body \{\
status\: \canceled\}\).
3. Gửi tiếp một request cập nhật trạng thái đơn hàng đó thành \delivered\ (\{\status\: \delivered\}\).
4. Quan sát kết quả.

**Kết quả mong đợi (Expected Result):**
Hệ thống phải trả về \400 Bad Request\ kèm thông báo lỗi *Không
thể
cập
nhật
đơn
hàng
đã
hủy*.

**Kết quả thực tế (Actual Result):**
Hệ thống trả về \200 OK\ và thông báo \{\message\:\Order
status
updated\}\. Đơn hàng chuyển sang \delivered\ bất hợp pháp.

**Test Case liên quan:** 
- TC_ORD_040, TC_ORD_037

**Link GitHub Issue:** 
👉 *[Sinh viên copy nội dung này tạo Issue trên GitHub và dán link vào đây]*
