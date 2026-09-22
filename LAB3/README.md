# BÁO CÁO THỰC HÀNH LAB 3: AN TOÀN VÀ BẢO MẬT HỆ THỐNG THÔNG TIN

## 1. THÔNG TIN SINH VIÊN
* **Họ và tên:** Nguyễn Hữu Bình
* **Mã số sinh viên (MSSV):** 1150080005
* **Lớp:** 11_CNPM1
* **Tên bài thực hành:** LAB 3 – Phân tích lỗ hổng, kiểm soát truy cập và phòng chống tấn công hệ thống
* **Link Video thuyết minh:** https://youtu.be/mGagW-wfEGE

---

## 2. PHIÊN BẢN MÔI TRƯỜNG THỰC HÀNH
* **Nền tảng ảo hóa:** VMware Workstation Pro
* **Hệ điều hành máy ảo (Guest OS):** Windows Server 2025 Standard Evaluation (Version 24H2, OS Build 26100.32230)
* **Cấu hình mạng:** Host-Only (Cô lập an toàn, không kết nối mạng ra ngoài)
* **Công cụ sử dụng:** Windows PowerShell, Event Viewer, Task Scheduler, System.Net.HttpListener, Curl

---

## 3. CÁCH DỰNG VÀ THIẾT LẬP MÔI TRƯỜNG
1. Khởi tạo máy ảo Windows Server 2025 trên VMware Workstation với cấu hình mạng Host-Only.
2. Thiết lập thư mục lưu trữ tài nguyên và bằng chứng số: `C:\LAB3\lab3_assets` và `C:\LAB3\Evidence`.
3. Kiểm tra và kích hoạt Baseline hệ thống ban đầu:
   - Microsoft Defender Antivirus: Kích hoạt chế độ Real-time Protection (`Enabled: True`).
   - Windows Firewall: Kích hoạt bảo vệ trên cả 3 Profile (Domain, Private, Public).
4. Thiết lập chính sách kiểm toán xác thực thông qua lệnh:
   ```cmd
   auditpol /set /subcategory:"Logon" /success:enable /failure:enable
