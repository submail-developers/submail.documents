# 空号检测 API
<br />
### **概览**
空号检测是 SUBMAIL 的号码筛选 API，根据提交的号码来判断号码是否正常。

------
 <br />

### **URL**

 <br />

` http://tpa.mysubmail.com/mdetect/batchCheck`

------

 <br />


### **http 请求方式**

 <br />

| **请求方式** | content-type 设置                                            |
| ------------ | ------------------------------------------------------------ |
| `http post`  | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

------

 <br />

### **请求参数**

 <br />

| **参数**    | **类型**     | **必需**/可选** | **默认** | **描述**                                     |
| ----------- | ------------ | --------------- | -------- | -------------------------------------------- |
| `appid`     | `string`     | `必需`          | 无       | 应用 appid，自控制台获取                     |
| `timestamp` | `string`     | `可选`          | 无       | Unix时间戳                                   |
| `sign_type` | `string`     | `可选`          | 无       | 加密方式，可选值md5、sha1、sha256            |
| `mobiles`   | `json array` | `必需`          | 无       | 要验证的号码，JSON数组类型，最大支持50个号码 |
| `signature` | `string`     | `必需`          | 无       | sha256 数据加密校验证书                      |

------

 <br />
### signature创建规则
 <br />
1.请将以下参数按顺序连接
   appid+appkey+timestamp（字符串不包括加号）

2.使用对应的加密方式对字符串加密

------
 <br />
###  **PHP代码示例**
```
<?php
    $post_data['timestamp'] = time();
    $post_data['appid'] = 'appid';
    $appkey= 'appkey';
    $post_data['mobiles'] = json_encode(array("18612345678","152012345678","10901893074"));
    $post_data['sign_type'] = "sha256";
    $post_data['signature'] = hash('sha256',$post_data['appid'].$appkey.$post_data['timestamp']);
    $curl = curl_init();

    curl_setopt_array($curl, array(
        CURLOPT_URL => "https://tpa.mysubmail.com/mdetect/batchCheck",
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => "POST",
        CURLOPT_POSTFIELDS => http_build_query($post_data),
        CURLOPT_HTTPHEADER => array(
            "Content-Type: application/x-www-form-urlencoded",
        ),
    ));

    $response = curl_exec($curl);
    $err = curl_error($curl);

    curl_close($curl);
    print_r(json_decode($response,true));
    print_r($err);
```
 <br />

##### 成功返回

```
/*
status状态描述
状态：0-空号，1-实号，2-停机，3-库无，4-沉默号，5-风险号，9-无效号码
*/
{
    "status": "success",//接口状态
    "code": 0,//错误码
    "data": [
        {
            "fee": 1,//是否计费
            "mobile": "152012345678",
            "area": "上海-上海",
            "type": "中国移动",
            "status": "1"//号码状态
        },
        {
            "fee": 1,
            "mobile": "18612345678",
            "area": "上海-上海",
            "type": "中国联通",
            "status": "1"
        },
        {
            "fee": 0,
            "message": "Invalid mobile number",
            "mobile": "10901893074",
            "status": "9"
        }
    ],
    "feeCount": 2//计费总数
}
```

 <br />

##### 请求失败

```
/*
错误码解释
1401：appid不正确
1402：无效的时间戳
1403：signature不正确
1404：appid已禁用
1405：IP白名单限制
1406：账户不存在或已注销
1407：账户已禁用
1408：服务已禁用
1409：号码参数不正确
1410：余额不足
1411：号码数量超过50个
*/
{
    "status": "error",
    "code": 1403,
    "msg": "Invalid signature with Normal"
}

status:接口状态		code:错误代码		msg:错误信息
```