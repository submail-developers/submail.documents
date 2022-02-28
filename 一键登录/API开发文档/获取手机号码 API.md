## 获取手机号码API



<br />

### **URL**

<br />

https://tpa.mysubmail.com/ocl/getMobile

------

<br />

### **http 请求方式**

<br />

| 请求方式    | content-type设置                                             |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

------

<br />

### **返回参数格式**

<br />

`jsonString`

------

<br />

### **是否需要授权**

<br />

##### 是


------

<br />

### **参数说明**

<br />

| 参数        | 类型     | 描述                                                 |
| ----------- | -------- | ---------------------------------------------------- |
| `appid`     | `string` | 在 SUBMAIL 一键登录服务中创建并且认证通过的应用 ID   |
| `signature` | `string` | `appkey`+时间戳+`token`拼接，并用`sha256`方式加密    |
| `type`      | `int`    | 服务商类型，1=中国移动，2=中国联通，3=中国电信       |
| `os`        | `string` | 手机操作系统，参数目前可选 IOS 和 Android            |
| `timestamp` | `string` | UNIX 时间戳                                          |
| `token`     | `string` | SDK 中获得的取号`token`                              |
| `auth`      | `int`    | 号码类型为电信号码时的必须参数，其他运营商忽略此参数 |

------

<br />

### **相应参数**

<br />

##### 取号成功

```
{

  "code":"0",   //code=0表示取号成功
   "send_id":"093c0a7df143c087d6cba9cdf0cf3738",   //接口请求唯一标识

  "mobile":"13888888888" //手机号码

}
```

<br />

##### 取号失败

```
{

  "code":"1113",   //code=1113表示运营商错误            

  "send_id":"093c0a7df143c087d6cba9cdf0cf3738",   //接口请求唯一标识

  "msg":"Operator error:103101" //运营商错误+运营商错误代码

}
```

<br />

------
