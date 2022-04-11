## API: balance/mail

<br>

### **概览**

<br>

`balance/mail` 是 SUBMAIL 的邮件余额查询 API。

使用 `balance/mail` 可以实时获取您账户的邮件余额。

---

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/balance/mail`

---

<br>

### **支持格式**

<br>


| 格式 | URL                                                    |
| ---- | ------------------------------------------------------ |
| json | https://api-v4.mysubmail.com/balance/mail.json（默认） |
| xml  | https://api-v4.mysubmail.com/balance/mail.xml          |

---

<br>

### **http 请求方式**

<br>


| 请求方式  | content-type设置                                             |
| --------- | ------------------------------------------------------------ |
| http post | multipart/form-data、x-www-form-urlencoded、application/json |

---

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/Xi096)

---
<br>
### balance/mail POST 方法 请求参数
<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/Xi096)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/Xi096)  \>  授权和验证方式 |
| `signature` | `string`    | 必需      | 无       | 应用密匙 _或 _数字签名参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/Xi096)  \>  授权和验证方式 |

---

<br>

### **代码示例**

<br>



##### 发送 CURL


```
curl -d "appid=your_appid&amp;signature=your_appkey" http://api-v4.mysubmail.com/balance/mail.json
```

<br>                    

##### 返回


```
{
"status": "success",
"balance": 50    // API 返回的当前邮件余额
"free_balance": 50    // API 返回的当前当日免费邮件余额
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

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/i22PE4)

------
