# Backtracking Algorithm

![Ảnh mô tả](/image/img2.jpeg)


## 1.Khái niệm:
 
- Quay lui là một kỹ thuật thiết kế giải thuật dựa trên đệ quy. Ý tưởng của quay lui là tìm lời giải từng bước, mỗi bước chọn một trong số các lựa chọn có thể nhận và đệ quy.

- Ưu và nhược điểm:
	 
	- Ưu điểm: Việc quay lui là thử tất cả các tổ hợp để tìm được một lời giải. Thế mạnh của phương pháp này là nhiều cài đặt tránh được việc phải thử nhiều trường hợp chưa hoàn chỉnh, nhờ đó giảm thời gian chạy.

	- Nhược điểm: Trong trường hợp xấu nhất độ phức tạp của quay lui vẫn là cấp số mũ do thường gặp phải các trường hợp sau:

		- Rơi vào tình trạng "thrashing": quá trình tìm kiếm cứ gặp phải bế tắc với cùng một nguyên nhân.

		- Thực hiện các công việc dư thừa: Mỗi lần chúng ta quay lui, chúng ta cần phải đánh giá lại lời giải trong khi đôi lúc điều đó không cần thiết.

		- Không sớm phát hiện được các khả năng bị bế tắc trong tương lai. Quay lui chuẩn, không có cơ chế nhìn về tương lai để nhận biết được nhánh tìm kiếm sẽ đi vào bế tắc.

## 2. Tư tưởng:

- Dùng để giải các bài toán liệt kê cấu hình. Mỗi cấu hình được xây dựng bằng từng phần tử. Mỗi phần tử lại được chọn bằng cách thử tất cả các khả năng.

- Các bước trong việc liệt kê cấu hình dạng x[1...n]:

	- Xét tất cả các giá trị x[1] có thể nhận, thử cho x[1] nhận các giá trị đó. Ứng với mỗi giá trị x[1] nhận được, ta sẽ:
	
	- Xét tất cả các giá trị x[2] có thể nhận, thử cho x[2] nhận các giá trị đó. Ứng với mỗi giá trị x[2] nhận được, ta sẽ:
	
	- Xét các giá trị x[3] có thể nhận, ... Làm liên tục cho tới khi:
	
	- ...
	
	- Xét tất cả các giá trị x[n] có thể nhận, thử cho x[n] nhận các giá trị đó.
	
	- Thông báo các cấu hình tìm được (x[1], x[2], x[3], ... x[n]).
	
- Bản chất của quay lui là một quá trình tìm kiếm theo chiều sâu.

- Quay lui cũng là đệ quy nhưng sẽ có thêm một hoặc vài lệnh phía sau đó để tiếp tục thực hiện sau quá trình đi sâu vào đệ quy.

- Ví dụ: Xét bài toán in các số từ 1 đến n sử dụng quay lui:

	- Code:
	
```C++
void Try(int n)
{
	if(n == 0) return;
	Try(n - 1);
	printf("%d ", n);
}
```

- Với n = 3:

	- **Try(3)**: Nhận thấy 3 != 0 do đó gọi đệ quy tới **Try(2)**.
	
	- **Try(2)**: Nhận thấy 2 != 0 do đó gọi đệ quy tới **Try(1)**.
	
	- **Try(1)**: Nhận thấy 1 != 0 do đó gọi đệ quy tới **Try(0)**.

	- **Try(0)**: Nhận thấy 0 == 0 do đó quay lui lại hàm đệ quy trước đó (tức **Try(1)**).
	
	- Khi quay lại **Try(1)**: Tiếp tục thực hiện lệnh printf() và in ra giá trị của **n** (tức in ra **1**). Lúc này, không còn lệnh nào nữa, do đó quay lui lại hàm đệ quy trước đó (tức **Try(2)**).

	- Khi quay lại **Try(2)**: Tiếp tục thực hiện lệnh printf() và in ra giá trị của **n** (tức in ra **2**). Lúc này, không còn lệnh nào nữa, do đó quay lui lại hàm đệ quy trước đó (tức **Try(3)**).

	- Khi quay lại **Try(3)**: Tiếp tục thực hiện lệnh printf() và in ra giá trị của **n** (tức in ra **3**). Lúc này, không còn lệnh nào nữa và kết thúc đệ quy.

