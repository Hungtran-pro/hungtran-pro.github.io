<!-- https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax -->

# Chào mừng các bạn đến blog thuật toán cơ bản

Đầu tiên, chúng ta sẽ cùng nhau đi tìm hiểu các khái niệm cơ bản của thuật toán.

## Thuật toán là gì?

Thuật là phương pháp, toán là toán học. Vậy nên, thuật toán là phương pháp toán học. Cụ thể hơn, ở mỗi bài toán, chúng ta sẽ cần tìm ra thuật toán phù hợp nhất với đề bài và áp dụng để giải quyết bài toán đó sao cho thời gian là ngắn nhất và quá trình xử lý là nhanh nhất có thể.

![Ảnh mô tả](/image/0702202201.png)

Như các bạn có thể nhìn thấy ở trên, tôi gọi A là điểm đầu, B là điểm đích. Các bạn có thể nhận thấy ngay có 4 đường(vàng, xanh lam, đỏ và tím) có thể đi từ A đến B và cũng tồn tại 1 đường(xanh lục) không đi tới B được. Hình ảnh minh hoạ tôi lấy ở trên cũng giống như 1 bài toán được đề ra vậy. A là các input đầu vào, B là các output đầu ra. Làm sao để chúng ta chọn được 4 đường đi tới B? Và phải làm sao chúng ta chọn được con đường tốt nhất(màu xanh lam) để giải quyết bài toán với thời gian là ngắn nhất.

Như vậy là các bạn đã có cái nhìn tổng quát về thuật toán là gì. Tiếp theo chúng ta sẽ đi đến với một số lưu ý khi code và độ phức tạp của thuật toán, đây chính là cách mà các bạn tự ước lượng thuật toán của mình để xem xem thuật toán này của mình đã là tốt nhất chưa. Có phải là đường màu xanh lam như trên hình kia không?

***Lưu ý: Trong bài viết này, chúng ta sẽ sử dụng ngôn ngữ lập trình C++ là chủ yếu.***

## I. Làm việc với các con số

- Các dạng số nguyên (int, long, long long)
Một số lỗi thường gặp:
```c++
int a = 123456789
long long b = a * a
cout << b << endl; //-1757895751
```

- Các dạng số không nguyên (float, double)
```C++
double x = 0.3 * 0.3 + 0.1
cout << setprecision(20) << x; // 0.99999999999999988898
```
Với dạng số học double, ở đây, chúng ta có thể thấy đáp án ra 1 số rất gần với 1 nhưng lại không phải là số 1. Vậy nên, nếu chúng ta sử dụng phép so sánh **x == 1** ở đây thì kết quả trả lại sẽ là **false**.

⇒ Khó có thể so sánh 2 số dạng float.

Vậy làm cách nào để có thể so sánh 2 số dạng không nguyên với nhau?

```C++
double ε = 1e-9
if(abs(a-b) < ε){
   // a and b are 
}
```

- Làm ngắn code
```C++
typedef  long long ll
#define ll long long
#define mod 1e-9
```

- Số học mo-dule.
Ở đây nhiều bạn có thể thắc mắc tại sao chúng ta phải dùng số học module? Hay chúng ta có thể dùng long long là được rồi.
Đáp án là không nhé. Đôi lúc để tránh đáp án quá to và dài, chúng ta sử dụng số mo-dule để làm giảm kết quả bài toán, tránh gây mất mát, sai lầm do số quá lớn. Hay đôi khi kết quả đầu ra quá lớn (lớn hơn khoảng chứa của long long) nên sẽ gây ra lỗi.

Ví dụ: Tính giai thừa của số n
```c++
int n;
cin >> n //n = 1000
long long kq = 1;
for(int i = 1; i <= n; i++){
    kq *= i;
}
cout << kq << endl;// kq = 0
```

Đoạn code đơn giản tính giai thừa của số n trên cho ra kq = 0 (hoặc 1 số khác tùy theo complier các bạn dùng) nhưng dễ nhận thấy đây là 1 số **sai** (hiện tượng tràn mảng, vượt ngoài phạm vi chứa của long long)

Chúng ta hãy thử dùng phép chia dư với số  mo-dule xem sao nhé.

```c++
const ll MOD = 1e9+7;
int n;
cin >> n //n = 1000
long long kq = 1;
for(int i = 1; i <= n; i++){
    kq = (kq * i) % MOD;
}
cout << kq << endl;// kq = 641419708
```

Với đoạn code trên, chúng ta có kết quả kq = 641419708 khá đẹp.
Như vậy, với cách chia dư cho số học mo-dule, ta được giá trị nằm trong khoảng **(0, m-1)**. Nhưng đôi khi số module của 1 số âm là 1 số âm hoặc "0". Vậy nên chúng ta cần thêm 1 bước sau:

```C++
x = x % m;
if (x < 0) x += m;
```

Tuy nhiên, cái trên chỉ sử dụng khi chúng ta có phép trừ hay phép toán nào đó làm cho biến x của khả năng trở thành 1 biến âm.

***Lưu ý: Code ngắn chưa chắc đã đúng và thời gian chạy ngắn nhất***

## II. Time Complexity (Độ phức tạp thuật toán)

