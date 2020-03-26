##  API:Internationalsms/send
<br>

### **概览**

<br>

`internationalsms/send` 是 SUBMAIL 的国际短信 API。 `internationalsms/send` 和短信 API bu 不共享短信模板，当使用` internationalsms/send` API 提交短信时，SUBMAIL 会自动为您创建模板，并进行发送。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/internationalsms/send`

##### `<备> https://api.submail.cn/internationalsms/send`

<br>

###  **支持格式**

<br>

格式 | URL
---|---
json |https://api.mysubmail.com/internationalsms/send.json（默认）
xml | https://api.mysubmail.com/internationalsms/send.xml

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

##### **是**

参阅 [API 授权和验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### **请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的短信应用ID
to |string|必需|无|收件人手机号码，使用标准的 E164 格式，e.g. +1778889901(仅支持单个手机号码，不支持 +86 国内手机号码)
content |string|必需|无|短信正文
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，content参数不参与加密计算)
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

注意：

```
content 可以传自定义内容，非必须短信签名，纯英文短信（包括标点符号，短信签名的[]也需英文）单条按140个字符计费，超过140个字符每132个字符计费一次，其他语言单条按70个字符计费，超过70个字符每67个字符计费一次。
content 参数将会与您账户中的短信模板进行匹配，如 API 返回 420 错误，请在您的账户中添加短信模板，并提交审核
请将 短信正文+du控制在 300 个字符以内。
```

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信

> * JSON
#### `POST URL`

https://api.mysubmail.com/internationalsms/send.json

#### `POST Data`

```
appid=your_app_id
&to=+17788xxxxxxxx
&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
&signature=your_app_key
```

#### `返回：`


```
{
    "status":"success"
    "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    "fee":0.046,
    "account_balance":14197.087
}
```
---
> * XML

#### `POST URL`

https://api.mysubmail.com/internationalsms/send.xml

#### `POST Data`


```
appid=your_app_id
&to=+17788xxxxxxxx
&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
&signature=your_app_key
```


#### `返回`

```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <send_id>61aed69029363042495078c756a1f836</send_id>
    <fee>0.046</fee>
    <account_balance>14197.087</account_balance>
</xml>

```
---

#### 使用 `CURL` 发送一封测试短信


> * JSON


#### `发送 CURL`

```
curl -d 'appid=your_app_id&to=%2B17788xxxxxxxx&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。&signature=your_app_key' https://api.mysubmail.com/internationalsms/send.json
```
#### `返回`
```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
      "fee":0.046,
      "account_balance":14197.087
}
```
---
> * XML
#### `发送 CURL`


```
curl -d 'appid=your_app_id&to=%2B17788xxxxxxxx&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。&signature=your_app_key' https://api.mysubmail.com/internationalsms/send.xml
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <fee>0.046</fee>
     <account_balance>14197.087</account_balance>
</xml>
```

---

<br>

### **返回码**

<br>

>*   JSON

#### `请求成功`


```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
      "fee":0.046,
      "account_balance":14197.087
}
```


#### `请求失败`

{
      "status":"error",
      "code":"1xx",
      "msg":"error message"
}

>* XML

#### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <fee>0.046</fee>
     <account_balance>14197.087</account_balance>
</xml>
```


#### `请求失败`


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

参阅 [API 错误代码](https://www.mysubmail.com/chs/documents/developer/c8ujr)