##  API:MMS/xsend
<br>

### **概览**

<br>

MMS/xsend 是 SUBMAIL 彩信 API。

mms/xsend 与 message/xsend 参数几乎一致，mms/xsend与其他短信服务不共享模板，需要您创建单独的模板进行发送

---

<br>

### **URL**

 <br>

##### `<主> https://api.mysubmail.com/mms/xsend`

##### `<备> https://api.submail.cn/mms/xsend`

<br>

###  **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/mms/xsend.json（默认）
xml |https://api.mysubmail.com/mms/xsend.xml

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
appid |string|必需|无|在 SUBMAIL 应用集成中创建的彩信应用ID
to |string|必需|无|收件人手机号码，现在彩信信仅支持一对一模式（即单条API请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。
project |string|必需|无|项目标记 (ID)
vars |jsonstring|必需|无|使用文本变量动态控制短信中的文本。参阅 [了解如何创建和使用文本变量](https://www.mysubmail.com//chs/documents/developer/oKraS3)
tag|string|可选|无|自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com//chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com//chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，vars参数不参与加密计算)
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://www.mysubmail.com//chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信

> * JSON
#### `POST URL`

https://api.mysubmail.com/mms/xsend.json

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
    "money_account":14197.23
}
```
---
> * XML

#### `POST URL`

https://api.mysubmail.com/mms/xsend.xml

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
    <money_account>14197.23</money_account>
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
      "money_account":14197
}
```
---
> * XML
#### `发送 CURL`


```
curl -d 'appid=your_app_id&to=138xxxxxxxx&&project=ThJBE4&signature=your_app_key' https://api.mysubmail.com/message/send.json
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <fee>1</fee>
      <money_account>14197.23</money_account>
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
      "money_account":14197.23
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
     <money_account>14197.23</money_account>
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

参阅 [API 错误代码](/chs/documents/developer/c8ujr)

