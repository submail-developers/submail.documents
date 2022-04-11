##  API: Balance/MMS

<br>

### **概览**

 <br>

`balance/mms` 是 SUBMAIL 的彩信余额查询 API。

使用 `balance/mms` 可以实时获取您账户的彩信余额。

 

------

<br>

### **URL**

<br>

##### `<主> https://api-v4.mysubmail.com/balance/mms`

------

<br>

### **支持格式**

<br>



| 格式   | URL                                                       |
| ------ | --------------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/balance/mms.json`**(默认)** |
| `xml`  | `https://api-v4.mysubmail.com/balance/mms.xml`            |

---

<br>

### **http 请求方式**

<br>



| 请求方式    | content-type设置                                          |
| ----------- | --------------------------------------------------------- |
| `http post` | `form-data` 、`x-www-form-urlencoded`、`application/json` |

---

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/P8IPN4)

------

<br>

### **balance/mms POST 方法 请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的彩信应用 ID                       |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |

------

<br>

### **代码示例**

<br>



##### 发送 CURL


```
curl -d "appid=your_appid&amp;signature=your_appkey" http://api-v4.mysubmail.com/balance/mms.json
```

<br>
##### 返回


```
{
"status": "success",
"balance": 100.15    // API 返回的当前彩信余额
}
               
```



------



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

------

<br>

###  **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/fbaT14)

------
