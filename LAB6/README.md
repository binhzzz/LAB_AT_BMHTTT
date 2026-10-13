# LAB 6: Triển khai Active Directory, LDAP Authentication, Captive Portal và Firewall Rules nâng cao trên pfSense

Repository này chứa tài liệu, câu trả lời và báo cáo thực hành cho **LAB 6** môn An toàn hệ thống thông tin.

## 📁 Cấu trúc thư mục
- `11_CNPM1_LAB6_1150080005_...`: Báo cáo chi tiết quá trình thực hiện bài tập thực hành.
- `README.md`: Tài liệu hướng dẫn và tổng quan nội dung lab.

## 🛠️ Nội dung chính & Các kịch bản cấu hình
1. **Phân đoạn mạng và Topology**: Thiết lập hệ thống mạng phân đoạn (WAN, LAN, MGMT, DMZ) tích hợp máy chủ Active Directory (AD).
2. **Tích hợp LDAP Authentication**: Cấu hình pfSense kết nối với Active Directory sử dụng Service Account và cơ chế tìm kiếm *Entire Subtree* để xác thực người dùng.
3. **Captive Portal & WebGUI Security**: 
   - Đặt Captive Portal trên phân vùng LAN để kiểm soát truy cập Internet.
   - Tách biệt hoàn toàn giao diện quản trị WebGUI sang mạng quản lý riêng (`MGMT` / `VMnet1`) nhằm cô lập và bảo mật hệ thống.
4. **Firewall Rules & Traffic Management**:
   - Thiết lập các quy tắc lọc lưu lượng dựa trên nguyên tắc ưu tiên (First-match).
   - Áp dụng Schedule cho các rule truy cập (ví dụ: Kịch bản chặn mạng xã hội ngoài giờ cho phép).
   - Xử lý trạng thái kết nối với Stateful Inspection và State Table Reset.

---
*Thực hiện bởi: Nguyễn Hữu Bình - MSSV: 1150080005*
