##  API:Voice/send
<br>

### 概览

<br>

`voice/send` 是 SUBMAIL 的语音通知 API。 当使用 `voice/send` API 提交语音通知时，您无需创建语音模板，SUBMAIL会根据您传入的内容，自动为您创建语音模板

---

<br>

### URL

<br>

##### `<主>  https://api.mysubmail.com/voice/send`

##### `<备> https://api.submail.cn/voice/send`

<br>

###  支持格式

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/voice/send.json（默认）
xml |https://api.mysubmail.com/voice/send.xml

---

<br>

### http 请求方式

<br>

请求方式| content-type设置
---|---
http post  | multipart/form-data、x-www-form-urlencoded、application/json
---

<br>

### 是否需要授权

<br>

##### **是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### 请求参数

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的语音应用 ID
to |string|必需|无|收件人手机号码，例：18688888888
content |string|必需|无|语音正文(content 参数将会与您账户中的语音模板进行匹配，如 API 返回 420 错误，请在您的账户中添加语音模板，并提交审核,请将语音正文控制在 255个字符以内。)
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，content参数不参与加密计算)
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### 代码示例

<br>

#### 发送一封测试语音

> * JSON
#### `POST URL`

https://api.mysubmail.com/voice/send.json

#### `POST Data`

```
appid=your_app_id
&to=138xxxxxxxx
&content= 亲爱爱顾客，快递员：XXX，因无法进入单元，已将您的快递包裹送至您小区的物业，请您及时取回，感谢您的惠顾
&signature=your_app_key
```

#### `返回：`


```
{
    "status":"success"
    "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    "fee":1,
    "money_account":"14197"
}
```
---
> * XML

#### `POST URL`

https://api.mysubmail.com/voice/send.json

#### `POST Data`


```
appid=your_app_id
&to=138xxxxxxxx
&content= 亲爱爱顾客，快递员：XXX，因无法进入单元，已将您的快递包裹送至您小区的物业，请您及时取回，感谢您的惠顾
&signature=your_app_key
```


#### `返回`

```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <send_id>61aed69029363042495078c756a1f836</send_id>
    <fee>1</fee>
    <money_account>14197</money_account>
</xml>
```
---

#### 使用 `CURL` 发送一封测试短信


> * JSON


#### `发送 CURL`

```
curl -d 'appid=your_app_id&to=%2B17788xxxxxxxx&content=亲爱爱顾客，快递员：XXX，因无法进入单元，已将您的快递包裹送至您小区的物业，请您及时取回，感谢您的惠顾&signature=your_app_key' https://api.mysubmail.com/voice/send.json
```
#### `返回`
```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
       "money_account":14197
}
```
---
> * XML
#### `发送 CURL`


```
curl -d 'appid=your_app_id&to=%2B17788xxxxxxxx&content=亲爱爱顾客，快递员：XXX，因无法进入单元，已将您的快递包裹送至您小区的物业，请您及时取回，感谢您的惠顾&signature=your_app_key' https://api.mysubmail.com/voice/send.xml
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <fee>1</fee>
     <money_account>14197</money_account>
</xml>
```

---

<br>

### 返回码

<br>

*   JSON

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

### 错误代码

<br>

参阅 [API 错误代码](/chs/documents/developer/c8ujr)