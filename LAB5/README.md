# LAB 5: Cài đặt và Cấu hình pfSense Firewall

* **Họ và tên:** Nguyễn Hữu Bình
* **Mã sinh viên:** 1150080005
* **Lớp / Môn học:** LAB_AT_BMHTTT (An toàn và Bảo mật hệ thống thông tin)
* **Thư mục bài làm:** `LAB5/`

---

## 📋 Nội dung thư mục
* `11_CNPM1_LAB5_1150080005_NguyenHuuBinh.docx`: Báo cáo chi tiết quá trình thực hành kèm hình ảnh minh chứng.
* `README.md`: Tài liệu tóm tắt nội dung bài lab và các câu hỏi ôn tập.

---

## 🛠️ Tổng quan bài thực hành pfSense Firewall
1. **Môi trường ảo hóa:** VMware Workstation Pro.
2. **Cấu hình giao diện mạng (Interfaces):**
   * **WAN (`em0`):** Nhận IP động qua DHCP từ mạng máy thật / NAT.
   * **LAN (`em1`):** Cấu hình IP tĩnh `10.0.0.1/8` kết nối nội bộ với máy trạm Client (Windows 10 qua mạng `VMnet1`).
3. **Truy cập trang quản trị web (WebConfigurator):**
   * Địa chỉ: `https://10.0.0.1`
   * Tài khoản mặc định: `admin` / `pfsense`
4. **Setup Wizard (9 bước):** Cấu hình thông tin tổng quan, múi giờ (`Asia/Ho_Chi_Minh`), xác thực giao diện WAN/LAN, đổi mật khẩu quản trị và hoàn tất (`Wizard completed`) để vào giao diện **Dashboard**.

---

## 💡 Giải đáp câu hỏi ôn tập / báo cáo

### 1. Phân biệt vai trò của NAT và firewall rule trong mô hình.
* **NAT (Network Address Translation):** Chuyển đổi địa chỉ IP/cổng để chia sẻ kết nối Internet hoặc ánh xạ cổng dịch vụ từ ngoài vào trong mạng nội bộ.
* **Firewall Rule:** Kiểm soát truy cập, quyết định cho phép (`Pass`) hoặc chặn (`Block`) các gói tin dựa trên IP, cổng (port) và giao thức để bảo mật hệ thống.

### 2. Vì sao nên tách máy chủ Web/Mail/FTP vào DMZ thay vì đặt trong LAN?
* Giúp cô lập các dịch vụ công khai Internet. Nếu máy chủ bị tấn công, hacker chỉ chiếm được vùng đệm DMZ, không xâm nhập được vào mạng LAN nội bộ chứa dữ liệu nhạy cảm.

### 3. Nếu rule Block nằm dưới một rule Pass tổng quát thì kết quả có thể như thế nào?
* Tường lửa xử lý luật theo cơ chế **First-Match** (từ trên xuống dưới). Gói tin sẽ khớp với rule `Pass` tổng quát ở phía trên và được cho phép đi qua, khiến rule `Block` phía dưới bị vô hiệu lực.

### 4. Muốn chặn ping nhưng vẫn cho truy cập web, cần cấu hình các rule nào?
* Đặt rule `Block` giao thức `ICMP` ở phía trên, và đặt rule `Pass` cho cổng TCP `80` (HTTP) và `443` (HTTPS) ở phía dưới.

### 5. Logging của firewall giúp ích gì trong xử lý sự cố?
* Cung cấp thông tin chi tiết về các kết nối bị chặn hoặc cho phép (IP, port, thời gian), giúp quản trị viên truy vết lỗi, phát hiện sự cố và nhận diện tấn công kịp thời.

### 6. Nêu ít nhất ba biện pháp hardening cho pfSense trong mô hình này.
1. Đổi mật khẩu tài khoản quản trị mặc định và vô hiệu hóa/đổi cổng SSH.
2. Bắt buộc sử dụng giao thức HTTPS và giới hạn dải IP được phép truy cập trang quản trị web.
3. Cấu hình luật tường lửa nghiêm ngặt (Strict Firewall Rules) ở vùng WAN và tắt các dịch vụ chẩn đoán không cần thiết
