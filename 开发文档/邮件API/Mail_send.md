## API: `Mail/send`

<br>

### **概览**

<br>

> `mail/send` 是 SUBMAIL 的邮件 API。 `mail/send` API 不仅提供强大的邮件发送功能, 并在 API 中集成了地址簿发送功能。你可以通过设定一些参数来确定 API 以哪种模式发送。 

`mail/send` API 可以使用变量动态的控制每封邮件的内容。 了解如何使用[文本变量](https://www.mysubmail.com/chs/documents/developer/oKraS3)和[超链接变量](https://www.mysubmail.com/chs/documents/developer/1kU7X1)。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/mail/send`

##### `<备> https://api.submail.cn/mail/send`

<br>

### **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/mail/send.json（默认）
xml |https://api.mysubmail.com/mail/send.xml

---

<br>

### **http 请求方式**

<br>

请求方式| content-type设置
---|---
http post  | multipart/form-data、x-www-form-urlencoded、application/json

---

<br>

### **是否需要授权**

<br>

##### **是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### **请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的邮件应用ID
to|string|可选|无|收件人地址 (`多个联系人用半角“,”隔开：  e.g. "leo <leo@submail.cn>, <retro@submail.cn>, service@submail.cn",SUBMAIL 支持完整的 RFC 822 收件人标准，请确保您的邮件地址的有效性。请参见 维基百科 `[EMAIL ADDRESS RFC822 文档](https://en.wikipedia.org/wiki/Email_address))
from|e-mail|必需|无|发件人地址 ，标准的发件人地址 e.g. leo@submail.cn
from_name|string|可选|无|发件人称呼，显示名称 e.g. Submail （50个字符以内）
reply|e-mail|可选|无|回复地址`(标准的回复邮件地址 e.g. leo@submail.cn)`
cc|string|可选|无|抄送地址 `(多个抄送地址请用 “ , ”_半角逗__号_区分，请将抄送联系人控制在 5 个以内)`。
bcc|string|可选|无|密送地址`(多个密送地址请用 “ ,”_半角逗__号_或区分，请将密送联系人控制在 5 个以内)`。
subject|string|必需|无|邮件标题（200个字符以内）
text|string|可选|无|纯文本邮件正文（5000个字符以内）
html|string|可选|无|HTML 邮件正文（60 KB以内）
vars|json string|可选|无|使用文本变量动态控制邮件中的文本，参阅 [了解如何创建和使用文本变量](https://www.mysubmail.com)
links|json string|可选|无|使用超链接变量动态控制邮件中的超链接，参阅 [了解如何创建和使用超链接变量](https://www.mysubmail.com/chs/documents/developer/1kU7X1)
attachments|文件|可选|无|附件（文件数量不超过10个，文件总大小应小于5 MB）
headers|json string|可选|无|自定义 EMAIL 头文件指令，headers 是一个标准的 JSON 字符串，headers 参数可以让开发者在 EMAIL 的标头部分插入自定义指令（500个字符以内）。如：` {"X-Accept-Language": "zh-cn", "X-Priority":"3","X-Mailer": "My Application"}`
asynchronous|string|可选|false|异步选项，该值设为 true 时启用异步发送模式
tag|string|可选|无|自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，text，html，vars，links，attachments参数不参与加密计算)
signature|string|必需|无|应用密匙 _或 _数字签名|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

```
Submail 保留 x-submail-smtp-api 指令，请务必不要在邮件标头中使用此指令

自定义的 EMAIL headers 指令通常以字母 X- 开头，请将此规范应用到你的指令

vars,  links 和 headers 参数要求严格的 JSON 格式，以下是将参数转换为 JSON 格式的注意事项

json 字符串必须以双引号包含
json 字符串必须是 utf8 编码
不能有多余的逗号 如：[1,2,]
json 字符串首尾必须被大括号{}包含 
 
PS:大多数的语言都有专属的JSON解析器（ ENCODING 和 DECODEING 方法）。如 PHP，首先将需要的变量以数组形式(如 $var[‘key’]=value) 创建后，使用 json_encode($var)方法创建 JSON 字符串；
```

---

### **代码示例**

#### 发送一封测试邮件

*   JSON

#### `POST URL`

https://api.mysubmail.com/mail/send.json

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>
&subject=testing_Subject
&text=testing_text_body
&from=no-reply@submail.cn
&signature=your_app_key
```


#### `返回：`


```
{
   "status":"success",
   "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---
* XML

#### `POST URL`

https://api.mysubmail.com/mail/send.xml

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>
&subject=testing_Subject
&text=testing_text_body
&from=no-reply@submail.cn
&signature=your_app_key
```


#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <return>
        <item>
            <send_id>mFGyz</send_id>
            <to>eg@eg.com</to>
        </item>
    </return>
</xml>
```

---

#### 发送一封测试邮件，多收件人


*   JSON

#### `POST URL`

https://api.mysubmail.com/mail/send.json

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>,retro@submail.cn
&subject=testing_Subject
&text=testing_text_body
&from=no-reply@submail.cn
&signature=your_app_key
```


#### `返回：`


```
{
    "status":"success",
    "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---
* XML

#### `POST URL`

https://api.mysubmail.com/mail/send.xml

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>,retro@submail.cn
&subject=testing_Subject
&text=testing_text_body
&from=no-reply@submail.cn
&signature=your_app_key
```


##### `返回`


```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <return>
        <item>
            <send_id>mFGyz</send_id>
            <to>eg@eg.com</to>
        </item>
    </return>
</xml>
```

---

#### 发送一封带附件的测试邮件


*   JSON

#### `POST URL`

https://api.mysubmail.com/mail/send.json

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>,retro@submail.cn
&subject=testing_Subject
&text=testing_text_body
&from=no-reply@submail.cn
&attachments[]=/path/to/file1.txt
&signature=your_app_key
```
---

#### `返回：`


```
{
    "status":"success",
    "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```
---
* XML

#### `POST URL`

https://api.mysubmail.com/mail/send.xml

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>,retro@submail.cn
&subject=testing_Subject
&text=testing_text_body
&from=no-reply@submail.cn
&attachments[]=/path/to/file1.txt
&signature=your_app_key
```


#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
    <return>
        <item>
            <send_id>mFGyz</send_id>
            <to>eg@eg.com</to>
        </item>
    </return>
</xml>
```

---

<br>

### **错误代码**

<br>

> 参阅 [API 错误代码](/chs/documents/developer/c8ujr)