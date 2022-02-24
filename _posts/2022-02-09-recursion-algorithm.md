# Recursive Algorithm

![Ảnh mô tả](/image/img1.jpg)


## 1. Khái niệm:
 
- Đệ quy là quá trình mà trong đó **một hàm gọi lại chính nó** theo một cách trực tiếp hoặc gián tiếp. Khi đó, hàm đó được gọi là **hàm đệ quy**.

- Đệ quy thường được sử dụng trong những bài toán mà bài toán đó có thể được phân rã thành những bài toán nhỏ hơn nhưng có cùng dạng với bài toán ban đầu. Việc phân rã bài toán lớn thành một hoặc nhiều bài toán con có cùng dạng sẽ được thực hiện liên tục cho đến khi gặp bài toán con đơn giản đến mức có thể dễ dàng suy ra ngay được kết quả mà không cần phân rã nữa. Sau khi đã có được kết quả của bài toán con đơn giản nhất, dựa vào kết quả đó ta quay lại tìm kết quả của các bài toán con đã được phân rã trước đó và tìm được kết quả của bài toán ban đầu. Việc phân rã như vậy còn được gọi là **chia để trị**.

- Ví dụ: Xét bài toán tính tổng các số từ 1 đến n, ta có 2 cách tiếp cận cơ bản nhất như sau: Gọi hàm **f(n)** là hàm tính tổng các số từ 1 đến n.

	- Cách tiếp cận 1:
	 
		 - Cộng lần lượt các số từ 1 đến n:  **f(n)** = 1 + 2 + 3 + ... + n.
		 
	- Cách tiếp cận 2:
	
		- Đệ quy: 
			- **f(n) = 1** nếu n = 1.
			
			- **f(n) = n + f(n - 1)** nếu n > 1.
			
			Giả sử n = 4:
      
			**f(4) = 4 + f(3)** (do 4 > 1), ta cần phải tính **f(3)**.
      
			**f(3) = 3 + f(2)** (do 3 > 1), ta cần phải tính **f(2)**.
      
			**f(2) = 2 + f(1)** (do 2 > 1), ta cần phải tính **f(1)**.
      
			Dễ thấy **f(1) = 1** do đó ta quay tại tính **f(2)**, từ **f(2)** ta tính được **f(3)** rồi tính được **f(4)**.
      
	- Code:
	
 ```C++
 // Cách tiếp cận 1:
int f(int n)
{
	int sum = 0;
	for(int i = 1; i <= n; ++i) sum += i;
	return sum;
}

// Cách tiếp cận 2:
int f(int n)
{
	if(n == 1) return n;
	return (n + f(n - 1));
}
```

- Ưu điểm và nhược điểm của đệ quy:

	- Ưu điểm: Dễ xây dựng, code đơn giản, dễ hiểu.
	
	- Nhược điểm: Tốn bộ nhớ, chậm, độ sâu đệ quy hữu hạn.
	
## 2. Giải thuật đệ quy:

- Nếu lời giải của bài toán P được thực hiện bằng lời giải của bài toán P' có dạng giống như bài toán P thì đó là một lời giải đệ quy.

- Giải thuật tương ứng với lời giải như vậy được gọi là giải thuật đệ quy. Cần chú ý: P' tuy có dạng giống như P nhưng phải dễ giải hơn P và việc giải P' không cần đến P.

- Ý tưởng: Biểu diễn bài toán P dưới dạng một hoặc nhiều bài toán P' nhỏ hơn và thêm 1 hoặc vài điều kiện cơ sở để dừng đệ quy.

- Cấu trúc của 1 hàm đệ quy gồm 2 phần:

	- Bài toán cơ sở: Là bài toán đơn giản nhất, có thể dễ dàng suy ra được kết quả mà không cần giải thông qua bất kỳ bài toán con đơn giản nào khác.
	
	- Phần đệ quy: Nếu bài toán hiện tại chưa thể giải được bằng bài toán cơ sở, ta hãy xác định bài toán con của nó và gọi đệ quy để giải bài toán con đó cho đến khi gặp bài toán cơ sở. Từ kết quả của bài toán cơ sở, ta quay lại giải các bài toán con lớn hơn và suy ra được kết quả của bài toán ban đầu.
	
- Code: Xét hàm đệ quy của bài toán trong ví dụ của phần 1:

```C++
int f(int n)
{
	if(n == 1) return n; // Bài toán cơ sở
	return (n + f(n - 1)); // Phần đệ quy
}
```

## 3. Đệ quy đuôi: 

- Một hàm đệ quy được gọi là hàm đệ quy đuôi nếu như lời gọi đệ quy là điều cuối cùng được thực thi bởi hàm.

- Ví dụ: Hàm tìm ước chung lớn nhất của 2 số nguyên dương a và b theo giải thuật Euclid sau đây là 1 hàm đệ quy đuôi:

```C++
int gcd(int a, int b)
{
	if(b == 0) return a;
	return gcd(b, a % b);
}
```

- Ưu điểm của đệ quy đuôi: Nhanh hơn và ít tốn bộ nhớ hơn so với đệ quy thông thường.
	
