# BỘ TEST CASE — MODULE LOGIN | PERFEX CRM

| Thông tin | Chi tiết |
|-----------|----------|
| **Dự án** | Perfex CRM - Anh Tester Demo |
| **Module** | Login |
| **Tổng TC** | 38 |
| **Ngày tạo** | 2026-05-15 |

---

## 1. Đăng nhập — Happy Path

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_001 | Login | Đăng nhập thành công với email và password đúng | 1. Truy cập /admin/authentication · 2. Nhập Email: admin@demo.anhtester.com · 3. Nhập Password: Test@12345 · 4. Click nút "Login" | Chuyển hướng đến /admin/ (Dashboard). Trang hiển thị tiêu đề "Dashboard" |
| CRM_LOGIN_TC_002 | Login | Đăng nhập thành công + Remember me duy trì phiên 7 ngày | 1. Truy cập /admin/authentication · 2. Nhập Email: admin@demo.anhtester.com · 3. Nhập Password: Test@12345 · 4. Tick checkbox "Remember me" · 5. Click "Login" · 6. Đóng trình duyệt hoàn toàn · 7. Mở lại trình duyệt và truy cập /admin/ | Bước 5: Chuyển đến Dashboard. Bước 7: Vẫn đăng nhập, không yêu cầu login lại |
| CRM_LOGIN_TC_003 | Login | Đăng nhập bằng phím Enter thay vì click nút Login | 1. Truy cập /admin/authentication · 2. Nhập Email: admin@demo.anhtester.com · 3. Nhập Password: Test@12345 · 4. Nhấn phím Enter | Chuyển hướng đến Dashboard |

---

## 2. Đăng nhập — Validation trường trống

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_004 | Login | Để trống cả Email và Password | 1. Truy cập /admin/authentication · 2. Không nhập gì vào Email và Password · 3. Click "Login" | Hiển thị 2 thông báo "Trường bắt buộc nhập." trong div.alert-danger. Vẫn ở trang Login |
| CRM_LOGIN_TC_005 | Login | Để trống Email và nhập Password | 1. Để trống Email · 2. Nhập Password: Test@12345 · 3. Click "Login" | Hiển thị "Trường bắt buộc nhập." cho trường Email |
| CRM_LOGIN_TC_006 | Login | Nhập Email và để trống Password | 1. Nhập Email: admin@demo.anhtester.com · 2. Để trống Password · 3. Click "Login" | Hiển thị "Trường bắt buộc nhập." cho trường Password |

---

## 3. Đăng nhập — Validation định dạng Email (Equivalence Partitioning)

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_007 | Login | Email thiếu ký tự @ | 1. Nhập Email: admindemo.anhtester.com · 2. Nhập Password: Test@12345 · 3. Click "Login" | Trình duyệt chặn form, hiển thị HTML5 tooltip: "Vui lòng nhập địa chỉ email hợp lệ." |
| CRM_LOGIN_TC_008 | Login | Email có 2 ký tự @ | 1. Nhập Email: admin@@demo.anhtester.com · 2. Nhập Password: Test@12345 · 3. Click "Login" | HTML5 tooltip: "Vui lòng nhập địa chỉ email hợp lệ." |
| CRM_LOGIN_TC_009 | Login | Email có khoảng trắng ở đầu | 1. Nhập Email: " admin@demo.anhtester.com" (có 1 space ở đầu) · 2. Nhập Password: Test@12345 · 3. Click "Login" | HTML5 tooltip hoặc server báo lỗi validation |
| CRM_LOGIN_TC_010 | Login | Email có khoảng trắng ở giữa | 1. Nhập Email: "admin @demo.anhtester.com" · 2. Nhập Password: Test@12345 · 3. Click "Login" | HTML5 tooltip: "Vui lòng nhập địa chỉ email hợp lệ." |
| CRM_LOGIN_TC_011 | Login | Email có khoảng trắng ở cuối | 1. Nhập Email: "admin@demo.anhtester.com " (có 1 space cuối) · 2. Nhập Password: Test@12345 · 3. Click "Login" | HTML5 tooltip hoặc server báo lỗi validation |
| CRM_LOGIN_TC_012 | Login | Email có dấu chấm ở cuối tên miền | 1. Nhập Email: admin@demo.anhtester.com. · 2. Nhập Password: Test@12345 · 3. Click "Login" | HTML5 tooltip: "Vui lòng nhập địa chỉ email hợp lệ." |
| CRM_LOGIN_TC_013 | Login | Email có 2 dấu chấm liên tiếp trong domain | 1. Nhập Email: admin@demo..anhtester.com · 2. Nhập Password: Test@12345 · 3. Click "Login" | HTML5 tooltip: "Vui lòng nhập địa chỉ email hợp lệ." |

---

