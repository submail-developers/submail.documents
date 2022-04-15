# API: Factor/detail - 详版运营商三要素
<br />
### **概览**
<br />
	`factor/detail` 是 SUBMAIL 的详版身份验证 API，可以根据身份证、手机号和姓名获取到验证信息和手机运营商信息。
<br />

------

<br />

### **URL**

<br />

`<主> http://tpa.mysubmail.com/factor/detail`

------



<br />

### **支持格式**

<br />

| **格式** | **URL**                                                |
| -------- | ------------------------------------------------------ |
| `json`   | `https://tpa.mysubmail.com/factor/detail.json`（默认） |
| `xml`    | `https://tpa.mysubmail.com/factor/detail.xml`          |

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

| 参数        | 类型     | 必需/可选 | 默认 | 描述                      |
| ----------- | -------- | --------- | ---- | ------------------------- |
| `appid`     | `string` | `必需`    | 无   | 三要素appid，自控制台获取 |
| `timestamp` | `string` | `必需`    | 无   | 时间戳                    |
| `name`      | `string` | `必需`    | 无   | 待验证的身份证姓名        |
| `idNo`      | `string` | `必需`    | 无   | 待验证的身份证号码        |
| `mobile`    | `string` | `必需`    | 无   | 待验证的号码              |
| `signature` | `string` | `必需`    | 无   | `sha256`加密校验数字证书  |

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

` http://tpa.mysubmail.com/factor/detail`	

##### POST Data
```
appid=your_app_id
&amp; timestamp =1605521294832
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

         "provider": -2,

         "data": "1"

       },

	"send_id": "4cf22ecb12342a5442df58c829a86690"

}
status:接口请求状态
send_id:唯一的请求标识
data:认证结果 
    1:三要素一致 
	2:手机号已实名，但是身份证和姓名均与实名信息不一致 
	3:手机号已实名，手机号和证件号一致，姓名不一致 
	4:手机号已实名，手机号和姓名一致，身份证不一致
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


	参阅 [API 错误代码](https://www.mysubmail.com/documents/D5IFc4)



------