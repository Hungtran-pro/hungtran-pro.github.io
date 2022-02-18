# Quy hoạch động 
Quy hoạch động (Dynamic Programming) là kĩ thuật được được dùng khi có một công thức truy hồi và một (hoặc một vài) trạng thái bắt đầu. Một bài toán được tính bởi các bài toán nhỏ hơn đã tìm ra trước đó (được lưu lại kết quả) giúp chúng ta giảm độ phức tạp của một số bài toán nhưng ngược lại cần rất nhiều không gian vật lý để lưu trữ.

![markdown](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/jl21im7uz7_1.JPG)

Vậy chúng ta cùng tìm hiểu xem quy hoạch động là gì?

### 1. Quy hoạch động là gì?

**Quy hoạch động** là một kĩ thuật thiết kế thuật toán theo kiểu chia bài toán lớn thành các bài toán con, sử dụng lời giải của các bài toán con để tìm lời giải cho bài toán ban đầu. 
Khác với chia để trị, quy hoạc động, thay vì gọi đệ quy, sẽ **tìm lời giải của các bài toán con và lưu vào bộ nhớ (thường là một mảng), và sau đó lấy lời giải của bài toán con ở trong mảng đã tính trước để giải bài toán lớn**. Việc lưu lại lời giải vào bộ nhớ khiến chúng ta không phải tính lại lời giải của các bài toán con mỗi khi cần, do đó, tiết kiệm được thời gian tính toán.

**Ưu điểm:**

* chương trình chạy nhanh, mang tính tối ưu hóa cao.

**Nhược điểm:**
   
* Không phải lúc nào sự kết hợp lời giải của bài toán con cũng cho ra lời giải bài toán lớn hơn.

* Số lượng các bài toán con cần giải quyết và lưu trữ đáp án có thể rất lớn, không thể chấp nhận được. Cho đến nay, chưa ai xác định được một cách chính xác những bài nào có thể được giải quyết hiệu quả bằng phương pháp quy hoạch động.

### 2. Làm thế nào để biết bài toán sử dụng thuật toán quy hoạch động?

Quy hoạch động có thể giải quyết các bài toán thỏa mãn các yêu cầu sau:

- **Bài toán lớn cần giải có thể phân rã được thành nhiều bài toán con**. Trong đó, sự
phối hợp lời giải của các bài toán con cho ta lời giải của bài toán lớn. (Bài toán con có lời giải đơn giản được gọi là cơ sở của qui hoạch động. Công thức phối hợp nghiệm của các bài toán con để có nghiệm của bài toán lớn được gọi là công thức truy hồi của qui hoạch động )

- **Phải có đủ không gian vật lý lưu trữ lời giải các bài toán con** (Bảng phương án của
qui hoạch động). Vì qui hoạch động đi giải quyết tất cả các bài toán con, do vậy nếu ta không lưu trữ được lời giải các bài toán con thì không thể phối hợp được lời giải giữa các bài toán con.

- Quá trình **giải quyết từ bài toán cơ sở** (bài toán con) để tìm ra lời giải bài toán lớn
phải được thực hiện sau hữu hạn bước dựa trên bảng phương án của qui hoạch
động.

### 3. Các ví dụ dễ dàng tiếp cận thuật toán

##### Ví dụ 1:  Bài toán **Fibonacci**
> Dãy Fibonacci là dãy vô hạn các số tự nhiên bắt đầu bằng 1 và 1, sau đó các số tiếp theo sẽ bằng tổng của 2 số liền trước nó, các số đầu tiên của dãy Fibonacci là 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610... 

Nếu tiếp cân bài toán theo cách đệ quy:
```cpp  
Long long fibonacci(n){
    if(n <= 1) return 1;
    else return fib(n - 1) + fib(n - 2);
}
```
Như trên, ta sẽ có rất nhiều bài toán con được tính đi tính lại, điển hình là các số fib(0) và fib(1).

![markdown](https://o2.edu.vn/wp-content/uploads/2021/10/fib-fig.png)

Quy hoạch động chính là một trong số những phương pháp có thể giúp chúng ta tối ưu hóa quá trình tính toán này. Mỗi bài toán con (số fibo) sẽ được lưu lại trước khi tính những bài toán con lớn hơn. Nhờ đó, mà việc tính toán giảm đi đáng kể, mỗi bài toán con chỉ cần tính đúng một lần.

Một ví dụ quy hoạch động với bài toán này như sau:
```cpp
long long fib(n){
    long long dp[n + 1];
    dp[0] = 1;
    dp[1] = 1;
    for(int i = 2; i <= n; i++) dp[i] = dp[i - 1] + dp[i - 2];
    return dp[n]
}
```
Ta có thể thấy các bước thực hiện giảm đi đáng kể

![markdown](https://scontent.fhan2-1.fna.fbcdn.net/v/t39.30808-6/273891675_804511194277010_8630044035101415095_n.jpg?_nc_cat=101&ccb=1-5&_nc_sid=730e14&_nc_ohc=cCzJoLfY29wAX9o74yi&_nc_ht=scontent.fhan2-1.fna&oh=00_AT_MHg6t69UIHYEsPZpJoTlt8nafuFr1kan3771NzabL8Q&oe=620EBBC7)

Nghe có vẻ giống như đệ quy (một bài toán lớn được chia nhỏ thành các bài toán con lồng nhau). Nhưng, phương pháp quy hoạch động sẽ lưu kết quả của bài toán con này, và khi được gọi, nó sẽ không cần phải tính lại, do đó làm giảm thời gian tính toán.


