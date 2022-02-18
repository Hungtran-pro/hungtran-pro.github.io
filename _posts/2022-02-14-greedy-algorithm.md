
# Greedy Algorithms
 1.[Giới thiệu mô hình Tham lam](#1)
 2. [Các nội dung trong việc xây dựng giải pháp Tham lam](#2)
 3. [Một số bài tập sử dụng Tham lam.](#3)

---
### 1. Giới thiệu mô hình Tham lam <a name = "1"> </a>
- **Giải thuật Tham lam (Greedy algorithm)** là một thuật toán xây dựng từng phần giải pháp, luôn lựa chọn quyết định mang lại lợi ích rõ ràng tối ưu nhất ở thời điểm hiện tại (hay còn gọi là lựa chọn tối ưu cục bộ)  với hy vọng giải pháp đó sẽ dấn tới giải pháp tối ưu toàn cục cho bài toán. Giải thuật Tham lam thường được áp dụng cho các vấn đề tối ưu hóa.
- **Giải thuật tham lam**: quyết định sớm và thay đổi đường đi thuật toán theo quyết định đó, và không bao giờ xét lại các quyết định cũ. Chính vì vậy trong nhiều bài toán tham lam có thể không cho kết quả chính xác nhất. Tham lam chỉ có thể áp dụng cho lớp bài toán thỏa mãn 2 điều kiện:
	-  *Ở mỗi bước, ta luôn tạo ra được một lựa chọn tốt nhất ở thời điểm đó.*
	- *Việc liên kết các kết quả mỗi bước sẽ cho ta kết quả tối ưu toàn cục*
	
- ‎**Giải thuật tham lam** nếu như có thể giải quyết một vấn đề, thì nó thường trở thành phương pháp tốt nhất để giải quyết vấn đề đó vì các thuật toán Greedy nói chung hiệu quả hơn các kỹ thuật khác như Lập trình động.

### 2.  Các nội dung trong việc xây dựng giải pháp sử dụng Tham lam. <a name = "2"></a>

Tổng quát, Tham lam được xây dựng bao gồm 5 thành phần chính:
```
1. Một tập các ứng viên (candidate member) mà giải pháp có thể tham lam
2. Một hàm lựa chọn (selection function) để theo đó lựa chọn ứng viên tốt nhất cho lời giải
3. Một hàm thực thi (feasibility function) để quyết định xem một ứng viên có thể được dùng để xấy dựng lời giải hay không.
4. Một hàm mục tiêu (objective function) để xác định giá trị của lời giải hoặc lời giải một phần.
5. Một hàm giải pháp (solution function) để chỉ ra khi nào ta tìm ra lời giải hoàn chỉnh.
```
Khi sử dụng tham lam hai lựa chọn quyết định Tham lam:

- **Lựa chọn tính chất để tham lam**: Khi chưa tìm được lời giải tối ưu toàn cục, nhưng ta biết giải pháp tối ưu cục bộ dựa theo một tính chất nào đó tùy thuộc vào từng yêu cầu trong bài toán và các bài toán con tiếp theo cũng sẽ thực hiện với tính chất như vậy cho tới khi tìm ra giải pháp hoàn chỉnh cho cả bài.
- **Lựa chọn cấu trúc con tối ưu**: Một bài toán con được gọi là 	``có cấu trúc tối ``ưu nếu lời giải tối ưu của bài toán con nằm trong lời giải tối ưu của bài toán lớn.

### 3. Một số bài tập sử dụng Tham lam. <a name="3"></a>
1. Bài toán lựa chọn hành động (activity selection problem)

- **Đè bài:** Cho tập gồm n hành động với hành động thứ i được xác định bởi thời gian bắt đầu là $s_i$  và thời gian kết thúc là $t_i$. Bài toán đặt ra là lựa chọn nhiều nhất các hành động có thể được thực hiện bởi người hoặc gì đó mà không xảy ra mâu thuẫn. Giả sử là một hành động chỉ được thực hiện đơn lẻ tại một thời điểm (Nói cách khác, tại một thời điểm, người này chỉ được thực hiện một nhiệm vụ và phải làm đến thời điểm kết thúc nhiệm vụ đó mới được thực hiện công việc tiếp theo)
- **Input:** 
	- số $n$ là số công việc đưa ra.
	- mảng $s$ với $s_i$ : thời điểm bắt đầu công việc thứ $i$
	- mảng $f$ với $f_i$ thời điểm kết thúc công việc thứ $i$.

- *Nhận xét:* Có thể thấy trong bài toán này mâu thuẫn sẽ xảy ra khi người này thực hiện 2 hành động liên tiếp $j$ và $j+1$ mà thời gian kết thúc của công việc $j$ lại lớn hơn thời gian bắt đầu công việc $j+1$. Vì vậy để giải quyết vấn đề này ta phải đưa ra lựa chọn tối ưu các công việc có không có khoảng thời gian thực hiện trùng nhau.

Để giải quyết vấn đề này, chúng ta có thể sử dụng đến  sinh hoặc quay lui để duyệt từng tập con các công việc trong $n$ công việc từ đó xét ra được trường hợp có số lượng nhiều nhất.  Tuy nhiên độ phức tạp trong cách giải quyết này là $2^n$ không phú hợp trong việc giải quyết đối với trường hợp $n$ lớn.
- **Giải quyết:**
	- Đầu tiên với bài toán chỉ có 1 hành động hoặc có nhiều hành động nhưng đôi một mâu thuẫn thì lựa chọn tốt nhất là chọn 1 hành động.
	- Nếu như có nhiều hơn 1 hành động phù hợp với nhau thì lựa chọn đầu tiên sẽ chọn hành động có kết thúc sớm nhất, các lần lựa chọn tiếp theo sẽ lựa chọn hành động có thời gian bắt đầu sau thời gian kết thúc hành động phía trước và có thời điểm kết thúc sớm nhất. Tiếp tục lựa chọn theo nguyên tắc đó cho các bước tiếp theo.
- **Biểu diễn thuật toán tham lam giải quyết bài toán Activity selection problem**

```
Algorithm Greedy_Activity_Selection (S[], T[], N)

Input: 
	- số n là số công việc đưa ra.
	- S[] thời điểm bắt đầu công việc.
	- F[] thời điểm kết thúc công việc.
Output: Số lượng công việc nhiều nhất có thể thực hiện.

Actions:
B1: Sắp xếp hành động (sắp xếp các hành động theo thứ tự ưu tiên về thời gian kết thúc)
B2: Khởi tạo (Lựa chọn hành động khởi đầu) khi đó, giả sử là i, opt = 1, N = N/{i}
B3: Lặp lại nguyên tắc chọn trên cho việc xét các hành động tiếp theo.
for each_activity j : N 
	if (S[j] <= F[i]) 
		opt++
		N = N/{j}
		i = j
B4: Trả lại kết quả
	return opt
```
- **Kiểm nghiệm**
```
- Input: N = 8;
	S[] = {1, 3, 0, 5, 8, 5, 9, 14}
	F[] = {2, 4, 6, 7, 9, 9, 12, 18}
- Ouput: opt
```
Tiến hành:
![image](https://user-images.githubusercontent.com/85023342/153767145-6ab64eae-6d86-4f03-829c-44c8f0bc6ed5.png)


- **Code C++**
```c++
#include <bits/stdc++.h>

using namespace std;

void sortFinishTime (int S[], int F[], int n) {
	for (int i =  0 ; i < n -  1; ++i) {
		for (int j = i +  1; j < n; ++j) {
			if (F[i] >= F[j]) {
				swap(F[i], F[j]);
				swap(S[i], S[j]);
			}
		}
	}
}

int Activity_Selection_Problem (int s[], int f[], int n)
{
	sortFinishTime(S, F, n); // Buoc 1
	int i = 0, opt = 1; // Khoi tao
	for (int j = i + 1; j < n; ++i) { // Lap
		if (S[j] >= F[i]) {
			i = j; 
			opt++;
		}
	} 
	return opt;
}

int main () {

	int n; cin >> n;
	
	int S[n], F[n];
	for (int i = 0; i < n; ++i) cin >> S[i];
	for (int i = 0; i < n; ++i) cin >> F[i];
	cout << Activity_Selection_Problem(S, F, n);
}
```



