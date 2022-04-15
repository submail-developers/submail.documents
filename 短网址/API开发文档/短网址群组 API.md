# API: ShortURL/Group - 短网址群组

 <br>

### **概览**

 <br>

`shorturl/group`是 SUBMAIL 的短网址群组 API。

使用` shorturl/group` API 可以获取、创建、编辑或删除您的短网址群组。

`shorturl/group`` API` 使用 `HTTP` 规范中的 `GET`, `POST`, `PUT`, `DELETE` 方法对短网址群组进行操作，使用 `GET` 方法获取单个或全部短网址群组、`POST` 方法创建新的短网址群组、`PUT` 方法更新或编辑一个短网址群组，或使用 `DELETE` 方法删除一个短网址群组。

 

---

<br>

### **URL**

<br>

##### ` <主>https://service.mysubmail.com/shorturl/group`
---

<br>

### **支持格式**

<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | ` https://service.mysubmail.com/shorturl/group.json`（默认） |
| `xml`  | `https://service.mysubmail.com/shorturl/group.xml`           |



---

<br>

###   **http 请求方式**

<br>

| `GET`    | `获取全部短网址，或获取指定的单个短网址` |
| -------- | ---------------------------------------- |
| `POST`   | `创建一个新的短网址`                     |
| `PUT`    | `编辑或更新一个短网址`                   |
| `DELETE` | `删除一个短网址`                         |

---

<br>

###  **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/ALdk5)



---

<br>

### **shorturl/group GET 方法（获取短网址群组）请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址应用 ID                     |
| `rows`      | `int`       | 可选      | 100      | 单次返回数据的行数<br>请将该值控制在10-1000之间，若指定了一个无效的 rows 参数，API 将默认返回 100行数据 |
| `offset`    | `int`       | 可选      | 0        | 数据偏移指针<br>该值可以指定返回数据的偏移指针，例：假如单次请求包含150条数据，rows参数采用50行，此时需要查询第51-100行的数据，请将 offset 参数设为1(即数据偏移50行)即可得到第51-100行的数据，offset=2时，将返回第101-150行数据，以此类推 |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |

---
<br>

### **shorturl/group POST 方法（创建短链接群组）请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短链接应用 ID                     |
| `name`      | `string`    | `必需`    | 无       | 短网址群组名称                                               |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |

---
<br>

### **shorturl/group PUT 方法（更新短链接群组）请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址的应用 ID                   |
| `name`      | `string`    | `必需`    | 无       | 短网址群组名称                                               |
| `group`     | `string`    | `必需`    | 无       | 要修改的短网址群组ID                                         |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |

---
<br>

### **shorturl/group DELETE 方法（删除短链接群组）请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址应用 ID                     |
| `group`     | `string`    | `必需`    | 无       | 需要删除的目标短网址群组                                     |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |

---
<br>


### **代码示例**

<br>

#### 使用 `CURL` GET方法获取短网址列表
<br>

##### 发送 CURL

```
curl -s "https://service.mysubmail.com/shorturl/group.json?appid=your_appid&amp;signature=your_appkey"
```

<br>

##### 返回


```
{
    "status": "success",
    "groups": [
        {
            "group": "09ae64b7adbfe917f58e5ddd5200915",
            "name": "submailTest",
            "create_at": "2019-07-17 07:24:28"
        }
    ]
}
```



---

<br>

#### 使用 `CURL` POST方法提交短网址群组

<br>

##### 发送 CURL

```
curl -d "appid=your_appid&amp;signature=your_appkey&amp;name=submail"。https://service.mysubmail.com/shorturl/group.json
```

<br>

##### 返回


```
{
    "status": "success",
    "group": "3c6a3e194526c5dd4cd3378ad6a7b4"
}
```

---



<br>

#### 使用 `CURL` PUT 方法修改短网址群组

<br>

##### 发送 CURL

```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;name=submailgroup=3c6a3e194526cdd4cd3378ad6a7b4" -X put https://service.mysubmail.com/shorturl/group.json
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

#### 使用 `CURL` DELETE 方法删除短网址群组

<br>

##### 发送 CURL

```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;group=3c6a3e194526cdd4cd3378ad6a7b4" -X delete  https://service.mysubmail.com/shorturl/group.json
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