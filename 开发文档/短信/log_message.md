##  API: log/message(BETA)

<br>

### **概览**

<br>

`log/message` 是 SUBMAIL 的短信发送日志查询 API。

`log/message` API 可以方便的查询详细的短信发送日志和状态记录，不仅如此，`log/message` API 还可以按短信模板、手机号码、发送状态、开始/结束日期等条件筛选日志的返回结果。

---

<br>

### **URL**

<br>

##### <主> https://api.mysubmail.com/log/message

##### <备> https://api.submail.cn/log/message

---

<br>

### **支持格式**

<br>

格式 | URL
---|---
json |https://api.mysubmail.com/log/message.json **（默认）**
xml |https://api.mysubmail.com/log/message.xml

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

参阅 [API 授权和验证机制](gbibb3)

---

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的短信应用ID
recipient |string|可选|全部联系人|按接收者返回数据（默认返回全部联系人数据，要指定返回某个联系人的日志，请将该值设为 该联系人的11位手机号码）
project |string|可选|全部项目标记|按短信项目标识返回数据
result_status |string|可选|无|全部数据，按发送状态返回数据 delivered , dropped。
start_date|UNIX时间戳|可选|当日凌晨00:00:00|日志查询的开始时间（使用 UNIX 时间戳格式）
end_date |UNIX时间戳|可选|当日23:59:59|日志查询的结束时间（使用 UNIX 时间戳格式）
order_by |string|可选|desc|返回数据时执行的升序或降序（asc or desc）
rows |string|可选|50|单次返回数据的行数（请将该值控制在10-1000之间，若指定了一个无效的 rows 参数，API 将默认返回 50 行数据）
offset |string|可选|0|数据偏移指针
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com//chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com//chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://www.mysubmail.com//chs/documents/developer/gbibb3)  \>  授权和验证方式

<br>

###  **参数说明：**

<br>

```
project   默认返回全部项目数据，要指定短信项目标识返回某个项目（即短信模板）的日志，请将该值设为该模板的项目标识
result_status   默认返回全部数据，要指定所有发送成功的日志，请将该值设为 delivered ，要查询发送失败的数据，请将该指 dropped
start_date   默认值：当日的凌晨 如：2015-04-05 00:00:00 如需指定开始时间：2015-04-05 00:00:00 请将其转换为 UNIX 时间戳格式 例：2015-04-05 00:00:00 的UNIX时间戳 1428163200
end_date   默认值：当日的23:59:59 如：2015-04-05 23:59:59如需指定结束时间：2015-04-05 23:59:59 请将其转换为 UNIX 时间戳格式 例：2015-04-05 23:59:59 的UNIX时间戳 1428249599
order_by   若希望返回的数据按照发送时间升序排列，请将 order_by 参数设为 asc，反之则设为 desc
offset   该值可以指定返回数据的偏移指针，例：假如单次请求的开始至结束日期包含150条数据，rows参数采用默认的50行，此时需要查询第51-100行的数据，请将 offset 参数设为1(即数据偏移50行)即可得到第51-100行的数据，offset=2时，将返回第101-150行数据，以此类推


```



---
#### 使用 POST 方法获取日志


*   JSON


#### POST URL

```
http://api.mysubmail.com/log/message.json
```

#### POST Data

```
appid=your_app_id
&signature=your_app_key
```


#### `返回`


