## 短网址 SUBHOOK 事件

  <br>

### **创建短网址事件 create**

 <br>

| `events`    | `create`                                                     |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `item`      | 短网址自定义标识。                                           |
| `long_url`  | 目标长网址                                                   |
| `short_url` | 目标短网址                                                   |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br> 

##### **推送示例**

 

```
{
   "app":"xxxx",
    "events":"create",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "item":"15221xxx6306",
    "long_url":"http://xxxxxx1/pages/xxxx/xxxxxxxxx.html?12",
    "short_url":"http://link.wiki/xxx/xxx",
    "signature":"b0da8d06abb883a0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

 

------

 <br>

### **短网址更新事件**

 <br>

| `events`    | `update`                                                     |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `item`      | 短网址自定义标识。                                           |
| `long_url`  | 目标长网址                                                   |
| `short_url` | 目标短网址                                                   |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br> 

##### **推送示例**

 

```
{
   "app":"xxxx",
    "events":"update",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "item":"15221xxx6306",
    "long_url":"http://xxxxxx1/pages/xxxx/xxxxxxxxx.html?12",
    "short_url":"http://link.wiki/xxx/xxx",
    "signature":"b0da8d06abb883a0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

 

------

 <br>

### **短网址删除事件 delete**

 <br>

| `events`    | `delete`                                                     |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `item`      | 短网址自定义标识。                                           |
| `long_url`  | 目标长网址                                                   |
| `short_url` | 目标短网址                                                   |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

 <br>

##### **推送示例**

 

```
{
   "events":"delete",
   "app":"xxxx",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "item":"15221xxx6306",
    "long_url":"http://xxxxxx1/pages/xxxx/xxxxxxxxx.html?12",
    "short_url":"http://link.wiki/xxx/xxx",
    "signature":"b0da8d06abb883a0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

 

------

 <br>

### **短网址群组创建事件 create_group**

 <br>

| `events`    | `create_group`                                               |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

 <br>

##### **推送示例**

 

```
{
   "events":"create_group",
   "app":"xxxx",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "signature":"b0da8d06abb883a0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

 

------

 <br>

### **更新短网址群组  update_group**

 <br>

| `events`    | `update_group`                                               |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

<br> 

##### **推送示例**

 

```
{
   "events":"update_group",
   "app":"xxxx",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "signature":"b0da8d0xxxx0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7",
}
```

 

------

 <br>

### **删除短网址群组**

 <br>

| `events`    | `delete_group`                                               |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

 <br>

##### **推送示例**

 

```
{
   "events":"delete_group",
   "app":"xxxx",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "signature":"b0da8d06axxx1140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

------

  <br>

### **访问事件 vist** 

 <br>

| `events`           | `visit`                                                      |
| ------------------ | ------------------------------------------------------------ |
| `app`              | 应用ID                                                       |
| `group`            | 短网址群组ID                                                 |
| `item`             | 短网址自定义标识。                                           |
| `long_url`         | 目标长网址                                                   |
| `short_url`        | 目标短网址                                                   |
| `agent`            | 用户代理                                                     |
| `coordinates`      | 坐标位置                                                     |
| `country_cn`       | 国家名（中文）                                               |
| `country_en`       | 国家名（英文）                                               |
| `iso_country_code` | iso国家编码                                                  |
| `province_Cn`      | 省份名（中文）                                               |
| `province_en`      | 省份名（英文）                                               |
| `city_cn`          | 城市名（中文）                                               |
| `city_en`          | 城市名（英文）                                               |
| `device`           | 设备类型                                                     |
| `brower`           | 浏览器类型                                                   |
| `browser_version`  | 浏览器版本号                                                 |
| `ip`               | 访问的ip地址                                                 |
| `os`               | 操作系统及其系统版本号                                       |
| `platform`         | 操作系统                                                     |
| `referrer`         | 跳转前网站地址                                               |
| `visit_at`         | 访问时间                                                     |
| `tag`              | 自定义标识                                                   |
| `timestamp`        | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`            | 32 位随机字符串                                              |
| `signature`        | 数字签名                                                     |

 

<br> 

##### **推送示例**

 

```
{
   "app":"xxx",
    "events":"visit",
    "agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.100 Safari/537.36",
    "browser":"Chrome",
    "browser_version":"75.0.3770.100",
    "city_cn":"上海",
    "city_en":"Shanghai",
    "coordinates":"31.0449,121.4012",
    "country_cn":"中国",
    "country_en":"China",
    "device":"Desktop",
    "group":"d41d975b89xxx31a31685269770f",
    "ip":"xxxxxx",
    "iso_country_code":"CN",
    "item":"152xxx6306",
    "long_url":"http://mysubmail.com/xxx/xxx",
    "os":"Intel Mac OS X 10_14_5",
    "platform":"Macintosh",
    "province_Cn":"上海",
    "province_en":"Shanghai",
    "referrer":"xxx",
    "short_url":"http://link.wiki/xxx/xxxyD",
    "signature":"8ed8389axxxxx242aa54e8d3e1e43",
    "tag":"af58a9ef867e790d0xxxxdd8868,18616761881,13",
    "timestamp":"1563389015",
    "token":"3b562f5fxxxxx87d85aea642547d47",
    "visit_at":" 2019-07-17 10:43:35"
}
```

 

------

  <br>

### **短网址审核通过 shorturl_accept**

 <br>

| `events`    | `shorturl_accept`                                            |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `item`      | 短网址自定义标识。                                           |
| `long_url`  | 目标长网址                                                   |
| `short_url` | 目标短网址                                                   |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

  <br>

##### **推送示例**

 

```
{
   "app":"xxxx",
    "events":"shorturl_accept",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "item":"15221xxx6306",
    "long_url":"http://xxxxxx1/pages/xxxx/xxxxxxxxx.html?12",
    "short_url":"http://link.wiki/xxx/xxx",
    "signature":"b0da8d06abb883a0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp": "1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

 

------

 <br>

### **短网址审核未通过 shorturl_reject**

 <br>

| `events`    | `shorturl_reject`                                            |
| ----------- | ------------------------------------------------------------ |
| `app`       | 应用ID                                                       |
| `group`     | 短网址群组ID                                                 |
| `item`      | 短网址自定义标识。                                           |
| `long_url`  | 目标长网址                                                   |
| `short_url` | 目标短网址                                                   |
| `tag`       | 自定义标识                                                   |
| `timestamp` | 事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名） |
| `token`     | 32 位随机字符串                                              |
| `signature` | 数字签名                                                     |

 <br>

##### **推送示例**

 

```
{
   "app":"xxxx",
    "events":"shorturl_create",
    "group":"d41d975b899d3xxxx1a31685269770f",
    "item":"15221xxx6306",
    "long_url":"http://xxxxxx1/pages/xxxx/xxxxxxxxx.html?12",
    "short_url":"http://link.wiki/xxx/xxx",
    "signature":"b0da8d06abb883a0581140f0d8d9166d",
    "tag":"af58a9ef867e790d0ee2c85e5cdd8868,18616761881,14",
    "timestamp":"1563389055",
    "token":"74ce84d1464xxxx976e2ba4ffe9f7"
}
```

------

 