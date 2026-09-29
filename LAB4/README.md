# LAB 4: Network Surface Exploration and Evaluation with Nmap

## 📋 Thông tin sinh viên
* **Họ và tên:** Nguyễn Hữu Bình
* **Mã số sinh viên:** 1150080005
* **Lớp / Môn học:** An toàn hệ thống thông tin (CNPM)

---

## 🛠️ Mô hình và Môi trường thực hành
Bài thực hành được xây dựng trên môi trường ảo hóa **VMware Workstation** sử dụng mạng nội bộ **Host-Only (`VMnet1`)** để đảm bảo an toàn và tính cô lập.

### Bảng thông tin cấu hình IP mạng thực tế
| Thiết bị | Địa chỉ IP thực tế | Subnet Mask | Ghi chú |
| :--- | :--- | :--- | :--- |
| **Windows Host** | `192.168.56.1` | `255.255.255.0` | VMware Host-Only adapter (`VMnet1`) |
| **Kali VM** | `192.168.56.128` | `255.255.255.0` | Máy quét (Scanner) |
| **Windows 10 x64** | `192.168.56.101` | `255.255.255.0` | Máy đích (Target) |

---

## 🚀 Các bước thực hiện chính

### 1. Cấu hình mạng và kiểm tra kết nối
* **Kiểm tra card mạng trên Kali Linux:** Sử dụng lệnh `ip -br addr` để xác nhận card `eth0` thuộc dải mạng `192.168.56.0/24`.
* **Kiểm tra kết nối thông mạng (Ping):** Thực hiện lệnh `ping -c 4 192.168.56.101` từ Kali Linux sang máy đích Windows 10, kết quả đạt tỷ lệ phản hồi thành công (`0% packet loss`).

### 2. Quét cổng và nhận diện dịch vụ bằng Nmap
* **Quét ban đầu (Khi chưa tắt tường lửa):** Chạy lệnh `nmap -sV 192.168.56.101`, các cổng đều hiển thị ở trạng thái `filtered` do cơ chế bảo vệ của Windows Defender Firewall trên máy đích.
* **Quét sau khi tắt tường lửa:** Sau khi vô hiệu hóa Windows Defender Firewall trên Windows 10, thực hiện các lệnh quét chuyên sâu:
  * **Quét SYN Stealth (`sudo nmap -sS`):** Giúp rà quét các cổng TCP mở mà bắt tay không hoàn toàn, hạn chế bị ghi log ở mức ứng dụng.
  * **Nhận diện Hệ điều hành (`sudo nmap -O`):** Xác định chính xác phiên bản hệ điều hành của máy mục tiêu.

---

## 📊 Kết quả quét Nmap trên máy đích (Windows 10)

Các cổng dịch vụ đang mở (`open`) được ghi nhận:
* **Port 135/tcp** (`msrpc` - Microsoft RPC)
* **Port 139/tcp** (`netbios-ssn` - NetBIOS Session Service)
* **Port 445/tcp** (`microsoft-ds` - SMB / Active Directory)

**Thông tin nhận diện Hệ điều hành (OS Detection):**
* **Device type:** `general purpose`
* **Running:** `Microsoft Windows 10`
* **OS details:** `Microsoft Windows 10 1709 - 22H2`
* **Network Distance:** `1 hop`

---
*Báo cáo hoàn thành phục vụ cho việc nộp bài thực hành LAB 4.*
