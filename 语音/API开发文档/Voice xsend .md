##  API: Voice/XSend
<br>

### **概览**

<br>

`Voice/xsend` 是 SUBMAIL 的语音通知 API，语音通知仅支持验证码及通知类内容。

---

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/voice/xsend`

---
<br>

###  **支持格式**

<br>

| 格式   | URL                                                     |
| ------ | ------------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/voice/xsend.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/voice/xsend.xml`          |

---

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

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/J9mty)

---

<br>

### **请求参数**

<br>

| 参数           | 类型         | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ------------ | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`     | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的语音应用 ID                       |
| `to`           | `string`     | `必需`    | 无       | 收件人手机号码，该参数现在仅能提交一个位联系人。             |
| `project`      | `string`     | `必需`    | 无       | 项目标记，在 SUBMAIL > Voice >项目中查看你所创建的语音项目标记。请参见[获取项目 ID](https://www.mysubmail.com/documents/tvF3K4) |
| `vars`         | `jsonstring` | `必需`    | 无       | 使用文本变量动态控制语音中的文本。<br>参阅 [了解如何创建和使用文本变量](https://www.mysubmail.com/documents/wlyI31) |
| `timestamp`    | UNIX 时间戳  | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/J9mty)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`     | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/J9mty)  \>  授权和验证方式 |
| `sign_version` | `string`     | 可选      | 1        | signature加密计算方式(当sign_version传2时，vars参数不参与加密计算) |
| `signature`    | `string`     | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/J9mty)  \>  授权和验证方式 |

---

<br>

### **代码示例**

<br>

#### 发送一封测试语音

<br>
##### POST URL

```
https://api-v4.mysubmail.com/voice/xsend.json
```

<br>

##### POST DATA

```
appid=your_app_id
&amp;to=138xxxxxxxx
&amp;project=ThJBE4
&amp;signature=your_app_key
```

<br>
##### 返回


```
{
    "status":"success"
    "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    "fee":1,
    "money_account":14197
}
```

---

<br>
#### 使用 `CURL` 发送一封测试短信

<br>


##### 发送 CURL

```
url -d 'appid=your_app_id&amp;to=138xxxxxxxx&amp;project=ThJBE4&amp;signature=your_app_key' https://api-v4.mysubmail.com/voice/xsend.json
```

<br>
##### 返回
```
{
      "status":"success"
      "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
      "fee":1,
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
      "money_account":14197
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

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/smwHw2)

------
