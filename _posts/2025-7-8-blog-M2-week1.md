---
layout: post
title: "Recap Kiến Thức Tuần 2 Module 1 - AIO 2025"
date: 2025-06-09
categories: [Python, Numpy, Week2]
---

# Recap Kiến Thức Tuần 1 - AIO 2025

🔖 **Mục lục nhanh**:
- [1. Kiến thức cơ bản (Numpy)](#1-kiến-thức-cơ-bản)
  - [1.1. Giới thiệu NumPy](#11-kiểu-dữ-liệu)
  - [1.2. Cấu trúc dữ liệu: Mảng đa chiều](#12-danh-trong-python)
  - [1.3. 🔧 Các hàm tạo mảng cơ bản](#13-từ-điển-trong-python)
  - [1.4. 🔍 Indexing và Slicing](#14-hàm-trong-python)
  - [1.5. 🔄 Broadcasting - Phép toán thông minh](#15-rẽ-nhánh-trong-python)
  - [1.6. 🖼️ Ứng dụng vào Machine Learning/Deep Learning](#16-ứng-dụng-thực-tế)
- [2. Kiến thức mở rộng](#2-kiến-thức-mở-rộng)
  - [2.1. Cosine Similarity](#21-SQL)
  - [2.2. NoSQL và MongoDB](#22-python-methodology)
- [3. Tổng kết](#3-tổng-kết)

---

## 1. Kiến Thức Cơ Bản

### 📚 Giới thiệu NumPy

NumPy (Numerical Python) là một thư viện Python mạnh mẽ dành cho tính toán khoa học. Nó cung cấp:

- **Mảng đa chiều hiệu quả**: Cấu trúc dữ liệu cơ bản cho machine learning
- **Tính toán vectorized**: Xử lý toàn bộ mảng cùng lúc thay vì từng phần tử
- **Tích hợp tốt**: Là nền tảng cho pandas, scikit-learn, TensorFlow...

### 🎯 Tại sao cần NumPy?

```python
# Cách Python thuần túy - chậm
python_list = [1, 2, 3, 4]
result = []
for i in python_list:
    result.append(i * 2)

# Cách NumPy - nhanh và ngắn gọn
import numpy as np
arr = np.array([1, 2, 3, 4])
result = arr * 2  # Tự động nhân tất cả phần tử
```

### 📊 Cấu trúc dữ liệu: Mảng đa chiều

#### 1D Array (Mảng 1 chiều)
```python
# Giống như danh sách điểm số của một học sinh
scores = np.array([8, 9, 7, 10])
print(scores.shape)  # (4,) - 4 phần tử
```

#### 2D Array (Mảng 2 chiều - Ma trận)
```python
# Giống như bảng điểm của cả lớp
class_scores = np.array([
    [8, 9, 7, 10],    # Học sinh 1
    [6, 8, 9, 7],     # Học sinh 2
    [9, 10, 8, 9]     # Học sinh 3
])
print(class_scores.shape)  # (3, 4) - 3 học sinh, 4 môn
```

#### 3D Array (Mảng 3 chiều)
```python
# Giống như điểm của nhiều lớp trong nhiều học kỳ
school_scores = np.array([
    [[8, 9, 7], [6, 8, 9]],    # Học kỳ 1
    [[9, 8, 10], [7, 9, 8]]    # Học kỳ 2
])
print(school_scores.shape)  # (2, 2, 3) - 2 học kỳ, 2 lớp, 3 môn
```

### 🔧 Các hàm tạo mảng cơ bản

#### Tạo mảng đặc biệt
```python
# Mảng toàn số 0 - hữu ích để khởi tạo
zeros_arr = np.zeros((3, 4))
print(zeros_arr)
# [[0. 0. 0. 0.]
#  [0. 0. 0. 0.]
#  [0. 0. 0. 0.]]

# Mảng toàn số 1 - hữu ích để tạo mask
ones_arr = np.ones((2, 3))
print(ones_arr)
# [[1. 1. 1.]
#  [1. 1. 1.]]

# Dãy số liên tiếp - giống range() nhưng mạnh hơn
sequence = np.arange(0, 10, 2)  # từ 0 đến 10, bước nhảy 2
print(sequence)  # [0 2 4 6 8]
```

#### Reshape - Thay đổi hình dạng
```python
# Ví dụ: Chuyển dữ liệu 1D thành bảng 2D
data = np.arange(12)  # [0, 1, 2, ..., 11]
table = data.reshape(3, 4)  # Chuyển thành bảng 3x4
print(table)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Flatten - Chuyển về 1D
flat_data = table.flatten()
print(flat_data)  # [0 1 2 3 4 5 6 7 8 9 10 11]
```

### 🔍 Indexing và Slicing

#### Slicing cơ bản
```python
# Ví dụ: Bảng điểm học sinh
grades = np.array([
    [8, 9, 7, 10],  # Toán, Lý, Hóa, Sinh
    [6, 8, 9, 7],
    [9, 10, 8, 9]
])

# Lấy điểm Toán của tất cả học sinh
math_scores = grades[:, 0]  # [8, 6, 9]

# Lấy điểm của học sinh đầu tiên
first_student = grades[0, :]  # [8, 9, 7, 10]

# Lấy điểm Lý và Hóa của 2 học sinh đầu
physics_chemistry = grades[0:2, 1:3]
# [[9, 7],
#  [8, 9]]
```

#### Boolean Indexing
```python
# Tìm học sinh có điểm Toán >= 8
high_math_students = grades[grades[:, 0] >= 8]
print(high_math_students)

# Tìm tất cả điểm >= 9
excellent_grades = grades[grades >= 9]
print(excellent_grades)  # [9, 10, 9, 10, 9]
```

### 📈 Các phép toán thống kê

```python
# Dữ liệu doanh thu theo tháng của các cửa hàng
revenue = np.array([
    [100, 120, 110, 130],  # Cửa hàng 1
    [90, 100, 95, 105],    # Cửa hàng 2
    [110, 130, 125, 140]   # Cửa hàng 3
])

# Tổng doanh thu tất cả
total_revenue = np.sum(revenue)
print(f"Tổng doanh thu: {total_revenue}")

# Doanh thu trung bình theo tháng (axis=0)
monthly_avg = np.mean(revenue, axis=0)
print(f"Doanh thu TB theo tháng: {monthly_avg}")

# Doanh thu trung bình của từng cửa hàng (axis=1)
store_avg = np.mean(revenue, axis=1)
print(f"Doanh thu TB từng cửa hàng: {store_avg}")

# Cửa hàng có doanh thu cao nhất
best_store = np.argmax(np.sum(revenue, axis=1))
print(f"Cửa hàng tốt nhất: {best_store}")
```

### 🔄 Broadcasting - Phép toán thông minh

Broadcasting cho phép thực hiện phép toán giữa các mảng có kích thước khác nhau:

```python
# Ví dụ: Tăng lương cho nhân viên
salaries = np.array([
    [3000, 3500, 4000],  # Phòng A
    [2800, 3200, 3800],  # Phòng B
    [3200, 3600, 4200]   # Phòng C
])

# Tăng lương đồng loạt 500k cho tất cả
new_salaries = salaries + 500
print("Lương sau khi tăng:")
print(new_salaries)

# Tăng lương theo % khác nhau cho từng phòng
bonus_rate = np.array([0.1, 0.15, 0.12])  # 10%, 15%, 12%
bonus_salaries = salaries * (1 + bonus_rate.reshape(-1, 1))
print("Lương sau khi tăng theo %:")
print(bonus_salaries)
```

### 🖼️ Ứng dụng vào Machine Learning/Deep Learning

#### 1. Softmax Function
```python
def softmax(x):
    """
    Chuyển đổi điểm số thành xác suất
    Ví dụ: [2, 1, 0] -> [0.67, 0.24, 0.09]
    """
    # Trừ max để tránh overflow
    x_stable = x - np.max(x)
    exp_x = np.exp(x_stable)
    return exp_x / np.sum(exp_x)
```

#### 2. Tạo dữ liệu ngẫu nhiên
```python
# Seed để reproducible
np.random.seed(42)

# Dữ liệu phân phối chuẩn
normal_data = np.random.randn(1000)  # mean=0, std=1

# Dữ liệu uniform
uniform_data = np.random.uniform(0, 1, 1000)

# Chọn ngẫu nhiên
choices = np.random.choice(['A', 'B', 'C'], size=100, p=[0.5, 0.3, 0.2])
```

#### 3. Tiền xử lý ảnh (image preprocessing) trước khi huấn luyện mô hình bằng pytorch

> Pytorch yêu cầu định dạng ảnh là CHW (Channels, Height, Width) vì vậy cần chuyển đổi kênh màu.

```python
# Hàm chuẩn hóa ảnh
def transform(img, img_size=(224, 224)):
    img = img.resize(img_size)
    img = np.array(img)[..., :3]  # Đảm bảo lấy 3 kênh RGB
    img = torch.tensor(img).permute(2, 0, 1).float()  # Đổi thành (C, H, W)
    normalized_img = img / 255.0  # Chuẩn hóa về [0, 1]

    return normalized_img

# Định nghĩa bộ dataset
class CIFARDataset(Dataset):
    def __init__(
        self,
        X, y,
        transform=None
    ):
        self.transform = transform
        self.img_paths = X
        self.labels = y

    def __len__(self):
        return len(self.img_paths)

    def __getitem__(self, idx):
        img_path = self.img_paths[idx]
        img = Image.open(img_path).convert("RGB")

        if self.transform:
            img = self.transform(img) # Áp dụng hàm chuẩn hóa vào bộ dataset

        return img, self.labels[idx]
```

## 2. Kiến Thức Mở Rộng
### 2.1 SQL
#### Database là gì?
Hãy tưởng tượng một database như một thư viện khổng lồ được tổ chức cực kỳ khoa học. Thay vì sách, chúng ta có dữ liệu. Và thay vì kệ sách, chúng ta có các **bảng (tables)**. Mỗi bảng chứa một loại thông tin cụ thể, ví dụ: một bảng lưu trữ thông tin khách hàng, một bảng khác lưu trữ thông tin sản phẩm, và một bảng nữa là lịch sử đơn hàng.

Trong mỗi bảng, dữ liệu được sắp xếp theo **hàng (rows)** và **cột (columns)**. Mỗi hàng là một bản ghi duy nhất (ví dụ: thông tin của một khách hàng cụ thể), và mỗi cột là một thuộc tính của bản ghi đó (ví dụ: tên, địa chỉ, số điện thoại của khách hàng).

Hầu hết các database mà chúng ta làm việc ngày nay là **cơ sở dữ liệu quan hệ (relational databases)**. Điều này có nghĩa là các bảng có thể được liên kết với nhau thông qua các mối quan hệ logic, giúp chúng ta dễ dàng kết hợp thông tin từ nhiều nguồn khác nhau.

---

#### SQL: Ngôn ngữ giao tiếp với dữ Liệu

SQL là ngôn ngữ tiêu chuẩn để giao tiếp với cơ sở dữ liệu quan hệ, chuyên biệt cho các tác vụ như:

* **Truy vấn dữ liệu:** Lấy thông tin.
* **Thao tác dữ liệu:** Thêm, sửa, xóa dữ liệu.
* **Định nghĩa dữ liệu:** Xây dựng cấu trúc database.

SQL được sử dụng rộng rãi nhờ tính hiệu quả và khả năng tương thích với nhiều hệ quản trị cơ sở dữ liệu (MySQL, PostgreSQL, SQL Server, Oracle...).

---

#### SQL trong phân tích dữ liệu

Dựa trên các kỹ năng cần thiết cho Data Analysis, SQL được chia thành 4 cấp độ chính:

##### 1. Basics (Cơ bản)

Đây là những câu lệnh nền tảng để trích xuất và sắp xếp dữ liệu.

* **`SELECT`**: Chọn cột dữ liệu.
    ```sql
    SELECT customer_name, email
    FROM customers;
    ```
* **`FROM`**: Chỉ định bảng nguồn.
    ```sql
    SELECT *
    FROM products;
    ```
* **`WHERE`**: Lọc hàng theo điều kiện.
    ```sql
    SELECT product_name, price
    FROM products
    WHERE price > 50;
    ```
* **`GROUP BY`**: Nhóm các hàng để tổng hợp.
    ```sql
    SELECT category, COUNT(product_id) AS num_products
    FROM products
    GROUP BY category;
    ```
* **`ORDER BY`**: Sắp xếp kết quả.
    ```sql
    SELECT customer_name, total_orders
    FROM customers
    ORDER BY total_orders DESC;
    ```
* **`HAVING`**: Lọc các nhóm đã được tổng hợp.
    ```sql
    SELECT category, AVG(price) AS avg_price
    FROM products
    GROUP BY category
    HAVING AVG(price) > 100;
    ```

##### 2. Intermediate (Trung cấp)

Nâng cao khả năng lọc và xử lý dữ liệu với các toán tử và hàm.

* **`BETWEEN`**: Lọc giá trị trong phạm vi.
    ```sql
    SELECT order_id, order_date
    FROM orders
    WHERE order_date BETWEEN '2025-01-01' AND '2025-01-31';
    ```
* **`LIKE`**: Tìm kiếm mẫu chuỗi.
    ```sql
    SELECT customer_name, email
    FROM customers
    WHERE customer_name LIKE 'Nguyen%';
    ```
* **`NULL`**: Kiểm tra giá trị rỗng.
    ```sql
    SELECT product_name
    FROM products
    WHERE description IS NULL;
    ```
* **`IN`**: Kiểm tra giá trị trong danh sách.
    ```sql
    SELECT product_name, category
    FROM products
    WHERE category IN ('Electronics', 'Books');
    ```
* **`OFFSET` / `LIMIT`**: Phân trang kết quả.
    ```sql
    SELECT customer_name
    FROM customers
    ORDER BY customer_id
    LIMIT 10 OFFSET 20;
    ```
* **`COALESCE`**: Trả về giá trị không `NULL` đầu tiên.
    ```sql
    SELECT product_name, COALESCE(description, 'No description available') AS product_description
    FROM products;
    ```

##### 3. Joins (Kết Nối Bảng)

Kỹ năng thiết yếu để kết hợp dữ liệu từ nhiều bảng.

* **`INNER JOIN`**: Trả về hàng trùng khớp ở cả hai bảng.
    ```sql
    SELECT o.order_id, c.customer_name
    FROM orders o
    INNER JOIN customers c ON o.customer_id = c.customer_id;
    ```
* **`LEFT JOIN`**: Trả về tất cả hàng từ bảng trái và các hàng trùng khớp từ bảng phải.
    ```sql
    SELECT c.customer_name, o.order_id
    FROM customers c
    LEFT JOIN orders o ON c.customer_id = o.customer_id;
    ```
* **`RIGHT JOIN`**: Tương tự `LEFT JOIN`, ưu tiên bảng phải.
    ```sql
    SELECT p.product_name, oi.quantity
    FROM order_items oi
    RIGHT JOIN products p ON oi.product_id = p.product_id;
    ```
* **`SELF JOIN`**: Kết nối một bảng với chính nó.
    ```sql
    SELECT e1.employee_name AS employee, e2.employee_name AS manager
    FROM employees e1
    JOIN employees e2 ON e1.manager_id = e2.employee_id;
    ```

##### 4. Advanced (Nâng cao)

Các kỹ thuật mạnh mẽ cho phân tích dữ liệu phức tạp.

* **`WINDOW FUNCTIONS`**: Thực hiện tính toán trên một tập hợp con các hàng liên quan.
    ```sql
    SELECT
        order_id,
        total_amount,
        AVG(total_amount) OVER (PARTITION BY DATE_TRUNC('month', order_date)) AS monthly_avg_amount
    FROM
        orders;
    ```
* **`RANK()` / `DENSE_RANK()` / `ROW_NUMBER()`**: Xếp hạng các hàng.
    ```sql
    SELECT
        product_name,
        category,
        price,
        RANK() OVER (PARTITION BY category ORDER BY price DESC) AS price_rank_in_category
    FROM
        products;
    ```
* **`PIVOT`**: Chuyển đổi hàng thành cột để tổng hợp. (Cú pháp tùy DBMS)
    ```sql
    SELECT
        ProductName,
        [2023] AS Sales_2023, 
        [2024] AS Sales_2024  
    FROM
        (
            SELECT
                p.ProductName,
                YEAR(s.SaleDate) AS SaleYear,
                s.Quantity AS SoldQuantity
            FROM
                Products p
            JOIN
                Sales s ON p.ProductID = s.ProductID
            WHERE
                YEAR(s.SaleDate) IN (2023, 2024) 
        ) AS SourceData
    PIVOT
    (
        SUM(SoldQuantity) 
        FOR SaleYear IN ([2023], [2024])
    ) AS PivotedSalesByYear;
    ```
* **`CTE` (Common Table Expressions)**: Định nghĩa các tập kết quả tạm thời để dễ đọc và quản lý.
    ```sql
    WITH MonthlySales AS (
        SELECT
            DATE_TRUNC('month', order_date) AS sales_month,
            SUM(quantity * price) AS total_monthly_sales
        FROM
            orders
        GROUP BY
            sales_month
    )
    SELECT
        sales_month,
        total_monthly_sales
    FROM
        MonthlySales
    WHERE
        total_monthly_sales > 10000;
    ```
    
### 2.2 Python Methodology

### 2.2.1: CƠ BẢN VỀ CLEAN CODE VÀ PEP-8

#### I. Clean code

Clean code là mã nguồn rõ ràng, dễ đọc, dễ bảo trì, có khả năng mở rộng và dễ dàng kiểm thử.

- **Readable (dễ đọc và dễ hiểu)**: Code nên được viết sao cho người khác có thể dễ dàng hiểu được mục đích và cách thức hoạt động.
- **Maintainable (dễ bảo trì)**: Clean code nên dễ dàng sửa đổi, mở rộng và tái sử dụng mà không gây ra lỗi phụ.
- **Testable (dễ kiểm thử)**: Code sạch nên được thiết kế để dễ dàng viết unit test và thực hiện kiểm thử tự động.
- **Extensible (có khả năng mở rộng)**: Code được thiết kế để dễ dàng thêm tính năng mới mà không cần thay đổi code hiện tại.

##### Mục tiêu của clean code

Clean code giúp các lập trình viên dễ dàng làm việc với nó như sửa lỗi, mở rộng tính năng và tái sử dụng.

##### Lợi ích của clean code

Clean code giúp tăng hiệu suất làm việc, cải thiện hợp tác nhóm và giảm chi phí bảo trì dài hạn

- **Giảm thiểu lỗi**: mã dễ đọc và dễ hiểu giúp phát hiện và ngăn ngừa lỗi hiệu quả hơn.
- **Giảm chi phí và thời gian phát triển**: mã sạch giúp việc gỡ lỗi và phát triển tính năng mới nhanh hơn.
- **Tăng hiệu suất làm việc của nhóm**: khi mọi thành viên trong nhóm đều hiểu và làm việc với cùng một phong cách clean code thì hợp tác sẽ hiệu quả hơn và nếu có người mới tham gia dự án thì có thể nhanh chóng hòa nhập và bắt đầu đóng góp vào dự án.
- **Dễ dàng mở rộng**: Clean code có cấu trúc rõ ràng, dễ dàng thêm tính năng mới mà không làm ảnh hưởng đến hệ thống hiện tại.

#### II. PEP-8

**PEP-8 (Python Enhancement Proposal 8)** là **tiêu chuẩn định dạng code Python chính thức**, do Guido van Rossum – cha đẻ của Python – tạo ra. Mục tiêu của PEP-8 là đảm bảo **tính nhất quán và dễ đọc** trên toàn dự án, **giảm lỗi**, và **cải thiện hiệu quả làm việc nhóm**.

##### Các quy tắc chính của PEP-8 bao gồm:

- **Quy tắc đặt tên (Naming Convention)**
    - **Biến/Hàm**: snake_case (chữ thường, dấu gạch dưới)
    - **Class**: PascalCase (viết hoa chữ cái đầu mỗi từ)
    - **Hằng số**: UPPER_CASE (tất cả chữ hoa, dấu gạch dưới)
- **Thụt lề**: Luôn dùng **4 khoảng trắng** cho mỗi cấp thụt lề, không dùng tab.
- **Khoảng trắng**: Thêm khoảng trắng hai bên phép toán (a = b + c), sau dấu phẩy (f(a, b)) và không thêm trong ngoặc.
- **Giới hạn độ dài dòng code**: Tối đa **79 ký tự/dòng** cho mã nguồn và **72 ký tự/dòng** cho docstring/comment
- **Tổ chức Import đúng chuẩn**: Sắp xếp theo thứ tự: thư viện chuẩn, thư viện bên thứ ba và module nội bộ
- **Dòng trắng và cấu trúc hàm/class**: Sử dụng **2 dòng trắng** để phân tách các định nghĩa class và **1 dòng trắng** giữa các hàm/phương thức trong class

##### Tài liệu hóa (Documentation) và Công cụ hỗ trợ

Để code dễ hiểu hơn, bạn cần tài liệu hóa bằng **docstring** (đặt trong cặp ba nháy kép """ sau định nghĩa hàm) và sử dụng **type hints** (annotations). Docstring có thể theo nhiều định dạng như Google style hay NumPy style và type hints giúp kiểm tra kiểu dữ liệu tĩnh, phát hiện lỗi sớm.

Các công cụ kiểm tra và định dạng code tự động giúp tuân thủ PEP-8 và Clean Code:

- **Flake8**: Kiểm tra cú pháp, style (PEP-8), phát hiện lỗi logic và độ phức tạp
- **Black**: Định dạng code tự động, chuẩn hóa style
- **Pylint**: Phân tích tĩnh code, đánh giá chất lượng
- **Mypy**: Kiểm tra kiểu dữ liệu tĩnh dựa trên type annotations.

Bên cạnh đó, cũng nên tổ chức dự án Python theo cấu trúc chuẩn, bao gồm các thư mục cho mã nguồn (src/), kiểm thử (tests/), tài liệu (docs/), tài nguyên (resources/), và các file cấu hình như README.md, .gitignore

### 2.2.2: VIẾT CODE PYTHONIC

**Code Pythonic** nghĩa là tận dụng tối đa tính năng và đặc điểm riêng của Python để viết code. Code Pythonic **dễ đọc, dễ hiểu, ngắn gọn như đọc tiếng Anh**, đồng thời tuân thủ các quy ước và triết lý của Python

#### Triết lý Python (The Zen of Python)

Triết lý này, được Tim Peters viết trong PEP 20, bao gồm 19 nguyên tắc hướng dẫn thiết kế Python. Một số nguyên tắc tiêu biểu là:

- **Beautiful is better than ugly** (Cái đẹp tốt hơn cái xấu).
- **Explicit is better than implicit** (Rõ ràng tốt hơn ẩn ý).
- **Simple is better than complex** (Đơn giản tốt hơn phức tạp).
- **Complex is better than complicated** (Phức tạp vẫn tốt hơn rắc rối).
- **Flat is better than nested** (Phẳng tốt hơn lồng nhau).

#### Các Kỹ thuật Pythonic Phổ biến

- **Indexes và Slices**: Cho phép truy cập và thao tác linh hoạt với các phần tử trong chuỗi (list, tuple, string) bằng cú pháp sequence[start:stop:step]
    - Ví dụ: data[::2] (phần tử chẵn), data[::-1] (đảo ngược)
- **List, Dict, Set Comprehensions**: Viết code gọn và nhanh hơn cho việc tạo danh sách, từ điển, tập hợp.
    - Ví dụ: squares = [n**2 for n in numbers]
- **Context Managers (với with)**: Cơ chế quản lý tài nguyên, giúp tự động giải phóng tài nguyên (đóng file, kết nối DB) khi khối lệnh kết thúc, ngay cả khi có lỗi.
    - Ví dụ: with open('file.txt', 'r') as f:
    - Có thể tạo context manager riêng với decorator @contextmanager từ contextlib
- **So Sánh và Điều Kiện - Pythonic Style**:
    - So sánh với None: Dùng is hoặc is not (if x is None) thay vì ==
    - So sánh Boolean: Không cần so sánh tường minh (if is_active: thay vì if is_active == True)
    - Kiểm tra chuỗi/list/dict rỗng: Tận dụng truthiness (if not my_list:)
    - Kiểm tra trong collection: Dùng in (if item in my_list:)
    - Chaining comparison: So sánh chuỗi (if 0 < x <= 10:)
- **Properties và dấu underscore _**
    - @property: Cho phép sử dụng method như thuộc tính, giúp code gọn và dễ kiểm soát truy cập.
    - _var (Single Underscore): Quy ước cho biến private hoặc "internal use"
    - __var (Double Underscore): Name mangling, giúp tránh xung đột khi kế thừa
    - __var (Double Underscore hai bên): Dành cho phương thức đặc biệt (magic/dunder methods)
    - _ (Một dấu gạch dưới): Dùng làm biến tạm không quan trọng

### 2.2.3: NGUYÊN LÝ CHUNG ĐỂ VIẾT CODE TỐT

Phần này tập trung vào các nguyên lý cốt lõi giúp tạo ra mã bền vững và dễ bảo trì

- **DRY (Don't Repeat Yourself - Đừng lặp lại chính mình)**
    - **Nguyên tắc**: Tránh lặp lại code, mỗi kiến thức nên được định nghĩa một lần duy nhất
    - **Lợi ích**: Giảm lỗi, code ngắn gọn, dễ bảo trì, tăng khả năng tái sử dụng.
    - **Áp dụng**: Tách các đoạn code lặp lại thành functions, classes, hoặc modules.
- **YAGNI (You Aren't Gonna Need It - Bạn sẽ không cần đến nó)**
    - **Nguyên tắc**: Không thêm tính năng cho đến khi thực sự cần thiết, tránh phức tạp hóa không cần thiết.
    - **Lợi ích**: Tránh lãng phí thời gian, giảm technical debt.
- **KISS (Keep It Simple, Stupid - Giữ cho nó đơn giản, ngốc nghếch)**
    - **Nguyên tắc**: Luôn ưu tiên các giải pháp đơn giản và dễ hiểu nhất.
    - **Lợi ích**: Code dễ đọc, debug, bảo trì và mở rộng, giảm bug.
- **Defensive Programming (Lập trình phòng thủ)**
    - **Nguyên tắc**: Luôn giả định rằng sẽ có lỗi xảy ra, kiểm tra đầu vào và xử lý ngoại lệ.
    - **Lợi ích**: Tạo code bền vững, có khả năng ứng phó với tình huống không lường trước.
    - **Xử lý lỗi**: Luôn bắt lỗi cụ thể thay vì chung chung, sử dụng logging thay vì print, và tạo custom exceptions khi cần thiết.
- **Separation of Concerns (Phân chia trách nhiệm)**
    - **Nguyên tắc**: Phân chia code thành các module, class hoặc hàm riêng biệt, mỗi phần chỉ đảm nhiệm một chức năng cụ thể.
    - **Lợi ích**: Dễ bảo trì, dễ kiểm thử, tăng khả năng tái sử dụng.

### 2.2.4: NGUYÊN TẮC SOLID VÀ DESIGN PATTERNS

Các nguyên tắc SOLID và Design Patterns là những công cụ mạnh mẽ để thiết kế hệ thống phần mềm có tính mở rộng, linh hoạt và dễ bảo trì.

#### Giới thiệu Nguyên tắc SOLID

**SOLID** là một tập hợp 5 nguyên tắc thiết kế hướng đối tượng được Robert C. Martin (Uncle Bob) đưa ra:

1. **Single Responsibility Principle (SRP - Nguyên tắc Trách nhiệm Đơn lẻ)**
   - **Nguyên tắc**: Mỗi lớp chỉ nên có **một lý do để thay đổi**. Tập trung vào một nhiệm vụ duy nhất.
   - **Áp dụng**: Chia nhỏ các lớp lớn thành các module nhỏ hơn, mỗi module có một trách nhiệm cụ thể.

2. **Open/Closed Principle (OCP - Nguyên tắc Mở/Đóng)**
   - **Nguyên tắc**: Mở để mở rộng, đóng để sửa đổi. Code nên dễ dàng thêm chức năng mới mà không cần sửa đổi code hiện có.
   - **Áp dụng**: Sử dụng abstraction (ABC) và mở rộng thông qua kế thừa hoặc composition.

3. **Liskov Substitution Principle (LSP - Nguyên tắc Thay thế Liskov)**
   - **Nguyên tắc**: Các lớp con phải thay thế được lớp cha mà không làm thay đổi tính đúng đắn của chương trình.
   - **Áp dụng**: Đảm bảo hành vi nhất quán của lớp con so với lớp cha, tránh thêm các điều kiện tiên quyết mạnh hơn hoặc ném ra ngoại lệ mới.

4. **Interface Segregation Principle (ISP - Nguyên tắc Phân tách Giao diện)**
   - **Nguyên tắc**: Nhiều interface nhỏ chuyên biệt tốt hơn một interface lớn. Client không nên bị buộc phụ thuộc vào các phương thức mà họ không sử dụng.
   - **Áp dụng**: Tách nhỏ interface thành các interface chuyên biệt, dùng ABC hoặc typing.Protocol.

5. **Dependency Inversion Principle (DIP - Nguyên tắc Đảo ngược Sự phụ thuộc)**
   - **Nguyên tắc**: Các module cấp cao không nên phụ thuộc trực tiếp vào module cấp thấp, mà cả hai nên phụ thuộc vào abstraction (interfaces/protocols).
   - **Áp dụng**: Dùng Abstract Base Classes (ABC) hoặc typing.Protocol, hoặc đơn giản là duck typing.

#### Áp dụng SOLID vào Python

Python với **dynamic typing** và **duck typing** hỗ trợ rất tốt cho việc áp dụng SOLID. Module abc (Abstract Base Classes) và typing.Protocol giúp định nghĩa interface rõ ràng, trong khi **composition over inheritance** khuyến khích việc kết hợp các đối tượng nhỏ để đạt được SRP và giảm phụ thuộc.

#### Các Design Patterns Phổ Biến

Design Patterns là các giải pháp tái sử dụng cho các vấn đề thiết kế phần mềm phổ biến. Chúng được chia thành ba nhóm chính:

- **Creational Patterns (Mẫu Khởi tạo)**: Liên quan đến việc tạo đối tượng một cách linh hoạt.
    - **Factory Pattern**: Tạo đối tượng mà không cần biết lớp con cụ thể, ẩn logic phức tạp.
    - **Singleton Pattern**: Chỉ tạo duy nhất một instance của một lớp, thường dùng cho logging, database.
- **Structural Patterns (Mẫu Cấu trúc)**: Xác định mối quan hệ giữa các đối tượng.
    - **Adapter Pattern**: Cho phép các interface không tương thích làm việc với nhau.
    - **Decorator Pattern**: Thêm chức năng mới cho đối tượng mà không sửa đổi cấu trúc hiện có.
- **Behavioral Patterns (Mẫu Hành vi)**: Xác định cách giao tiếp giữa các đối tượng.
    - **Command Pattern**: Đóng gói yêu cầu như một đối tượng, cho phép tham số hóa client với các hoạt động khác nhau.
    - **Template Method Pattern**: Định nghĩa khung thuật toán trong một phương thức, cho phép các lớp con định nghĩa lại các bước cụ thể mà không thay đổi cấu trúc thuật toán.

Để sử dụng Design Patterns hiệu quả, bạn cần **nắm vững 5 nguyên tắc SOLID**, **sử dụng Design Patterns phù hợp** với vấn đề cần giải quyết, **áp dụng SOLID vào Python** bằng cách tận dụng các đặc điểm của ngôn ngữ, và quan trọng nhất là **tránh lạm dụng** chúng.

### 2.3. SKILL FOR AIO 2025

> Dưới sự tác động mạnh mẽ của Trí tuệ nhân tạo trong việc hỗ trợ trong học tập, làm việc đòi hỏi mỗi người cần khả năng sở hữu những kỹ năng cần thiết trong việc nghiên cứu, học tập trong quá trình học khóa AIO 2025. "SKILL FOR AIO 2025" sẽ cung cấp các kỹ năng cần thiết, lộ trình học tập hiệu quả và phương pháp tiếp cận thực tế để chinh phục khóa học.

### Cách Tìm Kiếm Tài Liệu Học Thuật

#### Tìm kiếm các tài liệu thông qua các website uy tín như:

- **Google Scholar**
<div class="row mt-3">
    <div class="col-full mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Blog/Week1/GoogleScholar.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Hình 3: Giao diện Google Scholar.
</div>
    - Tìm kiếm bài báo, sách, luận văn về AI.
    - Bổ sung các kiến thức ngoài tài liệu của khóa học.
    - Nhanh gọn về các nghiên cứu mới nhất.

- **Papers With Code**
<div class="row mt-3">
    <div class="col-full mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Blog/Week1/PaperWithCode.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Hình 4: Giao diện Papers With Code.
</div>
    - Tìm bài báo kèm mã nguồn thực nghiệm, rất hữu ích để học thuật toán mới.
    - Cung cấp các Dataset phổ biến theo từng chủ đề, các SOTA của từng phương thức.

- **Group AIO-QAs-Verified**
<div class="row mt-3">
    <div class="col-full mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Blog/Week1/AIOGroup.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Hình 4: Group FB AIO-QAs-Verified.
</div>
    - Hỗ trợ giải đáp thắc mắc hoặc các vấn đề trong quá trình học tập, nghiên cứu.
    - Kết nối và chia sẻ các cơ hội học tập và làm việc cho thành viên trong cộng đồng AIO.

---

### Sử dụng các công cụ trong quá trình học tập/nghiên cứu

#### Đọc tài liệu và Papers

- **Sử dụng ChatGPT hoặc các công cụ tương tự** như perplexity, Gemini để tạo ra guidelines cho kỹ năng đọc hoặc Research Plan:
    - **Tạo Reading Skill Paper với perplexity**
    - **Tạo Research Plan với ChatGPT**

- **Flow đọc Papers hiệu quả** với kinh nghiệm của TA Đình Vinh

- **Sử dụng công cụ NotebookLM** cùng với kỹ năng prompting hỗ trợ cho việc đọc paper/document.

#### Hiện thực Code

- **Jupyter Notebook**
    - Sử dụng thông qua Anaconda Navigator, Pycharm.
    - Chỉ phù hợp với các máy có tài nguyên lớn để chạy các chương trình lớn như Quá trình training model có thể mất hàng tháng.

- **Google Colab**
    - **Công cụ lập trình Online với tài nguyên miễn phí (GPU, TPU, ....)**
    - **Hỗ trợ chạy nhanh hơn trong quá trình Chạy chương trình.**
    - **Có thể Lưu trữ trong Google Drive.**
    - **Sử dụng Gemini trong coding trong Colab**

- **Hỗ trợ Code**
    
    Ngoài Gemini hỗ trợ trong Colab, các công cụ AI khác thể hiện hiệu quả mạnh mẽ giúp đọc hiểu và xử lý Code như Claude(Opus 4, Sonnet 4), Grok(Grok 3),…

#### Xây dựng tài liệu

- **Sử dụng Latex thông qua công cụ online Overleaf**
    - Phù hợp với nghiên cứu khoa học.
    - Chỉnh sửa tài liệu trực tiếp với nhiều người tham gia.
    - Hỗ trợ format chỉn chu cho các công thức toán học, tiêu đề và chỉ mục.
---

### Kết Luận

SKILL FOR AIO 2025 là thiết yếu giúp quá trình học tập, nghiên cứu với việc nắm rõ các nguồn tài liệu uy tín và thành thạo các công cụ hỗ trợ cho quá trình đọc tài liệu/Papers, Hiện thực Code và Xây dựng tài liệu sẽ giúp cho các học viên AIO hiệu quả hơn với chặng đường suốt khóa học.
    


