## API: Message/Send

<br>

### **概览**

<br>

[一分钟快速集成短信验证码\[图文教程\]](https://www.mysubmail.com/documents/NMBtl2)

`message/send` 是 SUBMAIL 的短信 API。 `message/send` API 提供强大的短信发送功能, 并允许用户自定义短信签名及正文，无需提前创建模板，SUBMAIL 会根据您提交的短信签名和内容，自动创建模板并发送。

------

<br>

### URL
<br>

#####  `https://api-v4.mysubmail.com/message/send`
------



<br>

###  **支持格式**
<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/message/send.json `**（默认）** |
| `xml`  | `https://api-v4.mysubmail.com/message/send.xml`              |

------


<br>

### **http 请求方式**
<br>

| 请求方式    | content-type设置                                             |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data、x-www-form-urlencoded、application/json` |

------


<br>

### **是否需要授权**
<br>

##### 是

#####  参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

------


<br>

### **请求参数**
<br>

| 参数           | 类型        | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `to`           | `string`    | `必需`    | 无       | 收件人手机号码，该API仅支持一对一模式（即单条API请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。 |
| `content`      | `string`    | `必需`    | 无       | 短信正文<br>（正文中必须提交有效的短信签名，且您的短信签名必须放在短信的最前端，e.g.【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。<br>`content `参数将会与您账户中的短信模板进行匹配，如无匹配 API会创建一个短信模板并提交到人工审核，审核通过后下次提交相似短信（内容达到一定匹配度）则不会触发人工审核直接进行下发，如审核失败则第二次请求返回 420 错误，审核失败会触发SUBHOOK中模板template_reject事件<br>请将短信正文控制在 1000 个字符以内。） |
| `tag`          | `string`    | 可选      | 无       | 自定义标签功能，该标签可用作SUBHOOK追踪<br>（32 个字符以内，添加了 tag 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。tag参数不参加加密计算） |
| `timestamp`    | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `sign_version` | `string`    | 可选      | 无       | signature加密计算方式<br>(当sign_version传2时，content参数不参与加密计算) |
| `signature`    | `string`    | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式。当sign_type=normal时signature应传appkey的值。 |

------

<br>

### **代码示例**

<br>

#### 发送一封测试短信

<br>

##### POST URL

```
https://api-v4.mysubmail.com/message/send.json
```

<br>

##### POST DATA

```
appid=your_app_id
&amp;to=138xxxxxxxx
&amp;content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
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
curl -d 'appid=your_app_id&amp;to=138xxxxxxxx&amp;content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。&amp;signature=your_app_key' https://api-v4.mysubmail.com/message/send.json
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
      "msg":"error message"
}
```

------

<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------
