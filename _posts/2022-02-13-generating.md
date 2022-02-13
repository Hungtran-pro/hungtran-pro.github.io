![Ảnh giới thiệu thuật toán sinh](/image/thuatToanSinh.png)

## Thuật toán sinh (Generative Algorithm)

- Mô hình thuật toán sinh được dùng để giải các bài toán liệt kê, bài toán đếm, vài toán tối ưu, bài toán tồn tại thỏa mã hai điều kiện:
    - Xác định được điểm đầu và điểm cuối của thuật toán.
    - Từ điểm giữa ta có thể xác định được điểm đến tiếp theo dựa trên 1 quy tắc nào đó.

Thuật toán:

```pascal
Begin:
Bước 1: (bước khởi tạo)
    <Thiết lập cấu hình đầu tiên>;
Bước 2: (bước lặp)
while(<Lặp khi cấu hình chưa phải cuối cùng>) do
    <Đưa ra cấu hình hiện tại>;
    <Sinh ra cấu hình kế tiếp>;
endwhile;
End
```

Bài tập: Liệt kê dãy nhị phân có độ dài là n

Ví dụ: n = 4
