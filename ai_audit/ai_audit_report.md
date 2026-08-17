# AI Audit Report — Mẫu 5 mục cho mỗi Artifact

*Phụ lục bắt buộc đính kèm cho mọi bài tập có dùng AI (HW#01–HW#06, Seminar).*
*Tài liệu được biên soạn lại từ Med Kharbach, PhD (2026) — Mẫu Chính sách Sử dụng AI cho Giáo dục Đại học.*
*Giấy phép CC BY-NC-SA 4.0. Phiên bản này được FIT@HCMUS điều chỉnh cho môn CS423 / CSC15003 Kiểm chứng Phần mềm.*

---

## 1. Thông tin Sinh viên

| Mục | Giá trị |
| :--- | :--- |
| **Họ tên sinh viên (in hoa):** |HỒ GIA HUY |
| **MSSV:** | 23127376 |
| **Lớp / Khoá:** |23KTPM2 / 23CLC |
| **Mã bài tập (ví dụ HW#00, HW#02):** |HW06 |
| **Ngày làm bài:** |17/08/2026 |
| **Công cụ AI đã dùng:** | Antigravity |
| **Công cụ AI đã dùng:** | `[X] Có`  `[] Không` |

---

## 2. Hướng dẫn (đọc trước khi điền)
* Thêm 1 hàng cho mỗi artifact AI sinh (test case, script, checklist, OpenAPI spec, JMeter plan…).
* Dán nguyên văn prompt — **KHÔNG** paraphrase.
* Dán nguyên văn output AI (hoặc kèm screenshot có chú thích trong báo cáo).
* Gắn nhãn: `VALID` / `INVALID` / `INCOMPLETE`.
* Lý do phải dẫn chiếu slide, mục ISTQB, hoặc RFC kỹ thuật.
* Hiển thị bản sửa với phần thay đổi được tô sáng.
* *Hàng mẫu in nghiêng — thay trước khi nộp.*

---

## 3. Bảng Audit — 1 hàng / artifact

| (1) Prompt + Công cụ | (2) Output AI | (3) Verdict | (4) Lý do (ISTQB) | (5) Bản SV sửa |
| :--- | :--- | :--- | :--- | :--- |
| **Artifact #1**<br>**Thời gian:** 2026-08-17 17:46:25 UTC+7<br>**Công cụ:** Antigravity (Gemini 3.6 Flash)<br>**Prompt:**<br>*"Đọc và phân tích HW06 sau đó hãy xây dựng cây thư mục cấu trúc bài nộp"* | Phân tích đề bài HW06, tự động sinh khung cây thư mục bài nộp (`reports/`, `postman/`, `test_cases/`, `agent_skill/`, `api_spec/`, `bugs/`, `ai_audit/`, `.github/`) và khởi tạo file `README.md`. Trong `README.md` ban đầu hiển thị đường dẫn tuyệt đối dạng `file:///c:/Users/...`. | `INCOMPLETE` | **ISTQB Test Organization & Quality Attributes (Portability):** Theo Section 14 đề bài HW06, cấu trúc bài nộp gói trong file zip phải mang tính tương đối (relative) và dễ di động. Việc AI xuất đường dẫn tuyệt đối local (`file:///c:/...`) khiến liên kết bị hỏng khi chấm bài trên môi trường khác. | Phản hồi yêu cầu AI điều chỉnh lại Section 3 trong `README.md`, vẽ lại sơ đồ cây thư mục tương đối dạng ASCII Tree (`<StudentID>_HW06_AI_API_<SelfAssessedGrade>/`) loại bỏ path cố định. |
| **Artifact #2**<br>**Thời gian:** 2026-08-17 17:48:38 UTC+7<br>**Công cụ:** Antigravity (Gemini 3.6 Flash)<br>**Prompt:**<br>*"tại readme.md cấu trúc bài nộp nên vẽ ra thành cây thư mục không dùng path cố định"* | Cập nhật Section 3 trong `README.md` thành sơ đồ cây thư mục trực quan dạng ASCII Tree dạng tương đối `<StudentID>_HW06_AI_API_<SelfAssessedGrade>/`, loại bỏ hoàn toàn các đường dẫn tuyệt đối local `file:///c:/...`. | `VALID` | **ISTQB Test Documentation Standards:** Sơ đồ cây thư mục ASCII Tree biểu diễn trực quan, chính xác cấu trúc gói bài nộp tương đối theo đúng quy định Section 14, đảm bảo tính di động và dễ rà soát khi chấm bài. | Chấp nhận và giữ nguyên bản sửa của AI (dùng trực tiếp). |

---

## 4. Tổng kết Độ chính xác AI

| Chỉ số | Số lượng | Tỉ lệ |
| :--- | :---: | :---: |
| **Tổng artifact AI sinh đã audit** | 2 | 100% |
| **VALID** *(đúng, dùng nguyên)* | 1 | 50% |
| **INVALID** *(sai; loại bỏ)* | 0 | 0% |
| **INCOMPLETE** *(chấp nhận sau khi sửa)* | 1 | 50% |

---

## 5. Kết luận — Khi nào nên / không nên dùng AI?

AI (Antigravity) thể hiện khả năng phân tích yêu cầu đề bài kiểm thử API (HW06) rất nhanh chóng và thiết lập khung thư mục bài nộp bao phủ đầy đủ các thành phần deliverables (báo cáo, test cases, Postman, CI/CD, agent skill, AI audit log). Tuy nhiên, ở lượt prompt đầu tiên (Artifact #1), AI có khuynh hướng chèn các đường dẫn tuyệt đối local (`file:///c:/...`) vào tài liệu Markdown (`INCOMPLETE`). Khi sinh viên chủ động rà soát (human audit) và phát prompt định hướng lại (Artifact #2), AI đã xuất ra sơ đồ cây thư mục tương đối di động (ASCII Tree) chính xác và đạt chuẩn (`VALID`).

---

## 6. Mandatory Disclosure (dán nguyên văn)

> "Cấu trúc cây thư mục bài nộp và tài liệu khởi tạo này được sinh phiên bản đầu bởi Antigravity (Gemini 3.6 Flash); tôi đã rà soát và chỉnh sửa phần hiển thị cây thư mục tương đối trong README.md, loại bỏ absolute paths; phần thông tin sinh viên và bảng tự đánh giá do tôi tự điền. AI Audit Report chi tiết đính kèm ở Phụ lục A. Tôi cam đoan không dùng AI để sinh bất kỳ artifact nào thuộc danh mục bị cấm."

**Chữ ký:**

| | |
| :--- | :--- |
| **Họ tên sinh viên (in hoa):** |HỒ GIA HUY |
| **MSSV:** |23127376 |
| **Lớp / Khoá:** |23KTPM2 / 23CLC |
| **Môn học:** | CS423 / CSC13003 – Kiểm chứng Phần mềm |
| **Giảng viên:** |LÂM QUANG VŨ |
| **Ngày:** |17/08/2026 |
| **Chữ ký:** |Hồ Gia Huy |

---

## Tham khảo
* Kharbach, M. (2026). AI Use Policy Templates for Higher Education. CC BY-NC-SA 4.0.
* ISTQB Foundation Level Syllabus (latest version).
* Hardman, P. (2025). A Post-AI Learning Taxonomy.
* Fuster Rabella, M. (2025). OECD Education Working Paper No. 338.
* Perkins, M., Roe, J., & Furze, L. (2025). AI Assessment Scale.
* Anthropic (2025). Building reliable AI test agents — engineering blog.
* DeepEval & Promptfoo documentation — testing frameworks for LLM systems.