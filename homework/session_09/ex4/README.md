# Bài 4 — Lưu trữ dữ liệu đơn giản với Docker Volume

## Mục tiêu
Tạo Named Volume để dữ liệu còn sau khi container dừng/xóa.

## Các lệnh đã thực hiện

```bash
# 1. Tạo named volume
docker volume create easy-volume

# 2. Kiểm tra volume đã có
docker volume ls

# 3. Ghi dữ liệu vào volume (container Alpine, tự xóa sau khi chạy)
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"

# 4. Đọc lại dữ liệu bằng container khác (cùng volume)
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
```

## Kết quả mong đợi

```text
Luu tru du lieu Docker
```

## Giải thích ngắn

| Lệnh | Việc |
|------|------|
| `docker volume create easy-volume` | Tạo volume tên `easy-volume` |
| `-v easy-volume:/data` | Gắn volume vào thư mục `/data` trong container |
| `--rm` | Xóa container sau khi chạy xong (volume vẫn giữ data) |
| Container thứ 2 `cat /data/test.txt` | Chứng minh data bền vững ngoài lifecycle container |

## Dọn dẹp (tuỳ chọn)

```bash
docker volume rm easy-volume
```
