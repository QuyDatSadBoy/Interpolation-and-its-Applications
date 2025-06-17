# Interpolation and its Applications

## Giới thiệu

Repository này chứa các thuật toán nội suy (interpolation) và ứng dụng của chúng trong xử lý dữ liệu và hình ảnh. Dự án tập trung vào việc triển khai Linear Interpolation để giải quyết các bài toán thực tế như:

- Xử lý dữ liệu thiếu trong chuỗi số liệu 1D
- Thay đổi kích thước hình ảnh (Image Resizing)

## Cấu trúc Repository

```
Interpolation-and-its-Applications/
├── code_update/
│   ├── 4.1DInterpolation.ipynb      # Nội suy 1D cho dữ liệu thiếu
│   └── 6.ImageResizing_linear.ipynb # Nội suy tuyến tính cho thay đổi kích thước ảnh
└── README.md
```

## Tính năng chính

### 1. Nội suy tuyến tính 1D (Linear Interpolation)

**File:** `code_update/4.1DInterpolation.ipynb`

#### Thuật toán cơ bản
```python
def linear_interpolation(p1, p2, x):
    x1, y1 = p1
    x2, y2 = p2
    if x1 != x2:
        y = ((x2-x)/(x2-x1))*y1 + ((x-x1)/(x2-x1))*y2
    else:
        y = y1
    return y
```

#### Tính năng:
- **Xử lý dữ liệu thiếu (None values)**: Tự động phát hiện và điền vào các giá trị thiếu trong chuỗi dữ liệu
- **Hai thuật toán tìm giá trị None**:
  - `algorithm1`: Tìm vị trí cuối cùng của None trong mảng
  - `algorithm2`: Tìm vị trí đầu tiên của None trong mảng
- **Xử lý các trường hợp biên**: Khi None ở đầu hoặc cuối mảng

#### Ví dụ sử dụng:
```python
# Dữ liệu có giá trị thiếu
data = [None, 2.2, 2.0, 2.2, None, 2.7, None, 4.9, None]
result = process_data(data)
# Kết quả: [2.2, 2.2, 2.0, 2.2, 2.45, 2.7, 3.8, 4.9, 4.9]
```

### 2. Thay đổi kích thước hình ảnh bằng nội suy tuyến tính

**File:** `code_update/6.ImageResizing_linear.ipynb`

#### Tính năng:
- **Phóng to ảnh**: Sử dụng nội suy tuyến tính để tăng kích thước ảnh
- **Xử lý 2 bước**:
  1. **Bước 1**: Nội suy theo chiều ngang (width)
  2. **Bước 2**: Nội suy theo chiều dọc (height)
- **Hỗ trợ scaling factor tùy chỉnh**: Có thể điều chỉnh tỷ lệ phóng to

#### Quy trình xử lý:
1. Đọc ảnh gốc (grayscale)
2. Xác định tỷ lệ phóng to (w_scale_factor, h_scale_factor)
3. Nội suy theo từng hàng để tăng chiều rộng
4. Nội suy theo từng cột để tăng chiều cao
5. Lưu ảnh kết quả

#### Ví dụ sử dụng:
```python
# Đọc ảnh
source = cv2.imread('nature.jpg', 0).tolist()

# Thiết lập tỷ lệ phóng to 2x
w_scale_factor = 2
h_scale_factor = 2

# Thực hiện nội suy và lưu kết quả
cv2.imwrite('nature_linear_2x.jpg', processed_image)
```

## Yêu cầu hệ thống

- Python 3.9+
- Jupyter Notebook
- Thư viện cần thiết:
  ```
  opencv-python
  numpy
  math (built-in)
  ```

## Cài đặt

1. Clone repository:
```bash
git clone https://github.com/QuyDatSadBoy/Interpolation-and-its-Applications.git
cd Interpolation-and-its-Applications
```

2. Cài đặt dependencies:
```bash
pip install opencv-python numpy jupyter
```

3. Chạy Jupyter Notebook:
```bash
jupyter notebook
```

## Sử dụng

### Nội suy dữ liệu 1D:
1. Mở file `code_update/4.1DInterpolation.ipynb`
2. Chạy các cell theo thứ tự
3. Thử nghiệm với dữ liệu của bạn bằng cách thay đổi biến `data`

### Thay đổi kích thước ảnh:
1. Mở file `code_update/6.ImageResizing_linear.ipynb`
2. Đặt ảnh cần xử lý vào cùng thư mục và đổi tên thành `nature.jpg`
3. Chạy các cell để thực hiện nội suy
4. Kết quả sẽ được lưu với tên `nature_linear_2x.jpg`

## Nguyên lý hoạt động

### Linear Interpolation
Công thức nội suy tuyến tính giữa hai điểm (x₁, y₁) và (x₂, y₂) tại điểm x:

```
y = ((x₂-x)/(x₂-x₁)) * y₁ + ((x-x₁)/(x₂-x₁)) * y₂
```

### Xử lý dữ liệu thiếu
1. Tìm vị trí của giá trị None
2. Xác định điểm bắt đầu (begin) và điểm kết thúc (end) gần nhất
3. Áp dụng nội suy tuyến tính hoặc extrapolation tùy vào vị trí

### Image Resizing
1. **Horizontal Interpolation**: Nội suy các pixel mới giữa các pixel gốc theo chiều ngang
2. **Vertical Interpolation**: Nội suy các pixel mới theo chiều dọc dựa trên kết quả bước 1

## Ưu điểm

- **Đơn giản và hiệu quả**: Thuật toán nội suy tuyến tính dễ hiểu và triển khai
- **Xử lý robust**: Có thể xử lý các trường hợp biên và dữ liệu thiếu
- **Ứng dụng đa dạng**: Từ xử lý dữ liệu số đến xử lý hình ảnh
- **Code rõ ràng**: Jupyter notebook với documentation chi tiết

## Hạn chế

- Chỉ hỗ trợ nội suy tuyến tính (có thể mở rộng cho các phương pháp khác)
- Xử lý ảnh chỉ ở mức grayscale
- Chưa tối ưu hóa cho ảnh kích thước lớn

## Đóng góp

Mọi đóng góp đều được chào đón! Vui lòng:
1. Fork repository
2. Tạo branch mới cho tính năng
3. Commit thay đổi
4. Tạo Pull Request

## Tác giả

**QuyDatSadBoy**
- GitHub: [@QuyDatSadBoy](https://github.com/QuyDatSadBoy)
