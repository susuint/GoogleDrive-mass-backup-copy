# Công Cụ Sao Lưu Folder Google Drive - Hướng Dẫn Sử Dụng (Tiếng Việt)

## 📖 Tổng Quan

Công cụ này giúp bạn sao lưu toàn bộ folder từ Google Drive với các tính năng nâng cao bao gồm tải xuống đa luồng, tự động kiểm tra và cơ chế thử lại thông minh. Được tối ưu hóa cho tốc độ và độ tin cậy.

---

## 🌟 Tính Năng Chính

- ✅ **Sao Lưu Toàn Bộ Folder**: Backup toàn bộ folder được share từ Google Drive
- ✅ **Đặt Tên Tự Động**: Tạo folder backup với hậu tố "_BACKUP"
- ✅ **Kiểm Tra File**: Kiểm tra kích thước và MD5 checksum trước khi xóa
- ✅ **Ghi Log Thông Minh**: Logging dựa trên JSON để tránh backup trùng lặp
- ✅ **Tự Động Dọn Dẹp**: Tự động xóa file local sau khi upload thành công
- ✅ **Cơ Chế Retry**: Xử lý lỗi mạng với retry thông minh
- ✅ **Theo Dõi Tiến Trình**: Giám sát tiến trình theo thời gian thực
- 🚀 **Tải Xuống Đa Luồng**: 3-5 file được tải xuống đồng thời
- 🚀 **Tự Động Tối Ưu**: Tự động điều chỉnh số workers dựa trên RAM/CPU khả dụng
- 🚀 **Không Cảnh Báo Timeout**: Chạy mượt mà không có cảnh báo không cần thiết

---

## 🚀 Hướng Dẫn Bắt Đầu Nhanh

### Bước 1: Mở trong Google Colab

1. Upload file `.ipynb` lên Google Drive
2. Mở bằng Google Colab
3. Script đã sẵn sàng sử dụng!

### Bước 2: Cấu Hình Thiết Lập

Tìm phần **CẤU HÌNH CHÍNH** ở đầu script:

```python
# ⚙️  CẤU HÌNH CHÍNH - CHỈNH SỬA Ở ĐÂY

# 📁 ID của folder gốc (từ URL Google Drive)
SOURCE_FOLDER_ID = 'id-folder-nguon-cua-ban'

# 📁 ID của folder đích lưu backup (tùy chọn)
BACKUP_PARENT_ID = 'id-folder-dich-cua-ban'  # hoặc None cho thư mục gốc

# 🏷️  Hậu tố cho folder backup
FOLDER_SUFFIX = '_BACKUP'

# 🚀 Số luồng tải xuống đồng thời
MAX_WORKERS = None  # None = tự động, hoặc đặt 4, 6, 8...
```

### Bước 3: Lấy ID Folder

**Cách lấy ID Folder từ Google Drive:**

1. Mở Google Drive trong trình duyệt
2. Điều hướng đến folder bạn muốn backup
3. Nhìn vào URL trong trình duyệt:
   ```
   https://drive.google.com/drive/folders/1ZY4ab0XlPHa5_t10XnSvPbWUvJRdN4Nx
                                            ↑ Đây là ID Folder
   ```
4. Copy toàn bộ phần sau `/folders/`

**Ví dụ:**
- URL folder nguồn: `https://drive.google.com/drive/folders/1ABC123xyz`
- ID folder nguồn: `1ABC123xyz`

### Bước 4: Chạy Script

1. Click **Runtime** → **Run all** trong menu Google Colab
2. Khi được yêu cầu, xác thực với tài khoản Google của bạn
3. Quá trình backup sẽ tự động bắt đầu
4. Theo dõi tiến trình trong output

---

## ⚙️ Các Tùy Chọn Cấu Hình

### SOURCE_FOLDER_ID
- **Bắt buộc**: Có
- **Mô tả**: ID của folder bạn muốn backup
- **Cách tìm**: Xem Bước 3 ở trên
- **Ví dụ**: `'1ZY4ab0XlPHa5_t10XnSvPbWUvJRdN4Nx'`

