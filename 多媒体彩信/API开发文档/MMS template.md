## API: MMS/Template

 <br>

### **概览**

 <br>

`MMS/template` 是 SUBMAIL 的彩信模板 API。

使用 `MMS/template` 可以获取、创建、编辑或删除您的彩信模板。

 `MMS/template`API 使用 `HTTP` 规范中的 `GET`, `POST`, `PUT`, `DELETE` 方法对模板进行操作，使用 `GET` 方法获取单个或全部模板、`POST` 方法创建新的彩信模板并提交至 SUBMAIL 人工审核、`PUT` 方法更新或编辑一个彩信模板，或使用 `DELETE` 方法删除一个模板。

彩信模板引擎支持 `SUBHOOK` 异步推送状态，彩信模板在后台人工审核后，会使用 `SUBHOOK` 进行主动推送状态。

------

<br>

### **URL**

<br>

`<主> https://api-v4.mysubmail.com/mms/template`

------

<br>

### **支持格式**

<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/mms/template.json `**（默认）** |
| `xml`  | `https://api-v4.mysubmail.com/mms/template.xml`              |
| `yaml` | `https://api-v4.mysubmail.com/mms/template.yaml`             |

------

<br>

### **http 请求方式**

<br>

| `GET`    | `获取全部模板列表，或获取指定的单个模板`                |
| -------- | ------------------------------------------------------- |
| `POST`   | `创建一个新的彩信模板，并提交至 SUBMAIL 进行人工审核`   |
| `PUT`    | `编辑或更新一个彩信模板，并提交至 SUBMAIL 进行人工审核` |
| `DELETE` | `删除一个彩信模板`                                      |

------

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/P8IPN4)

------

<br>

### **MMS/template GET 方法（获取模板列表）请求参数**

<br>

| 参数          | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`       | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的彩信应用 ID                       |
| `template_id` | `string`    | 可选      | 无       | 模板ID（可选）<br>要获取单个模板，请将在此参数中提交该模板ID。为空则获取最新的1000个彩信模板 |
| `timestamp`   | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  `Timestamp` UNIX 时间戳 |
| `sign_type`   | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |
| `signature`   | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |

------
<br>

### **MMS/template POST 方法（创建模板）请求参数**

<br>

| 参数            | 类型             | 必需/可选 | 默认     | 描述                                                         |
| --------------- | ---------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`         | `string`         | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的彩信应用 ID                       |
| `mms_type`      | `mms` or `video` | 可选      | `mms`    | 模板类型：视频彩信请将该参数设置为 `video` ，普通图文彩信可忽略该参数 |
| `mms_title`     | `string`         | 可选      | 无       | 模板标题<br>*创建模板时可以在此参数中提交当前模板的标题，作为模板备注信息* |
| `mms_signature` | `string`         | `必需`    | 无       | 彩信模板签名<br>*请使用您的公司名或应用、APP、网站名作为您的彩信签名，请将彩信签名和彩信标题的字符总和控制在64个字符以内。* |
| `mms_subject`   | `string`         | `必需`    | 无       | 彩信模板主题<br>*彩信标题通常显示在彩信的顶部，请将彩信签名和彩信标题的字符总和控制在64个字符以内。* |
| `mms_content`   | `json`           | `必需`    | 无       | 彩信模板正文<br>*彩信正文为jsonArray类型，具体参数展示参考MMS_CONTEANT参数表，以及参数示列。* |
| `timestamp`     | UNIX 时间戳      | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  `Timestamp` UNIX 时间戳 |
| `sign_type`     | `string`         | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |
| `signature`     | `string`         | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |

------
<br>

### **MMS/template PUT 方法（更新模板）请求参数**

<br>

