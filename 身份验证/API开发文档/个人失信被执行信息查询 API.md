# API: Factor/enforcement - 个人失信被执行信息查询
<br />
### 概览
<br />
`Factor/enforcement`是submail的个人失信被执行信息查询API，输入姓名和身份证号查询是否被法院列入失信被执行人名单并返回详情。

------------


<br />
### URL
<br />
```
<主> http://tpa.mysubmail.com/factor/enforcement  
<备> https://tpa.mysubmail.com/factor/enforcement
```

------------


<br />
### http请求方式
<br />
| 请求方式  | content-type设置                                             |
| --------- | ------------------------------------------------------------ |
| http post | multipart/form-data、x-www-form-urlencoded、application/json |

------------


<br />
### 返回参数格式
<br />
`jsonString`

------------


<br />
### 请求参数说明
<br />
| 参数      | 是否必填 | 类型   | 类型                                               |
| --------- | -------- | ------ | -------------------------------------------------- |
| appid     | 是       | string | 在 SUBMAIL 身份认证服务中创建并且认证通过的应用 ID |
| timestamp | 是       | string | UNIX 时间戳                                        |
| signature | 是       | string | 签名，详细规则看下方介绍                           |
| idNo | 是 | string | 身份证号码
| name | 是 | string | 用户姓名

------------


<br />
### signature创建规则
<br />
1. 请将以下参数按照字段升序（A-Z）排列    appkey 、idNo 、name 、timestamp
2. 创建签名字符串 ：以"key=value" + "&amp;"（连接符）+ "key=value" 的方式连接所有参数
3. 创建签名：拼接签名字符串示例string = "appkey=xxxx&amp;idNo=xxxx&amp;name=xxxx×tamp=xxxxxxxxxx"，然后使用sha256(string)创建签名  
   注：中文需要使用urlencode处理后再参与创建签名
   

------------


<br />
### 响应消息
<br />
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
        'code'       => '02',                                     //结果状态码   01：无记录  02：有记录
        'msg'        => '有记录',                                  //结果描述
        'idCardNo'   => '......'                                  //用户身份证号码
        'idCardName' => '......'                                  //用户姓名
        'info'       => '......'                                  //被执行详细信息
    };
}
```

------------