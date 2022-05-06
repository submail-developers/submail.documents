# 银行卡四要素标准版     API: Factor/card_auth
### 概览
`Factor/card_auth`是submail的银行卡四要素标准版认证API，验证姓名、身份证号码(限单个)、银行卡号(限单个)、银行预留手机号(仅支持国内11位号码)
是否一致。
***  
### URL
```
<主> http://tpa.mysubmail.com/factor/card_auth  
<备> https://tpa.mysubmail.com/factor/card_auth
```
***
### http请求方式
| 请求方式 | content-type设置 |
| --- | --- |
| http post | multipart/form-data、x-www-form-urlencoded、application/json |
***
### 返回参数格式
`jsonString`
***
### 请求参数说明
| 参数 | 是否必填 | 类型 | 类型 |
| --- | --- | --- | --- |
| appid | 是 | string | 在 SUBMAIL 身份认证服务中创建并且认证通过的应用 ID |
| timestamp | 是 | string | UNIX 时间戳 |
| signature | 是 | string | 签名，详细规则看下方介绍|
| name | 是 | string | 用户姓名
| idNo | 是 | string | 身份证号码，限单个
| cardNumber | 是 | string | 银行卡号，限单个
| mobile | 是 | string | 银行预留手机号，仅支持国内11位号码

***
### signature创建规则
1. 请将以下参数按照字段升序（A-Z）排列    appkey、timestamp、idNo、name、cardNumber、mobile
2. 创建签名字符串 ：以"key=value" + "&"（连接符）+ "key=value" 的方式连接所有参数
3. 创建签名：拼接签名字符串示例string = "appkey=xxxx&idNo=xxxx&name=xxxx&timestamp=xxxxxxxxxx"，然后使用sha256(string)创建签名  
   注：中文需要使用urlencode处理后再参与创建签名
***
### 响应消息
```
API请求失败
{
    'status'  : 'error' ,                                          // 状态描述
    'send_id' : 'ee05d1635db847a2bf3c8317434539d6',                // API流水号
    'code'    : 1201 ,                                             // API返回的状态码    详情查看 API错误代码与描述  文档
    'msg'     : 'Incorrect APP ID.' ,                              // API返回的描述、  
}
```
```
API请求成功
{
    'status'  : 'success' ,                                       // 状态描述
    'send_id' : 'ee05d1635db847a2bf3c8317434539d6',               // API流水号
    'result' : {
         'identical' => true,                                     //true 认证一致    false 认证不一致
         'bankName' => '招商银行',                                  //银行名称
         'cardType' => '金卡',                                     //银行卡类型 
         'cardCategory' => '借记卡',                                //银行卡类别
         'remark' => '认证一致'                                     //备注
    };
}
```
