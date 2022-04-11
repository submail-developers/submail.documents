##  API: SMS/XSend

<br>

### **概览**

<br>


`sms/xsend` 是 SUBMAIL 的短信 API 的升级版本。

与 `sms/send` API 一样，`sms/xsend`  提供完整且强大的短信发送功能，区别于 `sms/send` API，`sms/xsend` 无需提交短信内容和短信签名，仅需提交您创建的短信模版的 ID（*请参见 [获取项目 ID](https://www.mysubmail.com/documents/BfKJ23)*），并可以使用文本变量动态的控制每封短信的内容。 

**了解如何使用[文本变量](https://www.mysubmail.com/documents/wlyI31)。**

使用 `sms/xsend` API 你将可以使用 SUBMAIL 编辑器高效、可视化地创建/管理你的短信模板。当用户请求使用此项目进行触发时，SUBMAIL 会立即执行发送动作，无需担心发送延迟问题。

------

<br>

### **URL**
<br>

##### `https://api-v4.mysubmail.com/sms/xsend`

------
<br>

###  **支持格式**

<br>

| 格式   | URL                                                   |
| ------ | ----------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/sms/xsend.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/sms/xsend.xml`          |

------
<br>

### **http 请求方式**
<br>

| 请求方式    | content-type设置                                             |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

------
<br>

### **是否需要授权**
<br>


##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

------
<br>

### **请求参数**
<br>

| 参数           | 类型         | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ------------ | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`     | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用 ID                       |
| `to`           | `string`     | `必需`    | 无       | 收件人手机号码，该API 仅支持一对一模式（即单条 API 请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。 |
| `project`      | `string`     | `必需`    | 无       | 模版 ID<br>在 SUBMAIL > sms >项目中查看你所创建的短信模版 ID。请参见[获取项目 ID](https://www.mysubmail.com/documents/BfKJ23) |
| `vars`         | `jsonstring` | `必需`    | 无       | 使用文本变量动态控制短信中的文本。<br>参阅 [了解如何创建和使用文本变量](https://www.mysubmail.com/documents/wlyI31) |
| `tag`          | `string`     | 可选      | 无       | 自定义标签功能，该标签可用作 SUBHOOK 追踪（32 个字符以内，当请求传入此参数时则 SUBHOOK 推送时也会携带此参数。tag参数不参加加密计算） |
| `timestamp`    | UNIX 时间戳  | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`     | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `sign_version` | `string`     | 可选      | 无       | signature 加密计算方式(当 sign_version 传 2 时，vars 参数不参与加密计算) |
| `signature`    | `string`     | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------

<br>

### **代码示例**

<br>

#### 发送一封测试短信

<br>


##### POST URL

```
https://api-v4.mysubmail.com/sms/xsend.json
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
    "status": "success",
    "send_id": "c2f0e679ad8dxxxxxf6cb71bf2925665e0",
    "fee": 1,
    "sms_credits": "21129",
    "transactional_sms_credits": "0"
}
```

---

<br>

#### 使用 CURL 发送一封测试短信

<br>

##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;to=138xxxxxxxx&amp;project=ThJBE4&amp;signature=your_app_key' https://api-v4.mysubmail.com/sms/xsend.json
```

<br>

##### 返回

```
{
    "status": "success",
    "send_id": "c2f0e679ad8dxxxxxf6cb71bf2925665e0",
    "fee": 1,
    "sms_credits": "21129",
    "transactional_sms_credits": "0"
}
```

---

<br>

#### 返回值

<br>

##### 请求成功


```
{
    "status": "success",
    "send_id": "c2f0e679ad8dxxxxxf6cb71bf2925665e0",
    "fee": 1,
    "sms_credits": "21129",
    "transactional_sms_credits": "0"
}
```

<br>

##### 请求失败


```
{
      "status":"error",
      "code":"1xx",
      "msg":"error sms"
}
```

------

<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------
