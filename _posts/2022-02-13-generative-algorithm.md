# Generative Algorithm

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

**Bài tập 1**: Liệt kê dãy nhị phân có độ dài là n

Ví dụ: n = 4.

| STT |   Dãy   | STT |   Dãy   |
|-----|---------|-----|---------|
|  0  | 0 0 0 0 |  8  | 1 0 0 0 |
|  1  | 0 0 0 1 |  9  | 1 0 0 1 |
|  2  | 0 0 1 0 |  10 | 1 0 1 0 |
|  3  | 0 0 1 1 |  11 | 1 0 1 1 |
|  4  | 0 1 0 0 |  12 | 1 1 0 0 |
|  5  | 0 1 0 1 |  13 | 1 1 0 1 |
|  6  | 0 1 1 0 |  14 | 1 1 1 0 |
|  7  | 0 1 1 1 |  15 | 1 1 1 1 |

*Dựa trên điều kiện thuật toán sinh, hãy tìm điểm đầu, điểm cuối và quy luật sinh của thuật toán?*



```CPP
#include<iostream>
using namespace std;
#define ll long long
const ll Mod = 1e9+7;
int arr[15];
bool stop_flag;

void initialize(int n){
    for(int i = 0; i < n; i++) arr[i] = 0;
    stop_flag = false;
}

void display_to_screen(int n){
    for(int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
}

void next_structure(int n){
    int i = n - 1;
    while(i >= 0 && arr[i] == 1) i--;
    if(i == -1){
        stop_flag = true;
        return;
    }
    else{
        arr[i] = 1;
        i += 1;
        while(i < n) arr[i++] = 0;
    }
}

int main(){
    int n;
    cin >> n;
    initialize(n);
    while(!stop_flag){
        display_to_screen(n);
        next_structure(n);
    }
    cout << "Chuong trinh chay xong!";
}
```

**Bài tập 2**: Liệt kê tất cả các hoán bị n phần tử từ 1 ⇒ n.

Ví dụ: n = 3.

| STT | Dãy   |
|-----|-------|
|  0  | 1 2 3 |
|  1  | 1 3 2 |
|  2  | 2 1 3 |
|  3  | 2 3 1 |
|  4  | 3 1 2 |
|  5  | 3 2 1 |

*Dựa trên điều kiện thuật toán sinh, hãy tìm điểm đầu, điểm cuối và quy luật sinh của thuật toán?*



```CPP
#include<iostream>
using namespace std;
#define ll long long
const ll Mod = 1e9+7;
int arr[15];
bool stop_flag;

void initialize(int n){
    for(int i = 0; i < n; i++) arr[i] = i + 1;
    stop_flag = false;
}

void display_to_screen(int n){
    for(int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
}

void next_structure(int n){
    int i = n - 2;
    while(i >= 0 && arr[i] > arr[i+1]) i--;
    if(i == -1){
        stop_flag = true;
        return;
    }
    else{
        int j = n - 1;
        while(arr[j] < arr[i]) j--; // Tim vi tri so be hon arr[i] nhung lon nhat
        swap(arr[i], arr[j]);
        i += 1;
        j = n - 1; // Thiet lap j ve tri vi cuoi cung cua mang arr
        while(i < j) swap(arr[i++], arr[j--]);
    }
}

int main(){
    int n;
    cin >> n;
    initialize(n);
    while(!stop_flag){
        display_to_screen(n);
        next_structure(n);
    }
    cout << "Chuong trinh chay xong!";
}
```