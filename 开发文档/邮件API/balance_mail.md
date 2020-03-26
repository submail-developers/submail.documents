
## API: `balance/mail

<br>

### **概览**

<br>

`balance/mail` 是 SUBMAIL 的邮件余额查询 API。

使用 `balance/mail` 可以实时获取您账户的邮件余额。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/balance/mail`

##### `<备> https://api.submail.cn/balance/mail`

---

<br>

### **支持格式**

<br>


格式 | URL
---|---
json | https://api.mysubmail.com/balance/mail.json（默认）
xml |https://api.mysubmail.com/balance/mail.xml

---

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

**是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---
### balance/mail POST 方法 请求参数


参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的短信应用ID
timestamp |UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type |string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙 _或 _数字签名参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3gbibb3)  \>  授权和验证方式

---

<br>

### **代码示例**

<br>

*  JSON

#### `发送 CURL：`


```
curl -d "appid=your_appid&signature=your_appkey" http://api.mysubmail.com/balance/mail.json
```

​                            

#### `返回：`


```
{
"status": "success",
"balance": 50    // API 返回的当前邮件余额
"free_balance": 50    // API 返回的当前当日免费邮件余额
}
```
---
*   XML                          

#### `发送 CURL：`


```
curl -d "appid=your\_appid&signature=your\_appkey" http://api.mysubmail.com/balance/mail.xml
```

​                            

#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
<status>success</stats>
<balance>50</balance>     // API 返回的当前邮件余额
<free_balance>50</free_balance>     // API 返回的当前当日免费邮件余额
</xml>
```
---

### **返回码**

*   JSON


#### `请求成功：`


```
{
"status":"success"
}
```

​                                

#### `请求失败：`


```
{
"status":"error",
"code":"1xx",
"msg":"error message"
}
```

---

<br>

###  **XML**

<br>

#### `请求成功：`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
<status> success </status>
</xml>
```

​                                

#### `请求失败：`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
<status> error </status>
<code> 1xx </code>
<msg> error message </msg>
</xml>
```

---

<br>

### **错误代码**

<br>

> 参阅 [API 错误代码](https://www.mysubmail.com/chs/documents/developer/c8ujr)