Một bài toán có thể thực hiện bằng nhiều thuật toán khác nhau. Lựa chọn giải thuật nhanh nhất để giải quyết bài toán là một nhu cầu của thực tế. Vì vậy cần phải có một ước lượng cụ thể bằng toán học để xác định mức độ nhanh chậm của mỗi giải thuật.

Với Time Complexity **O(n)** ước lượng được, chúng ta sẽ có cách nhìn tổng quát, đánh giá xem *"Liệu thuật toán của chúng ta viết ra đã đủ nhanh chưa? Có cần cải thiện ở phần nào nữa không?"*

Độ phức tạp của thuật toán phụ thuộc vào 2 yếu tố:
- Kích thước của dữ liệu đầu vào.
- Phần cứng của máy tính.

Tuy nhiên, nếu ta coi độ phức tạp của thuật toán là số các phép toán sơ cấp thực hiện thì yếu tố phần cứng không còn ảnh hưởng đến quá trình xác định thời gian thực hiện của thuật toán. Với quan niệm này, độ phức tạp của thuật toán chỉ còn phụ thuộc vào kích thước của dữ liệu đầu vào.

![Bảng độ phức tạp của thuật toán](/image/BangDoPhucTapCuaThuatToan.png)
![Biểu đồ độ phức tạp của thuật toán](/image/BieuDoDoPhucTapThuatToan.png)

1. Các luật tính toán độ phức tạp

- Nếu code chỉ có 1 dòng lệnh đơn thuần thì độ phức tạp là **O(1)**
```C++
a++;
b++;
c = a + b;
```

- Nếu code gồm 1 vòng lặp và tăng giảm hằng số c thì độ phức tạp là **O(n)**
```C++
for(int i = 1; i <= n; i++){
    <Code O(1)>
}
```

- Nếu code gồm các k vòng lặp lồng nhau và đều duyệt qua tất cả các dữ liệu đầu vào như nhau thì độ phức tạp của thuật toán là O(n^k)

```C++
for(int i = 1; i <= n; i++){
    for(int i = 1; i <= n; i++){
        <Code O(1)>
    }
} //O(n^2)
```

- Nếu code gồm 1 vòng lặp và được chia hoặc nhân với 1 hằng số c thì độ phức tạp thuật toán là **O(log(n))**

```C++
for(int i = 1; i <= n; i = i * c){
    <Code O(1)>
} //O(log(n))
```

- Nếu code gồm 1 vòng lặp và được chia hoặc nhân với 1 hàm số mũ thì độ phức tạp thuật toán là **O(log(log(n)))**

```C++
for(int i = 1; i <= n; i = pow(i, c)){
    <Code O(1)>
} //O(log(log(n)))
```

Một số ví dụ về độ phức tạp của thuật toán:

```C++
for(int i = 1; i < 3 * n; i++){
    <Code O(1)>
}

for(int i = 1; i < 5 + n; i++){
    <Code O(1)>
}

for(int i = 1; i < n; i += 2){
    <Code O(1)>
}
```
Dù các dòng code ở trên chạy độc lập với nhau và có số lượng lặp là khác nhau nhưng tổng độ phức tạp vẫn được coi là **O(n)**

Thuật toán sau đây được coi là có độ phức tạp **O(n^2)**

```C++
for(int i = 1; i <= n; i++){
    for(int j = 1; j <= i; j++){
        <Code O(1)>
    }
}
```

Giải thích:
> Lượng tính toán: 1 + 2 + ... + n = 1 / 2 + (n^2 + n) = O(n^2)

Lí giải cho việc này, thì có 1 định nghĩa sau đây:
- Nếu 1 thuật toán gồm các giai đoạn liên tiếp nhau, thì tổng thời gian độ phức tạp ddwuocj tính bằng thwoif gian lớn nhất của 1 giai đoạn. Hay còn gọi là thời gian của bottleneck (nút thắt cổ chai).

Ví dụ:
```C++
for(int i = 1; i <= n; i++){
    <Code O(1)>
}

for(int i = 1; i < 5 + n; i++){
    for(int j = 1; j <= n; j++){
        <Code O(1)>
    }
}

for(int i = 1; i < n; i++){
    <Code O(1)>
}
// Độ phức tạp của thuật toán trên là O(n^2)
```

Nhưng đôi khi cũng có các yếu tố khác n
Ví dụ:
```C++
for(int i = 1; i < 5 + n; i++){
    for(int j = 1; j <= m; j++){
        <Code O(1)>
    }
} //O(nm)
```

Vậy tổng lượng thời gian của vòng lặp là bao nhiêu?

```C++
void f(int n){
    if(n == 1) return;
    f(n-1);
}
```

Nhận thấy khi ta gọi **f(n)** thì chúng ta đang gọi hàm con này n lần ⇒ **O(n)**
Tiếp theo, phần code bên trong có độ phức tạp là **O(1)**
⇒ Tổng độ phức tạp là **O(n)**

Vậy độ phức tạp của thuật toán dưới đây là bao nhiêu?

```C++
void g(int n){
    if(n == 1) return;
    g(n-1);
    g(n-1);
}
```

##Như vậy, thông qua bài viết đầu tiên, các bạn cũng đã nắm được khái niệm thuật toán, các con số, và độ phức tạp của thuật toán. Chúng ta sẽ đến với các thuật toán kinh điển ở các trang tiếp theo.