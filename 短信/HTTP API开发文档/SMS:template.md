##  API: SMS/Template

<br>

### **概览**

<br>

`sms/template` 是 SUBMAIL 的短信模板 API。

使用 `sms/template` 可以获取、创建、编辑或删除您的短信模板。

`sms/template` API 使用 `HTTP` 规范中的 `GET`, `POST`, `PUT`, `DELETE` 方法对模板进行操作，使用 `GET` 方法获取单个或全部模板、`POST` 方法创建新的短信模板并提交至 SUBMAIL 人工审核、`PUT` 方法更新或编辑一个短信模板，或使用 `DELETE` 方法删除一个模板。

短信模板引擎支持 `SUBHOOK` 异步推送状态，短信模板在后台人工审核后，会使用 `SUBHOOK` 进行主动推送状态。

------


<br>

### **URL**
<br>

##### ` https://api-v4.mysubmail.com/sms/template`

------
<br>

### **支持格式**
<br>

| 格式   | URL                                                      |
| ------ | -------------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/sms/template.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/sms/template.xml`          |
| `yaml` | `https://api-v4.mysubmail.com/sms/template.yaml`         |

------

<br>

### **http 请求方式**
<br>

- GET         获取全部模板列表，或获取指定的单个模板
- POST       创建一个新的短信模板，并提交至 SUBMAIL 进行人工审核
- PUT         编辑或更新一个短信模板，并提交至 SUBMAIL 进行人工审核
- DELETE     删除一个短信模板

------


<br>

### **是否需要授权**
<br>

##### **是**

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

------
<br>

### **sms/template GET 方法（获取模板列表）请求参数**
<br>

| 参数          | 类型          | 必需/可选 | 默认     | 描述                                                         |
| ------------- | ------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`       | `string`      | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用 ID                       |
| `template_id` | `string`      | 可选      | 无       | 模板ID<br>（要获取单个模板，请将在此参数中提交该模板 ID。为空则获取最新的 1000 个短信模板） |
| `offset `     | `string`      | 可选      | 0        | 数据偏移指针<br>（默认值为0，默认返回最近50个模板信息。offset=1时，查询第51-100个模板，<br>offset=2时，查询第101-150个模板，以此类推。） |
| `timestamp`   | `UNIX 时间戳` | 可选      | 无       | 参阅 [API 授权与验证机制]( https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`   | `string`      | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制]( https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `signature`   | `string`      | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API 授权与验证机制]( https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------
<br>

### **sms/template POST 方法（创建模板）请求参数**
<br>

| 参数            | 类型        | 必需/可选 | 默认     | 描述                                                         |
| --------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`         | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用 ID                       |
| `sms_title`     | `string`    | 可选      | 无       | 模板标题<br>（创建模板时可以在此参数中提交当前模板的标题，作为模板标记） |
| `sms_signature` | `string`    | `必需`    | 无       | 短信模板签名<br>(请使用您的公司名或应用、APP、网站名作为您的短信签名，请将签名字数控制在 2-10 个字符以内，并使用全角大括号“【”和“】”包括，如:“【SUBMAIL】”) |
| `sms_content`   | `string`    | 必需      | 无       | 短信正文<br>(提交短信模板正文，请将模板正文字数控制在 500 个字符以内。可使用文本变量 参阅[了解如何创建和使用文本变量](https://www.mysubmail.com/documents/wlyI31)) |
| `timestamp`     | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制]( https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`     | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制]( https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `signature`     | `string`    | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制]( https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------
<br>

### **sms/template PUT 方法（更新模板）请求参数**
<br>

| 参数            | 类型        | 必需/可选 | 默认     | 描述                                                         |
| --------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`         | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用 ID                       |
| `template_id`   | `string`    | `必需`    | 无       | 需要更新的模板 ID<br>（在 SUBMAIL > sms >项目中查看您所创建的短信模版 ID。请参见 [获取项目 ID](https://www.mysubmail.com/documents/BfKJ23)） |
| `sms_title`     | `string`    | 可选      | 无       | 模板标题<br>（创建模板时可以在此参数中提交当前模板的标题，作为模板标记） |
| `sms_signature` | `string`    | `必需`    | 无       | 短信模板签名<br>(请使用您的公司名或应用、APP、网站名作为您的短信签名，请将签名字数控制在2-15个字符以内，并使用全角大括号“【”和“】”包括，如:“【SUBMAIL】”) |
| `sms_content`   | `string`    | `必需`    | 无       | 短信正文<br>(提交短信模板正文，请将模板正文字数控制在500个字符以内。可使用文本变量 参阅[了解如何创建和使用文本变量](https://www.mysubmail.com/documents/wlyI31)) |
| `timestamp`     | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`     | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `signature`     | `string`    | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------
<br>

### **sms/template DELETE 方法（删除模板）请求参数**
<br>

| 参数          | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`       | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `template_id` | `string`    | 可选      | 无       | 需要删除的模板 ID<br>（在 SUBMAIL > sms >项目中查看你所创建的短信模版 ID。请参见 [获取项目 ID](https://www.mysubmail.com/documents/BfKJ23)) |
| `timestamp`   | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`   | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `signature`   | `string`    | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------

<br>

### **代码示列**

<br>

#### 使用 CURL GET方法获取模板列表

<br>

##### 发送 CURL


```
curl -s "https://api-v4.mysubmail.com/sms/template.json?appid=your_appid&amp;signature=your_appkey"
```

<br>

##### 返回


```
{
"status": "success",
"start_row": 1,
"end_row": 50,
"templates":[
	{
    "template_id": "FIJe14",
    "sms_title": "账户更改邮箱验证码",
    "sms_signature": "【SUBMAIL】",
    "sms_content": "您正在执行更改登录邮箱操作，验证码：@var(code) ，请在工单内提供此验证码",
    "add_date": "2016-01-08 21:28:04",
    "edit_date": "2016-01-08 21:28:04",
    "template_status": "2",
    "template_status_description": "通过审核"
       }
	]
}
```

---

<br>

#### 使用 CURL POST方法提交短信模板

<br>



##### 发送 CURL


```
curl -d "appid=your_appid&amp;signature=your_appkey&amp;sms_title=POST方法测试&amp;sms_signature=【SUBMAIL】&amp;sms_content=您的验证码是：@var(code)，请在10分钟内输入。" http://api.mysubmail.com/sms/template.json
```

<br>

##### 返回


```
{
    "status": "success",
    "template_id": "FsoAF3"    // API 返回的模板ID，作为请求 API 的 PROJECT 参数
}
```

---

<br>

#### 使用 CURL PUT 方法修改短信模板

<br>



##### 发送 CURL


```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;template_id=FsoAF3&amp;sms_title=PUT方法更新模板测试&amp;sms_signature=【SUBMAIL】&amp;sms_content=您的验证码是：@var(code)，请在30分钟内输入。" -X put http://api.mysubmail.com/sms/template.json
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


#### 使用 CURL DELETE 方法删除短信模板

<br>


##### 发送 CURL

<br>

```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;template_id=FsoAF3" -X delete http://api.mysubmail.com/sms/template.json
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

#### template_status 模板状态描述

<br>

| 模板状态            | 描述       |
| ------------------- | ---------- |
| template_status : 0 | 未提交审核 |
| template_status : 1 | 正在审核   |
| template_status : 2 | 审核通过   |
| template_status : 3 | 未通过审核 |

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
    "msg":"error sms"
}
```

------

<br>




### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------
