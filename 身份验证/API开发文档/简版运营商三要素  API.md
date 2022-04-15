# API: Factor/simple - 简版运营商三要素
<br />
### **概览**
<br />
	`factor/simple` 是 SUBMAIL 的简版身份验证 API，根据身份证、手机号和姓名验证是否为本人。

------

<br />

### **URL**

<br />

` <主> http://tpa.mysubmail.com/factor/simple`

`<备> https://tpa.mysubmail.com/factor/simple`

------

<br />

### **支持格式**

<br />

| 格式   | URL                                                    |
| ------ | ------------------------------------------------------ |
| `json` | `https://tpa.mysubmail.com/factor/simple.json`（默认） |
| `xml`  | `https://tpa.mysubmail.com/factor/simple.xml`          |

------



<br />

### **http 请求方式**

<br />

| 请求方式    | content-type 设置                                            |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

------

<br />

### **请求参数**

<br />

| 参数        | 类型     | 必需/可选 | 默认 | 描述                       |
| ----------- | -------- | --------- | ---- | -------------------------- |
| `appid`     | `string` | `必需`    | 无   | 三要素 appid，自控制台获取 |
| `timestamp` | `string` | `必需`    | 无   | 时间戳                     |
| `name`      | `string` | `必需`    | 无   | 待验证的身份证姓名         |
| `idNo`      | `string` | `必需`    | 无   | 待验证的身份证号码         |
| `mobile`    | `string` | `必需`    | 无   | 待验证的号码               |
| `signature` | `string` | `必需`    | 无   | `sha256`加密校验数字证书   |

------

 <br />
### signature创建规则
<br />
1.请将以下参数按照字段升序（A-Z）排列
   appkey、idNo 、mobile、name、timestamp

2.创建签名字符串 ：以"key=value"&nbsp;+&nbsp;"&amp;"（连接符）+&nbsp;"key=value"&nbsp;的方式连接所有参数

3.创建签名：拼接签名字符串示例string = "appkey=xxxx&amp;idNo=xxxx&amp;mobile=188xxxx&amp;name=张三&amp; timestamp=1614759954"，然后使用sha256(string)创建签名

注：中文需要使用urlencode处理后再参与创建签名
------
<br />
### **代码示例**

<br />

#### 发送验证到

<br />

##### POST

` http://tpa.mysubmail.com/factor/simple`



##### POST Data
```
appid=your_app_id
&amp; timestamp=1605521294832
&amp;name=张三
&amp;idNo=310000xxxxxxxxxxxx
&amp;mobile=130xxxxxxxx
&amp;signature=sha256加密后字符串
```
<br />

##### 返回

```
{

	"status": "success",

	"result": {

       "provider": 2,

       "identical": "true"

 	},

	"send_id": "4cf22ecb12342a5442df58c829a86690"

}
status:接口请求状态		identical:认证结果，true匹配/false不匹配		send_id:唯一的请求标识
provider:运营商 1:移动 2:电信 3:联通 携号转网的返回对应的运营商 -1:移动 -2:电信 -3:联通
```

<br />

##### 请求失败

```
{

	"status": "error",

	"code": 1210,

	"msg": "Empty APP ID."

}
status:接口请求状态		code:错误代码		msg:错误信息
```



------

 

 <br />

### **错误代码**

<br />


##### 	参阅 [API 错误代码](https://www.mysubmail.com/documents/D5IFc4)



------