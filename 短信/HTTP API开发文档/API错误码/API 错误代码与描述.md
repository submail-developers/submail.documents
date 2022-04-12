# API 错误代码与描述

<br>


| 错误代码 | 描述                                                         | Description                                                  |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 101      | 不正确的 APP ID                                              | Incorrect APP ID                                             |
| 102      | 此应用已被禁用，请至 submail > 应用集成 > 应用 页面开启此应用 | This APP has been disabled                                   |
| 103      | 未启用的开发者，此应用的开发者身份未验证，请更新您的开发者资料 | Developer is not available                                   |
| 104      | 此开发者未通过验证或此开发者资料发生更改。请至应用集成页面更新你的开发者资料 | Developer is not available, please update your developer identity |
| 105      | 此账户已过期                                                 | This account is expired                                      |
| 106      | 此账户已被禁用                                               | This account has been disabled                               |
| 107      | sign_type （验证模式）必须设置为 MD5（MD5签名模式）或 SHA1（SHA1签名模式）或 normal (密匙模式). | Invalid sign_type. The sign_type must be set as MD5 or SHA1 or normal |
| 108      | signature 参数无效                                           | Invalid signature                                            |
| 109      | appkey 无效                                                  | Invalid appkey                                               |
| 110      | sign_type 错误                                               | Invalid sign_type                                            |
| 111      | 空的 signature 参数                                          | Empty signature                                              |
| 112      | 应用的订阅与退订功能已禁用。                                 | This APP’s subscription system has been disabled             |
| 113      | 请求的 APPID 已设置 IP 白名单，您的 IP 不在此白名单范围      | APPID request has been set IP whitelist your IP is not in the scope of this white list |
| 114      | 该手机号码在账户黑名单中，已被屏蔽                           | This phone number has been blocked by account blocklist      |
| 115      | 该手机号码请求超限                                           | This phone number request frequency limit                    |
| 116      | 签名错误，该签名已被其他应用使用并已申请固定签名             | The SMS signature has been using other appid                 |
| 117      | 该模板已失效，短信模板签名与固定签名不一致或你的账户已取消固签，请联系 SUBMAIL 管理员 | The SMS templates error                                      |
| 118      | 该模板已失效，请联系SUBMAIL管理员                            | The SMS templates error                                      |
| 119      | 您不具备使用该API的权限，请联系SUBMAIL管理员                 | Permission Denied                                            |
| 120      | 模板已失效                                                   | The SMS templates error                                      |
| 151      | 错误的 UNIX 时间戳                                           | timestamp error                                              |
| 152      | 错误的 UNIX 时间戳，请将请求 UNIX 时间戳 至 发送 API 的过程控制在6秒以内 | Invalid timestamp                                            |
| 201      | 未知的 addressbook 模式                                      | Unkown address book model                                    |
| 202      | 错误的收件人地址                                             | Incorrect recipient email address                            |
| 203      | 错误的收件人地址。如果你正在使用 adressbook , 你所标记的地址薄不包含任何联系人。 | Incorrect recipient e-mail address! if you are using the addressbook model, this addressbook does not have any contacts |
| 251      | 错误的收件人地址（message）                                  | Incorrect recipient message address                          |
| 252      | 错误的收件人地址（message）如果你正在使用 adressbook 模式，你所标记的地址薄不包含任何联系人。 | Incorrect recipient message address, if you are using the addressbook model, this addressbook does not have any contacts |
| 253      | 此联系人已退订你的短信系统。                                 | This contact has unsubscribed your messaging system.         |
| 305      | 没有填写项目标记                                             | Project ID cannot be empty                                   |
| 306      | 无效的项目标记                                               | Invalid Project ID                                           |
| 307      | 错误的 json 格式。 请检查 vars 和 links 参数                 | Incorrect json format, please check vars and link parameters |
| 310      | tag参数长度不能超过32个字符。                                | The tag is limited to 32 characters                          |
| 401      | 短信签名不能为空。                                           | Message signature cannot be empty                            |
| 402      | 请将短信签名控制在40个字符以内。                             | Please limit message signature to 40 characters              |
| 403      | 短信正文不能为空                                             | Message content cannot be empty                              |
| 404      | 请将短信内容（加上签名）控制在1000个字符以内。               | Please limit message content and signature to 1000 characters |
| 405      | 依据当地法律法规，以下’$var’词或短语不能出现在短信中。       | According to local laws and regulations, the following '$var' word or phrase can not appear in a text message |
| 406      | 项目标记不能为空                                             | Project ID cannot be empty                                   |
| 407      | 无效的项目标记                                               | Invalid Project ID                                           |
| 408      | 你不能向此联系人或此地址簿中包含的联系人发送完全相同的短信。 | You cannot send same messages to this contact or the contact in the address book |
| 409      | 尝试发送的短信项目正在审核中，请稍候再试。                   | This SMS project is being reviewed, please try again later.  |
| 410      | multi 参数无效                                               | empty multi value                                            |
| 411      | 您必须为每条短信模板提交一个短信签名，且该签名必须使用全角大括号”【“和”】“包括起来，请将短信签名的字数控制在2至10字符以内（括号不计算字符数） | empty sms signature                                          |
| 412      | 请将短信签名的字数控制在10字符以内（括号不计算字符数）       | empty sms signature                                          |
| 413      | 请将短信签名的字数控制在2到10个字符之间（括号不计算字符数）  | empty sms signature                                          |
| 414      | 请提交短信正文                                               | empty sms content                                            |
| 415      | 请将短信正文的字数控制在1000个字符以内                       | Please limit sms content to 1000 characters                  |
| 416      | 请将短信标题的字数控制在64个字符以内                         | Please limit sms content to 64 characters                    |
| 417      | 请提交需要更新的模板ID                                       | Empty template Id                                            |
| 418      | 尝试更新的模板不存在                                         | Target template does not exist                               |
| 419      | 短信正文不能为空                                             | The sms content cannot be empty                              |
| 420      | 找不到可匹配的模板                                           | There is no template match                                   |
| 422      | 请控制您的模板长度在255个字符内。                            | Please limit message content and signature to 255 characters |
| 501      | 错误的目标地址簿标识                                         | Invalid target addresbook sign.                              |
| 901      | 你今日的发送配额已用尽。如需提高发送配额，请至 submail > 应用集成 >应用 页面开启更多发送配额 | Your quota has been filled for the day                       |
| 903      | 您的短信发送许可已用尽或您的余额不支持本次的请求数量。如需继续发送，请至 submail.cn > 商店 页面购买更多发送许可后重试。 | Your message account credit is not enough to support your sending request |
| 904      | 您的账户余额已用尽或您的余额不支持本次的请求数量。如需继续充值，请至 submail.cn > 商店 页面购买更多发送许可后重试。 | Your money account credit is not enough to support your charge request |
| 905      | 您的账户余额已用尽或您的余额不支持本次的请求数量。如需继续充值，请至 submail.cn > 商店 页面购买更多发送许可后重试。 | Your transactional sms credit is not enough to support your sending request |

---

**注：** 当 API  返回 307或者 309错误时，服务器会给出具体的 JSON decoding 错误原因。

```
json_decoding_error 参数将以数字形式标注错误代码

json_decoding_error:

1 = 到达了最大堆栈深度

2 = 无效或异常的 JSON

3 = 控制字符错误，可能是编码不对

4 = 语法错误

5 = 异常的 UTF-8 字符，也许是因为不正确的编码
```

------