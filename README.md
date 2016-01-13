#**I.Cách cài đặt phần mềm trên các distro khác nhau**

##**Biên dịch phần mềm**
- Phương pháp này **không phụ thuộc bạn dùng distro nào miễn là dùng Linux** là đều có thể dùng. Bước đầu tiên khi muốn thực hiện phương pháp cài đặt này là bạn phải có file source của nó(có định dạng thường là file nén tag.gz. tar.bz2,..). Sau khi down file source về bạn tiến hành giải nén nó ra, sau đó vào trong thư mục giải nén thực hiện quá trình đầu tiên là check thư viện và các config file. biên dịch phần mềm cần phải đầy đủ thư viện thì mới có thể biên dịch được. Nó không thể tự động tìm các gói phụ thuộc để cài đặt . 
- Biên dịch phần mềm làm giảm thiểu rủi ro một cách tối ưu nhất có thể cho hệ thống phát sinh từ những thành phần hay module trong phần mềm. Bạn có thể tùy chỉnh cài đặt những thành phần nào vào hệ thống ở bước đầu tiên.
- Ngoài ra, sử dụng phương pháp này bạn có thể tối ưu hóa tài nguyên hệ thống . Đối với kiến thức trong tương lai, biên dịch có thể cho bạn những kiến thức cơ bản đầu tiên về biên dịch kernel trên Linux và đích cuối cùng chính là tự mình biên dịch một distro linux cho riêng mình.

###**Bên dịch phần mềm httpd:**
- **Bước 1:** Tải httpd-2.4.10.tar.bz2
 
- **Bước 2:** Giải nén tập tin + #unzip                  để giải nén                       name_package.zip
 + #tar -xvzf              để giải nén                       name_package.tar.gz
 + #tar -jvxf              để giải nén                       name_package.tar.bz2
 + #tar -x                 để giải nén                       name_package.tgz
 
- **Bước 3:** Tạo thư mục để cài phần mềm
 + Tạo thư mục httpd trong thư mục /usr/local/
 + Sử dụng lệnh #ll để kiểm tra thư mục vừa tạo
 
- **Bước 4:** Vào thư mục vừa giải nén để chuẩn bị biên dịch
 + [root@localhost ~]# cd httpd-2.4.10
- Đọc file README hoặc INSTALL để xem hướng dẫn cài đặt.
 + [root@localhost httpd-2.4.10]# vi README
 + [root@localhost httpd-2.4.10]# vi INSTALL- **Bước 5:** Cấu hình cho gói phần mềm (Bước này xảy ra lỗi nhiều nhất)
 + [root@localhost httpd-2.4.10]# ./configure –prefix=/usr/local/httpd/ –with-included-apr
 + #–prefix là nơi sẽ cài phần mềm vào giống như chọn đường dẫn để cài phần mềm trong windows.
 + #–with-included-apr: trong tập tin INSTALL có hướng dẫn là tải apr và apr-util rồi copy vào /httpd-2.4.10/srclib/
 
- **Bước 6:** Biên dịch cho gói phần mềm:
 + #make
 + [root@localhost httpd-2.4.10]# make

- **Bước 7:** Cài đặt gói phần mềm httpd vừa biên dịch:
 + #make install
 + [root@localhost httpd-2.4.10]# make install
- Khởi động dịch vụ httpd:
 + [root@localhost ~]# /usr/local/httpd/bin/apachectl start
- Xong các bước trên các bạn cài phần mềm w3m để lướt web trên giao diện dòng lệnh:
 + [root@localhost ~]# yum install w3m 
 + [root@localhost ~]# w3m localhost

#**II.Sự khác nhau giữa update, upgrade và dist-upgrade**
- **Update** là cập nhật các gói mới trong máy.
- **Upgrade** là nâng cấp lên phiên bản mới hơn.
- **Dist-upgrade** nằm trong lệnh : *sudo apt-get dist-upgrade* .
Lệnh này nâng cấp toàn hệ thống tới một phiên bản mới hơn. Nó báo APT sử dụng hệ thống giải quyết xung đột thông minh và nó sẽ thử nâng cấp những gói quan trọng nhất.

#**III.Tìm hiểu và cài đặt Apache làm Webserver**
- Web Server là máy chủ có dung lượng lớn, tốc độ cao, được dùng để lưu trữ thông tin như một ngân hàng dữ liệu, chứa những website đã được thiết kế cùng với những thông tin liên quan khác. (các mã Script, các chương trình, và các file Multimedia).

##**1.Apache là một phần mềm có nhiều tính năng mạnh và linh hoạt dùng để làm Web Server.**
- Hỗ trợ đầy đủ những giao thức HTTP trước đây như HTTP/1.1
- Có thể cấu hình và mở rộng với những module của công ty thứ ba.
- Cung cấp source code đầy đủ với license không hạn chế.
- Chạy trên nhiều hệ điều hành như Windows NT/9X, Netware 5.x, OS/2 và hầu hết các hệ điều hành Unix.

