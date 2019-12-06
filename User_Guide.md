# DNS User Guide 

DNS IP server: 125.212.204.209:53
## Dig command

Là tool dùng để cung test dns server

```
# Run dig để query từ một DNS server
dig @<dns_server> <domain_name>
#Ví dụ:
dig @125.212.204.209 cloudrity.com.vn
dig @8.8.8.8 github.com.vn         #Test query tư Google DNS        
```

Kiểm tra kết quả

> ;; Got answer:
> ;; ->>HEADER<<- opcode: QUERY, **status: NOERROR**, id: 7572
> ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

> ;; OPT PSEUDOSECTION:
> ; EDNS: version: 0, flags:; udp: 512
> ;; QUESTION SECTION:
> ;github.com.			IN	A

> ;; ANSWER SECTION:
> **github.com.		59	IN	A	140.82.118.3**
>
> ;; **Query time: 12 msec**
> ;; SERVER: 192.168.0.1#53(192.168.0.1)
> ;; WHEN: Thu Jan  9 16:07:09 2014
> ;; MSG SIZE  rcvd: 45

Trong đó:

- Status: Trang thái trả về 
	- NOERROR: Trạng thái ok
	- RESUFED: Server không cho phép query
	- NXDOMAIN: 
-  ANSWER SECTION: Chưa thông tin IP của domain_name từ query
- Query time: độ trễ
- MSG SIZE: Kích thước respones
