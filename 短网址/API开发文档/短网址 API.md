## API：ShortURL

<br>

### **概览**

<br>

`Shorturl`是 SUBMAIL 的短网址 API。

使用 Shorturl API 可以获取、创建、编辑或删除您的短网址。

`shorturl API` 使用 `HTTP` 规范中的 `GET`, `POST`, `PUT`, `DELETE` 方法对短网址进行操作，使用 `GET` 方法获取单个或全部短网址、`POST` 方法创建新的短网址并提交至 SUBMAIL 人工审核、`PUT` 方法更新或编辑一个短网址，或使用 `DELETE` 方法删除一个短网址。

短网址引擎支持 `SUBHOOK` 异步推送状态，短网址在后台人工审核后，会使用 `SUBHOOK` 进行主动推送状态。

---

<br>

### **URL**

<br>

##### `<主> https://service.mysubmail.com/shorturl`

---
<br>

### **支持格式**

<br>

| 格式   | URL                                                   |
| ------ | ----------------------------------------------------- |
| `json` | `https://service.mysubmail.com/shorturl.json`（默认） |
| `xml`  | `https://service.mysubmail.com/shorturl.xml`          |

---

<br>

### **http 请求方式**

<br>

| GET    | 获取全部短网址，或获取指定的单个短网址 |
| ------ | -------------------------------------- |
| POST   | 创建一个新的短网址                     |
| PUT    | 编辑或更新一个短网址                   |
| DELETE | 删除一个短网址                         |

---

<br>

### **是否需要授权**

<br>

##### **是**

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/ALdk5)

---

<br>

### **ShortURl GET 方法（获取短网址列表）请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址应用ID                      |
| `short_url` | `string`    | `必需`    | 无       | 短网址<br>*要获取单个模板，请将在此参数中提交您要查询的具体短网址。为空则获取所有的短网址。* |
| `rows`      | `int`       | 可选      | 100      | 单次返回数据的行数<br>*请将该值控制在10-1000之间，若指定了一个无效的 rows 参数，API 将默认返回 100行数据* |
| `offset`    | `int`       | 可选      | 0        | 数据偏移指针<br>*该值可以指定返回数据的偏移指针，例：假如单次请求包含150条数据，rows参数采用50行，此时需要查询第51-100行的数据，请将 offset 参数设为1(即数据偏移50行)即可得到第51-100行的数据，offset=2时，将返回第101-150行数据，以此类推* |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |



---

<br>

### **ShortURl POST 方法（创建短网址）请求参数**

<br>

| 参数              | 类型         | 必需/可选 | 默认      | 描述                                                         |
| ----------------- | ------------ | --------- | --------- | ------------------------------------------------------------ |
| `appid`           | `string`     | `必需`    | 无        | 在 SUBMAIL 应用集成中创建的短网址应用ID                      |
| `model `          | `string`     | 可选      | url       | 设置 URL 访问模式<br>*设置 URL 参数为 url-scheme 为 App 内链模式（或微信小程序）; 设置参数为 mp-wechat 为微信公众号模式，需授权 SUBMAIL 小程序 |
| `url `            | `string`     | `必需`    | 无        | 默认目标网址。<br>*您需要处理成短网址的长网址。*             |
| `group`           | `string`     | 可选      | 无        | 短网址群组ID                                                 |
| `item`            | `string`     | 可选      | 无        | 自定义标记。<br>*手机号码，国际手机号码，邮件地址，或任意字符串,此参数通常配合 短网址群组功能使用。（最大长度不能超过32位）* |
| `domain`          | string       | 可选      | link.wiki | 域名选择。<br>*SUBMAIL提供的域名选择：lin**k.wiki、suburl.cn、yc2.co、v2c.co、sw2.co*<br>*企业版支持自定义域名设置。* |
| `access_password` | `string`     | 可选      | 无        | 访问密码。                                                   |
| `access_limit`    | `int`        | 可选      | 无        | 访问次数限制。                                               |
| `expire`          | `int`        | 可选      | 无        | 设置短链接过期时间,按小时计算，默认过期时间为当前套餐的最大时长。 |
| `routes`          | `jsonString` | 可选      | 无        | 短网址路由。<br>*此参数支持对桌面端，移动端，app，机器人的路由跳转操作<br>具体参数示列请参考ShortUrl Routes参数说明* |
| `tag`             | `string`     | 可选      | 无        | 此参数用于标记一次 API 请求（最大长度不超过 64 位）<br>添加了 tag 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。 |
| `timestamp`       | UNIX 时间戳  | 可选      | 无        | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type`       | `string`     | 可选      | `normal`  | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature`       | `string`     | `必需`    | 无        | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |



