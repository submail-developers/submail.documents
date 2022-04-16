# SUBMAIL API V4 更新文档

<br>

### 概览

<br>

SUBMAIL API V4 是基于 API V3 的重构，大幅提高了系统稳定性和运行效率；

新版 API 提供更多丰富的产品接口功能，优化工作流，API 响应更迅捷，新版接口向下兼容（详情请参阅新功能与接口变动-兼容性变动），业务层 100% 兼容旧版 API；

------

<br>

### 本次更新涉及产品

<br>

短信、国际短信、多媒体彩信（视频/图文）、语音、邮件、地址簿

------

<br>

### 如何升级？

<br>

| URL  | https://api-v4.mysubmail.com |
| ---- | ---------------------------- |

从 V3 API 升级至新版 API，请将原接口域名 `api.mysubmail.com` 更换为 `api-v4.mysubmail.com` 即可完成接口升级（仅短信、国际短信、多媒体彩信（视频/图文）、语音、邮件、地址簿 等产品）；

旧版接口 `https://api.mysubmail.com/message/send`  > 升级新版接口  `https://api-v4.mysubmail.com/message/send`

新版接口同时支持 `http` 和 `https` 

------

<br>

### 新特性

<br>

新增 `yaml` 返回码格式；

新版本在原有的 `xml` 和 `json` 返回码的基础上增加了`yaml` 格式返回码，要使用 `yaml` 返回码，请在 API 接口的结尾使用 `.yaml` 后缀; 例：`https://api-v4.mysubmail.com/service/timestamp.yaml`

新增 SHA256 数字签名模式

------

<br>

## 新功能与接口变动

<br>

### 短信

<br>

##### 新增接口

- 增加 REPORT 离线分析报告接口  `sms/reports` （[查看开发文档](https://www.mysubmail.com/documents/Hvmb02)）
- 增加群发接口 `sms/batchsend` （[查看开发文档](https://www.mysubmail.com/documents/AzD4Z4)）与 `sms/batchxsend`（[查看开发文档](https://www.mysubmail.com/documents/G5KBR)）
- 增加定时任务接口 `sms/timedtask` （[查看开发文档](https://www.mysubmail.com/documents/AzD4Z4)）
- 新版日志接口 `sms/log` （[查看开发文档](https://www.mysubmail.com/documents/onhvw)）
- `sms/send`（[查看开发文档](https://www.mysubmail.com/documents/FppOR3)） 和 `sms/xsend` （[查看开发文档](https://www.mysubmail.com/documents/OOVyh)） 单发接口支持 GET 方式提交数据

<br>

##### 兼容性变动

- 移除了短信发送接口返回码中的 `sms_credits`  和 `transactional_sms_credits` 短信余额参数；要获取当前余额请使用 `sms/balance` 接口获取
- 模板 API `template/get` 中 `add_date` 和 `edit_date` 现在使用时间戳返回

<br>

##### 新增 CMPP 协议支持

开放 CMPP 协议接入，SUBMAIL CMPP 协议基于中国移动短消息 CMPP 2 通讯协议（ [CMPP 接入文档](https://www.mysubmail.com/documents/qoRzr1)）

------

<br>

### 国际短信

<br>

##### 兼容性变动

- 移除了国际短信发送接口返回码中的 `account_balance`  余额参数；要获取当前余额请使用 `internationalsms/balance` 接口获取
- 模板 API `template/get` 中 `add_date` 和 `edit_date` 现在使用时间戳返回

<br>

##### 新增 SMPP 协议支持

开放 SMPP 协议接入 ，支持 SMPP 3.4 通讯协议（[查看 SMPP 接入文档](https://www.mysubmail.com/documents/mJ0Su1)）

------

<br>

### 多媒体彩信

<br>

##### 兼容性变动

- 移除了彩信发送接口返回码中的 `money_account`  余额参数；要获取当前余额请使用 `mms/balance` 接口获取
- 模板 API `template/get` 中 `add_date` 和 `edit_date` 现在使用时间戳返回

------

<br>



### 语音

<br>

##### 兼容性变动

- 移除了语音呼叫接口返回码中的 `money_account`  余额参数；要获取当前余额请使用 `voice/balance` 接口获取
- 模板 API `template/get` 中 `add_date` 和 `edit_date` 现在使用时间戳返回

------