```
{
    "status":"success",
    "appid":"your_app_id",
    "count":2,
    "start_row":1,
    "end_row":2,
    "start_date":"2014-11-24 00:35:14",
    "end_date":"2015-04-02 16:00:00",
    "results":[
               {
               "sendID":"7ac69ff98e48c9b3b0f49afa5a0788c7",
               "project":"Gy1CR1",
               "recipient":"138xxxxxxxx",
               "message":"\u5982\u9700\u91cd\u7f6e\u60a8\u7684 SUBMAIL \u8d26\u6237\u5bc6\u7801\uff0c\u8bf7\u5728\u91cd\u7f6e\u9875\u9762\u8f93\u5165\u6b64\u9a8c\u8bc1\u7801\uff1a1425 \uff0c\u5e76\u8f93\u5165\u65b0\u7684\u5bc6\u7801\u3002",
               "signature":"\u3010SUBMAIL\u3011",
               "result_status":"delivered",
               "api":"message\/xsend",
               "send_date":"2015-01-19 15:21:27",
               "sent_date":"2015-01-19 15:21:27",
               "length":56,
               "credit":1
               },{
               "sendID":"e5c77f9a1c6728140c06824196eaa480",
               "project":"Gy1CR1",
               "recipient":"138xxxxxxxx",
               "message":"\u5982\u9700\u91cd\u7f6e\u60a8\u7684 SUBMAIL \u8d26\u6237\u5bc6\u7801\uff0c\u8bf7\u5728\u91cd\u7f6e\u9875\u9762\u8f93\u5165\u6b64\u9a8c\u8bc1\u7801\uff1a1325 \uff0c\u5e76\u8f93\u5165\u65b0\u7684\u5bc6\u7801\u3002",
               "signature":"\u3010SUBMAIL\u3011",
               "result_status":"sending",
               "api":"message\/xsend",
               "send_date":"2015-01-19 15:20:52",
               "sent_date":"2015-01-19 15:20:53",
               "length":56,
               "credit":1
               }
               ]
}

```
---
* XML

#### `POST URL`

```
http://api.mysubmail.com/log/message.xml
```


#### POST Data

```
appid=your_app_id&signature=your_app_key
```


#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status>success</status>
    <appid>your_app_id</appid>
    <count>2</count>
    <start_row>1</start_row>
    <end_row>2</end_row>
    <start_date>2014-11-24 00:35:14</start_date>
    <end_date>2015-04-02 16:00:00</end_date>
    <results>
        <result>
            <sendID>7ac69ff98e48c9b3b0f49afa5a0788c7</sendID>
            <project>Gy1CR1</project>
            <recipient>138xxxxxxxx</recipient>
            <message>如需重置您的 SUBMAIL 账户密码，请在重置页面输入此验证码：1425 ，并输入新的密码。</message>
            <signature>【SUBMAIL】</signature>
            <result_status>delivered</result_status>
            <api>message/xsend</api>
            <send_date>2015-01-19 15:21:27</send_date>
            <sent_date>2015-01-19 15:21:27</sent_date>
            <length>56</length>
            <credit>1</credit>
        </result>
        <result>
            <sendID>e5c77f9a1c6728140c06824196eaa480</sendID>
            <project>Gy1CR1</project>
            <recipient>138xxxxxxxx</recipient>
            <message>如需重置您的 SUBMAIL 账户密码，请在重置页面输入此验证码：1325 ，并输入新的密码。</message>
            <signature>【SUBMAIL】</signature>
            <result_status>sending</result_status>
            <api>message/xsend</api>
            <send_date>2015-01-19 15:20:52</send_date>
            <sent_date>2015-01-19 15:20:53</sent_date>
            <length>56</length>
            <credit>1</credit>
        </result>
    </results>
