# BÁO CÁO CÁC HỆ QUẢN TRỊ CƠ SỞ DỮ LIỆU

### 1. Mô hình hệ thống:
***
#### * Sản phẩm bán trong hệ thống
> Điện thoại Iphone
#### * Hình thức kinh doanh, quản lý
> Bán hàng onilne 
#### * Nền tảng xây dựng phần mềm
> Xây dựng trên nền tảng Website

### 2. Đối tượng sự dụng:
***
#### Phần mềm tập chung vào 2 đối tượng người dùng
##### * Người quản lý (**Admin**)
##### * Người mua (**Customer**)

### 3. Cách thức xây dựng hệ quản trị cơ sở dữ liệu:
***
#### a) Đối tượng:
* Sản phẩm (Iphone)
* Tài khoản
* Hóa đơn
* Phiếu nhập, xuất
* Kho

#### b) Nghiên cứu các hệ thống dữ liệu sẵn có
> Phần mền có tham khảo hệ thống dữ liệu từ các trang bán điện thoại uy tín của việt nam (thegioiđiong.com.vn, fptshop.com, ...)

#### c) Thiết kế cấu trúc dữ liệu và các đặc tả dữ liệu, các quan hệ
> **Bản thiết kế cuối cùng**

##### Chức năng quản lý sản phẩm
![Chức năng quản lý sản phẩm](https://github.com/Group-Java/app/blob/master/doc/img/product.png "Chức năng quản lý sản phẩm")

##### Chức năng mua hàng
![Chức năng mua hàng](https://github.com/Group-Java/app/blob/master/doc/img/buy.png "Chức năng mua hàng")

##### Chức năng quản lý kho
![Chức năng quản lý kho](https://github.com/Group-Java/app/blob/master/doc/img/stock.png "Chức năng quản lý kho")

##### Chức năng quản lý tài khoản
![Chức năng quản lý tài khoản](https://github.com/Group-Java/app/blob/master/doc/img/account.png "Chức năng quản lý tài khoản")

https://github.com/Group-Java/app/blob/master/doc/img/product.png

#### d) Mô tả các rằng buộc toàn vẹn và các trigger, stroe proceduce có thể có.
##### > Các trigger có thể có:
* Kiểm tra insert sản phẩm vào kho, nếu tồn tại phiếu nhập
* Kiểm tra update sản phẩm trong kho, nếu tồn tại hoá đơn và phiếu xuất ở trạng thái thành công
* Kiểm tra update hóa đơn khi hóa đơn chưa bị lock
* Không được phép xoá  phieu nhap , phieu xuat, hoa don , chi tiet hoa don
##### > Các Store Proceduce có thể có:
* Thêm sản phẩm vào kho khi có phiếu nhập
* Khi hoá đơn ở trạng thái thành công, phiếu xuất ở trạng thái thành công và thì sẽ thay đổi trạng thái bán của sản phẩm trong kho
* Khi thấy trong kho có sự thay đổi ( thêm sản phẩm, thay đổi trạng thái bán, ..) số lượng tồn sẽ thay đổi trong bảng “sản phẩm tùy chọn”
* Hoá đơn chuyển sang trạng thái không thành công, phiếu xuất sẽ bị lock , ghi chú lại sự kiện và số lượng tồn sẽ được phục hồi
* Khi các sản phẩm trong hoá đơn chi tiết ở trạng thái thành công, sẽ tính tổng giá trong hoá đơn
* Liệt kê, tìm kiếm danh sách sản phẩm
* Liệt kê tìm kiếm, thêm, sửa xóa danh sách hóa đơn, phiếu nhập, xuất, bảo hành, giao hàng, phiếu đặt, ...
* Kiểm tra validation
* Thông kê doanh số, kho bãi, …
##### > Các rằng buộc toàn vẹn có thể có:
* Email tài khoản là duy nhât (Unique)
* Imel sản phẩm trong kho là duy nhất (Unique)

#### e) Hệ quản trị cơ sở được sử dụng:
> Phần mềm sử dụng hệ quản trị MySQL

### 4. Thiết lập các tình huống xỷ lý tranh chập đồng thời
***
#### * **Tình huống 1**:  Xử lý các giao tác trong giỏ hàng khi khách hàng đặt cùng lúc
#### * **Tình hướng 2**:  Xứ lý các giao tác khi nhập kho giữa 2 admin kho cùng lúc

### 5. Các xây dựng phần mềm
***
#### a) Phân tích yêu cầu
##### Mục đích của phần mềm?
1. Quản lý sản phẩm, kho bãi
2. Quản lý bán hàng, hoá đơn
3. Quản lý doang thu, thống kê lãi lỗ
##### Định nghĩa các thành phần của phần mềm (kiến trúc của phần mềm, có các chức nào, hoạt động của từng chức năng)
* Phần mền sẽ chia ra các giao diện dành riêng cho từng user
...1. Giao diện website bán hàng: dành cho user Khách hàng
...2. Giao diện quản trị bán hàng: dành cho admin
* Viết theo mô hình MVC
* Các chức năng:
...1. Giao diện website: 
......Giỏ hàng: Có cho phép thay đổi số lượng đặt, Phương thức thanh toán theo dạng COD. Khách hàng không được phép hủy hóa đơn sau khi submit. Nếu muốn hủy liên hệ admin để hủy
......Tìm kiếm, Lọc
......Phân trang
....2. Giao diện khách hàng: 
......Chỉnh sửa thông tin tài khoản
......Xem thông tin đơn hàng
......Đổi mật khẩu
...3. Giao diện Admin:
......Xem hóa đơn (tạo, sửa hóa đơn)
......Lập phiếu nhập, xuất: Cho phép 2 nhân viên nhập kho cùng lúc
......Thêm, sửa sản phẩm
......Xem tình trạng kho hàng, báo cáo
#### b) Thiết kế và lập trình phần mềm
##### Sử dụng kỹ thuật, ngôn ngữ nào để xây dựng hệ thống
> Sử dụng Django (python)
#### Đặc điểm nào của kỹ thuật giúp bạn quyết định lựa chọn?.
> Hỗ trợ mô hình 3 lớp giúp dễ dàng cho công việc chỉnh sửa và phát triền phầm mền
#### c) Quá trình kiểm thử và đảm bảo chất lượng phần mềm
##### Các thao tác kiểm thử phần mềm 
* Kiểm thử tải: Nhóm có viết tool kiểm thử các đường link có trả lời không!
* Kiểm thử tự động: Sử dụng Selenium tự động hóa các quá trình mua hàng, đăng nhập, tranh chấp 

### 6. Hướng dẫn sử dụng và cài đặt
***
#### Chuẩn bị:
1. Python 2.7
2. Mysql
#### Thực hiện:
1. Cài đặt Python
> Windown
...Down load python 2.7 : https://www.python.org/downloads/
...Cài đặt môi trường. My computer - >Properties - > Advanced - >Envirnoment Variables 
...Tại System variables chọn “Path” - > Edit
...Chọn New -> Điên và đường dẫn thư mục python gồm “Python27” và “Python27\Script”
> Linux (Ubuntu)
Chạy lệnh sau: 
``` shell
    sudo apt-get update
    sudo apt-get install python-pip python-dev libpq-dev
```
2. Cài đặt Mysql;
> Tạo database tên: thietbididong
3. Cài đặt phần mềm:
* Clone hoặc download source tại: https://github.com/peter-dinh/django-e-commerce
* Install library: pip install -r requirements.txt  (gồm: Django, Pillow, Mysql-python)
* Truy cập va thư mục cùng cấp với file manage.py
* Install Database: python manage.py migrate
* Kiểm tra table trong database: Nếu chưa có table. Quay lại thực thi lại bước 4
* Install Trigger & Stored: Copy script trong 2 file trigger.sql va trored.sql  vào SQL và execute (file trong folder “/db”)
* Tạo tài khoản admin: python manage.py createsuperuser
* Khởi động app: python manage.py runserver –insecure
* Giao diện admin: Gõ url: “http://localhost:8000/admin”