| 参数            | 类型             | 必需/可选 | 默认     | 描述                                                         |
| --------------- | ---------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`         | `string`         | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的彩信应用 ID                       |
| `template_id`   | `string`         | `必需`    | 无       | 需要更新的模板 ID<br>*在 SUBMAIL >MMS >项目中查看你所创建的短信项目标记。请参见 [获取项目 ID](https://www.mysubmail.com/documents/vqdNJ3)* |
| `mms_type`      | `mms` or `video` | 可选      | `mms`    | 模板类型：视频彩信请将该参数设置为 `video` ，普通图文彩信可忽略该参数 |
| `mms_title`     | `string`         | 可选      | 无       | 模板标题（可选）<br>*创建模板时可以在此参数中提交当前模板的标题，作为模板备注* |
| `mms_signature` | `string`         | `必需`    | 无       | 短信模板签名<br>*请使用您的公司名或应用、APP、网站名作为您的彩信签名，请将彩信签名和彩信标题的字符总和控制在64个字符以内。* |
| `mms_subject`   | `string`         | `必需`    | 无       | 彩信模板主题<br>*彩信标题通常显示在彩信的顶部，请将彩信签名和彩信标题的字符总和控制在64个字符以内。* |
| `mms_content`   | `json`           | `必需`    | 无       | 彩信模板正文<br>*彩信正文为jsonArray类型，具体参数展示参考MMS_CONTEANT参数表，以及参数示列。* |
| `timestamp`     | UNIX 时间戳      | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  `Timestamp` UNIX 时间戳 |
| `sign_type`     | `string`         | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |
| `signature`     | `string`         | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |

------
<br>

### **MMS/template DELETE 方法（删除模板）请求参数**

<br>

| 参数          | 类型        | 必需/可选 | 默认     | 描述                                                         |
| ------------- | ----------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`       | `string`    | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的彩信应用 ID                       |
| `template_id` | `string`    | `必需`    | 无       | 需要删除的模板 ID<br>*在 SUBMAIL >MMS >项目中查看你所创建的彩信项目标记。请参见 [获取项目 ID](https://www.mysubmail.com/documents/vqdNJ3)* |
| `timestamp`   | UNIX 时间戳 | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  `Timestamp` UNIX 时间戳 |
| `sign_type`   | `string`    | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |
| `signature`   | `string`    | `必需`    | 无       | 应用密匙 *或* 数字签名<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/P8IPN4) >  授权和验证方式 |

------
<br>

### **MMS_CONTENT参数**

<br>

| 参数         | 类型     | 必需/可选        | 默认 | 描述                                                         |
| ------------ | -------- | ---------------- | ---- | ------------------------------------------------------------ |
| `text`       | `string` | 可选             | 无   | 文字内容<br>jsonArray数组中text参数与媒体(image或者audio)文件参数不能同时为空。 |
| `image`      | `json`   | 可选             | 无   | 彩信图片<br>image参数为json类型还包含image.data ，image.type两个参数。具体数据格式参考代码示列。 |
| `image.data` | `base64` | `携带图片时必需` | 无   | 图片BASE64数据                                               |
| `image.type` | `string` | `携带图片时必需` | 无   | 图片类型<br> 支持类型 image/jpg, image/jpeg, image/png, image/gif |
| `audio`      | `json`   | 可选             | 无   | 音频文件<br>audio参数为json类型还包含audio.data ，audio.type两个参数。具体数据格式参考代码示列。 |
| `audio.data` | `base64` | `携带音频时必需` | 无   | 音频BASE64数据                                               |
| `audio.type` | `string` | `携带音频时必需` | 无   | 音频类型<br>支持类型 audio/mp3, audio/wav, audio/midi        |
| `video`      | `json`   | 可选             | 无   | 视频文件<br>video参数为json类型还包含video.data ，video.type两个参数。具体数据格式参考代码示列。 |
| `video.data` | `base64` | `携带视频时必需` | 无   | 视频BASE64数据                                               |
| `video.type` | `string` | `携带视频时必需` | 无   | 视频类型<br>支持类型 video/3gp, video/3gpp, video/mp4        |

<br>
**注意：**

1. `mms_content` 为json数组类型。
2. 彩信模板最大支持9页，`mms_content`参数中每一组数据为一页，并且依次排序。
3. 彩信模板每一页必须至少包含一种类型数据，媒体文件或者文字。
4. 单模板仅支持一种媒体类型，图片或音频，即图片+文字，或音频+文字，并将彩信标题+签名+媒体文件+正文文字的大小总和控制在 85KB 以内。
5. 媒体文件中的数据必须是 base64 编码，并通过 type 参数正确的说明文件类型。
6. 单个图片或音频文件的大小应控制在 85 KB以内。

------

<br>

### **MMS_CONTENT参数JSON数据示列**

<br>

##### 图片+文字

```
[
    {
        "image":{
            "data":"/9j/4QAYRXhpZgAASUkqAAgAAAAAAAAAAAAAAP/sABFEdWNr………………", 
            "type":"image/jpeg"
        },
        "text":"test-image"
    }
]
```
<br>
##### 视频+文字

```
[
    {
        "video":{
            "data":"/9j/4QAYRXhpZgAASUkqAAgBBBBBBBBBBP/sABFEdWNr………………",
            "type":"video/mp4"
        },
        "text":"test-video"
    }
]
```

<br>
##### 音频+文字

```
[
    {
        "audio":{
            "data":"/9j/4QAYRXhpZgAASUkqAAgBBBBBBBBBBP/sABFEdWNr………………",
            "type":"audio/wav"
        },
        "text":"test-audio"
    }
]
```

