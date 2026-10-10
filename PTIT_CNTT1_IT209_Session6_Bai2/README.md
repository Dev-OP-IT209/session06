# Bài 2: Cấu hình phân quyền Nhóm và sudoers bằng visudo

## 1. Các lệnh đã thực hiện

### Bước 1: Tạo nhóm và tài khoản người dùng
sudo groupadd devops-admin
sudo adduser deployer
sudo usermod -aG devops-admin deployer

### Bước 2: Cấu hình /etc/sudoers bằng visudo
Chạy lệnh cấu hình an toàn:
sudo visudo

Thêm dòng sau vào cuối tệp tin:
%devops-admin ALL=(ALL) NOPASSWD: /usr/bin/systemctl start *, /usr/bin/systemctl stop *, /usr/bin/systemctl restart *, /usr/bin/systemctl status *

---

## 2. Nhật ký kiểm tra (Verification Logs)

### Bước 1: Chuyển sang tài khoản deployer
$ su - deployer

### Bước 2: Kiểm tra các quyền sudo được cấp
$ sudo -l

Kết quả đầu ra:
Matching Defaults entries for deployer on server:
    env_reset, mail_badpass, ...

User deployer may run the following commands on server:
    (ALL) NOPASSWD: /usr/bin/systemctl start *, /usr/bin/systemctl stop *, /usr/bin/systemctl restart *, /usr/bin/systemctl status *

### Bước 3: Kiểm tra khởi động lại dịch vụ không cần mật khẩu
$ sudo systemctl restart cron

Kết quả: Lệnh thực thi thành công ngay lập tức mà không yêu cầu nhập mật khẩu.