## 4. Đăng nhập — Giá trị biên Email (Boundary Value Analysis)

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_014 | Login | Email đúng 160 ký tự (max boundary) | 1. Nhập Email 160 ký tự: aaaa...aaa@demo.anhtester.com (139 chữ 'a' + @demo.anhtester.com = 160 ký tự) · 2. Nhập Password: Test@12345 · 3. Click "Login" | Server chấp nhận và xử lý. Hiển thị "Email hoặc Password không đúng." (vì email không tồn tại) |
| CRM_LOGIN_TC_015 | Login | Email 161 ký tự vượt giới hạn max+1 | 1. Nhập Email 161 ký tự: aaaa...aaa@demo.anhtester.com (140 chữ 'a' + @demo.anhtester.com = 161 ký tự) · 2. Nhập Password: Test@12345 · 3. Click "Login" | Hệ thống từ chối: hiển thị thông báo lỗi vượt quá độ dài cho phép hoặc cắt bớt ký tự |

---

## 5. Đăng nhập — Sai thông tin đăng nhập (Equivalence Partitioning)

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_016 | Login | Email đúng và password sai | 1. Nhập Email: admin@demo.anhtester.com · 2. Nhập Password: WrongPass!999 · 3. Click "Login" | Hiển thị "Email hoặc Password không đúng." trong div.alert-danger |
| CRM_LOGIN_TC_017 | Login | Email không tồn tại trong hệ thống | 1. Nhập Email: nonexist_user@demo.anhtester.com · 2. Nhập Password: Test@12345 · 3. Click "Login" | Hiển thị "Email hoặc Password không đúng." (không tiết lộ email có tồn tại hay không) |
| CRM_LOGIN_TC_018 | Login | Password đúng nội dung nhưng sai chữ hoa/thường | 1. Nhập Email: admin@demo.anhtester.com · 2. Nhập Password: test@12345 (chữ 't' thường thay vì 'T' hoa) · 3. Click "Login" | Hiển thị "Email hoặc Password không đúng." |

---

## 6. Bảo mật — CAPTCHA & Khóa tài khoản (State Transition)

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_019 | Login | Đăng nhập sai 3 lần liên tiếp — chưa hiện CAPTCHA | 1. Nhập Email: admin@demo.anhtester.com + Password: Wrong111 → Click Login · 2. Nhập Email: admin@demo.anhtester.com + Password: Wrong222 → Click Login · 3. Nhập Email: admin@demo.anhtester.com + Password: Wrong333 → Click Login | Mỗi lần hiển thị "Email hoặc Password không đúng." CAPTCHA chưa xuất hiện |
| CRM_LOGIN_TC_020 | Login | Đăng nhập sai lần thứ 4 — reCAPTCHA xuất hiện | 1. Đã sai 3 lần liên tiếp (Pre-condition) · 2. Nhập Email: admin@demo.anhtester.com · 3. Nhập Password: Wrong444 · 4. Click "Login" | reCAPTCHA xuất hiện trên form Login. Hiển thị "Email hoặc Password không đúng." |
| CRM_LOGIN_TC_021 | Login | CAPTCHA reset sau đăng nhập thành công | 1. Đăng nhập sai 4 lần (CAPTCHA đã hiện) · 2. Nhập đúng Email: admin@demo.anhtester.com + Password: Test@12345 + vượt CAPTCHA → Login · 3. Logout · 4. Nhập Email: admin@demo.anhtester.com + Password: WrongAgain1 → Click Login | Bước 2: Vào Dashboard. Bước 4: Hiển thị lỗi, CAPTCHA chưa xuất hiện (đã reset về 0) |
| CRM_LOGIN_TC_022 | Login | Đăng nhập sai 10 lần liên tiếp — tài khoản bị khóa | 1. Đăng nhập sai liên tiếp 10 lần (vượt CAPTCHA mỗi lần từ lần 4) · Email: admin@demo.anhtester.com · Password lần lượt: Wrong001 đến Wrong010 | Lần thứ 10: Tài khoản bị khóa. Thông báo "Tài khoản đã bị khóa. Vui lòng liên hệ Admin." |
| CRM_LOGIN_TC_023 | Login | Đăng nhập vào tài khoản đã bị khóa bằng đúng password | 1. Nhập Email: locked_user@demo.anhtester.com · 2. Nhập Password: Test@12345 · 3. Click "Login" | Từ chối đăng nhập. Thông báo tài khoản đã bị khóa, yêu cầu liên hệ Admin |

---

## 7. Bảo mật — Injection & CSRF

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_024 | Login | SQL Injection vào trường Email | 1. Nhập Email: ' OR 1=1 -- · 2. Nhập Password: anything · 3. Click "Login" | Hệ thống chặn, không bypass authentication. Không lỗi 500. Hiển thị lỗi validation hoặc "Email hoặc Password không đúng." |
| CRM_LOGIN_TC_025 | Login | XSS script vào trường Email | 1. Nhập Email: `<script>alert('XSS')</script>` · 2. Nhập Password: anything · 3. Click "Login" | Hệ thống escape/encode input. Không thực thi script. Hiển thị lỗi validation |
| CRM_LOGIN_TC_026 | Login | Submit form khi thiếu CSRF token | 1. Mở DevTools · 2. Xóa/sửa trường hidden csrf_token_name thành "invalid" · 3. Nhập Email: admin@demo.anhtester.com · 4. Nhập Password: Test@12345 · 5. Click "Login" | Server từ chối request (403 Forbidden hoặc thông báo lỗi CSRF). Không đăng nhập được |

