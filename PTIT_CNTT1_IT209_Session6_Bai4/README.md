# Bài 4: Quản lý tiến trình nền với nohup và tín hiệu Kill

## 1. Các lệnh thực hiện

### Bước 1: Khởi tạo và gán quyền thực thi cho script
chmod +x loop-monitor.sh

### Bước 2: Khởi chạy tiến trình ngầm độc lập bằng nohup
nohup ./loop-monitor.sh > /dev/null 2>&1 &

---

## 2. Nhật ký kiểm tra (Verification Logs)

### Bước 1: Tra cứu PID và kiểm tra tiến trình đang chạy
$ ps aux | grep loop-monitor.sh

Kết quả:
user1    14520  0.0  0.1   6824  3028 pts/0    S    15:00   0:00 /bin/bash ./loop-monitor.sh

### Bước 2: Kiểm tra dữ liệu log được ghi liên tục
$ tail -n 10 /tmp/monitor.log

Kết quả:
System time: Sat Oct 10 15:00:05 UTC 2026
System time: Sat Oct 10 15:00:10 UTC 2026
System time: Sat Oct 10 15:00:15 UTC 2026

### Bước 3: Tắt tiến trình an toàn bằng tín hiệu SIGTERM (15)
$ kill -15 14520

### Bước 4: Xác nhận tiến trình đã ngắt
$ ps aux | grep loop-monitor.sh
(Không còn tiến trình loop-monitor.sh xuất hiện)
