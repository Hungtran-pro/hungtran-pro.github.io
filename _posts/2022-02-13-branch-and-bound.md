# Nhánh cận (Branch and Bound)

![Ảnh mô tả](/image/10022022.png)

## Nhánh cận là gì?

- Nhánh cận trong quay lui:
	- Là một kỹ thuật đánh giá việc tiếp tục đào sâu có tạo ra cấu hình tốt hơn cấu hình tốt nhất mà ta đang lưu trữ hay không.

	- Nhờ có nhánh cận mà ta có thể đưa ra quyết định **quay lui sớm hơn** Backtracking cổ điển.

## Phương pháp

Thuật toán nhánh cận thường được dùng trong việc giải quyết các bài toán tối ưu tổ hợp. Bài toán được phát biểu dưới dạng như sau:

Tìm min{f(X) : X ∈ D}, với D = { X = (x1, x2, ..., xn) ∈ A1 x A2 x ... x An : X thỏa mãn tính chất P}.

	- X ∈ D được gọi là một phương án của bài toán.
	- Hàm f(X) được gọi là mục tiêu của bài toán.
	- Miền D được gọi là tập phương án của bài toán.


Để giải quyết bài toán trên, ta có thể sử dụng thuật toán quay lui duyệt các phần tử X ∈ D, phần tử X* làm cho F(X*) đạt giá trị nhỏ nhất (hoặc lớn nhất) là phương án tối ưu của bài toán. Thuật toán nhánh cận có thể giải quyết được bài toán đặt ra nếu ta xây dựng được một hàm g xác định trên tất cả phương án bộ phận cấp k của bài toán sao cho:

	g(a1, a2, ..., ak) <= min{f(X) : X ∈ D, xi = ai, i = 1, 2, ..., k}


Nói cách khác, giá trị của hàm g tại phương án bộ phận cấp k là g(a1, a2, ... , ak) không vượt quá giá trị nhỏ nhất của hàm mục tiêu trên tập con các phương án:

	D(a1, a2, ..., ak) = {X ∈ D: xi = ai, i = 1, 2, ..., k}

Giá trị của hàm g(a1, a2, ..., ak) là cận dưới của hàm mục tiêu trên tập D(a1, a2, ..., ak). Hàm g được gọi là hàm cận dưới, g(a1, a, ..., ak) gọi là cận dưới của tập D(a1, a2, ..., ak).

Giả sử ta đã có hàm g. Để giảm bớt khối lượng duyệt trên tập phương án, bằng thuật toán quay lui ta xác định được X* là phương án làm cho hàm mục tiêu có giá trị nhỏ nhất trong số các phương án tìm được f* = f(X*). Ta gọi X* là phương án tốt nhất hiện có, f* là kỉ lục hiện tại.

Nếu f* < g(a1, a2, ..., ak) thì f* <= min{f(X) : X ∈ D, xi = ai, i = 1, 2, ..., k}

Điều này có nghĩa tập D(a1, a2, ..., ak) chắc chắn không chứa phương án tối ưu. Trong trường hợp này ta không cần thiết phải khai triển phương án bộ phận (a1, a2, ..., ak). Tập D(a1, a2, ..., ak) cũng bị loại bỏ khỏi quá trình duyệt. Nhờ đó, số lượng các phương án cần duyệt nhỏ đi trong quá trình tìm kiếm. Thuật toán nhánh cận tổng quát được mô tả chi tiết như sau:


![Ảnh mô tả](/image/branchandbound.jpg)


## Ví dụ

Giải bài toán cái túi bằng thuật toán nhánh cận.

Một nhà thám hiểm cần đem theo 1 cái tụi trọng lượng không vượt quá b. Có n đồ vật cần đem theo. Đồ vật thứ i có trọng lượng ai và giá trị sử dụng ci. Hãy tìm cách đưa đồ vật vào túi cho nhà thám hiểm sao cho tổng giá trị sử dụng các đồ vật trong túi là lớn nhất.

**Input:**
	- Dòng đầu tiên ghi lại 2 số n và b tương ứng với số lượng đồ vật và trọng lượng tối đa của túi.
	- N dòng kế tiếp, mỗi dòng ghi lại bộ đôi ai, ci tương ứng với trọng lượng và giá trị sử dụng của vật thứ i.

**Output:** 
	- Dòng đầu tiên ghi lại giá trị tối ưu của bài toán.
	- Dòng kế tiếp ghi lại phương án tối ưu của bài toán.

![Ảnh mô tả](/image/caitui.png)

Chương trình giải quyết bài toán được thực hiện như dưới đây:

```c++
#include <iostream>
#include <fstream>
#define MAX 100
using namespace std;
int X[MAX]; // phương án tối ưu của bài toán
int n; //số lượng đồ vật
float b, weight=0; //trọng lượng túi
float cost=0; // giá trị sử dụng phương án hiện tại
int XOPT[MAX]; //phương án tối ưu của bài toán
float FOPT=0; //giá trị tối ưu của bài toán
float A[MAX], C[MAX];//vector trọng lượng và giá trị sử dụng
void Init (void) { //đọc dữ liệu
	ifstream fp("caitui.in"); fp>>n;fp>>b;
	for(int i=1; i<=n; i++){
		fp>>A[i]>>C[i];
	}
	fp.close();
}
void Result(void) {//đưa ra giá trị và phương án tối ưu
	cout<<"Giá trị tối ưu:"<<FOPT<<endl;
	cout<<"Phương án tối ưu:";
	for(int i=1; i<=n; i++)
		cout<<XOPT[i]<<" ";
}
void Update(void) { //cập nhật phương án tối ưu
	if (cost> FOPT){
		FOPT =cost;
		for (int i=1; i<=n; i++)
			XOPT[i]=X[i];
	}
}
void Back_Track(int i){
	int j, t = (int)((b-weight)/A[i]); //giá trị khởi đầu
	for(int j= t; j>=0; j--){
		X[i] = j;
		weight = weight+A[i]*X[i]; //trọng lượng phương án bộ phận
		cost = cost + C[i]*X[i]; //giá trị phương án bộ phận
		if (i==n) Update(); //ghi nhận kỷ lục
		else if ( cost + ( C[i+1]*((b- weight)/A[i+1]))>FOPT) //kiểm tra cận
		Back_Track(i+1);
		weight = weight-A[i]*X[i];
		cost = cost - C[i]*X[i];
	}
}
int main (void ){ //chương trình chính
	Init();
	Back_Track(1);
	Result();
}
```