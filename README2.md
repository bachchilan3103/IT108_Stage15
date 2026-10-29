# PHÂN TÍCH RỦI RO CHIA SẺ DỮ LIỆU VÀ PHÂN QUYỀN TRUY CẬP

## 1. Phân tích vi phạm Quy tắc Cờ Đỏ Bảo mật

Hành động của An vi phạm quy tắc bảo mật vì đã chia sẻ tài liệu chứa số điện thoại khách hàng cho người bên ngoài bằng chế độ `Anyone with the link` và cấp quyền `Editor`.

- **Lộ dữ liệu:** Bất kỳ ai có đường link đều có thể truy cập tài liệu, kể cả người không được An cho phép trực tiếp.
- **Cấp quyền quá rộng:** Quyền `Editor` cho phép người truy cập chỉnh sửa và có thể xóa nội dung, gây mất dữ liệu quan trọng.
- **Không kiểm soát người truy cập:** Khi đường link bị phát tán lên mạng xã hội, An không thể đảm bảo chỉ cộng tác viên được truy cập tài liệu.

Đây là lỗi chia sẻ dữ liệu không an toàn, có thể gây rò rỉ thông tin khách hàng và ảnh hưởng đến uy tín của Startup.

## 2. Thiết lập lại cấu trúc phân quyền

### 2.1. Lựa chọn mức quyền cho cộng tác viên

Nên cấp quyền theo đúng công việc cần thực hiện:

| Mức quyền | Chức năng |
|---|---|
| `Viewer` | Chỉ xem tài liệu, không chỉnh sửa |
| `Commenter` | Xem và thêm nhận xét, không sửa trực tiếp nội dung |
| `Editor` | Chỉnh sửa nội dung tài liệu |

Đối với cộng tác viên chỉ cần góp ý, An nên cấp quyền `Commenter`. Nếu người đó thực sự cần sửa dữ liệu, An mới cấp quyền `Editor` sau khi cân nhắc.

### 2.2. Chế độ chia sẻ an toàn

An nên chọn `Restricted` thay vì `Anyone with the link`, sau đó nhập chính xác email của cộng tác viên cần truy cập.

Cách này giúp giới hạn quyền truy cập cho những tài khoản được chỉ định, giảm nguy cơ người lạ sử dụng đường link để xem hoặc sửa dữ liệu.

Không có chế độ chia sẻ nào an toàn tuyệt đối 100%, nhưng `Restricted` kết hợp với phân quyền phù hợp sẽ giúp hạn chế rủi ro.

### 2.3. Ngăn cộng tác viên mời thêm người lạ

An cần kiểm tra và tắt tùy chọn cho phép Editor chia sẻ tài liệu hoặc thay đổi quyền truy cập với người khác, nếu dịch vụ đang sử dụng hỗ trợ tính năng này.

Đồng thời, An nên giới hạn quyền chia sẻ cho chủ sở hữu hoặc người quản lý tài liệu để tránh việc cộng tác viên tự ý cấp quyền cho người ngoài.

