##  API: FlashSMS/XSend

<br>

### **概览**

<br>


`flashsms/xsend` 是 SUBMAIL 的针对闪信 开发的 API 。

闪信正文内容最大长度不超过66个字符，编辑完成后，需要联系客服在运营商报备，在报备完成后，即可发送

------

<br>

### **URL**
<br>

##### `https://api-v4.mysubmail.com/flashsms/xsend`

------
<br>

###  **支持格式**

<br>

| 格式   | URL                                                        |
| ------ | ---------------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/flashsms/xsend.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/flashsms/xsend.xml`          |

------
<br>

### **http 请求方式**
<br>

| 请求方式       | content-type设置                                             |
| -------------- | ------------------------------------------------------------ |
| `post` , `get` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

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

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用 ID                       |
| `to`        | `string`    | `必需`    | 无       | 收件人手机号码，该API 仅支持一对一模式（即单条 API 请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。 |
| `project`   | `string`    | `必需`    | 无       | 模版 ID<br>在 SUBMAIL > Message >项目中查看你所创建的短信模版 ID。请参见[获取项目 ID](https://www.mysubmail.com/documents/BfKJ23) |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------

<br>

### **代码示例**


<br>


##### POST URL

```
https://api-v4.mysubmail.com/flashsms/xsend.json
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
}
```

---

<br>


##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;to=138xxxxxxxx&amp;project=ThJBE4&amp;signature=your_app_key' https://api.mysubmail.com/flashsms/xsend.json
```

<br>

##### 返回

```
{
    "status": "success",
    "send_id": "c2f0e679ad8dxxxxxf6cb71bf2925665e0",
    "fee": 1,
    "sms_credits": "21129",
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