---

## 8. UI/UX & Session

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_027 | Login | Password hiển thị dạng masked và toggle hiện/ẩn | 1. Nhập Password: Test@12345 · 2. Quan sát hiển thị · 3. Click nút toggle (hiện password) · 4. Click toggle lần nữa (ẩn password) | Bước 2: Ký tự hiển thị dạng ●●●●●●●●●. Bước 3: Hiển thị rõ "Test@12345". Bước 4: Quay lại dạng masked |
| CRM_LOGIN_TC_028 | Login | Kiểm tra placeholder của Email và Password | 1. Truy cập /admin/authentication · 2. Quan sát placeholder của trường Email · 3. Quan sát placeholder của trường Password | Email có placeholder "Email". Password có placeholder "Password" |
| CRM_LOGIN_TC_029 | Login | CSRF token tồn tại trong form HTML | 1. Truy cập /admin/authentication · 2. Mở DevTools → tab Elements · 3. Tìm trường hidden name="csrf_token_name" | Trường hidden tồn tại với value không rỗng. Value thay đổi mỗi lần tải trang |
| CRM_LOGIN_TC_030 | Login | Nhấn Back trên trình duyệt sau đăng nhập thành công | 1. Nhập Email: admin@demo.anhtester.com · 2. Nhập Password: Test@12345 · 3. Click "Login" → vào Dashboard · 4. Nhấn nút Back trên trình duyệt | Tự động redirect về Dashboard (không hiện lại form Login với dữ liệu cũ). Phiên vẫn active |

---

## 9. Khôi phục mật khẩu (Forgot Password)

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_031 | Forgot Password | Click link Forgot Password từ trang Login | 1. Truy cập /admin/authentication · 2. Click link "Forgot Password?" | Chuyển đến /admin/authentication/forgot_password. Hiển thị form với trường Email và nút Confirm |
| CRM_LOGIN_TC_032 | Forgot Password | Gửi email khôi phục thành công | 1. Truy cập trang Forgot Password · 2. Nhập Email: admin@demo.anhtester.com · 3. Click "Confirm" | Hiển thị thông báo thành công. Email khôi phục được gửi đến admin@demo.anhtester.com |
| CRM_LOGIN_TC_033 | Forgot Password | Để trống email trên trang Forgot Password | 1. Truy cập trang Forgot Password · 2. Không nhập Email · 3. Click "Confirm" | HTML5 validation: "Vui lòng điền vào trường này." (trường có attribute required) |
| CRM_LOGIN_TC_034 | Forgot Password | Nhập email không tồn tại trong hệ thống | 1. Truy cập trang Forgot Password · 2. Nhập Email: nonexist_user@demo.anhtester.com · 3. Click "Confirm" | Hiển thị thông báo: "Email không tồn tại" |
| CRM_LOGIN_TC_035 | Forgot Password | Rate limit — gửi quá 3 lần trong 15 phút | 1. Truy cập trang Forgot Password · 2. Nhập Email: admin@demo.anhtester.com → Click Confirm (lặp 4 lần trong 15 phút) | Lần 1-3: Gửi thành công. Lần 4: "Bạn đã gửi quá nhiều yêu cầu. Vui lòng thử lại sau." |
| CRM_LOGIN_TC_036 | Forgot Password | Link reset password còn hiệu lực trong vòng 1 giờ | 1. Gửi yêu cầu khôi phục cho Email: admin@demo.anhtester.com · 2. Mở email nhận được · 3. Click link reset (trong vòng 1 giờ) | Chuyển đến trang đặt mật khẩu mới. Form hoạt động bình thường |
| CRM_LOGIN_TC_037 | Forgot Password | Link reset password hết hạn sau 1 giờ | 1. Gửi yêu cầu khôi phục cho Email: admin@demo.anhtester.com · 2. Chờ hơn 1 giờ · 3. Click link trong email | Thông báo "Link khôi phục đã hết hạn." Không cho phép đặt mật khẩu mới |

---

## 10. Social Login

| TC ID | Module | Test Scenario | Test Steps | Expected Result |
|-------|--------|---------------|------------|-----------------|
| CRM_LOGIN_TC_038 | Login | Đăng nhập bằng Google (Social Login/SSO) | 1. Truy cập trang Login · 2. Click nút "Đăng nhập bằng Google" · 3. Chọn tài khoản Google: tester.crm@gmail.com · 4. Xác nhận quyền truy cập | Đăng nhập thành công, chuyển đến Dashboard |
