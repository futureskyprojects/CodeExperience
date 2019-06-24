# CAR TRACKING VERSION 1

## 1. NGUYÊN LÝ HOẠT ĐỘNG
  Sử dụng SocketIO để truyền dữ liệu, thiết bị định vị được gắn trên xe sẽ chịu trách nhiệm kết nối đến server và gửi dữ liệu về vị trí hoạt động của chính nó.
  Còn phía server sẽ chịu trách nhiệm nhận lấy các giá trị để xử lý, từ đó hiển thị vị trì và thôn tin tham chiếu từ thiết bị lên màn hình cho người quản lý xem.
## 2. PHÂN TÍCH VỀ CÁC CHỨC NĂNG CHÍNH
### 2.1. Về phía thiết bị
  - Là một bộ định vị được gắn trên xe
  - Đảm bảo được nguồn hoạt động
  - Luôn mang một giá trị định danh duy nhất (IMEI)
  - Gửi dữ liệu liên tục đến server.
  
### 2.2. Về phía máy chủ
#### a) Phía trang quản lý
    Trang quản lý tại phía máy chủ sẽ đảm nhận việc hiển thị thông tin sau khi được phân giải từ thiết bị, đồng thời cung cấp một số chức năng sau cho người dùng:
    - Có trang đăng nhập để đảm bảo tính bảo mật
    - Đăng ký không được công khai, trang đăng ký được thực hiện ngầm và do admin hoặc những người có thẩm quyền tạo tài khoản
    - Có trang quản lý danh sách thiết bị theo IMEI
    - Trang quản lý cơ giới (Danh sách xe)
    - Trang quản lý xe được gắn thiết bị
    - Trang đăng ký lịch trình xe
    - Trang quản lý có khả năng đưa ra được danh sách những xe có lịch trình
    - Trang quản lý danh sách các xe đang chạy
    - Map hiển thị thời gian thực danh sách các xe đang chạy
    - Có khả năng tham chiếu từ IMEI thiết bị để truy xuất ra thông tin xe được gắn vào và tài xế cùng cấc lịch trình và thông tin liên quan
    - Cho phép xem các thông số của các xe đang chạy trên map như: vị trí, vận tốc,... (Nên hiển thiện dạng popup khi nhấn vào marker)
    - Cho phép cập nhập, xóa các thông tin trong hệ thống đảm bảo mô bình CRUD
    - Có chức năng đăng xuất
    - Có chức năng lấy lại mật khẩu
    - Thực hiện lắng nghe được ở nhiều Rom khác nhau
    - Tự phân giải chuỗi vị trí ở client và cho hiển thị ngay sau đó
#### b) Về phía máy chủ nhận và truyền dữ liệu
    Ở đây, kiến nghị sử dụng SocketIO của NodeJS vì tính đơn giản, tiện dụng, đễ bảo trì và triển khai công nghệ. Các yêu cầu đối với server như sau:
    - Nhận được IMEI của thiết bị
    - Tạo Rom socket theo IMEI của mỗi thiết bị
    - Mỗi kết nối muốn xem thông tin được gửi lên của thiết bị phải join vào Rom có số IMEI tương ứng
    - Server nhận chuỗi vị trí của thiết bị và broadcast vào rom có IMEI tương ứng để các thiết bị khác trong Rom có khả năng nhận.
    - Server không thực hiện bất kỳ xử lý nào ngoài việc nhận và broadcast dữ liệu
 
 ## 3. MÔ HÌNH
