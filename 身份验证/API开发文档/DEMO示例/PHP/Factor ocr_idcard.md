# 身份证OCR识别     
### API: Factor/ocr_idcard
### 概览
`Factor/ocr_idcard`是submail的身份证OCR识别API，读写身份证图片上的身份信息。
***
### URL
```
<主> http://tpa.mysubmail.com/factor/ocr_idcard  
<备> https://tpa.mysubmail.com/factor/ocr_idcard
```
***
### http请求方式
| 请求方式  | content-type设置                                             |
| --------- | ------------------------------------------------------------ |
| http post | multipart/form-data、x-www-form-urlencoded、application/json |
***
### 返回参数格式
`jsonString`
***
### 请求参数说明
| 参数      | 是否必填 | 类型   | 类型                                               |
| --------- | -------- | ------ | -------------------------------------------------- |
| appid     | 是       | string | 在 SUBMAIL 身份认证服务中创建并且认证通过的应用 ID |
| timestamp | 是       | string | UNIX 时间戳                                        |
| signature | 是       | string | 签名，详细规则看下方介绍                           |
| ocr_type  | 是       | string | 0表示身份证正面，1表示身份证反面                   |
| file_type | 是       | string | 图片的格式(file                                    |
| file      | 是       | file   | 身份证图片文件 支持 png、jpeg、jpg                 |
| base64    | 是       | String | 身份证图片 BASE64 字符串                           |

***
### signature创建规则
1. 请将以下参数按照字段升序（A-Z）排列    appkey 、timestamp
2. 创建签名字符串 ：以"key=value" + "&amp;"（连接符）+ "key=value" 的方式连接所有参数
3. 创建签名：拼接签名字符串示例string = "appkey=xxxx×tamp=xxxxxxxxxx"，然后使用sha256(string)创建签名  
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
        'code'          => '',                                    //返回结果码
        'msg'           => '',                                    //结果描叙
        'race'          => '',                                    //(注:民族(汉字)
        'name'          => '',                                    //身份证姓名
        'gender'        => '',                                    //性别
        'idCardNumber'  => '',                                    //身份证号码
        'birthday'      => '',                                    //生日
        'address'       => '',                                    //地址
        'side'          => '',                                    //注:front/back 表示身份证的人像面/国徽面
        'validDate'     => '',                                    //有效日期
        'issuedBy'      => '',                                    //颁发机构
    };
}
```