#  API: MMS/XSend - 彩信模板发送
<br>

### **概览**

<br>

`MMS/xsend` 是 SUBMAIL 彩信 单发API。



---

<br>

### **URL**

 <br>

##### `https://api-v4.mysubmail.com/mms/xsend`

---
<br>

###  **支持格式**

<br>

| 格式   | URL                                                        |
| ------ | ---------------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/mms/xsend.json `**（默认）** |
| `xml`  | `https://api-v4.mysubmail.com/mms/xsend.xml`               |
| `yaml` | `https://api-v4.mysubmail.com/mms/xsend.yaml`              |

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

##### **是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/P8IPN4)

---

<br>

### **请求参数**

<br>

| 参数        | 类型         | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ------------ | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`     | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的彩信应用ID                        |
| `to`        | `string`     | `必需`    | 无       | 收件人手机号码，现在彩信信仅支持一对一模式（即单条API请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。 |
| `project`   | `string`     | `必需`    | 无       | 模板标记 (ID)                                                |
| `vars`      | `jsonstring` | 可选      | 无       | 使用文本变量动态控制彩信中的文本。<br>参阅 [了解如何创建和使用文本变量](https://www.mysubmail.com/documents/wlyI31) |
| `tag`       | `string`     | 可选      | 无       | 自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内，当请求传入此参数时则SUBHOOK推送时也会携带此参数） |
| `timestamp` | UNIX 时间戳  | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`     | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4)  \>  授权和验证方式 |
| `signature` | `string`     | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/P8IPN4)  \>  授权和验证方式 |

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信

<br>

##### POST URL

```
https://api-v4.mysubmail.com/mms/xsend.json
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
    "money_account":14197.23
}
```
---

<br>

#### 使用 `CURL` 发送一封测试短信

<br>


##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;to=138xxxxxxxx&amp;&amp;project=ThJBE4&amp;signature=your_app_key' https://api-v4.mysubmail.com/message/xsend.xml
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
      "money_account":14197.23
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