### BACKUP_PARENT_ID
- **Bắt buộc**: Không
- **Mô tả**: ID của folder nơi backup sẽ được lưu
- **Mặc định**: `None` (lưu vào thư mục gốc "My Drive")
- **Ví dụ**: `'1XYZ789abc'` hoặc `None`

### FOLDER_SUFFIX
- **Bắt buộc**: Không
- **Mô tả**: Hậu tố thêm vào tên folder backup
- **Mặc định**: `'_BACKUP'`
- **Ví dụ**: Nếu folder nguồn là "Photos", backup sẽ là "Photos_BACKUP"

### MAX_WORKERS
- **Bắt buộc**: Không
- **Mô tả**: Số luồng tải xuống đồng thời
- **Mặc định**: `None` (tự động phát hiện dựa trên tài nguyên hệ thống)
- **Giá trị đề xuất**: 
  - `None` - Để hệ thống tự phát hiện (khuyến nghị)
  - `3-4` - Cho hệ thống RAM thấp (< 4GB)
  - `5-8` - Cho hệ thống RAM tốt (8GB+)

---

## 📊 Hiểu Output Của Chương Trình

### Trong Quá Trình Backup

```
🚀 Số workers được sử dụng: 6
💾 RAM khả dụng: 12.5 GB
🖥️  CPU cores: 2
⚙️  Workers tối ưu: 6

📊 Tìm thấy 45 items trong folder

🚀 Bắt đầu tải xuống 40 files với 6 luồng đồng thời...
📥 Downloading example_file.pdf...
✅ Downloaded: example_file.pdf
✅ Uploaded: example_file.pdf (ID: 1ABC...)
🗑️  Cleaned up local file: example_file.pdf
```

### Thống Kê

```
📊 Download Stats: ✅ 38 success | ❌ 2 failed | ⏭️  5 skipped
📊 Upload Stats: ✅ 38 success | ❌ 0 failed
```

### Báo Cáo Cuối Cùng

```
📋 CHI TIẾT BÁO CÁO BACKUP
========================================
📁 Tổng số folders: 5
📄 Tổng số files: 38
💾 Tổng dung lượng: 2.45 GB (2,631,456,789 bytes)
✅ Files có MD5 validation: 38/38
🕐 Thời gian backup gần nhất: 2026-02-01T14:30:25
```

---

## 🔧 Tính Năng Nâng Cao

### 1. Backup Gia Tăng

Công cụ tự động theo dõi các file đã backup trong `backup_log.json`:
- Các file đã backup được **bỏ qua**
- Chỉ backup các file mới hoặc đã thay đổi
- Tiết kiệm thời gian và băng thông

### 2. Tự Động Thử Lại

Nếu file không thể tải xuống/upload:
- Tự động thử lại tối đa 3 lần cho mỗi file
- Sau khi backup ban đầu, các file thất bại được thử lại thêm 2 lần nữa
- Báo cáo cuối cùng hiển thị các file không thể backup

### 3. Kiểm Tra Xác Nhận

Mọi file đều được kiểm tra:
- **Kiểm tra kích thước**: Đảm bảo file tải xuống khớp với kích thước gốc
- **MD5 checksum**: Xác minh tính toàn vẹn của file sau khi upload
- **Verification**: Đếm số file trong folder nguồn vs backup

### 4. Quản Lý Bộ Nhớ

- Garbage collection thông minh để tránh tràn bộ nhớ
- Tự động dọn dẹp file tạm
- Kích thước chunk được tối ưu hóa cho truyền file nhanh

---

## 📝 Các Trường Hợp Sử Dụng Phổ Biến

### Trường Hợp 1: Backup Toàn Bộ Lần Đầu

```python
SOURCE_FOLDER_ID = '1ABC123xyz'
BACKUP_PARENT_ID = None  # Lưu vào thư mục gốc My Drive
FOLDER_SUFFIX = '_BACKUP'
MAX_WORKERS = None  # Tự động phát hiện
```

### Trường Hợp 2: Backup Vào Vị Trí Cụ Thể

```python
SOURCE_FOLDER_ID = '1ABC123xyz'
BACKUP_PARENT_ID = '1XYZ789abc'  # Folder "Backups" của bạn
FOLDER_SUFFIX = '_2026_Thang2'
MAX_WORKERS = 6
```

