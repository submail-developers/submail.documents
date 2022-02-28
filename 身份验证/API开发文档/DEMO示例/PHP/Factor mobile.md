# 二要素验证 手机号码
### API: Factor/mobile
### **概览**
	`factor/mobile` 是 SUBMAIL 的简版身份验证 API，根据手机号和姓名验证是否为本人。


 <br />

### **URL**

 <br />

`<主> http://tpa.mysubmail.com/factor/mobile`

`<备> https://tpa.mysubmail.com/factor/mobile`

------

 <br />

### **支持格式**

 <br />

| **格式** | **URL**                                                |
| -------- | ------------------------------------------------------ |
| `json`   | `https://tpa.mysubmail.com/factor/mobile.json`（默认） |
| `xml`    | `https://tpa.mysubmail.com/factor/mobile.xml`          |

------

 <br />

### **http 请求方式**

 <br />

| **请求方式**  | content-type 设置                                            |
| ------------- | ------------------------------------------------------------ |
| `http` `post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |



------

 <br />

### **请求参数**

 <br />

| **参数**    | **类型** | **必需/可选** | **默认** | **描述**                   |
| ----------- | -------- | ------------- | -------- | -------------------------- |
| `appid`     | `string` | `必需`        | 无       | 三要素 appid，自控制台获取 |
| `timestamp` | `string` | `必需`        | 无       | 时间戳                     |
| `name`      | `string` | `必需`        | 无       | 待验证的身份证姓名         |
| `mobile`    | `string` | `必需`        | 无       | 待验证的号码               |
| `signature` | `string` | `必需`        | 无       | sha256 加密校验数字证书    |

------

 <br />
### signature创建规则
1.请将以下参数按照字段升序（A-Z）排列
   appkey、mobile、name、timestamp

2.创建签名字符串 ：以"key=value"&nbsp;+&nbsp;"&amp;"（连接符）+&nbsp;"key=value"&nbsp;的方式连接所有参数

3.创建签名：拼接签名字符串示例string = "appkey=xxxx&amp;mobile=188xxxx&amp;name=张三&amp; timestamp=1602792765"，然后使用sha256(string)创建签名

注：中文需要使用urlencode处理后再参与创建签名
### **代码示例**

 <br />

#### 发送验证到

 <br />

##### POST

`http://tpa.mysubmailcom/factor/mobile`



##### POST Data
```
appid=your_app_id
&amp; timestamp=1602792765
&amp;name=张三
&amp;mobile=130xxxxxxxx
&amp;signature=sha256加密后字符串
```
 <br />

##### 返回

```
{

	"status":"success",

	"result":{ 
					'identical': True,
					'msg': '一致'
			},

	"send_id":"69639b23cbd2933746d87397bc379ab7"

}
status:接口请求状态	identical:认证结果，True一致/False不匹配  msg 认证结果描述  一致/不一致   	send_id:唯一的请求标识
```

 <br />

#####  请求失败

```
{

	"status": "error",

	"code": 1210,

	"msg": "Empty APP ID."

}
status:接口请求状态	code:错误代码	msg:错误信息
```

------

 <br />

### **错误代码**

 <br />

#####  参阅 [API 错误代码](https://www.mysubmail.com/documents/D5IFc4)



------