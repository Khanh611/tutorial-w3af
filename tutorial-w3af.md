# Hướng dẫn cài đặt w3af trên ubuntu 20.04

## Mục lục


1. [Cài đặt](#setup)
1. [Running w3af](#run-w3af)
   1. [Cấu hình plugin](#plugin-configuration)
   1. [Lưu cấu hình](#save-the-configuration)
   1. [Bắt đầu quét](#start-the-scan)


## Cài đặt <a name="setup"></a>

### Điều kiện bắt buộc

Đảm bảo rằng máy có sẵn các phần mềm sau trước khi cài đặt:

- Git client: ``sudo apt-get install git``
- Python 2.7: ``sudo apt install python2``
- Pip: ``curl https://bootstrap.pypa.io/get-pip.py --output get-pip.py`` ``sudo python2 get-pip.py``

### Cài đặt

- Clone source code về bằng lệnh:
```
git clone https://github.com/andresriancho/w3af.git
```

![git w3fa](https://user-images.githubusercontent.com/65669673/90966686-8a853300-e4ff-11ea-8fa8-eb31279bdf00.PNG)

- Các dependencies được cài đặt bằng cách chạy lệnh:
```
. /tmp/w3af_dependency_install.sh
```

*Lưu ý:*

- Để tạo ra file ``/tmp/w3af_dependency_install.sh`` vào thư mục w3af và chạy lệnh: `` python2.7 ./w3af_console ``

- Để cài đặt các dependencies máy cần cài: 

```
apt install npm
apt-get install -y build-essential
apt-get install -y python-dev
apt-get install libxml2 -y
apt-get install python-libxml2
apt-get install libxml2-dev libxslt1-dev -y
apt install libeccodes-dev -y
```

- Sau khi cài đặt xong vào thư mục w3af và chạy lệnh:
```
python2.7 ./w3af_console
```

![w3af_console](https://user-images.githubusercontent.com/65669673/90966700-b7d1e100-e4ff-11ea-96c0-3249bc6b4e5b.PNG)

## Running w3af <a name="run-w3af"></a>

``w3af`` có hai giao diện người dùng, giao diện người dùng console và giao diện người dùng đồ họa. Hướng dẫn sử dụng này sẽ tập trung vào giao diện người dùng console. Để kích hoạt giao diện người dùng console, chạy lệnh:

```
python2.7 ./w3af_console
w3af>>>
```

Tại đây, có thể định cấu hình cài đặt framework, plugin, khởi chạy quét và cuối cùng là khai thác lỗ hổng. Lệnh đầu tiên cần biết là ``help`` *(xin lưu ý rằng các lệnh phân biệt chữ hoa chữ thường)*:

![help](https://user-images.githubusercontent.com/65669673/90966720-07181180-e500-11ea-98b1-ce73050947bd.PNG)

Để vào menu cấu hình, chỉ cần nhập tên của nó và nhấn enter:

![http-setting](https://user-images.githubusercontent.com/65669673/90966729-3dee2780-e500-11ea-92c6-037d0742e46c.PNG)

Tất cả các menu cấu hình cung cấp các lệnh sau:
 - ``help`` Liệt kê danh sách các lệnh
 - ``view`` Liệt kê tất cả các tham số có thể cấu hình
 - ``set``  Thay đổi một giá trị
 - ``back`` Quay lại menu trước đó

Ví dụ:

![ex1](https://user-images.githubusercontent.com/65669673/90966754-96bdc000-e500-11ea-9946-96ba4f3ef789.PNG)

### Cấu hình plugin <a name="plugin-configuration"></a>

Các plugin được cấu hình bằng menu cấu hình "plugin"

![plugins](https://user-images.githubusercontent.com/65669673/90966769-d08ec680-e500-11ea-8727-5b978478a568.PNG)

Tất cả các plugin ngoại trừ các ``attack`` plugin có thể được cấu hình trong menu này. Liệt kê tất cả các plugin thuộc loại ``audit``:

![list audit](https://user-images.githubusercontent.com/65669673/90966784-f916c080-e500-11ea-8bf2-0098f6e036e7.PNG)

Kích hoạt các plugin ``xss`` và ``sqli`` và kiểm tra lại bằng lệnh:

![xss sqli](https://user-images.githubusercontent.com/65669673/90966802-46932d80-e501-11ea-99ce-9c5a719d10c7.PNG)

Hoặc nếu muốn biết chính xác chức năng của plugin, có thể chạy lệnh ``desc``:

![desc](https://user-images.githubusercontent.com/65669673/90966820-6b87a080-e501-11ea-87d9-172c7346aff3.PNG)

Cấu hình cho plugin:

![conf xss](https://user-images.githubusercontent.com/65669673/90966841-9d006c00-e501-11ea-86d6-ab7c81779466.PNG)

Các menu cấu hình cho plugin cũng có lệnh ``set`` để thay đổi các giá trị tham số và lệnh ``view`` để liệt kê các giá trị hiện có. Trong ví dụ trên đã tắt tính năng kiểm tra tập lệnh liên tục trên nhiều trang web của plugin ``xss``.

### Lưu cấu hình <a name="save-the-configuration"></a>

Khi cấu hình plugin và framework được thiết lập, có thể lưu thông tin này vào profile

![save](https://user-images.githubusercontent.com/65669673/90966883-02545d00-e502-11ea-99e2-d42bb6839a0b.PNG)

Profile được lưu dưới dạng tệp trong ``~/.w3af/profiles/``. Cấu hình đã lưu có thể được tải để chạy một quá trình quét mới

![use fast scan](https://user-images.githubusercontent.com/65669673/90966892-30d23800-e502-11ea-862d-2e61afe1f43a.PNG)

### Bắt đầu quét <a name="start-the-scan"></a>

Sau khi cấu hình tất cả các plugin mong muốn, phải cài mục tiêu quét và cuối cùng bắt đầu quét. Việc lựa chọn mục tiêu được thực hiện theo cách này

![target](https://user-images.githubusercontent.com/65669673/90966922-81e22c00-e502-11ea-8fa4-33677e68c59b.PNG)

Cuối cùng, chạy lệnh ``start`` để bắt đầu quét

![start](https://user-images.githubusercontent.com/65669673/90967049-f1a4e680-e503-11ea-9d66-efaba53d3e03.PNG)
