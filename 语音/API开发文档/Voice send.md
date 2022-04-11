##  API: Voice/Send
<br>

### **概览**

<br>

`voice/send` 是 SUBMAIL 的语音通知 API。 当使用 `voice/send` API 提交语音通知时，您无需创建语音模板，SUBMAIL会根据您传入的内容，自动为您创建语音模板。

---

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/voice/send`

---
<br>

###  **支持格式**

<br>

| 格式   | URL                                                    |
| ------ | ------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/voice/send.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/voice/send.xml`          |
| `yaml` | `https://api-v4.mysubmail.com/voice/send.yaml`         |

------

<br>

### **http 请求方式**

<br>

| 请求方式    | content-type设置                                             |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |
---

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/P8IPN4)

---

<br>

### **请求参数**

<br>

| 参数           | 类型        | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的语音应用 ID                       |
| `to`           | `string`    | `必需`    | 无       | 收件人手机号码，例：18688888888                              |
| `content`      | `string`    | `必需`    | 无       | 语音正文(content 参数将会与您账户中的语音模板进行匹配，如 API 返回 420 错误，请在您的账户中添加语音模板，并提交审核,请将语音正文控制在 255个字符以内。) |
| `timestamp`    | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4)  \>  授权和验证方式 |
| `sign_version` | `string`    | 可选      | 1        | signature加密计算方式(当sign_version传2时，content参数不参与加密计算) |
| `signature`    | `string`    | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/P8IPN4)  \>  授权和验证方式 |

---

<br>

### **代码示例**

<br>

#### 发送一封测试语音

<br>
##### POST URL

```
https://api-v4.mysubmail.com/voice/send.json
```



<br>
##### POST DATA

```
appid=your_app_id
&amp;to=138xxxxxxxx
&amp;content= 亲爱爱顾客，快递员：XXX，因无法进入单元，已将您的快递包裹送至您小区的物业，请您及时取回，感谢您的惠顾
&amp;signature=your_app_key
```


<br>
##### 返回


```
{
    "status":"success"
    "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    "fee":1,
    "money_account":"14197"
}
```

---
<br>

#### 使用 `CURL` 发送一封测试短信



<br>
##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;to=17788xxxxxxxx&amp;content=亲爱爱顾客，快递员：XXX，因无法进入单元，已将您的快递包裹送至您小区的物业，请您及时取回，感谢您的惠顾&amp;signature=your_app_key' https://api-v4.mysubmail.com/voice/send.json
```


<br>
##### 返回
```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
       "money_account":14197
}
```

---


<br>

#### 返回值

<br>



##### 请求成功


```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
      "fee":1,
      "sms_credits":14197
}
```


<br>
##### 请求失败


```
{
      "status":"error",
      "code":"1xx",
      "msg":"error message"
}
```

---

<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/fbaT14)

------