### Trường Hợp 3: Hệ Thống Tài Nguyên Hạn Chế

```python
SOURCE_FOLDER_ID = '1ABC123xyz'
BACKUP_PARENT_ID = None
FOLDER_SUFFIX = '_BACKUP'
MAX_WORKERS = 3  # Sử dụng ít luồng hơn
```

---

## 🛠️ Xử Lý Sự Cố

### Vấn Đề: "Authentication Failed"

**Giải pháp:**
1. Trong Colab, vào Runtime → Restart runtime
2. Chạy lại cell xác thực
3. Đảm bảo bạn đang sử dụng đúng tài khoản Google

### Vấn Đề: "Folder ID not found"

**Giải pháp:**
1. Kiểm tra ID folder có đúng không
2. Đảm bảo folder được share với bạn
3. Xác minh bạn có quyền truy cập folder

### Vấn Đề: "Quá nhiều file thất bại"

**Giải pháp:**
1. Kiểm tra kết nối internet của bạn
2. Thử giảm MAX_WORKERS xuống 3-4
3. Chạy lại backup (sẽ bỏ qua các file đã thành công)

### Vấn Đề: "Out of memory error"

**Giải pháp:**
1. Đặt MAX_WORKERS thành giá trị thấp hơn (3 hoặc 4)
2. Script sẽ tự động quản lý bộ nhớ tốt hơn
3. Cân nhắc backup theo batch nhỏ hơn

### Vấn Đề: "Backup rất chậm"

**Giải pháp:**
1. Tăng MAX_WORKERS lên 6-8 (nếu bạn có RAM tốt)
2. Kiểm tra tốc độ internet
3. File lớn tự nhiên mất nhiều thời gian hơn

---

## 📚 Tiện Ích Bổ Sung

### Xem Backup Log

Chạy cell này để xem tất cả file đã backup:

```python
if os.path.exists('backup_log.json'):
    with open('backup_log.json', 'r', encoding='utf-8') as f:
        log_data = json.load(f)
        print(json.dumps(log_data, indent=2, ensure_ascii=False))
```

### Tải Backup Log Về Máy

Lưu file log về máy tính của bạn:

```python
from google.colab import files
files.download('backup_log.json')
```

### Reset Backup Log

⚠️ **CẢNH BÁO**: Thao tác này sẽ xóa toàn bộ lịch sử backup và backup lại mọi thứ từ đầu!

```python
reset_log = {'backed_up_files': {}, 'last_run': None}
with open('backup_log.json', 'w', encoding='utf-8') as f:
    json.dump(reset_log, f, indent=2, ensure_ascii=False)
print("🔄 Backup log đã được reset!")
```

---

## ⚡ Mẹo Tối Ưu Hiệu Suất

1. **Workers Tối Ưu**: Để MAX_WORKERS là `None` để tự động phát hiện tốt nhất
2. **File Lớn**: Với folder có nhiều file lớn (>100MB), cân nhắc MAX_WORKERS = 3-4
3. **Nhiều File Nhỏ**: Với folder có nhiều file nhỏ, MAX_WORKERS = 6-8 hoạt động tốt
4. **Khả Năng Resume**: Nếu backup dừng, chỉ cần chạy lại - nó sẽ bỏ qua file đã hoàn thành
5. **Tốc Độ Internet**: Internet nhanh hơn = nhiều workers có lợi hơn

---

## 🔒 Quyền Riêng Tư & Bảo Mật

- **Xử Lý Local**: File chỉ được lưu tạm trong bộ nhớ của Colab
- **Tự Động Dọn Dẹp**: File local được xóa ngay sau khi upload
- **Không Chia Sẻ Bên Ngoài**: Dữ liệu của bạn không bao giờ rời khỏi hạ tầng của Google
- **Xác Thực**: Sử dụng xác thực Google OAuth2 chính thức
- **Quyền**: Chỉ yêu cầu quyền truy cập Drive API

---

## 📊 Khuyến Nghị Chiến Lược Backup

