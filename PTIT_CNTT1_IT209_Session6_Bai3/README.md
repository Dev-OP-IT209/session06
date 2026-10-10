# Bài 3: Cấu hình tường lửa UFW và chẩn đoán cổng mạng

## 1. Các lệnh cấu hình đã thực hiện

### Bước 1: Thiết lập chính sách mặc định của UFW
sudo ufw default deny incoming
sudo ufw default allow outgoing

### Bước 2: Cho phép các cổng mạng cần thiết
# Mở cổng SSH quản trị
sudo ufw allow 22/tcp

# Mở cổng ứng dụng Web
sudo ufw allow 8080/tcp

### Bước 3: Kích hoạt tường lửa UFW
sudo ufw enable

---

## 2. Nhật ký kiểm tra (Verification Logs)

### Bước 1: Kiểm tra trạng thái tường lửa chi tiết
$ sudo ufw status verbose

Kết quả đầu ra:
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
8080/tcp                   ALLOW IN    Anywhere                  
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
8080/tcp (v6)              ALLOW IN    Anywhere (v6)             

### Bước 2: Kiểm tra các cổng đang lắng nghe trên máy chủ
$ ss -tlnp

Kết quả đầu ra:
State      Recv-Q Send-Q Local Address:Port  Peer Address:Port Process
LISTEN     0      128    0.0.0.0:22          0.0.0.0:*         users:(("sshd",pid=850,fd=3))
LISTEN     0      511    0.0.0.0:8080        0.0.0.0:*         users:(("node",pid=1234,fd=18))
LISTEN     0      128       [::]:22             [::]:*         users:(("sshd",pid=850,fd=4))
