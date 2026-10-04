# Bài 3: Bảo mật tài nguyên bằng HTTP Basic Authentication

### 1. Cài đặt công cụ băm mật khẩu
Cài đặt `apache2-utils` để sử dụng lệnh `htpasswd`:
```bash
sudo apt update
sudo apt install apache2-utils -y
```

### 2. Tạo tài khoản và mật khẩu bảo mật
Tạo file `.htpasswd` lưu trữ ở `/etc/nginx/` (để tách biệt với thư mục web root, tránh bị lộ file):
```bash
sudo htpasswd -c /etc/nginx/.htpasswd admin_user
```
*(Hệ thống sẽ yêu cầu nhập mật khẩu 2 lần. Một bản mẫu file `.htpasswd` được đính kèm trong repository này).*

### 3. Cấu hình Nginx
Cấu hình yêu cầu xác thực tại đường dẫn `/admin`:
```bash
sudo nano /etc/nginx/sites-available/admin.conf
```
*(Nội dung file cấu hình `admin.conf` đã được đính kèm trong repository).*

### 4. Kiểm tra
*Lưu ý: Vì thẻ visa của em bị khoá nên không thể tạo droplet để chạy kiểm tra lệnh.*

- Truy cập không có mật khẩu (sẽ bị lỗi HTTP 401 Unauthorized):
  ```bash
  curl -I http://<IP_ADDRESS_DROPLET>/admin
  ```
- Truy cập kèm thông tin hợp lệ (sẽ thành công 200 OK):
  ```bash
  curl -u admin_user:<PASSWORD> http://<IP_ADDRESS_DROPLET>/admin
  ```