</xml>
```

---

#### 使用 `CURL`获取发送日志



*   JSON


#### `发送 CURL`


```
curl -d 'appid=your_message_appid&signature=your_message_key' https://api.mysubmail.com/log/message.json
```


#### `返回`


```
{
    "status":"success",
    "appid":"your_app_id",
    "count":2,
    "start_row":1,
    "end_row":2,
    "start_date":"2014-11-24 00:35:14",
    "end_date":"2015-04-02 16:00:00",
    "results":[
               {
               "sendID":"7ac69ff98e48c9b3b0f49afa5a0788c7",
               "project":"Gy1CR1",
               "recipient":"138xxxxxxxx",
               "message":"\u5982\u9700\u91cd\u7f6e\u60a8\u7684 SUBMAIL \u8d26\u6237\u5bc6\u7801\uff0c\u8bf7\u5728\u91cd\u7f6e\u9875\u9762\u8f93\u5165\u6b64\u9a8c\u8bc1\u7801\uff1a1425 \uff0c\u5e76\u8f93\u5165\u65b0\u7684\u5bc6\u7801\u3002",
               "signature":"\u3010SUBMAIL\u3011",
               "result_status":"delivered",
               "api":"message\/xsend",
               "send_date":"2015-01-19 15:21:27",
               "sent_date":"2015-01-19 15:21:27",
               "length":56,
               "credit":1
               },{
               "sendID":"e5c77f9a1c6728140c06824196eaa480",
               "project":"Gy1CR1",
               "recipient":"138xxxxxxxx",
               "message":"\u5982\u9700\u91cd\u7f6e\u60a8\u7684 SUBMAIL \u8d26\u6237\u5bc6\u7801\uff0c\u8bf7\u5728\u91cd\u7f6e\u9875\u9762\u8f93\u5165\u6b64\u9a8c\u8bc1\u7801\uff1a1325 \uff0c\u5e76\u8f93\u5165\u65b0\u7684\u5bc6\u7801\u3002",
               "signature":"\u3010SUBMAIL\u3011",
               "result_status":"sending",
               "api":"message\/xsend",
               "send_date":"2015-01-19 15:20:52",
               "sent_date":"2015-01-19 15:20:53",
               "length":56,
               "credit":1
               }
               ]
}
```
---
* XML
#### `发送 CURL`


```
curl -d 'appid=your_message_appid&signature=your_message_key' https://api.mysubmail.com/log/message.xml
```


####  `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status>success</status>
    <appid>your_app_id</appid>
    <count>2</count>
    <start_row>1</start_row>
    <end_row>2</end_row>
    <start_date>2014-11-24 00:35:14</start_date>
    <end_date>2015-04-02 16:00:00</end_date>
    <results>
        <result>
            <sendID>7ac69ff98e48c9b3b0f49afa5a0788c7</sendID>
            <project>Gy1CR1</project>
            <recipient>138xxxxxxxx</recipient>
            <message>如需重置您的 SUBMAIL 账户密码，请在重置页面输入此验证码：1425 ，并输入新的密码。</message>
            <signature>【SUBMAIL】</signature>
            <result_status>delivered</result_status>
            <api>message/xsend</api>
            <send_date>2015-01-19 15:21:27</send_date>
            <sent_date>2015-01-19 15:21:27</sent_date>
            <length>56</length>
            <credit>1</credit>
        </result>
        <result>
            <sendID>e5c77f9a1c6728140c06824196eaa480</sendID>
            <project>Gy1CR1</project>
            <recipient>138xxxxxxxx</recipient>
            <message>如需重置您的 SUBMAIL 账户密码，请在重置页面输入此验证码：1325 ，并输入新的密码。</message>
            <signature>【SUBMAIL】</signature>
            <result_status>sending</result_status>
            <api>message/xsend</api>
            <send_date>2015-01-19 15:20:52</send_date>
            <sent_date>2015-01-19 15:20:53</sent_date>
            <length>56</length>
            <credit>1</credit>
        </result>
    </results>
</xml>
```

---

<br>

### **返回码**

<br>

*   JSON

#### `请求成功`


```
{
    "status":"success"
}
```


#### `请求失败`


```
{
    "status":"error",
    "code":"1xx",
    "msg":"error message"
}
```

* XML

##### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status> success </status>
</xml>
```


#### `请求失败`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status> error </status>
    <code> 1xx </code>
    <msg> error message </msg>
</xml>
```

<br>

### **错误代码**

<br>

参阅 [API 错误代码](https://www.mysubmail.com/chs/documents/developer/c8ujr)