##**2. Tính năng cơ bản**
- Máy chủ web Apache có thể được bổ sung bằng một chương trình cho phép tích hợp chức năng tìm kiếm với một website. Các đơn vị phần mềm khác nhau có sẵn với hệ thống tìm kiếm HTDig cho phép đánh chỉ số toàn bộ website. Trình Iprogram sử dụng robot để tạo ta một chỉ số tìm kiếm mà chỉ số này có thể được duyệt bằng một CGI script phù hợp. 
- Các chức năng cơ bản của phần mềm này được mô tả ở phần dưới: 
 - Tạo ra một chỉ số của máy tìm kiếm (cho 1 hoặc nhiều website và/hoặc các phần của một webiste).
 - Sử dụng bộ lọc để hạn chế chức năng đánh chỉ số. Tiêu chuẩn lọc có thể là dạng tệp và URL đặc biệt.

- Các chương trình bổ sung bên ngoài có thể được sử dụng để đánh chỉ số các định dạng tệp (PDF, DOC,…).
- Các lựa chọn yêu cầu số tồn tại và các thuật toán tìm kiếm khác nhau có thể được sử dụng (các từ, phần của từ, các từ đồng nghĩa…).
- Trang tìm kiếm và bản liệt kê tương ứng có thể được chỉnh bằng việc sử dụng các tệp mẫu template đơn giản.
- Các nguyên âm biến âm sắc trong chuỗi tìm kiếm được hỗ trợ
- Robot hỗ trợ chuẩn cho việc "Loại trừ Robot" và "Xác thực WWW cơ bản" cho việc đánh chỉ số các nội dung được bảo vệ.

##**3. Cài đặt Apache**
- Update Ubuntu server: *sudo apt-get update*
- Cài đặt Apache với câu lệnh: *sudo apt-get install apache2*
- Nó có hỏi Y/N thì cứ ấn Y rồi Enter.
- Sau khi cài đặt, hãy thử trên trình duyệt: http://localhost


![Cài đặt thành công Apache](https://assets.digitalocean.com/articles/lamp_1404/default_apache.png)


- Sử dụng những lệnh sau để khởi động, kích hoạt và ngừng hoạt động của Apache:
 + *sudo /etc/init.d/apache2 start #start apache*
 + *sudo /etc/init.d/apache2 stop #stop apache*
 + *sudo /etc/init.d/apache2 restart #restart apache*

- Muốn Apache tự khởi động cùng hệ thống, gõ lệnh sau: *sudo update-rc.d apache2 defaults*
- Không muốn Apache tự khởi động cùng hệ thống, gõ lệnh sau: *sudo update-rc.d -f apache2 remove*

###**3.1) Cấu trúc thư mục cấu hình Apache trên Ubuntu**
- Mặc định trên Ubuntu, thư mục chứa các thiết lập của Apache sẽ nằm trong thư mục /etc/apache2. Trong thư mục đó, nó có một số thư mục và file cấu hình như sau:
- *conf-available/* – Thư mục này sẽ chứa các file thiết lập cấu hình sẵn của Apache trên Ubuntu, nhưng các thiết lập trong đây sẽ chưa được áp dụng vì Ubuntu không load thiết lập cấu hình trong thư mục này.
- *conf-enabled/* – Thư mục chứa các file thiết lập cấu hình của Apache trên Ubuntu đang được bật. Hãy hiểu là nếu thư mục này có một liên kết tượng trưng (symlink) qua một file module nào đó bên thư mục conf-available thì nó sẽ được bật.
- *mods-available/* – Thư mục chứa các file từng module của Apache trên Ubuntu nhưng chưa được bật.
- *mods-enabled/* – Thư mục chứa các file từng module của Apache trên Ubuntu đang được bật.
- *site-available/* – Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu nhưng chưa được bật.
- *site-enabled/* – Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu đang được bật.
- *apache2.conf* – File cấu hình Apache trên Ubuntu.
- *envvars* – File thiết lập các biến với giá trị sẵn để sử dụng trong các file cấu hình.
- *magic* – File thiết lập của module mod_mime_magic trên Apache.
- *ports.conf* – File cấu hình cổng mạng của Apache (mặc định là port 80).

###**3.2: Thư mục gốc chứa dữ liệu website của Apache trên Ubuntu**
- Mặc định, Apache trên Ubuntu sẽ sử dụng thư mục /var/www/html để chứa dữ liệu website gốc (load bằng IP hoặc hostname). Khi bạn vào đây sẽ thấy một file index.html, đó chính là file giao diện chào mừng mà bạn đã thấy ở trên.

##**IV.Thiết lập card mạng ảo trong Ubuntu**

###**1. Cấu hình bằng dòng lệnh**
- eth0 NIC IP 192.168.1.5
- eth0:0 first NIC alias: 192.168.1.6

 + Set eth0:0 bằng dòng lệnh với quyền user root
- Lệnh : *# ifconfig eth0:0 192.168.1.6 up*

- Lệnh: 
 + *# vi /etc/network/interfaces*
 + *auto eth0:1*
 + *iface eth0:1 inet static*
 + *name Ethernet alias LAN card*
 + *address 192.168.1.6*
 + *netmask 255.255.255.0*
 + *broadcast 192.168.1.255*
 + *network 192.168.1.0*

- Lưu lại và đóng lại file, sau đó restart lại network
 + Lệnh: *# /etc/init.d/networking restart*









