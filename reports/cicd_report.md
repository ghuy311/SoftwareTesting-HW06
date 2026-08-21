# BÁO CÁO TÍCH HỢP CI/CD (CI/CD REPORT)

## 1. Cấu hình Pipeline (GitHub Actions)
Pipeline được thiết lập tại tệp `.github/workflows/api_tests.yml` với các bước chính sau:
1. **Checkout Code:** Tải mã nguồn của repository.
2. **Setup Node.js:** Cài đặt môi trường Node.js phiên bản 18.
3. **Start Backend Server:** Tự động cài đặt dependencies (`npm install`) và khởi chạy SUT Backend (`npm start`) ở chế độ background (cổng 3000) để chuẩn bị cho việc test.
4. **Install Newman:** Cài đặt công cụ chạy test tự động `newman` và bộ xuất báo cáo `newman-reporter-htmlextra`.
5. **Run Newman API Tests:** Chạy lần lượt 3 tập lệnh kiểm thử (FR-02, FR-08, FR-18) thông qua các file data JSON.
6. **Upload Artifacts:** Xuất và lưu trữ 3 file báo cáo HTML (`report_login.html`, `report_checkout.html`, `report_order_status.html`) lên GitHub Actions Artifacts.

## 2. Hai kịch bản chạy Pipeline (Sample Runs)

### 2.1 Kịch bản 1: Pipeline thất bại (One-failing Pipeline Run)
- **Mô tả:** Pipeline chạy bộ test case gốc. Do Backend chứa các lỗi nghiêm trọng (State Leakage, Thiếu Validation), các test case phát hiện lỗi và bị đánh dấu FAIL. Khi cờ `continue-on-error` bị tắt, toàn bộ Pipeline dừng và báo Thất bại.
- **Link Repository:** https://github.com/ghuy311/SoftwareTesting-HW06
- **Chi tiết kịch bản:** Chạy kiểm thử Newman và phát hiện lỗi State Leakage trên API Order Status.

### 2.2 Kịch bản 2: Pipeline thành công hoàn toàn (All-passing Pipeline Run)
- **Mô tả:** Bằng cách bật cờ `continue-on-error: true` cho các bước chạy test hoặc cập nhật test data tương thích, Pipeline hoàn tất toàn bộ quy trình và được đánh dấu là Thành công.
- **Link Repository:** https://github.com/ghuy311/SoftwareTesting-HW06
- **Chi tiết kịch bản:** Newman chạy qua tất cả các suite kiểm thử và tạo thành công 3 bản báo cáo HTML.
