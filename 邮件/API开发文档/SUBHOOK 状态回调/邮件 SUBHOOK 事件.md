## 邮件 SUBHOOK 事件

<br>

### **请求 request**

<br>


| `events`    | `request`                                                    |
| ----------- | ------------------------------------------------------------ |
| `email`     | 此联系人的邮件地址                                           |
| `app`       | 应用 ID                                                      |
| `send_id`   | 发送ID（唯一标示）                                           |
| `tag`       | 自定义标签                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"request",  
"email":"leo@submail.cn",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **邮件发送已发送成功 delivered**

<br>

| `events`     | `delivered`                                                  |
| ------------ | ------------------------------------------------------------ |
| `email`      | 此联系人的邮件地址                                           |
| `message_id` | SMTP ID                                                      |
| `app`        | 应用 ID                                                      |
| `send_id`    | 发送ID（唯一标示）                                           |
| `tag`        | 自定义标签                                                   |
| `timestamp`  | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`      | 32 位随机字符串                                              |
| `signature`  | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"delivered",
"email":"leo@submail.cn",
"message_id":"<6b472f5f207f7777ce59c9e1fe9884ab>",
"app":10034,
"send_id":"oiidJ3",
"tag":"testtag",
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

<br>

### **邮件发送失败或丢失 dropped**

<br>

| `events`    | `dropped`                                                    |
| ----------- | ------------------------------------------------------------ |
| `email`     | 此联系人的邮件地址                                           |
| `reason`    | 发送失败的原因                                               |
| `app`       | 应用 ID                                                      |
| `send_id`   | 发送ID（唯一标示）                                           |
| `tag`       | 自定义标签                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"dropped",
"email":"leo@submail.cn",
"app":10034,
"reason":"421-Connection dropped xxxxx",
"send_id":"oiidJ3",
"tag":"testtag",
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

<br>

### **回弹 bounced**

<br>

| `events`     | `bounced`                                                    |
| ------------ | ------------------------------------------------------------ |
| `email`      | 此联系人的邮件地址                                           |
| `message_id` | SMTP ID                                                      |
| `reason`     | 发送失败的原因                                               |
| `app`        | 应用 ID                                                      |
| `send_id`    | 发送ID（唯一标示）                                           |
| `tag`        | 自定义标签                                                   |
| `timestamp`  | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`      | 32 位随机字符串                                              |
| `signature`  | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"bounced",
"email":"leo@submail.cn",
"message_id":"<6b472f5f207f7777ce59c9e1fe9884ab>",
"app":10034,
"reason":"550 Mail is rejected by xxxxx",
"send_id":"oiidJ3",
"tag":"testtag",
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

 <br>

### **阅读 opened**

<br>

| `events`       | `opened`                                                     |
| -------------- | ------------------------------------------------------------ |
| `email`        | 此联系人的邮件地址                                           |
| `app`          | 应用 ID                                                      |
| `send_id`      | 发送ID（唯一标示）                                           |
| `tag`          | 自定义标签                                                   |
| `ip`           | 联系人 IP 地址                                               |
| `agent`        | 浏览器                                                       |
| `platform`     | 操作系统                                                     |
| `device`       | 设备                                                         |
| `country_code` | 国家代码                                                     |
| `country`      | 国家                                                         |
| `province`     | 州/省份/直辖市                                               |
| `city`         | 城市                                                         |
| `latitude`     | 经度                                                         |
| `longitude`    | 纬度                                                         |
| `timestamp`    | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`        | 32 位随机字符串                                              |
| `signature`    | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"opened",  
"email":"leo@submail.cn",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"ip":"10.0.1.199",  
"agent":"Mozilla 5.0",  
"platform":"Mac OS X",  
"device":"desktop",  
"country_code":"CN",  
"country":"China",  
"province":"Shanghai",  
"city":"Shanghai",  
"latitude":"1.9034",  
"longitude":"29.022.2",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **打开超链接 clicked**

<br>

| `events`       | `clicked`                                                    |
| -------------- | ------------------------------------------------------------ |
| `email`        | 此联系人的邮件地址                                           |
| `url`          | 打开的超链接地址                                             |
| `app`          | 应用 ID                                                      |
| `send_id`      | 发送ID（唯一标示）                                           |
| `tag`          | 自定义标签                                                   |
| `ip`           | 联系人 IP 地址                                               |
| `agent`        | 浏览器                                                       |
| `platform`     | 操作系统                                                     |
| `device`       | 设备                                                         |
| `country_code` | 国家代码                                                     |
| `country`      | 国家                                                         |
| `province`     | 州/省份/直辖市                                               |
| `city`         | 城市                                                         |
| `latitude`     | 经度                                                         |
| `longitude`    | 纬度                                                         |
| `timestamp`    | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`        | 32 位随机字符串                                              |
| `signature`    | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"clicked",  
"email":"leo@submail.cn",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"url":"http://submail.cn",  
"ip":"10.0.1.199",  
"agent":"Mozilla 5.0",  
"platform":"Mac OS X",  
"device":"desktop",  
"country_code":"CN",  
"country":"China",  
"province":"Shanghai",  
"city":"Shanghai",  
"latitude":"1.9034",  
"longitude":"29.022.2",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **订阅 subscribe**