- Nhận thấy: **n** càng lớn thì càng lâu được in ra. Lý do là **n** càng lớn thì **Try(n)** được gọi càng sớm nên nó sẽ đi càng sâu và phần quay lại sẽ được thực hiện sau khi đã đi sâu nhất (Từ **Try(n - 1)** đến **Try(0)**) và từ **Try(0)** mới trở về **Try(n)**.

## 3. Mô hình thuật toán:

- Mã giả:

```C++
void Try(Mọi giá trị của j có thể gán cho x[i])
{
	<Thử cho x[i] = j>;
	<Đánh dấu đã chọn x[i] (nếu cần)>;
	if(<x[i] là phần tử cuối cùng của cấu hình>)
	{
		<Thông báo cấu hình vừa tìm được>;
	}
	else
	{
		<Gọi đệ quy với i + 1 để chọn tiếp x[i + 1]>; // Try(i + 1);
		<Xóa đánh dấu đã chọn x[i] (nếu cần)>;
	}
}
```

- Ví dụ: Xét bài toán in ra các xâu nhị phân có độ dài **n** bằng quay lui:

- Code:

```C++
int n;
int x[15];
// Hàm in xâu nhị phân có độ dài n vừa tìm được
void print()
{
	for(int i = 1; i <= n; ++i) printf("%d", x[i]);
	printf("\n");
}
// Hàm đệ quy - quay lui đi tìm từng cấu hình
void Try(int i)
{
	for(int j = 0; j <= 1; ++j)
	{
		x[i] = j;
		if(i == n) print();
		else Try(i + 1);
	}
}
```

- Công việc còn lại chỉ là nhập **n** và gọi **Try(1)**.

- Nhìn vào sơ đồ cây dưới đây ta có thể hiểu được quy trình đệ quy - quay lui với **n = 3**:

![Ảnh mô tả](/image/img3.png)

- Ví dụ với 4 cấu hình đầu tiên 000, 001, 010 và 011:
	
	- **Try(1)**:

		- Với j = 0: Gán x[i] = j (tức x[1] = 0). Nhận thấy i = 1 < n = 3 do đó gọi đệ quy tới **Try(2)**. 

	- **Try(2)**:

		- Với j = 0: Gán x[i] = j (tức x[2] = 0). Nhận thấy i = 2 < n = 3 do đó gọi đệ quy tới **Try(3)**. 

	- **Try(3)**:

		- Với j = 0: Gán x[i] = j (tức x[3] = 0). Nhận thấy i = 3 == n do đó in ra cấu hình đầu tiên là 000. Tiếp tục vòng lặp for(), lúc này j = 1.

		- Với j = 1: Gán x[i] = j (tức x[3] = 1). Nhận thấy i = 3 == n do đó in ra cấu hình thứ 2 là 001. Lúc này kết thúc vòng lặp for() và cũng không còn lệnh nào để thực hiện, do đó quay lui lại **Try(2)**.
	
	- Khi quay lại **Try(2)**: Tiếp tục vòng for() còn dang dở, lúc này j = 1.

		- Với j = 1: Gán x[i] = j (tức x[2] = 1). Nhận thấy i = 2 < n = 3 do đó gọi đệ quy tới **Try(3)**.

	- **Try(3)**:
	
		- Với j = 0: Gán x[i] = j (tức x[3] = 0). Nhận thấy i = 3 == n do đó in ra cấu hình thứ 3 là 010. Tiếp tục vòng lặp for(), lúc này j = 1.

		- Với j = 1: Gán x[i] = j (tức x[3] = 1). Nhận thấy i = 3 == n do đó in ra cấu hình thứ 4 là 011. Lúc này kết thúc vòng lặp for() và cũng không còn lệnh nào để thực hiện, do đó quay lui lại **Try(2)**.

	- Khi quay lại **Try(2)**: Lúc này, Lúc này kết thúc vòng lặp for() và cũng không còn lệnh nào để thực hiện, do đó quay lui lại **Try(1)**.

	- ...
	
	- Cứ thực hiện tương tự như vậy cho đến cấu hình cuối cùng là 111.
	
	
	
