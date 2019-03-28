# Build File là gì ?
Là một file json chứa thông tin về các module và thiết đặt trong ứng dụng

![](/res/management-system.png)

# Tại sao
- Dễ nắm bắt
- Dễ chỉnh sửa
- Có thể tự động hóa
- Dễ học, dễ dùng
- Hỗ trợ tham chiếu ngoại
- Tự động cài gói còn thiếu

# Sử dụng
một json build file chứa các thông tin về một instance

server/app.json
```json
{
    "base_url": "http://localhost:3000",
    "services": {
        "account": "services/account/router.js",
        "user": "services/user/router.js",
    }
}
```

Các trường đặc biệt :

|Tên|Kiểu|Mô tả|
|---|----|-----|
| base_url |string| thiết lập base url cho instance này |
| server |object| chứa các thông tin về server, bao gồm : ``host``, ``port``, ``protocol``, ``prefix`` |
|setting |object| chứa các thiết đặt cho instance này |
| addons |object| chứa danh sách các addons được kích hoạt |
| plugins |object| chứa danh sách các plugins được kích hoạt |
| services |object| chứa danh sách các services được kích hoạt |

# Tính năng

## 1. Tham chiếu ngoại
Để chạy nhiều instance, bạn có thể sử dụng một mảng chứa các đường dẫn của nó. Ví dụ :

### **Structure**

```
server
  ├── myApp.json
  ├── otherApp.json
  └── app.json
```

**server/app.json**
```json
[
    "server/myApp.json",
    "server/otherApp.json"
]
```

## 2. Global addons
để khai báo global instance mà có thể được chạy tự động trên mỗi instance. Thêm một instance rỗng chỉ chứa ``addons`` như sau

**server/global-addons.json**
```json
{
    "addons" : {
        "java_driver" : "@hyron/java-supporter"
    }
}
```

**server/app.json**
```json
[   
    "server/global-addons.json",
    "server/myApp.json",
    "server/otherApp.json"
]
```

## 3. Tự động cài gói còn thiếu
JSON build file sẽ tự động phát hiện và cài đặt những gói còn thiếu, sử dụng yarn package engine