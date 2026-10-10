# Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Các lệnh đã thực hiện

### Bước 1: Khởi tạo cấu trúc thư mục
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs

### Bước 2: Thay đổi chủ sở hữu và nhóm sở hữu
# Gán user hiện tại làm owner và www-data làm group
sudo chown -R $USER:www-data /var/www/my-app

### Bước 3: Phân quyền theo yêu cầu
# public: Owner (rwx), Group (r-x), Others (---) => 750
sudo chmod 750 /var/www/my-app/public

# logs: Owner (rwx), Group (rwx), Others (---) => 770
sudo chmod 770 /var/www/my-app/logs

---

## 2. Nhật ký kiểm tra (Verification Logs)

Chạy lệnh kiểm tra cấu trúc và quyền truy cập:
$ ls -la /var/www/my-app

Kết quả đầu ra:
drwxr-xr-x 4 root     www-data 4096 Oct 10 15:00 .
drwxr-xr-x 3 root     root     4096 Oct 10 15:00 ..
drwxrwx--- 2 myuser   www-data 4096 Oct 10 15:00 logs
drwxr-x--- 2 myuser   www-data 4096 Oct 10 15:00 public