<br>

| `events`    | `subscribe`                                                  |
| ----------- | ------------------------------------------------------------ |
| `email`     | 此联系人的邮件地址                                           |
| `app`       | 应用 ID                                                      |
| `send_id`   | 发送ID（唯一标示）                                           |
| `tag`       | 自定义标签                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"subscribe",  
"email":"leo@submail.cn",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **变更电邮地址 change_subscribe**

<br>

| `events`    | `change_subscribe`                                           |
| ----------- | ------------------------------------------------------------ |
| `email`     | 此联系人的邮件地址                                           |
| `new_email` | 变更后的邮件地址                                             |
| `app`       | 应用 ID                                                      |
| `send_id`   | 发送ID（唯一标示）                                           |
| `tag`       | 自定义标签                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"change_subscribe",  
"email":"leo@submail.cn",  
"new_email":"leo@submailer.cn",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **退订 unsubscribed**

<br>

| `events`    | `unsubscribe`                                                |
| ----------- | ------------------------------------------------------------ |
| `email`     | 此联系人的邮件地址                                           |
| `app`       | 应用 ID                                                      |
| `send_id`   | 发送ID（唯一标示）                                           |
| `tag`       | 自定义标签                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"unsubscribe",  
"email":"leo@submail.cn",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **被标记为垃圾邮件 marked_as_spam**

<br>

| `events`     | `marked_as_spam`                                             |
| ------------ | ------------------------------------------------------------ |
| `email`      | 此联系人的邮件地址                                           |
| `message_id` | SMTP ID                                                      |
| `app`        | 应用 ID                                                      |
| `send_id`    | 发送ID（唯一标示）                                           |
| `tag`        | 自定义标签                                                   |
| `timestamp`  | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`      | 32 位随机字符串                                              |
| `signature`  | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"marked_as_spam",  
"email":"leo@submail.cn",  
"message_id":"<6b472f5f207f7777ce59c9e1fe9884ab>",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **举报为垃圾邮件 report_as_spam**

<br>

| `events`     | `report_as_spam`                                             |
| ------------ | ------------------------------------------------------------ |
| `email`      | 此联系人的邮件地址                                           |
| `message_id` | SMTP ID                                                      |
| `app`        | 应用 ID                                                      |
| `send_id`    | 发送ID（唯一标示）                                           |
| `tag`        | 自定义标签                                                   |
| `timestamp`  | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`      | 32 位随机字符串                                              |
| `signature`  | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"report_as_spam",  
"email":"leo@submail.cn",  
"message_id":"<6b472f5f207f7777ce59c9e1fe9884ab>",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

---

<br>

### **邮件被拒收 rejected**

<br>

| `events`     | `rejected`                                                   |
| ------------ | ------------------------------------------------------------ |
| `email`      | 此联系人的邮件地址                                           |
| `message_id` | SMTP ID                                                      |
| `app`        | 应用 ID                                                      |
| `send_id`    | 发送ID（唯一标示）                                           |
| `tag`        | 自定义标签                                                   |
| `timestamp`  | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`      | 32 位随机字符串                                              |
| `signature`  | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"rejected",  
"email":"leo@submail.cn",  
"message_id":"<6b472f5f207f7777ce59c9e1fe9884ab>",  
"app":10034,  
"send_id":"oiidJ3",  
"tag":"testtag",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

------

<br>

### **收件箱 receivers**

<br>

| `events`    | `receivers`                                                  |
| ----------- | ------------------------------------------------------------ |
| `mail_to`   | 收件人                                                       |
| `mail_from` | 发件人                                                       |
| `subject`   | 邮件标题                                                     |
| `content`   | 邮件原始 eml 文件 (原始报文，需解析)                         |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{  
"events":"receivers",  
"mail_to":"xxx@xxxx.com",  
"mail_from":"xxx@xxxx.com",  
"subject":"test",  
"content":"******",  
"timestamp":1415014855,  
"token":"067ef7e2f286a9a56eabb07dc9657852",  
"signature":"a70d09a9345adfdd353d34a505dac4ca"  
}
```

------