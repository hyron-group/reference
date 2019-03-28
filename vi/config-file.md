# appcfg là gì ?
``appcfg.yaml`` là file chứa các thiết đặt của các module trong ứng dụng

![](/res/appConfig.png)

# Tại sao ?
- Dễ dàng tùy biến module
- Linh hoạt, đa dụng
- Dễ học, dễ dùng
- Cho phép kế thừa
- Hỗ trợ tham chiếu sâu
- Hỗ trợ tham chiếu nội
- Hỗ trợ tham chiếu ngoại
- Hỗ trợ khóa giá trị

# Phân loại

config có thể chia làm 2 loại theo cấp độ là : ``Module level`` và ``Application Level``

## **Module level**

### **1. Service config**

### **Structure**
```
service-name
  ├── controller/
  ├── model/
  ├── index.js
  ├── router.js
  └── appcfg.yaml
```

### **appcfg.yaml**
```yaml
page_size: 20
filter:
  - age
  - location
```

### **Sử dụng**
Service config có thể được truy cập bởi biến ``this.$config``
```js
getUsers(){
    var {page_size, filter} = this.$config;
    ...
}
```

Nếu đây là một UnofficialService
```js
module.exports = function(app, cfg){
    var {page_size, filter} = this.$config;
    ...
}
```

### **2. Plugins config**

### **Structure**
```
plugin-name
  ├── src/
  ├── lib/
  ├── index.js
  ├── hyron-plugin.js
  └── appcfg.yaml
```

### **appcfg.yaml**
```yaml
private_key: 123456
```

### **Sử dụng**
plugins/demo/hyron-plugin.js
```js
function handler(req, res, prev, cfg){
    var {private_key} = cfg;
    ...
}
```

### **3. Addons config**

### **Structure**
```
addon-name
  ├── src/
  ├── lib/
  ├── index.js
  ├── hyron-addon.js
  └── appcfg.yaml
```
### **appcfg.yaml**
```yaml
email: thangphung.work@gmail.com
```

### **Sử dụng**
addons/demo/hyron-addon.js
```js
module.exports = function(cfg){
    var {email} = cfg;
}
```

## **Application level**

### **Structure**
```
root
  ├── services/
  ├── addons/
  ├── plugins/
  ├── res/
  ├── server/
  ├── public/
  ├── index.js
  ├── package.json
  └── appcfg.yaml
```

### **appcfg.yaml**
```yaml
public_key: ahihi123
app_name: myApp
```

# Tính năng

## 1. Khóa trường
Để ngăn chặn việc kế thừa một trường, thêm '$' trước tên của trường đó. Ví dụ :
plugins/demo/appcfg.yaml
```yaml
$private_key: 123456
```

## 2. Tham chiếu sâu
Để truy cập vào một trường sâu trong 1 trường cha. Ví dụ :

addons/crud/appcfg.yaml
```yaml
schema:
  accounts:
    email: string
    password: string
```

addons/crud/hyron-addons.js
```js
const {getConfig} = require("hyron");

module.exports = function(cfg){
    var accountModel = getConfig("schema.accounts", {});
}
```

## 3. Tham chiếu nội

Giá trị một trường trong appcfg có thể được **tham chiếu nội** đến trường khác. Ví dụ :

```yaml
key1:
  child1: hello

key2: <#key1.child1> # hello
```

## 4. Tham chiếu ngoại
Giá trị một trường trong appcfg có thể được **tham chiếu ngoại** bởi một file ``yaml`` khác

models/account.yaml
```yaml
email: string
password: string
```

addons/crud/appcfg.yaml
```yaml
schema:
  account: <~models/account.yaml>
```

## 5. Kế thừa

``appcfg.yaml`` tại **Application Level** có thể ghi đè các config từ các config trong **Module Level** bằng cách định danh đến module đó (được khai báo trong build file)

### **appcfg.yaml**
```yaml
service_name:
  page_size: 50
  
addons_name:
  email: hyron.dev@gmail.com

plugins_name:
  private_key: abc123
```