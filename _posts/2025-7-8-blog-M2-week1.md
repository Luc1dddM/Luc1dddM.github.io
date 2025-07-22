---
layout: post
title: "Recap Kiến Thức Tuần 2 Module 1 - AIO 2025"
date: 2025-07-08
categories: [Python, Numpy, Week1]
---

# Recap Kiến Thức Tuần 1 Module 2 - AIO 2025

🔖 **Mục lục nhanh**:
- [1. Kiến thức cơ bản về NumPy](#1-kiến-thức-cơ-bản-về-numpy)
  - [1.1. Giới thiệu NumPy](#11-giới-thiệu-numpy)
  - [1.2. Cấu trúc dữ liệu: Mảng đa chiều](#12-cấu-trúc-dữ-liệu-mảng-đa-chiều)
  - [1.3. Các hàm tạo mảng cơ bản](#13-các-hàm-tạo-mảng-cơ-bản)
  - [1.4. Indexing và Slicing](#14-indexing-và-slicing)
  - [1.5. Broadcasting - Phép toán thông minh](#15-broadcasting---phép-toán-thông-minh)
  - [1.6. Ứng dụng vào Machine Learning/Deep Learning](#16-ứng-dụng-vào-machine-learningdeep-learning)
- [2. Kiến thức mở rộng](#2-kiến-thức-mở-rộng)
  - [2.1. NoSQL và MongoDB](#21-nosql-và-mongodb)
  - [2.2. Cosine Similarity](#22-cosine-similarity)
  - [2.3. Logical Thinking trong AI](#23-logical-thinking-trong-ai)
- [3. Tổng kết](#3-tổng-kết)

---

## 1. Kiến Thức Cơ Bản về NumPy

### 1.1. 📚 Giới thiệu NumPy

NumPy (Numerical Python) là thư viện Python mạnh mẽ và quan trọng nhất cho tính toán khoa học. Nó cung cấp:

- **Mảng đa chiều hiệu quả**: Cấu trúc dữ liệu nền tảng cho machine learning
- **Tính toán vectorized**: Xử lý toàn bộ mảng cùng lúc thay vì từng phần tử
- **Tích hợp tốt**: Là nền tảng cho pandas, scikit-learn, TensorFlow...

#### 🎯 Tại sao cần NumPy?

```python
# Cách Python thuần túy - chậm và dài dòng
python_list = [1, 2, 3, 4]
result = []
for i in python_list:
    result.append(i * 2)

# Cách NumPy - nhanh và ngắn gọn
import numpy as np
arr = np.array([1, 2, 3, 4])
result = arr * 2  # Tự động nhân tất cả phần tử
```

### 1.2. 📊 Cấu trúc dữ liệu: Mảng đa chiều

#### 1D Array (Mảng 1 chiều)
```python
# Ví dụ: Điểm số của một học sinh
scores = np.array([8, 9, 7, 10])
print(scores.shape)  # (4,) - 4 phần tử
```

#### 2D Array (Mảng 2 chiều - Ma trận)
```python
# Ví dụ: Bảng điểm của cả lớp
class_scores = np.array([
    [8, 9, 7, 10],    # Học sinh 1
    [6, 8, 9, 7],     # Học sinh 2
    [9, 10, 8, 9]     # Học sinh 3
])
print(class_scores.shape)  # (3, 4) - 3 học sinh, 4 môn
```

#### 3D Array (Mảng 3 chiều)
```python
# Ví dụ: Điểm số của nhiều lớp qua nhiều học kỳ
school_scores = np.array([
    [[8, 9, 7], [6, 8, 9]],    # Học kỳ 1
    [[9, 8, 10], [7, 9, 8]]    # Học kỳ 2
])
print(school_scores.shape)  # (2, 2, 3) - 2 học kỳ, 2 lớp, 3 môn
```

### 1.3. 🔧 Các hàm tạo mảng cơ bản

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

#### Reshape - Thay đổi hình dạng mảng
```python
# Chuyển dữ liệu 1D thành bảng 2D
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

### 1.4. 🔍 Indexing và Slicing

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

### 1.5. 🔄 Broadcasting - Phép toán thông minh

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

### 1.6. 🖼️ Ứng dụng vào Machine Learning/Deep Learning

#### Softmax Function
```python
def softmax(x):
    """
    Chuyển đổi điểm số thành phân phối xác suất
    Ví dụ: [2, 1, 0] -> [0.67, 0.24, 0.09]
    """
    # Trừ max để tránh overflow
    x_stable = x - np.max(x)
    exp_x = np.exp(x_stable)
    return exp_x / np.sum(exp_x)
```

#### Tạo dữ liệu ngẫu nhiên
```python
# Seed để đảm bảo kết quả có thể tái tạo
np.random.seed(42)

# Dữ liệu phân phối chuẩn
normal_data = np.random.randn(1000)  # mean=0, std=1

# Dữ liệu phân phối đều
uniform_data = np.random.uniform(0, 1, 1000)

# Chọn ngẫu nhiên với xác suất
choices = np.random.choice(['A', 'B', 'C'], size=100, p=[0.5, 0.3, 0.2])
```

#### Tiền xử lý ảnh cho PyTorch
```python
# Hàm chuẩn hóa ảnh
def transform(img, img_size=(224, 224)):
    """
    Chuyển đổi ảnh về định dạng phù hợp cho PyTorch
    PyTorch yêu cầu: CHW (Channels, Height, Width)
    """
    img = img.resize(img_size)
    img = np.array(img)[..., :3]  # Đảm bảo lấy 3 kênh RGB
    img = torch.tensor(img).permute(2, 0, 1).float()  # Đổi thành (C, H, W)
    normalized_img = img / 255.0  # Chuẩn hóa về [0, 1]
    
    return normalized_img

# Định nghĩa Dataset class
class CIFARDataset(Dataset):
    def __init__(self, X, y, transform=None):
        self.transform = transform
        self.img_paths = X
        self.labels = y
    
    def __len__(self):
        return len(self.img_paths)
    
    def __getitem__(self, idx):
        img_path = self.img_paths[idx]
        img = Image.open(img_path).convert("RGB")
        
        if self.transform:
            img = self.transform(img)
        
        return img, self.labels[idx]
```

---

## 2. Kiến Thức Mở Rộng

### 2.1. 🍃 NoSQL và MongoDB

#### NoSQL là gì?
NoSQL có 3 cách hiểu phổ biến:
- **No Relational** – không theo mô hình quan hệ
- **No RDBMS** – không dùng hệ quản trị cơ sở dữ liệu quan hệ truyền thống
- **Not Only SQL** – không chỉ có SQL

Dữ liệu được lưu trữ dưới dạng **key-value** hoặc **document**, không bị ràng buộc bởi cấu trúc bảng như SQL.

#### So sánh SQL vs NoSQL

| Tiêu chí | SQL (Relational) | NoSQL (Non-relational) |
|----------|------------------|------------------------|
| **Cấu trúc dữ liệu** | Có cấu trúc, lưu trong bảng | Phi cấu trúc/linh hoạt (JSON, key-value) |
| **Schema** | Cố định, phải định nghĩa trước | Linh hoạt, không cần định nghĩa trước |
| **Ngôn ngữ truy vấn** | SQL (SELECT, JOIN, GROUP BY...) | Mongo Query Language (MQL), API riêng |
| **Khả năng mở rộng** | Theo chiều dọc (scale-up) | Theo chiều ngang (scale-out) |
| **Quan hệ dữ liệu** | Hỗ trợ quan hệ phức tạp | Hạn chế hoặc không hỗ trợ JOIN |
| **Tính nhất quán** | Tuân thủ nghiêm ngặt ACID | BASE (eventual consistency) |
| **Hiệu suất** | Tốt với dữ liệu ổn định | Tốt với dữ liệu lớn, thay đổi thường xuyên |
| **Ví dụ** | MySQL, PostgreSQL, Oracle | MongoDB, Redis, Cassandra |

#### Khi nào nên dùng từng loại?

**✅ Dùng NoSQL khi:**
- Dữ liệu không có cấu trúc cố định
- Cần mở rộng dễ dàng theo chiều ngang
- Ứng dụng realtime, web-scale, big data
- Yêu cầu phân tán, không cần tính toàn vẹn dữ liệu chặt chẽ

**✅ Dùng SQL khi:**
- Dữ liệu có cấu trúc rõ ràng, mối quan hệ chặt chẽ
- Cần truy vấn phức tạp, báo cáo chính xác
- Hệ thống tài chính, kế toán, ngân hàng

#### Các loại NoSQL cơ bản

1. **Key-Value Store**: Lưu trữ dưới dạng cặp khóa-giá trị, truy xuất nhanh
2. **Document Store**: Dữ liệu nằm trong các tài liệu JSON/BSON, cấu trúc linh động
3. **Graph Database**: Lưu trữ theo mô hình đồ thị, phù hợp với quan hệ phức tạp

#### MongoDB - Hệ quản trị Document-Oriented

MongoDB sử dụng mô hình:
- **Document** = JSON/BSON object, có trường `_id` làm khóa chính
- **Collection** là tập hợp các document
- **Database** là tập hợp các collection

```json
{
  "_id": 1,
  "name": "Thai",
  "age": 20,
  "phone": ["0123", "1235"],
  "address": { "city": "Ha Noi", "postcode": "100" }
}
```

#### Mongo Query Language (MQL)

**Quản lý Database & Collection:**
```javascript
show dbs                     // liệt kê databases
use mydb                     // tạo hoặc chuyển sang database mydb
db.dropDatabase()            // xóa database hiện tại
db.createCollection("users") // tạo collection
db.users.drop()              // xóa collection users
```

**Chèn dữ liệu:**
```javascript
db.users.insertOne({ name: "Alice", age: 30 })
db.users.insertMany([
  { name: "Bob", age: 25 },
  { name: "Carol", age: 28 }
])
```

**Truy vấn dữ liệu:**
```javascript
db.users.find({ age: { $gt: 25 } })          // tất cả user > 25 tuổi
db.users.findOne({ name: "Alice" })           // 1 document đầu tiên
db.users.find({}, { name: 1, _id: 0 })       // chỉ hiển thị trường name
```

**Cập nhật & Xóa:**
```javascript
db.users.updateOne(
  { name: "Alice" },
  { $set: { age: 31 } }
)
db.users.deleteMany({ age: { $lt: 20 } })
```

### 2.2. 📏 Cosine Similarity

#### Giới thiệu
Trong thời đại dữ liệu bùng nổ, việc đo lường mức độ tương đồng giữa hai đối tượng (bài báo, hình ảnh, khách hàng) là kỹ năng thiết yếu. **Cosine Similarity** là công cụ toán học mạnh mẽ giúp giải quyết vấn đề này.

#### Nền tảng Đại số tuyến tính

- **Vector**: Đại diện cho một điểm dữ liệu trong không gian nhiều chiều
  - *Ví dụ*: `[TV, Radio, Newspaper] = [100, 20, 30]`
- **Ma trận**: Tập hợp nhiều vector, chính là bảng dữ liệu
- Trong machine learning, mọi đối tượng đều có thể biểu diễn bằng vector

#### Công thức Cosine Similarity

$$\text{cosine\_similarity}(\vec{x}, \vec{y}) = \frac{\vec{x} \cdot \vec{y}}{\|\vec{x}\| \cdot \|\vec{y}\|}$$

**Trong đó:**
- $\vec{x} \cdot \vec{y}$ là dot product (tích vô hướng)
- $\|\vec{x}\|, \|\vec{y}\|$ là norm (độ dài vector):
  - $\|\vec{x}\| = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}$

**Ý nghĩa:**
- **Cosine = 1**: Hoàn toàn giống nhau (cùng hướng)
- **Cosine = 0**: Không liên quan (vuông góc)
- **Cosine = -1**: Hoàn toàn đối lập

#### Tại sao Cosine Similarity quan trọng?

- Không bị ảnh hưởng bởi độ lớn của vector
- Dễ áp dụng với dữ liệu văn bản, ảnh, sản phẩm
- Là nền tảng cho nhiều thuật toán machine learning

#### Ứng dụng thực tế

**1. Xử lý ngôn ngữ tự nhiên (NLP):**
- Mỗi văn bản → vector (TF-IDF, Word2Vec...)
- Ứng dụng: So khớp câu hỏi-trả lời, gợi ý nội dung, phát hiện đạo văn

**2. Trích xuất nền ảnh:**
```
A = |I - B|
```
- I: ảnh hiện tại
- B: ảnh nền  
- A: vùng sai khác (foreground)

**3. Nhận dạng ảnh & K-Nearest Neighbors:**
- So sánh ảnh biển báo bằng Cosine Similarity
- K-NN: Tìm K điểm gần nhất với dữ liệu mới

### 2.3. 🧠 Logical Thinking trong AI

#### Tầm quan trọng
80% dự án AI thất bại do:
- Định nghĩa sai vấn đề
- Dữ liệu kém chất lượng  
- Thiếu tư duy hệ thống

#### 7 bước giải quyết vấn đề AI

1. **Xác định vấn đề rõ ràng**
2. **Chia nhỏ vấn đề (MECE)**
3. **Ưu tiên vấn đề (Impact-Feasibility)**
4. **Thu thập dữ liệu chất lượng**
5. **Phân tích dữ liệu sâu sắc**
6. **Đề xuất giải pháp khả thi**
7. **Triển khai & đánh giá liên tục**

#### Kỹ thuật hỗ trợ tư duy

- **5W1H & 5 Whys**: Làm rõ nguyên nhân gốc rễ
- **SMART Goals**: Mục tiêu rõ ràng, đo lường được
- **MECE & Logic Tree**: Phân tích toàn diện không bỏ sót
- **Impact-Feasibility Matrix**: Ưu tiên giải pháp hiệu quả

---

## 3. Tổng Kết

Tuần 2 của Module 1 đã cung cấp những kiến thức nền tảng quan trọng:

- **NumPy**: Công cụ tính toán khoa học mạnh mẽ, nền tảng cho machine learning
- **NoSQL & MongoDB**: Giải pháp lưu trữ dữ liệu linh hoạt cho thời đại big data
- **Cosine Similarity**: Phương pháp đo lường độ tương đồng trong AI
- **Logical Thinking**: Tư duy logic để giải quyết vấn đề AI hiệu quả

Những kiến thức này tạo nền tảng vững chắc cho việc học các chủ đề nâng cao hơn trong các tuần tiếp theo.

💡 **Lời khuyên**: Hãy thực hành thường xuyên với các ví dụ thực tế để nắm vững kiến thức đã học!