---

<br>

### **ShortURl PUT 方法（更新短链接）请求参数**

<br>

| 参数              | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`           | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址的应用 ID                   |
| `short_url`       | `string`    | `必需`    | 无       | 目标短网址                                                   |
| `url`             | `string`    | 可选      | 无       | 目标网址                                                     |
| `pause`           | `string`    | 可选      | 无       | 短网址模板是否暂停使用。<br>参数为true或者false              |
| `item`            | `string`    | 可选      | 无       | 自定义标记。<br>手机号码，国际手机号码，邮件地址，或任意字符串,此参数通常配合 短网址群组功能使用。（最大长度不能超过32位） |
| `access_password` | `string`    | 可选      | 无       | 访问密码                                                     |
| `access_limit`    | `int`       | 可选      | 无       | 访问次数限制                                                 |
| `expire`          | `int`       | 可选      | 无       | 设置短网址过期时间,按小时计算，默认过期时间为当前套餐的最大时长。 |
| `tag`             | `string`    | 可选      | 无       | 此参数用于标记一次 API 请求（最大长度不超过 32 位）<br>添加了 tag 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。 |
| `timestamp`       | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type`       | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature`       | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |

---

<br>

### **ShortURL DELETE 方法（删除短网址）请求参数**

<br>

| 参数        | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ----------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`     | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短网址应用 ID                     |
| `short_url` | `string`    | `必需`    | 无       | 需要删除的目标短网址                                         |
| `timestamp` | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  `Timestamp` UNIX 时间戳 |
| `sign_type` | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |
| `signature` | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/ALdk5) >  授权和验证方式 |

---
<br>

### **ShortURL Routes参数说明**

<br>

#### routes参数json结构说明
> #### routes 
> > ##### desktop ：可选参数。设置桌面端操作系统点击跳转的目标url，如果此参数不传则跳转到默认设置目标url。
> > > ##### windows ：可选参数。设置windows操作系统点击跳转的目标url，如果此参数不传则跳转到默认设置目标url。
> > > ##### mac ：可选参数。设置mac操作系统点击跳转的目标url，如果此参数不传则跳转到默认设置目标url。
> > > ##### linux ：可选参数。设置linux操作系统点击跳转目标url，如果此参数不传则跳转到默认设置目标url。

>> ##### mobile:可选参数。设置移动端操作系统点击跳转目标url,如果此参数不传则跳转到默认设置目标url。
>> > ##### device:可选参数。如果此参数不传则跳转到默认设置目标url。
>> > > ##### ios:可选参数。设置ios操作系统点击跳转目标url，如果此参数不传则跳转到默认设置目标url。
>> > > ##### android:可选参数。设置android操作系统点击跳转目标url，如果此参数不传则跳转到默认设置目标url。
>> > > ##### others:可选参数。设置除ios，android操作系统外点击跳转目标url，如果此参数不传则跳转到默认设置目标url。

