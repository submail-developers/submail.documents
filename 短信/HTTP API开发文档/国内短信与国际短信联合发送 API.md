# API: SMS/UnionSend - 国内短信与国际短信联合发送

<br>

### **概览**

<br>

`sms/unionsend` 是 SUBMAIL 的国内短信与国际短信联合发送 API，sms/unionsend 结合了国内短信和国际短信的发送接口，对不同国家的监管政策执行不同的发送策略，在单一接口实现全球化短信发送功能；

------

<br>

### ** URL**

<br>

#####  ` https://api-v4.mysubmail.com/sms/unionsend`

------



<br>

###  **支持格式**

<br>

| 格式   | URL                                                       |
| ------ | --------------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/sms/unionsend.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/sms/unionsend.xml`          |
| `yaml` | `https://api-v4.mysubmail.com/sms/unionsend.yaml`         |

------

<br>

### **http 请求方式**

<br>

| 请求方式 | content-type设置                                             |
| -------- | ------------------------------------------------------------ |
| `post`   | `multipart/form-data、x-www-form-urlencoded、application/json` |
| `get`    |                                                              |

------

<br>

### **是否需要授权**

<br>

##### 是

#####  参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

请注意：`sms/unionsend` 接口仅支持 `normal` 明文 验证模式，暂不支持 `MD5/SHA1/SHA256` 模式

------

<br>

### **请求参数**

<br>

| 参数                             | 类型                          | 必需/可选 | 默认 | 描述                                                         |
| -------------------------------- | ----------------------------- | --------- | ---- | ------------------------------------------------------------ |
| `appid`                          | `string`                      | `必需`    | 无   | 国内短信 AppID                                               |
| `signature`                      | `string`                      | `必需`    | 无   | 国内短信应用密钥（Appkey）                                   |
| `inter_appid`                    | `string`                      | `必须`    | 无   | 国际短信 AppID                                               |
| `inter_signature`                | `string`                      | `必须`    | 无   | 国际短信应用密钥（Appkey）                                   |
| `to`                             | `string`                      | `必需`    | 无   | 收件人手机号码，该API仅支持一对一模式（即单条API请求仅能发送一个联系人），该参数现在仅能提交一个位联系人。<br />*注：国际号段请使用标准的 E164 格式，e.g. +1778889901； 国内短信可直接使用11位国内手机号码进行发送， 国内号段同样支持 +86138xxxxx 格式* |
| `content`                        | `string`                      | `必需`    | 无   | 短信正文<br>（正文中必须提交有效的短信签名，且您的短信签名必须放在短信的最前端，e.g.【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。<br>`content `参数将会与您账户中的短信模板进行匹配，如无匹配 API会创建一个短信模板并提交到人工审核，审核通过后下次提交相似短信（内容达到一定匹配度）则不会触发人工审核直接进行下发，如审核失败则第二次请求返回 420 错误，审核失败会触发SUBHOOK中模板`template_reject`事件<br>请将短信正文控制在 1000 个字符以内。） |
| `inter_content`                  | `string`                      | 可选      | 无   | 国际短信正文，当发送为国际短信时（非+86），优先使用该参数中传递的正文；如该参数为空则使用 `content` 参数作为短消息正文进行发送; |
| `intersms_verify_code_transform` | `string` (`true`  or `false`) | 可选      | 无   | 是否提取短消息正文 `content` 参数中的验证码（数字 4 - 10 位），替换 `inter_content` 中的 `@var(code)` 变量；<br />要使用该功能，请在`inter_content` 传递国际短信的正文，并将验证码变量设置为 `@var(code)`<br /><u>*eg . your verify code is : @var(code)*</u> |
| `tag`                            | `string`                      | 可选      | 无   | 自定义标签功能，该标签可用作SUBHOOK追踪<br>（32 个字符以内，添加了 `tag` 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。`tag` 参数不参加加密计算） |

------

<br>

### **代码示例**

<br>

#### 发送一封测试短信

<br>

##### POST URL

```
https://api-v4.mysubmail.com/sms/unionsend.json
```

<br>

##### POST DATA

```
appid=your_app_id
&signature=your_app_key
&inter_appid=your_international_sms_appid
&inter_signature=your_international_sms_signature
&to=+86138xxxxxxxx
&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
&intersms_verify_code_transform=true
&inter_content=[SUBMAIL] your verify code is : @var(code)
```

<br>

##### 返回


```
{
    "status": "success",
    "send_id": "c2f0e679ad8dxxxxxf6cb71bf2925665e0",
    "fee": 1,
}
```

---

<br>

#### 使用 CURL 发送一封测试短信

<br>

##### 发送 CURL

```
curl -d '
appid=your_app_id&signature=your_app_key
&inter_appid=your_international_sms_appid
&inter_signature=your_international_sms_signature
&to=+852981xxxxxxx
&content=【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。
&intersms_verify_code_transform=true
&inter_content=[SUBMAIL] your verify code is : @var(code)
' https://api-v4.mysubmail.com/sms/unionsend.json
```

<br>

##### 返回

```
{
    "status": "success",
    "send_id": "c2f0e679ad8dxxxxxf6cb71bf2925665e0",
    "fee": 0.397
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
    "fee": 1
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

##### 参阅 [API 错误代码](