---

layout: post
title: "Tìm hiểu về vòng lặp trong Python"
date: 2025-06-09
categories: [Python, Lập trình cơ bản, Week1]
---

## Vòng lặp trong Python

### Đặt vấn đề

Ví dụ, chúng ta được giao nhiệm vụ in dòng chữ "Hello World!" 5 lần. Ta có thể viết:

```python
print("Hello World!")
print("Hello World!")
print("Hello World!")
print("Hello World!")
print("Hello World!")
```

Nhưng nếu phải in 1000 hay 100000 lần thì sao? Việc copy-paste như trên không còn hiệu quả. Giải pháp tối ưu là **sử dụng vòng lặp** để thực hiện thao tác lặp lại một cách hiệu quả hơn.

---

### Định nghĩa vòng lặp

**Vòng lặp** cho phép chúng ta **lặp lại một khối mã** dựa trên một điều kiện hoặc dựa trên các phần tử của một tập hợp.

---

## Vòng lặp `for`

Vòng lặp `for` được dùng để lặp qua các phần tử của một **đối tượng lặp** (`iterable`) như chuỗi (string), danh sách (list), tuple, dictionary, v.v.

<div class="row mt-3">
    <div class="col-full mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Blog/Week1/ForLoop.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Hình n: Cú pháp và luồng thực thi của vòng lặp `for`.
</div>

### Cú pháp

```python
# code trước for
for i in iterable:
    # khối mã cần thực thi
# code sau for
```

* `for`, `in`: là các **từ khóa (keywords)** của Python.
* `:` (dấu hai chấm): **bắt buộc** sau phần điều kiện của vòng lặp.
* **Thụt lề (indentation)**: xác định khối mã thuộc vòng lặp.

### Luồng thực thi

1. **Code trước for** (nếu có) được thực thi đầu tiên.
2. Mỗi lần lặp:

   * Gán phần tử hiện tại cho biến lặp `i`.
   * Thực thi **code bên trong vòng lặp**.
3. Sau khi kết thúc, **code sau for** (nếu có) sẽ được thực thi.

### Sử dụng `range()`

`range(n)` tạo ra một dãy số từ `0` đến `n - 1`. Ví dụ:

```python
for i in range(5):
    print(i)
```

Kết quả:

```
0
1
2
3
4
```

---

## Vòng lặp `while`

Vòng lặp `while` lặp lại **miễn là điều kiện vẫn đúng (`True`)**.

<div class="row mt-3">
    <div class="col-full mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Blog/Week1/WhileLoop.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Hình n: Cú pháp và luồng thực thi của vòng lặp `while`.
</div>

### Cú pháp

```python
# code trước while
while condition:
    # khối mã cần thực thi
# code sau while
```

### Luồng thực thi

1. **Code trước while** được thực thi trước (nếu có).
2. Trong mỗi lần lặp:

   * Nếu điều kiện đúng, **code trong while** được chạy.
   * Sau đó kiểm tra lại điều kiện.
3. Khi điều kiện trở thành **False**, vòng lặp kết thúc và **code sau while** (nếu có) sẽ được thực thi.

### Ví dụ

```python
i = 0
while i < 5:
    print(i)
    i += 1
print("done")
```

Kết quả:

```
0
1
2
3
4
done
```

---

## `break` và `continue` trong vòng lặp

### `break`

`break` được dùng để **thoát hoàn toàn khỏi vòng lặp**, ngay cả khi điều kiện hoặc danh sách chưa kết thúc.

#### Ví dụ

Tìm vị trí đầu tiên của phần tử có giá trị là 5:

```python
numbers = [1, 3, 5, 7, 5, 9]
for i in range(len(numbers)):
    if numbers[i] == 5:
        print(f"Found 5 at index {i}")
        break
```

**Giải thích:** Khi tìm thấy phần tử đầu tiên bằng 5, vòng lặp dừng ngay lập tức nhờ `break`.

---

### `continue`

`continue` được dùng để **bỏ qua phần còn lại của khối mã trong lần lặp hiện tại** và **chuyển sang lần lặp tiếp theo**.

#### Ví dụ

In các số từ 1 đến 10, **bỏ qua các số chẵn**, dùng `while`:

```python
i = 0
while i < 10:
    i += 1
    if i % 2 == 0:
        continue
    print(i)
```

**Giải thích:** Khi gặp số chẵn, `continue` khiến vòng lặp bỏ qua lệnh `print(i)` và quay lại đầu vòng lặp.

Kết quả:

```
1
3
5
7
9
```

---

## Kết luận

Vòng lặp là một công cụ rất mạnh trong lập trình giúp thực hiện các tác vụ lặp đi lặp lại một cách hiệu quả. Việc hiểu và vận dụng đúng các loại vòng lặp (`for`, `while`) cùng với các từ khóa điều khiển (`break`, `continue`) sẽ giúp bạn viết mã ngắn gọn, dễ hiểu và tối ưu hơn rất nhiều.
