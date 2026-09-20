Lỗi 1: Tính thiếu cước phí cho các km đầu tiên khi $distance > 2.0$Dòng mã lỗi: 
total_fare = distance * 4500.0;Nguyên nhân: Theo quy định, 2 km đầu tiên có giá cố định 
12.000 VNĐ, và chỉ từ km thứ 3 trở đi mới tính thêm 4.500 VNĐ/km cho phần vượt quá 2 km.
Hậu quả: Công thức cũ lại lấy toàn bộ quãng đường nhân với 4.500 VNĐ. Ví dụ đi 3 km, cước phí bị 
tính sai thành $3 \times 4.500 = 13.500$ VNĐ (thay vì $12.000 + (3 - 2) \times 4.500 = 16.500$ VNĐ).
Cách khắc phục: Sửa thành total_fare = 12000.0 + (distance - 2.0) * 4500.0;Lỗi 2: Sử dụng toán 
tử gán = thay vì toán tử so sánh == trong câu lệnh ifDòng mã lỗi: if (is_raining = 1)Nguyên 
nhân: Cú pháp is_raining = 1 thực hiện phép gán giá trị 1 vào biến is_raining. Biểu thức này 
luôn trả về giá trị 1 (tương đương true trong C), khiến câu lệnh điều kiện luôn luôn được thực 
thi dù nhập is_raining là 0 hay 1.Hậu quả: Khách đi lúc thời tiết bình thường (is_raining = 0) 
vẫn bị nhân thêm hệ số 1.2x (tăng 20% phụ phí).Cách khắc phục: Sửa toán tử gán = thành toán tử 
so sánh ==: if (is_raining == 1)

# Bảng Test Cases Đối Chứng - GrabRide Debug

| Trường hợp kiểm thử | Dữ liệu đầu vào | Kết quả sai thực tế | Kết quả đúng mong đợi |
| :--- | :--- | :--- | :--- |
| **TC01: Quãng đường > 2km, Không mưa** | `distance = 3.0`<br>`is_raining = 0` | `16.200 VND`<br>*(Do tính 3 * 4500 = 13.500, sau đó bị gán mưa nên x1.2 = 16.200)* | `16.500 VND`<br>*(12.000 + (3 - 2) * 4.500 = 16.500, giữ nguyên không nhân 1.2)* |
|                     |                 |                     |                       |
| **TC02: Quãng đường <= 2km, Không mưa** | `distance = 1.5`<br>`is_raining = 0` | `14.400 VND`<br>*(Tính đúng 12.000 nhưng bị tính sai phụ phí x1.2 = 14.400)* | `12.000 VND`<br>*(Cước cố định 12.000, không nhân 1.2)* |