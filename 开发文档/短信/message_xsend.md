##  API: Message/xsend
<br>

### **概览**

<br>

[一分钟快速集成短信验证码\[图文教程\]](https://www.mysubmail.com/chs/documents/help/SXaAM1)

`message/xsend` 是 SUBMAIL 的短信 API 的升级版本。

与 `message/send` API 一样，`message/xsend`  提供完整且强大的短信发送功能，区别于 `message/send` API，`message/xsend` 无需提交短信内容和短信签名，仅需提交你在 SUBMAIL MESSAGE 应用程序中创建的短信项目的标记（_请参见 [获取项目或地址薄的开发者标识](https://api.mysubmail.com/chs/documents/developer/MmSw12)_），并可以使用文本变量动态的控制每封短信的内容。 了解如何使用[文本变量](https://www.mysubmail.com/chs/documents/developer/oKraS3)。

使用 `message/xsend` API 你将可以使用 SUBMAIL 编辑器高效、可视化地创建/管理你的短信模板。当用户请求使用此项目进行触发时，SUBMAIL 会立即执行发送动作，无需担心发送延迟问题。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/message/xsend`

##### `<备> https://api.submail.cn/message/xsend`

<br>

###  **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/mail/xsend.json（默认）
xml |https://api.mysubmail.com/mail/xsend.xml

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
to |string|必需|无|收件人手机号码，现在短信仅支持一对一模式（即单条API请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。
project |string|必需|无|项目标记 (ID)，在 SUBMAIL > Message >项目中查看你所创建的短信项目标记。请参见[获取项目或地址薄的开发者标识](https://www.mysubmail.com/chs/documents/developer/MmSw12)
vars |jsonstring|必需|无|使用文本变量动态控制短信中的文本。参阅 [了解如何创建和使用文本变量](https://api.mysubmail.com/chs/documents/developer/oKraS3)
tag|string|可选|无|自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，vars参数不参与加密计算)
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信

> * JSON
#### `POST URL`

https://api.mysubmail.com/message/xsend.json

#### `POST Data`

```
appid=your_app_id
&to=138xxxxxxxx
&project=ThJBE4
&signature=your_app_key
```

#### `返回：`


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

https://api.mysubmail.com/message/xsend.xml

#### `POST Data`


```
appid=your_app_id
&to=138xxxxxxxx
&project=ThJBE4
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
curl -d 'appid=your_app_id&to=138xxxxxxxx&&project=ThJBE4&signature=your_app_key' https://api.mysubmail.com/message/xsend.xml
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
curl -d 'appid=your_app_id&to=138xxxxxxxx&&project=ThJBE4&signature=your_app_key' https://api.mysubmail.com/message/xsend.json
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

参阅 [API 错误代码](https://api.mysubmail.com/chs/documents/developer/c8ujr)