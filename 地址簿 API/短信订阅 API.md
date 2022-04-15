# API: AddressBook/SMS/Subscribe - 短信订阅

<br>

### **概览**

<br>

`addressbook/sms/subscribe` 是 SUBMAIL 的短信订阅 API ，使用 `addressbook/sms/subscribe` API 管理你的短信订阅用户。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/addressbook/sms/subscribe`

##### `<备> https://api.submail.cn/addressbook/sms/subscribe`

------

<br>

### **支持格式**

<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | `https://api.mysubmail.com/addressbook/sms/subscribe.json`（默认） |
| `xml`  | `https://api.mysubmail.com/addressbook/sms/subscribe.xml`    |

---

<br>

### **http 请求方式**

<br>

##### **`POST`**

---

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

---

<br>

### **请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认        | 描述                                                         |
| ----------- | ----------- | --------- | ----------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无          | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `address`   | `string`    | `必需`    | 无          | 联系人 11 位 手机号码 e.g.13xxxxxxxxx                        |
| `target`    | `string`    | 可选      | `subscribe` | 地址簿标识，将联系人添加到目标地址簿<br>忽略此参数，SUBMAIL 默认将联系人添加到订阅地址簿。<br>请参见 [获取项目或地址簿的开发者标识](https://www.mysubmail.com/documents/BfKJ23) |
| `timestamp` | UNIX 时间戳 | `必需`    | 无          | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal`    | API 授权模式（ ` md5 or sha1 or normal `）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无          | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe) >  授权和验证方式 |



---

<br>

### **代码示例**

<br>

#### 添加一个短信联系人到订阅地址簿

<br>

##### POST 

```
https://api.mysubmail.com/addressbook/sms/subscribe.json
```

<br>

##### POST Data


```
appid=your_app_id
&amp;address=138xxxxxxxx
&amp;signature=your_app_key
```

<br>

##### 返回


```
{
    "status":"success"
}
```

---

<br>

#### 添加一个短信联系人到目标地址簿

<br>

##### POST 

```
https://api.mysubmail.com/addressbook/sms/subscribe.json
```

<br>

##### POST Data


```
appid=your_app_id
&amp;address=138xxxxxxxx
⌖=ThJBE4
&amp;signature=your_app_key
```

<br>

##### 返回


```
{
    "status":"success"
}
```

------

<br>

##### 使用 `CURL` 添加一个短信联系人到订阅地址簿

<br>

##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;address=138xxxxxxxx&amp;signature=your_app_key' https://api.mysubmail.com/addressbook/sms/subscribe.json
```

<br>

##### 返回


```
{
      "status":"success"
}
```

---

<br>

#### 使用 `CURL` 添加一个短信联系人到目标地址簿

<br>

##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;address=138xxxxxxxx⌖=ThJBE4&amp;signature=your_app_key' https://api.mysubmail.com/addressbook/message/subscribe.json
```

<br>

##### 返回


```
{
      "status":"success"
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

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------