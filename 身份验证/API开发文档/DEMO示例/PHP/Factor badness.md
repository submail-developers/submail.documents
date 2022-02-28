# 不良行为查询     
### API: Factor/badness
### 概览
`Factor/badness`是submail的不良行为查询API。
***
### URL
```
<主> http://tpa.mysubmail.com/factor/badness  
<备> https://tpa.mysubmail.com/factor/badness
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
| idNo      | 是       | string | 身份证号码                                         |
| name      | 是       | string | 用户姓名                                           |
***
### signature创建规则
1. 请将以下参数按照字段升序（A-Z）排列    appkey 、idNo 、name 、timestamp
2. 创建签名字符串 ：以"key=value" + "&amp;"（连接符）+ "key=value" 的方式连接所有参数
3. 创建签名：拼接签名字符串示例string = "appkey=xxxx&amp;idNo=xxxx&amp;name=xxxx×tamp=xxxxxxxxxx"，然后使用sha256(string)创建签名  
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
        'code'   => '02',                                         //结果状态码   01：无记录  02：有记录
        'msg'    => '有记录（**）',                                 //结果描述+身份状态
        'bType'  => '*****************',                          //不良类型, A 再逃 、B 前科 、C 吸毒 、D 涉毒 、E 涉案人员 、 F 犯罪嫌疑人 Z 正常
        'tag'    => '***',                                        //不良详情
        'years'  => '***',                                        //距今时间
    };
    注意：
        无记录的状态下，bType、tag、years这三个参数不存在
}
```