>>> ##### app:可选参数。设置微信以及支付宝点击跳转目标url，如果此参数不传则跳转到对应手机操作系统设置的目标跳转url。
>>> > ##### wechat:可选参数。设置微信app内点击跳转目标url，如果此参数不传则跳转到对应手机操作系统设置的目标跳转url。
>>> > ##### alipay:可选参数。设置支付宝app内点击跳转目标url，如果此参数不传则跳转到对应手机操作系统设置的目标跳转url。

>> ##### robot:可选参数。设置机器人点击跳转目标地址，如果此参数不传则跳转到默认设置目标url。

---
<br>

#### routes参数json字符串示列
```
{
        "desktop": {
            "windows": {"url":"https://www.mysubmail.com/windows","model":"url"},
            "mac": {"url":"https://www.mysubmail.com/mac","model":"url"},
            "linux": {"url":"https://www.mysubmail.com/linux","model":"url"},
	    "other": {"url":"https://www.mysubmail.com/other","model":"url"}
        },
        "mobile": {
            "device": {
                "ios": {"url":"weixin://dl/business/?ticket=***","model":"url-scheme"},
                "android": {"url":"https://www.mysubmail.com/android","model":"url"},
                "others": {"url":"https://www.mysubmail.com/others","model":"url"}
            },
            "app": {
                "wechat":{"url":"https://www.mysubmail.com/wechat","model":"url"},
                "alipay": {"url":"https://www.mysubmail.com/alipay","model":"url"},
                "others": {"url":"https://www.mysubmail.com/others","model":"url"}
            }
        },
        "robot": {"url":"https://www.mysubmail.com/robot","model":"url"}
    }
```

---
<br>

### **代码示例**

<br>

#### 使用 `CURL` GET方法获取模板列表

<br>
##### 发送 CURL 

```
curl -s "https://service.mysubmail.com/shorturl?appid=your_appid&amp;signature=your_appkey"
```

<br>
##### 返回


```
{
    "status": "success",
    "urls": [
        {
            "short_url": "http://link.wiki/anPi5G",
            "long_url": "http://mysubmail.cn/developer",
            "items": "",
            "access_password": "0",
            "access_limit": "0",
            "pause": "false",
            "routes": {
							"desktop": {
							"windows": {"url":"https://www.mysubmail.com/windows","model":"url"},
								"mac": {"url":"https://www.mysubmail.com/mac","model":"url"},
								"linux": {"url":"https://www.mysubmail.com/linux","model":"url"},
								"other": {"url":"https://www.mysubmail.com/other","model":"url"}
								},
								"mobile": {
										"device": {
												"ios": {"url":"weixin://dl/business/?ticket=***","model":"url-scheme"},
												"android": {"url":"https://www.mysubmail.com/android","model":"url"},
												"others": {"url":"https://www.mysubmail.com/others","model":"url"}
										},
										"app": {
												"wechat":{"url":"https://www.mysubmail.com/wechat","model":"url"},
												"alipay": {"url":"https://www.mysubmail.com/alipay","model":"url"},
												"others": {"url":"https://www.mysubmail.com/others","model":"url"}
										}
								},
								"robot": {"url":"https://www.mysubmail.com/robot","model":"url"}
						},
            "qrcode": "http://suburl.cn/qrcode?url=httxxxink.wiki/KSWfb5",
            "tag": "test2",
            "create_at": "2019-07-17 10:28:11",
            "review_status": "2",
            "review_status_description": "通过审核",
            "expire_by_hours": "168",
            "expire_at": "2019-07-24 10:28:11"
        },
        {
            "short_url": "http://sw2.co/bTOCOG",
            "long_url": "http://www.baidu.com",
            "items": "",
            "access_password": "0",
            "access_limit": "0",
            "pause": "false",
             "routes": {
              "desktop": {
                "windows": "https://www.mysubmail.com/windows",
                "mac": "https://www.mysubmail.com/mac",
                "linux": "https://www.mysubmail.com/linux"
                         },
              "mobile": {
                "device": {
                  "ios": "https://www.mysubmail.com/ios",
                  "android": "https://www.mysubmail.com/android",
                  "others": "https://www.mysubmail.com/others"
                        },
               "app": {
                 "wechat": "https://www.mysubmail.com/chs/store",
                 "alipay": "https://www.mysubmail.com/slinks"
                      }
                        },
              "robot": "https://www.mysubmail.com/robot"
                      },
            "qrcode": "http://suburl.cn/qrcode?url=httxxxink.wiki/KSWfb5",
            "tag": "",
            "create_at": "2019-07-17 09:57:47",
            "review_status": "2",
            "review_status_description": "通过审核",
            "expire_by_hours": "168",
            "expire_at": "2019-07-24 09:57:47"
        }
    ]
}
```