<br>
##### 图片+文字：多页

```
[
    {
        "image":{
            "data":"/9j/4QAYRXhpZgAASUkqAAgAAAAAAAAAAAAAAP/sABFEdWNr………………", 
            "type":"image/jpeg"
        },
        "text":"text1"
    },{
        "image":{
            "data":"/9j/4QAYRXhpZgAASUkqBBBBBBBBBBBBBBBBBBBP/sABFEdWNr………………", 
            "type":"image/jpeg"
        },
        "text":"text2"
    },{
        "image":{
            "data":"/9j/4QAYRXhpZgAASUkqAAgCCCCCCCCCCCCCCCP/sABFEdWNr………………", 
            "type":"image/jpeg"
        },
        "text":"text3"
    }
] 
```

------

 <br>

### **代码示例**

<br>

#### 使用 `CURL` GET方法获取模板列表 
<br>

##### 发送 CURL

```
curl -s "https://api-v4.mysubmail.com/mms/template.json?appid=your_appid&amp;signature=your_appkey&amp;template_id=FIJe14"
```

<br>
##### 返回


```
{
"status": "success",
"template": {
    "template_id": "FIJe14",
    "mms_title": "账户更改邮箱验证码",
    "mms_signature": "【SUBMAIL】",
    "mms_content": [
    {
        "image":{                           
                     "url":"https://xxxxxxxxxxx/xxxl32d5a1.png", 
                      "type":"image/png"
                      },
       "text":"您的验证码是1234."
    }
                             ]
    "mms_subject":"邮箱更改通知",
    "create_at": "2016-01-08 21:28:04",
    "edit_at": "2016-01-08 21:28:04",
    "template_status": "2",
    "template_status_description": "通过审核"
    }
}
```

---



<br>

#### 使用 `CURL` POST方法提交彩信模板 

<br>

##### 发送 CURL

```
curl -d 'appid=your_appid&amp;signature=your_appkey&amp;mms_title=POST方法测试&amp;mms_signature=【SUBMAIL】&amp;mms_subject=post标题提交测试&amp;mms_content=[
    {
        "image":{
                        "data":"/9j/4QAYRXhpZgAASUkqAAgAAAAAAAAAAAAAAP/sABFEdWNr…", 
                        "type":"image/jpeg"
                      },
       "text":"text1"
    },{
        "image":{
                        "data":"/9j/4QAYRXhpZgAASUkqAAgBBBBBBBBBBBBBBBAP/sABFEdWNr…", 
                        "type":"image/jpeg"
                      },
        "text":"text2"
    },{
        "image":{
                        "data":"/9j/4QAYRXhpZgAASUkqCCCCCCCCCCCCCCCCCC/sABFEdWNr…", 
                        "type":"image/jpeg"
                     },
       "text":"text3"
    }
]
 ' http://api-v4.mysubmail.com/mms/template.json
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

#### 使用 `CURL` PUT 方法修改短信模板


<br>


##### 发送 CURL

```
curl --data 'appid=your_appid&amp;signature=your_appkey&amp;mms_title=POST方法测试&amp;mms_signature=【SUBMAIL】&amp;mms_subject=post标题提交测试&amp;mms_content=[
    {
        "image":{
                        "data":"/9j/4QAYRXhpZgAASUkqAAgAAAAAAAAAAAAAAP/sABFEdWNr…", 
                        "type":"image/jpeg"
                      },
        "text":"text1"
    },{
        "image":{
                        "data":"/9j/4QAYRXhpZgAASUkqAAgABBBBBBBBBBBBAP/sABFEdWNr…", 
                        "type":"image/jpeg"
                       },
        "text":"text2"
    },{
        "image":{
                        "data":"/9j/4QAYRXhpZgAASUkqAAgCCCCCCCCCCCCP/sABFEdWNr…", 
                        "type":"image/jpeg"
                      },
       "text":"text3"
    }
]'
   http://api-v4.mysubmail.com/mms/template.json
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

#### 使用 `CURL` DELETE 方法删除短信模板

<br>

##### 发送 CURL

```
curl --data "appid=your_appid&amp;signature=your_appkey&amp;template_id=FsoAF3" -X delete http://api-v4.mysubmail.com/mms/template.json
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

| `template_status : 0` | `未提交审核` |
| --------------------- | ------------ |
| `template_status : 1` | `正在审核`   |
| `template_status : 2` | `审核通过`   |
| `template_status : 3` | `未通过审核` |

 

------

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

------

<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/fbaT14)

------