### Cho Folder Nhỏ (< 1GB, < 100 files)
- MAX_WORKERS: Auto hoặc 4-6
- Thời gian dự kiến: 5-15 phút
- Tần suất chạy: Hàng tuần hoặc khi cần

### Cho Folder Trung Bình (1-10GB, 100-1000 files)
- MAX_WORKERS: Auto hoặc 6-8
- Thời gian dự kiến: 30-90 phút
- Tần suất chạy: Hàng tuần

### Cho Folder Lớn (> 10GB, > 1000 files)
- MAX_WORKERS: Auto hoặc 4-6 (để ổn định)
- Thời gian dự kiến: 2+ giờ
- Tần suất chạy: Hàng tháng
- Cân nhắc: Chia thành các sub-folder nhỏ hơn

---

## ❓ Câu Hỏi Thường Gặp

**H: Tôi có thể backup nhiều folder cùng lúc không?**
Đ: Thay đổi SOURCE_FOLDER_ID và chạy lại script cho mỗi folder.

**H: Công cụ này có xóa file gốc của tôi không?**
Đ: Không! Nó chỉ tạo bản sao. File gốc của bạn không bị động đến.

**H: Điều gì xảy ra nếu backup dừng giữa chừng?**
Đ: Chỉ cần chạy lại script. Nó sẽ bỏ qua các file đã backup.

**H: Tôi có thể lên lịch backup tự động không?**
Đ: Không trực tiếp trong Colab, nhưng bạn có thể đặt nhắc nhở để chạy định kỳ.

**H: Tôi cần bao nhiêu dung lượng lưu trữ?**
Đ: Ít nhất bằng kích thước folder nguồn, cộng thêm một chút buffer.

**H: Công cụ có hoạt động với folder được share không?**
Đ: Có! Miễn là bạn có quyền xem/tải xuống.

---

## 🆘 Hỗ Trợ

Nếu bạn gặp vấn đề:

1. **Kiểm tra phần xử lý sự cố** ở trên
2. **Xem lại các thông báo output** - chúng thường chỉ ra vấn đề
3. **Xác minh cài đặt cấu hình** của bạn có đúng không
4. **Thử giảm MAX_WORKERS** nếu gặp lỗi
5. **Kiểm tra quota lưu trữ Google Drive** - bạn cần có không gian trống

---

## 📝 Lịch Sử Thay Đổi

**Phiên bản 2.0 (Tối ưu hóa)**
- Thêm tải xuống đa luồng
- Tự động tối ưu dựa trên tài nguyên hệ thống
- Cải thiện quản lý bộ nhớ
- Tăng cường xử lý lỗi và logic retry
- Theo dõi tiến trình tốt hơn
- Loại bỏ cảnh báo timeout

**Phiên bản 1.0**
- Phát hành ban đầu
- Chức năng backup cơ bản
- Tải xuống đơn luồng

---

## ✅ Thực Hành Tốt Nhất

1. **Test Trước**: Thử backup một folder nhỏ trước
2. **Theo Dõi Tiến Trình**: Xem output để phát hiện lỗi
3. **Kết Nối Ổn Định**: Sử dụng kết nối internet ổn định
4. **Đủ Dung Lượng**: Đảm bảo đủ không gian Google Drive
5. **Giữ File Log**: Tải backup_log.json về để lưu trữ
6. **Backup Thường Xuyên**: Chạy định kỳ cho các folder quan trọng
7. **Xác Minh Kết Quả**: Kiểm tra báo cáo verification cuối cùng

---

## 🎯 Dấu Hiệu Thành Công

Backup của bạn thành công khi bạn thấy:

```
✅ BACKUP COMPLETED SUCCESSFULLY!
✅ VERIFICATION PASSED: Tất cả files đã được backup!
📁 Backup folder: [Tên folder của bạn]_BACKUP
🔗 Link: https://drive.google.com/drive/folders/[ID]
```

---

**Chúc Bạn Backup Thành Công! 🎉**

*Công cụ này được thiết kế để làm cho việc backup Google Drive trở nên đơn giản, nhanh chóng và đáng tin cậy. Nếu bạn có đề xuất hoặc phản hồi, vui lòng cho chúng tôi biết!*
