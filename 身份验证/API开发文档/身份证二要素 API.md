

# API: Factor/idcard - 身份证二要素 
<br />

### **概览**
`factor/idcard` 是 SUBMAIL 的简版身份验证 API，根据身份证号和姓名验证是否为本人。

------
 <br />

### **URL**

 <br />

`<主> http://tpa.mysubmail.com/factor/idcard`

`<备> https://tpa.mysubmail.com/factor/idcard`

------

 <br />

### **支持格式**

 <br />

| **格式** | **URL**                                                |
| -------- | ------------------------------------------------------ |
| `json`   | `https://tpa.mysubmail.com/factor/idcard.json`（默认） |
| `xml`    | `https://tpa.mysubmail.com/factor/idcard.xml`          |

------

 <br />

### **http 请求方式**

 <br />

| **请求方式** | content-type 设置                                            |
| ------------ | ------------------------------------------------------------ |
| `http post`  | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

------

 <br />

### **请求参数**

 <br />

| **参数**    | **类型** | **必需**/可选** | **默认** | **描述**                       |
| ----------- | -------- | --------------- | -------- | ------------------------------ |
| `appid`     | `string` | `必需`          | 无       | 三要素应用 appid，自控制台获取 |
| `timestamp` | `string` | `必需`          | 无       | 时间戳                         |
| `name`      | `string` | `必需`          | 无       | 待验证的身份证姓名             |
| `idNo`      | `string` | `必需`          | 无       | 待验证的身份证号码             |
| `signature` | `string` | `必需`          | 无       | sha256 数据加密校验证书        |

------

 <br />
### signature创建规则
 <br />
1.请将以下参数按照字段升序（A-Z）排列
   appkey、idNo 、name、timestamp

2.创建签名字符串 ：以"key=value"&nbsp;+&nbsp;"&amp;"（连接符）+&nbsp;"key=value"&nbsp;的方式连接所有参数

3.创建签名：拼接签名字符串示例string = "appkey=xxxx&amp;idNo =xxxxx&amp;name=张三&amp; timestamp=1614759954"，然后使用sha256(string)创建签名

注：中文需要使用urlencode处理后再参与创建签名

------
 <br />
###  **代码示例**

 <br />

#### 发送验证到

 <br />

##### POST

	`http://tpa.mysubmail.com/factor/idcard`



##### POST Data
```
appid=your_app_id
&amp; timestamp=1605521294832
&amp;name=张三
&amp;idNo=310000xxxxxxxxxxxx
&amp;signature=sha256加密后字符串
```
 <br />

##### 返回

```
{
'status': 'success',
'result': {'bank_msg': '核查一致',
		   'bank_idCard': '3300xxxxxxxxxxxx1234',
		   'bank_name': '张xx',
		   'bank_sex': '男',
		   'bank_area': '上海市',
		   'bank_birthday': '1996年01月11日',
		   'bank_status': '01'},
'send_id': '65b87f7bd907e4219f041af0abcdefgh'
}
status:接口请求状态 result:返回结果  bank_msg:结果说明  bank_msg:证件号码  bank_name:姓名  bank_sex:性别
bank_area:归属地  bank_birthday:出生年月  bank_status:结果状态码 01 通过 02 不通过   send_id:请求唯一标识
```

 <br />

##### 请求失败

```
{
'status': 'error',
 'code': '1204',
 'msg': 'Invalid signature'
 }

status:接口状态		code:错误代码		msg:错误信息
```

------

 <br />

### **错误代码**

 <br />

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/D5IFc4)



------