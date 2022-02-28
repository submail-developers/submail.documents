## 国际短信 SUBHOOK 事件

<br>

### **请求 request**

<br>


| `events`    | `request`                                                    |
| ----------- | ------------------------------------------------------------ |
| `address`   | 此联系人的手机号码                                           |
| `app`       | 应用 ID                                                      |
| `send_id`   | 该条短信的唯一发送标识，可在 API 请求时获取                  |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"request",
"address":"+138xxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

<br>

### **国际短信发送成功delivered**

<br>


| `events`    | `delivered`                                                  |
| ----------- | ------------------------------------------------------------ |
| `address`   | 此联系人的手机号码                                           |
| `app`       | 应用 ID                                                      |
| `send_id`   | 该条国际短信的唯一发送标识，可在 API 请求时获取              |
| `tag`       | 32位随机数字符串                                             |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"delivered",
"address":"+138xxxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"timestamp":1415235639,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

<br>

### **国际短信发送失败 dropped**

<br>


| `events`    | `dropped`                                                    |
| ----------- | ------------------------------------------------------------ |
| `address`   | 此联系人的手机号码                                           |
| `app`       | 应用 ID                                                      |
| `send_id`   | 该条国际短信的唯一发送标识，可在 API 请求时获取              |
| `tag`       | 32位随机数字符串                                             |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"dropped",
"address":"138xxxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

<br>

### **国际短信正在发送中sending**

<br>


| `events`    | `sending`                                                    |
| ----------- | ------------------------------------------------------------ |
| `address`   | 此联系人的手机号码                                           |
| `app`       | 应用 ID                                                      |
| `tag`       | 32位随机数字符串                                             |
| `send_id`   | 该条短信的唯一发送标识，可在 API 请求时获取                  |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br>

##### **推送示例**


```
{
"events":"sending",
"address":"+138xxxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---