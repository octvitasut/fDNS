# DNS User Guide 

DNS IP server: 125.212.204.209:53
## Dig command

Là tool dùng để cung test dns server

```bash
# Run dig để query từ một DNS server
dig @<dns_server> <domain_name>
#Ví dụ:
dig @125.212.204.209 cloudrity.com.vn
dig @8.8.8.8 github.com.vn         #Test query tư Google DNS        
```

Kiểm tra kết quả

```bash
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7572
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;github.com.			IN	A

;; ANSWER SECTION:
github.com.		59	IN	A	140.82.118.3

;; Query time: 12 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Thu Jan  9 16:07:09 2014
;; MSG SIZE  rcvd: 45
```
Trong đó:

- Status: Trang thái trả về 
	- NOERROR: Trạng thái ok
	- RESUFED: Server không cho phép query
	- NXDOMAIN: 
-  ANSWER SECTION: Chưa thông tin IP của domain_name từ query
- Query time: độ trễ
- MSG SIZE: Kích thước respones

## fDNS_Portal
Truy nhập portal giám sát
Giả sử portal hoạt động trên địa chỉ IP 192.168.2.2
=> Truy nhập portal tại đường dẫn **http://192.168.2.2/facileManager/**
Account và password là tài khoản super admin được tạo ra khi cài đặt theo hướng dẫn trong deployment guid
![alt text][PORTAL]
[PORTAL]: https://github.com/octvitasut/fDNS/common/images/portal.png "Màn hình login portal giám sát"

Thêm, sửa, xóa zones, domains trên portal giám sát
- Thêm zone mới:
![alt text][PORTAL]

[PORTAL]: https://github.com/octvitasut/fDNS/blob/master/common/images/portal.png "Màn hình login portal giám sát"

- Thêm domain (record) trong zone đã tạo:
Thêm ACL List
![alt text][ACL_LIST]
[ACL_LIST]: https://github.com/octvitasut/fDNS/common/images/acl_list.png "ACL"

Lựa chọn All server để tạo cấu hình cho toàn bộ server DNS được quản lý hay chọn từng server để tạo cấu hình riêng cho từng server
Chọn add new để tạo một ACL mới:
Nhập tên ACL và ấn save để tạo ACL

![alt text][ACL_LIST_NEW]
[ACL_LIST_NEW]: https://github.com/octvitasut/fDNS/common/images/acl_list_add_new.png "ACL add new"

Thêm IP vào ACL bằng cách chọn dâu cộng ở tên ACL
![alt text][ACL_LIST_ADD_IP]
[ACL_LIST_ADD_IP]: https://github.com/octvitasut/fDNS/common/images/acl_list_add_IP1.png "ACL add IP"

Nhập các list IP vào Matched Address List để add IP vào acl
Nhấn Save để lưu lại
![alt text][ACL_LIST_ADD_IP2]
[ACL_LIST_ADD_IP2]: https://github.com/octvitasut/fDNS/common/images/acl_list_add_IP2.png "ACL add IP"

Setting Tsig key
Chọn Menu key để thực hiện setting tsig key
- Key Name: Tên tsig key
- View
- Algorithm: Thuật toán sử dụng
- Secret: Giá trị key (nhập value vào đây)

![alt text][TSIG_KEY]
[TSIG_KEY]: https://github.com/octvitasut/fDNS/common/images/acl_list_add_IP2.png "add tsig key"

Cấu hình các option cho Bind9
Chọn Menu option để thực hiện  tạo option cho Bind9

![alt text][BIND9_OPTION]
[BIND9_OPTION]: https://github.com/octvitasut/fDNS/common/images/bind9_options.png "Bind9 Option"

- Option Name: tên các option trong Bind9
- Option Value: Giá trị setting tương ứng với cấu hình

Cấu hình control cho Bind9 (cấu hình remote bằng rndc)

![alt text][RNDC_CONTROL]
[RNDC_CONTROL]: https://github.com/octvitasut/fDNS/common/images/rndc_control.png "rndc control"

Vào Menu Operations => Chọn Add new để thêm config về rndc.
Ghi chú: Cấu hình phải tương ứng với cấu hình của rndc trong file /etc/rndc.conf

![alt text][RNDC_CONFIG]
[RNDC_CONFIG]: https://github.com/octvitasut/fDNS/common/images/rndc_config.png "rndc config"

Cấu hình của rndc:
- IP address: Địa chỉ listen của bind9 để control
- Port: Port để nhận lệnh từ rndc
- Allowed Address List: Danh sách IP được phép remote (có thể thêm ACL list)
- Key: Giá trị tsig key để xác thực (tạo tsig key trong cấu hình tsig key). => rndc phải có tsig-key để có thể remote

Cấu hình statistic cho Bind9
![alt text][STATISTIC]
[STATISTIC]: https://github.com/octvitasut/fDNS/common/images/statistic.png "statistic"

Vào Menu Operations => Statistics => Chọn Add new để thêm config về statistic

![alt text][STATISTIC_CONFIG]
[STATISTIC_CONFIG]: https://github.com/octvitasut/fDNS/common/images/statistic_config.png "statistic config"

Cấu hình của statsitic
- IP address: Địa chỉ listen của bind9 để xuất report
- Port: 
- Allowed Address List: Danh sách IP được phép truy cập (có thể thêm ACL list)






