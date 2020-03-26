##  API:voice/verify 
<br>

### **概览**

<br>

`voice/verify` 是 SUBMAIL 的语音验证码 API 。

集成语音验证码 API 可以让您的网站或应用具备语音验证码功能，在某些极端条件下短信无法送达至用户手机时，语音验证码以电话的形式主动呼叫用户手机，自动语音播报验证码或校验码以达到验证用户身份的目的。

`voice/verify` 已内置语音播报模板，开发者在发起API请求时，传入4位数字验证码，即可完成API请求。

 

（PS: SUBMAIL 语音功能可绑定主叫号码（即主叫号码透传功能），例如您的公司热线电话是：02166957999，语音验证码的主叫号码将显示为：021-66957999，详情请发起工单开通此功能或致电 SUBMAIL 咨询）。

---

<br>

### **URL**

<br>

##### `<主>  https://api.mysubmail.com/voice/verify`

##### `<备> https://api.submail.cn/voice/verify`

<br>

###  **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/voice/verify.json（默认）
xml |https://api.mysubmail.com/voice/verify.xml

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
appid |string|必需|无|在 SUBMAIL 应用集成中创建的语音应用 ID
to |string|必需|无|收件人11位手机号码(仅支持单个手机号码)
code|int|必需|无|4-10位数字（此数字为语音播报的4-10位数字验证码）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### **代码示例**

<br>

#### 发送一封测试语音

> * JSON
#### `POST URL`

https://api.mysubmail.com/voice/verify.json

#### `POST Data`

```
appid=your_app_id
&to=138xxxxxxxx
&code=1234
&signature=your_app_key
```

#### `返回：`


```
{
    "status":"success"
    "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    "money_account":14197
}
```
---
> * XML

#### `POST URL`

https://api.mysubmail.com/voice/verify.xml

#### `POST Data`


```
appid=your_app_id
&to=138xxxxxxxx
&code=1234
&signature=your_app_key
```


#### `返回`

```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <send_id>61aed69029363042495078c756a1f836</send_id>
    <money_account>100.95</money_account>
</xml>
```
---

#### 使用 `CURL` 发送一封测试短信


> * JSON


#### `发送 CURL`

```
curl -d 'appid=your_app_id&to=138xxxxxxxx&code=1234&signature=your_app_key' https://api.mysubmail.com/voice/verify.json
```
#### `返回`
```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
      "money_account":"100.95"
}
```
---
> * XML
#### `发送 CURL`


```
curl -d 'appid=your_app_id&to=138xxxxxxxx&code=1234&signature=your_app_key' https://api.mysubmail.com/voice/verify.xml
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
     <send_id>61aed69029363042495078c756a1f836</send_id>
     <money_account>100.95</money_account>
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
      "money_account":"100.95"
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
     <money_account>100.95</money_account>
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