---



<br>

#### 使用 `CURL` POST方法提交短网址
<br>


##### 发送 CURL

```
curl -d "appid=your_appid&amp;signature=your_appkey&amp;url=https://www.api.submail.cn&amp;group=09ae645ddd5200915&amp;item=test&amp;routes={"desktop":{"windows":"https://www.mysubmail.com/windows","mac":"https://www.mysubmail.com/mac","linux":"https://www.mysubmail.com/linux"},"mobile":{"device":{"ios":"https://www.mysubmail.com/ios","android":"https://www.mysubmail.com/android","others":"https://www.mysubmail.com/others"},"app":{"wechat":"https://www.mysubmail.com/wechat","alipay":"https://www.mysubmail.com/alipay"}},"robot":"https://www.mysubmail.com/robot"}"。" https://service.mysubmail.com/shorturl.json
```

<br>
##### 返回


```
{
    "status": "success",
    "short_url": "http://link.wiki/KSWfb5",
    "long_url": "https://blog.csdn.net/fdipzone/article/details/42463727/32132131、321///23123/32132133213",
    "routes": {
        "desktop": {
            "windows": {"url":"https://www.mysubmail.com/windows","model":"url"},
            "mac": {"url":"https://www.mysubmail.com/mac","model":"url"},
            "linux": {"url":"https://www.mysubmail.com/linux","model":"url"},
						"other": {"url":"https://www.mysubmail.com/other","model":"url"}
        },
        "mobile": {
            "device": {
                "ios": {"url":"weixin://dl/business/?ticket=***","model":"url-scheme"},
                "android": {"url":"https://www.mysubmail.com/android","model":"url"},
                "others": {"url":"https://www.mysubmail.com/others","model":"url"}
            },
            "app": {
                "wechat":{"url":"https://www.mysubmail.com/wechat","model":"url"},
                "alipay": {"url":"https://www.mysubmail.com/alipay","model":"url"},
								"others": {"url":"https://www.mysubmail.com/others","model":"url"}
            }
        },
        "robot": {"url":"https://www.mysubmail.com/robot","model":"url"}
    },
    "qrcode": "http://suburl.cn/qrcode?url=httxxxink.wiki/KSWfb5",
    "expire_at": "2021-04-01 16:33:42"
}
```

**qrcode:为目标短网址生成的二维码地址。**



---



<br>

#### 使用 `CURL` PUT 方法修改短网址

<br>
##### 发送 CURL

```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;short_url=http://link.wiki/iM/GuvPeD&amp;url=https://www.mysubmail.com&amp;pause=true&amp;item=submail&amp;expire=100" -X put https://service.mysubmail.com/shorturl.json
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

#### 使用 `CURL` DELETE 方法删除短网址
<br>


##### 发送 CURL

```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;short_url=http://link.wiki/iM/GuvPeD" -X delete  https://service.mysubmail.com/shorturl.json
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

#### review_status 短网址状态描述

<br>

| `review_status : 0` | `未提交审核` |
| :------------------ | :----------- |
| `review_status : 1` | `正在审核`   |
| `review_status : 2` | `审核通过`   |
| `review_status : 3` | `未通过审核` |

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

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/LmoB14)

------
