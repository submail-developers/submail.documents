## API：Shorturl/info

<br>

### **概览**

<br>

`Shorturl/info`是 短网址 版本信息 API。

使用 `shorturl/info` API 可以获取您的短网址当前的版本信息、短网址/群组用量、和总访问量信息。

---

<br>

### **URL**

<br>

##### `<主> https://service.mysubmail.com/shorturl/info`

---
<br>

### **支持格式**

<br>

| 格式   | URL                                                        |
| ------ | ---------------------------------------------------------- |
| `json` | `https://service.mysubmail.com/shorturl/info.json`（默认） |
| `xml`  | `https://service.mysubmail.com/shorturl/info.xml`          |

---

<br>

### **http 请求方式**

<br>

| 请求方式    | content-type 设置                                            |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

---

<br>

### **是否需要授权**

<br>

##### **是**

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/ALdk5)

---

<br>

### **shorturl/info 请求参数**

<br>

| 参数        | 类型     | 必需/可选 | 默认     | 描述                                                         |
| ----------- | -------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string` | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址应用ID                      |
| `sign_type` | `string` | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string` | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |



---

<br>

### **代码示例**

<br>

#### 使用 `CURL` 方法获取版本信息

<br>
##### 发送 CURL 

```
curl -d 'appid=your_app_id&amp;signature=your_app_key' https://service.mysubmail.com/shorturl/info.json
```

<br>
##### 返回


```
{
    "status": "success",
    "info": {
        "level": "1", // 当前版本，0：免费版 ；1：基础版；2：高级版；3：企业版；4：旗舰版
        "max_shorturl": "500", 		//当前版本最大短网址数量
        "max_shorturl_group": "100", 		//当前版本最大群组数量
        "max_shorturl_customize_domain": "0", 		//当前版本最大自定义域名数量
        "start_at": "2020-12-03 00:00:00", 		//版本开始日期
        "expride_at": "2024-06-01 23:59:59", 		//版本到期时间
        "current_used_shorturl_count": "31", 		// 已使用的短网址数量
        "visit_at_this_month": "241", 		//本月访量
        "visit_count": "11462", 		// 全部访量
        "created_shorturl_count": "471", 		//已创建的短网址总数
        "expired_shorturl_count": "399", 		// 已过期的短网址总数
        "current_used_group_shorturl_count": 0, 		// 已使用的群组短网址数量
        "created_group_shorturl_count": 0, 		//已创建的群组短网址总数
        "expired_group_shorturl_count": 0, 		// 已过期的群组短网址总数
        "current_used_group_count": 0  	// 已使用的群组
    }
}
```



---

<br>

#### Info level 短网址版本信息描述

<br>

| `level : 0` | 免费版 |
| :---------- | :----- |
| `level : 1` | 基础版 |
| `level : 2` | 高级版 |
| `level : 3` | 企业版 |
| `level : 4` | 旗舰版 |

---
<br>
#### 返回值

<br>
##### 请求成功

```
{
      "status":"success",
			"info": {...}
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

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/LmoB14)

------
