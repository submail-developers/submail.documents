
## API: balance/voice

<br>

### **概览**

<br>

`balance/voice`是 SUBMAIL 的语音余额查询 API。

使用 `balance/voice` 可以实时获取您账户的语音余额

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/balance/voice`

##### `<备> https://api.submail.cn/balance/voice`

---

<br>

### **支持格式**

<br>

格式 | URL
---|---
json |https://api.mysubmail.com/balance/voice.json（默认）
xml |https://api.mysubmail.com/balance/voice.xml

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

参阅 [API 授权和验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)

---
<br>

### **balance/sms POST 方法 请求参数**

<br>



参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的语音应用 ID
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### **代码示例**

<br>

*   JSON

#### `发送 CURL`


```
curl -d "appid=your_appid&signature=your_appkey" http://api.mysubmail.com/balance/voice.json
```

​                            

#### `返回`


```
{
"status": "success",
"balance": 100.15    // API 返回的当前语音余额
}
```
---

*XML
                            

#### `发送 CURL`


```
curl -d "appid=your_appid&signature=your_appkey" http://api.mysubmail.com/balance/voice.xml
```

​                            

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
<status>success</stats>
<balance>100.15</balance>     // API 返回的当前语音余额
</xml>
```
---

<br>

### **返回码**

<br>

*   JSON


#### `请求成功`


```
{
"status":"success"
}
```

​                                

#### `请求失败`


```
{
"status":"error",
"code":"1xx",
"msg":"error message"
}
```

---

* XML

#### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
<status> success </status>
</xml>
```

​                                

#### `请求失败`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
<status> error </status>
<code> 1xx </code>
<msg> error message </msg>
</xml>
```

<br>

### **错误代码**

<br>

参阅 [API 错误代码](https://www.mysubmail.com/chs/documents/developer/c8ujr)