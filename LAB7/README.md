# LAB 7
## XÂY DỰNG CHÍNH SÁCH WEB PROTECTION TRÊN MÔ HÌNH pfSense + WEB PROXY

## 1. THÔNG TIN SINH VIÊN
* **Họ và tên:** Nguyễn Hữu Bình
* **Mã số sinh viên (MSSV):** 1150080005
* **Lớp:** 11_CNPM1
* **Tên bài thực hành:** LAB 7 – Xây dựng chính sách Web Protection trên mô hình pfSense + Web Proxy (E2Guardian + Squid + ClamAV)

---

## 2. TỔNG QUAN KIẾN TRÚC VÀ MÔ HÌNH

Bài thực hành tập trung vào việc thiết kế và xây dựng hệ thống kiểm soát nội dung web (Web Protection) ở tầng ứng dụng (L7), tách biệt rõ ràng với tầng firewall lọc gói tin (L3/L4):
* **pfSense Firewall:** Đóng vai trò làm Gateway/Firewall chính, kiểm soát định tuyến, cấp phát, chặn các kết nối trực tiếp (chống bypass qua cổng 80/443) và chuyển hướng luồng web.
* **WEB-PROXY (Ubuntu Server 24.04 LTS - IP: `10.6.0.30`):** Chạy dịch vụ **E2Guardian** (`:8080`) làm điểm tiếp nhận request từ client, kết hợp với **Squid** (`127.0.0.1:3128`) làm upstream proxy và tích hợp **ClamAV** để quét mã độc/virus khi tải file.
* **DMZ-WEB (IP: `172.16.6.10`):** Máy chủ mô phỏng các website kiểm thử với nhiều nhóm chính sách khác nhau (Normal, Geo-Sim China/Middle East, Job Search, Weapons/Politics/Religion, Education, Entertainment/Games, Streaming, Download/EICAR).

---

## 3. CÁC BƯỚC THỰC HIỆN VÀ CẤU HÌNH CHÍNH

### A. Chuẩn bị WEB-PROXY và Website mô phỏng
1. Cài đặt các gói phần mềm bắt buộc trên Ubuntu Server (`10.6.0.30`):
   ```bash
   sudo apt update
   sudo apt install -y squid e2guardian clamav clamav-daemon curl openssl
