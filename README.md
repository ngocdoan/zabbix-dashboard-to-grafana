# zabbix-dashboard-to-grafana
## Zabbix


1. Mở X-Frame-Options trên zabbix cho phép được nhúng dashboard hoặc map trên site khác
Trên Zabbix server:
Apache: sửa file cấu hình 

> vi /etc/httpd/conf.d/zabbix.conf

thêm trong thẻ 

    <Directory "/usr/share/zabbix">
     Header always unset X-Frame-Options
     Header set X-Frame-Options "ALLOWALL"
    </Directory>

Khởi động lại Apache

> systemctl restart httpd

2. Bật user Guest trong Zabbix
3. Set quyền đọc dữ liệu cho Guest
4. Set Dashboard hoặc Map sang chế độ Public

## Grafana

1. Cấu hình Grafana cho phép iframe website
Sửa file 

> vi /etc/grafana/grafana.ini

sửa false thành true và bỏ dấu comment ;

`disable_sanitize_html = true`

Khởi động lại Grafana

> systemctl restart grafana-server

2. Nhúng iframe zabbix trong grafana
- Add panel
- Chọn loại Text Panel >> Html



Nhúng đoạn code sau:
````<iframe src="http://link.here" title="Title here" style="width:100%; height:100%; padding:0; margin:0; border:none;"></iframe>````

Thêm &kiosk=1 sau link để ko hiện zabbix panel.
