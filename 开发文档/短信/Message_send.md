##  API: Message/send
<br>

### **概览**

<br>

[一分钟快速集成短信验证码\[图文教程\]](https://www.mysubmail.com/chs/documents/help/SXaAM1)

`message/send` 是 SUBMAIL 的短信 API。 `message/send` API 提供强大的短信发送功能, 并允许用户自定义短信签名及正文，无需提前创建模板，SUBMAIL 会根据您提交的短信签名和内容，自动创建模板并发送

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/message/send`

##### `<备> https://api.submail.cn/message/send`

<br>

###  **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/mail/send.json **（默认）**
xml |https://api.mysubmail.com/mail/send.xml

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

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### **请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的短信应用ID
to |string|必需|无|收件人手机号码，现在短信仅支持一对一模式（即单条API请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。
content |string|必需|无|短信正文`（正文中必须提交有效的短信签名，且您的短信签名必须放在短信的最前端，e.g.【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。content 参数将会与您账户中的短信模板进行匹配，如无匹配 API会创建一个短信模板并提交审核，如审核失败则返回 420 错误请将 短信正文控制在 350 个字符以内。）`
tag|string|可选|无|自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内，添加了 tag 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，content参数不参与加密计算)
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信

> * JSON
#### `POST URL`

https://api.mysubmail.com/message/send.json

#### `POST Data`

```
appid=your_app_id
&to=138xxxxxxxx
&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
&signature=your_app_key
```

#### `返回`


```
{
    "status":"success"
    "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    "fee":1,
    "sms_credits":14197
}
```
---
> * XML

#### `POST URL`

https://api.mysubmail.com/message/send.xml

#### `POST Data`


```
appid=your_app_id
&to=138xxxxxxxx
&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
&signature=your_app_key
```


#### `返回`

```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <send_id>61aed69029363042495078c756a1f836</send_id>
    <fee>1</fee>
    <sms_credits>14197</sms_credits>
</xml>
```
---

#### 使用 `CURL` 发送一封测试短信


> * JSON


#### `发送 CURL`

```
curl -d 'appid=your_app_id&to=138xxxxxxxx&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。&signature=your_app_key' https://api.mysubmail.com/message/send.json
```
#### `返回`
```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
      "fee":1,
      "sms_credits":14197
}
```
---
> * XML
#### `发送 CURL`


```
curl -d 'appid=your_app_id&to=138xxxxxxxx&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。&signature=your_app_key' https://api.mysubmail.com/message/send.xml
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <fee>1</fee>
     <sms_credits>14197</sms_credits>
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
      "fee":1,
      "sms_credits":14197
}
```


#### `请求失败`

```
{
      "status":"error",
      "code":"1xx",
      "msg":"error message"
}
```

>* XML

#### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <fee>1</fee>
     <sms_credits>14197</sms_credits>
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