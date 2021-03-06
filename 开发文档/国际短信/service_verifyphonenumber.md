
## API: service/verifyphonenumber

<br>

### **概览**

<br>

`service/verifyphonenumber`是SUBMAIL的国际号码归属地国家查询API。

使用 `service/verifyphonenumber ` 可以查询您传入的国际手机号码的归属地国家和单价等信息。

---

<br>

### **URL**

<br>

##### `<主>  https://api.mysubmail.com/service/verifyphonenumber`

##### `<备> https://api.submail.cn/service/verifyphonenumber`

---

<br>

### **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/service/verifyphonenumber.json（默认）
xml | https://api.mysubmail.com/service/verifyphonenumber.xml

<br>

### **http 请求方式**

<br>

请求方式| content-type设置
---|---
http post  | multipart/form-data、x-www-form-urlencoded、application/json
---

<br>

### **是否需要授权**

<br>

##### **是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---
<br>

### **balance/sms POST 方法 请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
to |string|必需|无|需要验证的国际手机号码，使用标准的 E164 格式，e.g. +1778889901

---

<br>

### **代码示例**

<br>

*   JSON

#### `发送一封测试短信`

#### POST

```
https://api.mysubmail.com/service/verifyphonenumber.json
```
#### POST Data

```
to=+17788xxxxxxxx
```

​                            

#### `返回`


```
{
    "status":"success" 
    "to":"+17788xxxxxxxx"
    "country_code":"1",
    "country_region":"CA", 
    "country_name":"Canada"，
    "price":"0.070"
}
```
---

* XML
#### POST

```
https://api.mysubmail.com/service/verifyphonenumber.xml
```

#### POST Data

```
to=+17788xxxxxxxx
```

​                            

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <to>+17788xxxxxxxx</to>
    <country_code>1</country_code>
    <country_region>CA</country_region>
    <country_name>Canada</country_name>
    <price>0.070</price>
</xml>
```
