# 如何获取微信小程序 URL Scheme 
<br>
## 在线生成小程序 URL Scheme
<br>
在[小程序管理后台](https://mp.weixin.qq.com "小程序管理后台")「工具」-「生成 URL Scheme」入口可以获取打开小程序任意页面的 URL Scheme。适用于从短信、邮件、微信外网页等场景打开小程序。

<br>
![](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/e77c3dc8bfeb9542fea880d180bf3698.png)
![](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/db0b9759e8943ea6cb69fdf40b09fe7d.png)



------

<br>

## auth.getAccessToken

<br>

> 本接口应在服务器端调用，详细说明参见微信官方文档 - [服务端API](https://developers.weixin.qq.com/miniprogram/dev/framework/server-ability/backend-api.html)。
>
> 文档来源：微信官方文档 - 小程序 - [auth.getAccessToken](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/access-token/auth.getAccessToken.html) 

<br>

获取小程序全局唯一后台接口调用凭据（`access_token`）。**调用绝大多数后台接口时都需使用 access_token，开发者需要进行妥善保存。**

<br>

### 请求地址

<br>

```text
GET https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&amp;appid=APPID&amp;secret=APPSECRET
```

<br>

### 请求参数

<br>

| 属性       | 类型   | 默认值 | 必填 | 说明                                                         |
| :--------- | :----- | :----- | :--- | :----------------------------------------------------------- |
| grant_type | string |        | 是   | 填写 client_credential                                       |
| appid      | string |        | 是   | 小程序唯一凭证，即 AppID，可在「[微信公众平台](https://mp.weixin.qq.com/) - 设置 - 开发设置」页中获得。（需要已经成为开发者，且帐号没有异常状态） |
| secret     | string |        | 是   | 小程序唯一凭证密钥，即 AppSecret，获取方式同 appid           |

<br>

### 返回值

<br>

#### Object

返回的 JSON 数据包

| 属性         | 类型   | 说明                                           |
| :----------- | :----- | :--------------------------------------------- |
| access_token | string | 获取到的凭证                                   |
| expires_in   | number | 凭证有效时间，单位：秒。目前是7200秒之内的值。 |
| errcode      | number | 错误码                                         |
| errmsg       | string | 错误信息                                       |

**errcode 的合法值**

| 值    | 说明                                                         | 最低版本 |
| :---- | :----------------------------------------------------------- | :------- |
| -1    | 系统繁忙，此时请开发者稍候再试                               |          |
| 0     | 请求成功                                                     |          |
| 40001 | AppSecret 错误或者 AppSecret 不属于这个小程序，请开发者确认 AppSecret 的正确性 |          |
| 40002 | 请确保 grant_type 字段值为 client_credential                 |          |
| 40013 | 不合法的 AppID，请开发者检查 AppID 的正确性，避免异常字符，注意大小写 |          |

<br>

#### 返回数据示例

正常返回

```json
{"access_token":"ACCESS_TOKEN","expires_in":7200}
```

错误时返回

```json
{"errcode":40013,"errmsg":"invalid appid"}
```

### <br>

------

<br>

## urlscheme.generate

<br>

> 本接口应在服务器端调用，详细说明参见微信官方文档 - [服务端API](https://developers.weixin.qq.com/miniprogram/dev/framework/server-ability/backend-api.html)。
>
> 文档来源：微信官方文档 - 小程序 - [urlscheme.generate](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/url-scheme/urlscheme.generate.html) 

> 本接口支持[云调用](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/guide/openapi/openapi.html)。需开发者工具版本 >= `1.02.1904090`（最新[稳定版下载](https://developers.weixin.qq.com/miniprogram/dev/devtools/stable.html)），`wx-server-sdk` >= `0.4.0`

<br>

获取小程序scheme码，适用于短信、邮件、外部网页等拉起小程序的业务场景。**通过该接口，可以选择生成到期失效和永久有效的小程序码**，目前仅针对国内非个人主体的小程序开放，详见[获取URL scheme码](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/url-scheme.html)。

调用方式：

- [HTTPS 调用](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/url-scheme/urlscheme.generate.html#method-http)
- [云调用](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/url-scheme/urlscheme.generate.html#method-cloud)

<br>

## HTTPS 调用

<br>

### 请求地址

<br>

```text
POST https://api.weixin.qq.com/wxa/generatescheme?access_token=ACCESS_TOKEN
```

<br>

### 请求参数

<br>

| 属性         | 类型    | 默认值 | 必填 | 说明                                                         |
| :----------- | :------ | :----- | :--- | :----------------------------------------------------------- |
| access_token | string  |        | 是   | [接口调用凭证](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/access-token/auth.getAccessToken.html) |
| jump_wxa     | Object  |        | 否   | 跳转到的目标小程序信息。                                     |
| is_expire    | boolean | false  | 否   | 生成的scheme码类型，到期失效：true，永久有效：false。        |
| expire_time  | number  |        | 否   | 到期失效的scheme码的失效时间，为Unix时间戳。生成的到期失效scheme码在该时间前有效。最长有效期为1年。生成到期失效的scheme时必填。 |

**jump_wxa 的结构**

| 属性  | 类型   | 默认值 | 必填 | 说明                                                         |
| :---- | :----- | :----- | :--- | :----------------------------------------------------------- |
| path  | string |        | 是   | 通过scheme码进入的小程序页面路径，必须是已经发布的小程序存在的页面，不可携带query。path为空时会跳转小程序主页。 |
| query | string |        | 是   | 通过scheme码进入小程序时的query，最大128个字符，只支持数字，大小写英文以及部分特殊字符：!#$&amp;'()*+,/:;=?@-._~ |

<br>

### 返回值

<br>

#### openlink

生成的小程序scheme码

<br>

### 异常返回

<br>

#### Object

JSON

| 属性    | 类型   | 说明     |
| :------ | :----- | :------- |
| errcode | number | 错误码   |
| errmsg  | string | 错误信息 |

**errcode 的合法值**

| 值    | 说明                                                | 最低版本 |
| :---- | :-------------------------------------------------- | :------- |
| 40002 | 暂无生成权限                                        |          |
| 40013 | 生成权限被封禁                                      |          |
| 85079 | 小程序未发布                                        |          |
| 40165 | 参数path填写错误                                    |          |
| 40212 | 参数query填写错误                                   |          |
| 85401 | 参数expire_time填写错误，时间间隔大于1分钟且小于1年 |          |
| 44990 | 生成Scheme频率过快（超过100次/秒）                  |          |
| 85400 | 长期有效Scheme达到生成上限10万                      |          |
| 45009 | 单天生成Scheme数量超过上限50万                      |          |

<br>

#### 返回值说明

如果调用成功，会直接返回生成的小程序scheme码。如果请求失败，会返回 JSON 格式的数据。

<br>

#### 示例

请求

```json
{
    "jump_wxa":
    {
        "path": "/pages/publishHomework/publishHomework",
        "query": ""
	    },
    "is_expire":true,
    "expire_time":1606737600
}
```

返回

```text
{
 "errcode": 0,
 "errmsg": "ok",
 "openlink": Scheme,
}
```

<br>

## 云调用

<br>

> [云调用](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/guide/openapi/openapi.html)是小程序·云开发提供的在云函数中调用微信开放接口的能力，需要在云函数中通过 `wx-server-sdk` 使用。

<br>

### 接口方法

<br>

```js
openapi.urlscheme.generate
```

> 需在 `config.json` 中配置 `urlscheme.generate` API 的权限，[详情](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/guide/openapi/openapi.html#usage-3)

<br>

### 请求参数

<br>

| 属性       | 类型    | 默认值 | 必填 | 说明                                                         |
| :--------- | :------ | :----- | :--- | :----------------------------------------------------------- |
| jumpWxa    | Object  |        | 否   | 跳转到的目标小程序信息。                                     |
| isExpire   | boolean | false  | 否   | 生成的scheme码类型，到期失效：true，永久有效：false。        |
| expireTime | number  |        | 否   | 到期失效的scheme码的失效时间，为Unix时间戳。生成的到期失效scheme码在该时间前有效。最长有效期为1年。生成到期失效的scheme时必填。 |

**jumpWxa 的结构**

| 属性  | 类型   | 默认值 | 必填 | 说明                                                         |
| :---- | :----- | :----- | :--- | :----------------------------------------------------------- |
| path  | string |        | 是   | 通过scheme码进入的小程序页面路径，必须是已经发布的小程序存在的页面，不可携带query。path为空时会跳转小程序主页。 |
| query | string |        | 是   | 通过scheme码进入小程序时的query，最大128个字符，只支持数字，大小写英文以及部分特殊字符：!#$&amp;'()*+,/:;=?@-._~ |

<br>

### 返回值

<br>

#### openlink

生成的小程序scheme码

<br>

### 异常

<br>

#### Object

JSON

| 属性    | 类型   | 说明     |
| :------ | :----- | :------- |
| errCode | number | 错误码   |
| errMsg  | string | 错误信息 |

**errCode 的合法值**

| 值   | 说明 | 最低版本 |
| :--- | :--- | :------- |
|      |      |          |

<br>

### 示例

<br>

请求

```js
const cloud = require('wx-server-sdk')
cloud.init({
  env: cloud.DYNAMIC_CURRENT_ENV,
})
exports.main = async (event, context) => {
  try {
    const result = await cloud.openapi.urlscheme.generate({
        jumpWxa: {
          path: '/pages/publishHomework/publishHomework',
          query: ''
        },
        isExpire: true,
        expireTime: 1606737600
      })
    return result
  } catch (err) {
    return err
  }
}
```

返回

```text
{
 "errcode": 0,
 "errmsg": "ok",
 "openlink": Scheme,
}
```

------