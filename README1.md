# PHÂN TÍCH RỦI RO LƯU TRỮ DỮ LIỆU VÀ HYBRID WORKFLOW

## 1. Phân tích hậu quả của thảm họa dữ liệu truyền thống

Trong tình huống trên, Nam lưu code trên máy tính cá nhân và gửi nhiều phiên bản qua Zalo. Cách làm này có thể gây ra các hậu quả sau:

**1. Mất dữ liệu quan trọng**

Nam đã xóa đoạn code cần thiết rồi nhấn `Ctrl + S`, khiến nội dung sai được lưu đè lên file cũ. Nếu không có bản sao lưu, Nam có thể phải viết lại toàn bộ đoạn code đã mất.

**2. Nhầm lẫn giữa các phiên bản**

Việc tạo nhiều file như `main_v1.py`, `main_v2.py` và `main_final.py` khiến Nam khó xác định đâu là bản mới nhất. Các thành viên trong nhóm cũng có thể sử dụng nhầm phiên bản code.

**3. Khó khôi phục dữ liệu**

File lưu cục bộ không tự động cung cấp lịch sử thay đổi để quay lại trạng thái trước đó. Khi lưu đè nội dung sai, Nam không thể khôi phục dễ dàng nếu không có bản sao phù hợp.

**4. Ảnh hưởng đến tiến độ làm việc nhóm**

Khi code quan trọng bị mất, Nam phải dành thời gian viết lại và kiểm tra chương trình. Điều này có thể làm chậm tiến độ của dự án Smart Food.

## 2. Đề xuất quy trình thiết lập Hybrid Workflow

Nam nên kết hợp lưu trữ cục bộ với Cloud và sử dụng công cụ quản lý phiên bản để hạn chế nguy cơ mất dữ liệu.

**Bước 1: Lưu dự án trên máy tính**

Nam tiếp tục viết code trên máy cá nhân để thuận tiện chỉnh sửa và chạy thử chương trình. Tuy nhiên, không nên chỉ giữ duy nhất một bản code trên máy.

**Bước 2: Đồng bộ dự án lên Cloud**

Nam có thể sử dụng OneDrive hoặc Google Drive để đồng bộ thư mục dự án. Khi file được cập nhật, dữ liệu sẽ được đồng bộ lên Cloud theo cơ chế của dịch vụ đã thiết lập.

**Bước 3: Bật tính năng Version History**

Nam cần kiểm tra tính năng lịch sử phiên bản của dịch vụ Cloud đang sử dụng. Khi code bị sửa sai hoặc lưu đè, Nam có thể mở lịch sử phiên bản, chọn bản còn nguyên vẹn và khôi phục lại.

**Bước 4: Sử dụng Git để quản lý code**

Nam nên sử dụng Git để lưu lại các mốc thay đổi bằng lệnh `git add`, `git commit` và đẩy code lên GitHub bằng `git push`. Nhờ đó, nhóm có thể theo dõi các phiên bản và phối hợp làm việc tốt hơn.

**Bước 5: Kiểm tra khả năng khôi phục**

Nam nên thử khôi phục một file mẫu để chắc chắn rằng lịch sử phiên bản hoạt động. Khi xảy ra sự cố, Nam mở Version History, chọn phiên bản phù hợp và nhấn Restore nếu dịch vụ hỗ trợ.

Sau khi thiết lập, Nam vẫn làm việc trên máy tính như bình thường nhưng có thêm bản sao trên Cloud và lịch sử thay đổi. Điều này giúp giảm nguy cơ mất code và rút ngắn thời gian khôi phục khi gặp sự cố.

