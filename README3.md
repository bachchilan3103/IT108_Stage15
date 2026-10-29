# THIẾT KẾ HYBRID WORKFLOW VÀ TỐI ƯU ĐỒNG BỘ LOCAL – CLOUD

## 1. Báo cáo phân tích luồng dữ liệu I/O

Mô hình Hybrid Workflow cho phép lập trình viên làm việc trực tiếp trên SSD Local để đạt tốc độ xử lý nhanh, đồng thời đồng bộ source code quan trọng lên Cloud để dự phòng khi xảy ra sự cố.

### Luồng dữ liệu từ Ctrl + S đến khi xuất hiện tích xanh

1. **Ghi dữ liệu Local:** Khi nhấn `Ctrl + S`, trình soạn thảo lưu nội dung mới vào file trên SSD của máy tính.
2. **Phát hiện thay đổi:** Phần mềm Cloud Sync phát hiện file vừa được chỉnh sửa trong thư mục đồng bộ.
3. **Kiểm tra và đồng bộ:** Phần mềm kiểm tra thay đổi rồi tải dữ liệu mới lên Cloud thông qua Internet.
4. **Xác nhận hoàn tất:** Sau khi đồng bộ thành công, biểu tượng tích xanh xuất hiện trên file để báo trạng thái theo quy ước của dịch vụ đang sử dụng.

Lưu ý: Nhấn `Ctrl + S` chỉ lưu file trên máy tính, không có nghĩa dữ liệu đã được tải lên Cloud ngay lập tức. Nếu mất mạng hoặc đồng bộ gặp lỗi, file có thể chưa được bảo vệ trên Cloud.

## 2. Thiết kế kiến trúc thư mục Cloud

### 2.1. Sơ đồ tổ chức thư mục

```text
Startup-Project/
├── Code/
│   ├── src/
│   ├── package.json
│   ├── package-lock.json
│   └── .gitignore
├── Docs/
│   ├── README.md
│   ├── SRS.docx
│   └── API-Documentation.md
├── Assets/
│   ├── Images/
│   ├── Icons/
│   └── Designs/
└── Backup/
    └── Release-Notes/
```

- **Code:** Chứa source code, file cấu hình và các file cần thiết để cài đặt dự án.
- **Docs:** Chứa tài liệu mô tả yêu cầu, hướng dẫn sử dụng và tài liệu kỹ thuật.
- **Assets:** Chứa hình ảnh, biểu tượng và các tài nguyên phục vụ giao diện.
- **Backup:** Chứa các bản sao lưu hoặc bản phát hành quan trọng.

### 2.2. Xử lý bẫy node_modules

Thư mục `node_modules` chứa rất nhiều thư viện được cài đặt từ các gói phụ thuộc. Đồng bộ toàn bộ thư mục này có thể làm tăng thời gian đồng bộ và chiếm nhiều dung lượng Cloud.

Cách xử lý là tạo file `.gitignore` trong thư mục dự án với nội dung:

```gitignore
node_modules/
.env
```

Trong đó:

- `node_modules/`: Không đưa thư mục thư viện đã cài đặt vào Git.
- `.env`: Không đưa file chứa thông tin cấu hình bí mật lên kho Git.

**Lưu ý quan trọng:** `.gitignore` chỉ kiểm soát những file Git theo dõi, không tự động loại trừ `node_modules` khỏi phần mềm đồng bộ Cloud như OneDrive hoặc Google Drive. Muốn loại trừ khỏi Cloud Sync, cần cấu hình quy tắc loại trừ riêng nếu dịch vụ hỗ trợ.

Để khôi phục thư viện khi cần, lập trình viên sử dụng `package.json` và `package-lock.json`, sau đó chạy:

```bash
npm install
```

Như vậy, source code chính vẫn được lưu trữ và bảo vệ, trong khi các thư viện có thể được cài đặt lại thay vì đồng bộ hàng vạn file nhỏ.

## 3. Sử dụng Files On-Demand để tiết kiệm dung lượng

Files On-Demand cho phép xem các file trong Cloud ngay trên máy tính mà không cần tải toàn bộ nội dung về ổ cứng.

- **Online-only:** File nằm trên Cloud, chỉ tải xuống khi cần mở.
- **Locally available:** File đã được tải về máy và có thể sử dụng khi không có Internet.
- **Always available:** File được giữ trên máy để truy cập ngoại tuyến.

Nam nên giữ source code đang phát triển trên SSD Local để chạy chương trình nhanh, còn tài liệu và tài nguyên ít sử dụng có thể để ở chế độ Online-only.

