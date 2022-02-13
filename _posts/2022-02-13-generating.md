# Thuật toán sinh (Generative Algorithm)

![Ảnh giới thiệu thuật toán sinh](/image/thuatToanSinh.png)

## 1. Khái niệm

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

## 2. Bài tập

Bài tập 1: Liệt kê dãy nhị phân có độ dài là n

Ví dụ: n = 4.

| STT | Dãy | STT | Dãy |
| 0 | 0 0 0 0 | 8 | 1 0 0 0 |
| 1 | 0 0 0 1 | 9 | 1 0 0 1 |
| 2 | 0 0 1 0 | 10 | 1 0 1 0 |
| 3 | 0 0 1 1 | 11 | 1 0 1 1 |
| 4 | 0 1 0 0 | 12 | 1 1 0 0 |
| 5 | 0 1 0 1 | 13 | 1 1 0 1 |
| 6 | 0 1 1 0 | 14 | 1 1 1 0 |
| 7 | 0 1 1 1 | 15 | 1 1 1 1 |

*Dựa trên điều kiện thuật toán sinh, hãy tìm điểm đầu, điểm cuối và quy luật sinh của thuật toán?*
<details><summary>Answer</summary>
<p>

#### We can hide anything, even code!

    ```ruby
      puts "Hello World"
    ```

</p>
</details>

Bài tập 2: Liệt kê tất cả các hoán bị n phần tử từ 1 ⇒ n.

Ví dụ: n = 3.

| STT | Dãy |
| 0 | 1 2 3 |
| 1 | 1 3 2 |
| 2 | 2 1 3 |
| 3 | 2 3 1 |
| 4 | 3 1 2 |
| 5 | 3 2 1 |

*Dựa trên điều kiện thuật toán sinh, hãy tìm điểm đầu, điểm cuối và quy luật sinh của thuật toán?*
<details><summary>Answer</summary>
<p>

#### We can hide anything, even code!

    ```ruby
      puts "Hello World"
    ```

</p>
</details>