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
