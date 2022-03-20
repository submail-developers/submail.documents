# SUBMAIl SMPP 协议接入文档

SUBMAIL SMPP 协议基于 SMPP 3.4 通讯协议。 
参考开发文档：《**Short Message Peer to Peer Protocol Specification v3.4**》 《**CDMA 数字蜂窝移动通信网扩展短消息实体到短消息中心 的接口协议规范 SMPP v3.4** 》



基于 SMPP 通讯协议，接入 SUBMAIL SMPP 可实现短消息发送、状态接收等功能；要接入SUBMAIL SMPP 网关，请前往 国际短信-》创建/管理 APPID 页面创建一个 SMPP 应用；



## 参数示例：

| SMPP参数       | 示例               | 描述                                                         |
| -------------- | ------------------ | ------------------------------------------------------------ |
| IP/URL         | smpp.mysubmail.com | 接口URL，如果您的系统仅支持 IP 对接或无法使用域名，请联系商务或售后支持 |
| Port           | 9000               | SMPP 端口号                                                  |
| User/System ID | appid              | 用户名 / System ID；前往 国际短信-》创建/管理 APPID 页面获取 |
| Passwrod       | smpp key           | 密码；前往  国际短信-》创建/管理 APPID 页面获取              |

请注意：

1. 每个独立的 SMPP 应用默认为 2 个TCP链路，支持 BIND_TRANSMITTER（TX）、BIND_RECEIVER (RX)，和 BIND_TRANSCEIVER（TRX）类型的连接，初始流速默认为 100/秒；
2. SMPP 要求必须指定一个 授权的 IP 进行绑定；您可以绑定多个 IP;
3. 当链路已成功登录并已占用超过最大链路限制后，其他链路将无法继续使用该 APPID 进行登录；
4. SMPP 短消息正文编码支持 GSM 7 和 UCS 2编码；
5. SMPP 支持自定义 Sender （仅支持部分国家）



#### SUBMAIL SMPP 网关支持常用 SMPP 指令

## SMPP 指令支持列表：

| 指令             | 指令描述                    |
| ---------------- | --------------------------- |
| BIND_TRANSMITTER | 发送器 TX 连接/登录         |
| BIND_RECEIVER    | 接收器 RX 连接/登录         |
| BIND_TRANSCEIVER | 收发器 TRX 连接/登录        |
| UNBIND           | 链路拆除                    |
| GENERIC_NACK     | *generic_nack* 无效指令应答 |
| SUBMIT_SM        | 短消息发送                  |
| DELIVER_SM       | 短消息发送状态获取          |
| ENQUIRE_LINK     | 链路检测（心跳包）          |

除上述列表中的指令外，其他 SMPP 指令均不被支持；如遇特殊需求，请联系商务或售后支持；



## 关于长短信

SUBMAIl SMPP 网关支持长短信发送，支持 UDHI 模式和 **message_payload** 模式，最大字符限制为1000 字，包含签名，正文、标点符号和空格；SMPP 短信长度与短信正文编码相关 **gsm7** 编码通常普通短信支持 140 ~ 160字，长短信为 134 ~ 154字；**UCS 2**编码普通的短信长度为 70 字，长短信为 67 字；全球许多国家或地区的短信长度规范不统一，详情请联系 SUBMAIL 商务和售后部门；

##### UDHI 模式

要使用 **UDHI** 模式发送长短信，请正确的设置 **esm_class** 参数 和 正文的 **UDHI** 头；

正文头采用 6 字节 **UDHI**，格式：05 00 03 XX MM NN

- byte 1 : 05, 表示剩余协议头的长度
- byte 2 : 00, 这个值在 GSM 03.40 规范 9.2.3.24.1中规定，表示随后的这批超长短信的标识位长度为 1（格式中的 XX 值）
- byte 3 : 03, 这个值表示剩下短信标识的长度
- byte 4 : XX，这批短信的唯一标志(被拆分的多条短信,此值必需一致)，事实上，SME(手机或者SP)把消息合并完之后，就重新记录，所以这个标志是否唯 一并不是很 重要。
- byte 5 : MM, 这批短信的数量。如果一个超长短信总共 5 条，这里的值就是 5。
- byte 6 : NN, 当前短信的序号。如果当前短信是这批短信中的第一条的值是 1，第二条的值是 2。

示例：05 00 03 39 02 01

请注意：GSM7 编码中有部分字符占用 2 个字节，如括号 “[” 和 “]”，如果您的短信正文中包含 2 字节的字符时，应限制每条短信的最大长度-1；例：普通短信 160 字，减去 6 字节 UDHI 头 减1 ，既153字符 （160-6-1=153）



##### message_payload 模式

要使用 **message_payload**（TLV） 模式, **sms_lenth** 必须设置为 0，将全部的短消息正文设置在 **message_payload** 参数中发送

**message_payload** 最大支持 1000 字



## 错误/状态码

SUBMAIL SMPP 网关除透传短消息实际状态外会有一些特殊的状态码，如模板审核拒绝、频率超限、余额不足等

| 状态码  | 交互方式   | 描述                                                         |
| ------- | ---------- | ------------------------------------------------------------ |
| SUBERRL | DELIVER_SM | 提交失败（长短信并包超时）                                   |
| NONECHN | DELIVER_SM | 不支持的国家或地区                                           |
| OVERRUN | DELIVER_SM | 短信正文超过最大长度限制（1000字）                           |
| RGBLOCK | DELIVER_SM | 用户屏蔽区                                                   |
| BEYONDD | DELIVER_SM | SMPP应用请求超限（请前往 国际短信-》创建/管理 APPID 页面设置发送限制参数） |
| FRQEBYD | DELIVER_SM | 发送超限（相同内容同一天内对同一手机号发送超过15条）         |
| UBLOCKD | DELIVER_SM | 自定义黑名单 （请前往短信-》创建/管理 APPID 页面设置或管理黑名单） |
| REJECTD | DELIVER_SM | 审核拒绝<br />此状态与网关REJECTD状态码一致，如遇相同内容全部返回该错误码，则模板审核被拒，请前往 短信-》创建 /管理模板页面查看具体驳回原因，修改后重新提交该模板进行审核即可正常发送 |
| BALANCE | DELIVER_SM | 余额不足                                                     |
| BLOCKED | DELIVER_SM | 系统屏蔽                                                     |
| BEYONDT | DELIVER_SM | 模板发送超限；请前往 国际短信-》创建 /管理模板页面 更改此模板发送限制 |

