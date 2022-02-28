## jssdk集成文档
<br>
### 1、概述
<br>
本机号码认证适用于移动端 H5 页面，用户只需输入自己的手机号码，即可完成本机号码校验。
暂不支持微信小程序认证，App 应用端本机号码认证建议使用[一键登录](https://www.mysubmail.com/onepass "一键登录")。

校验环境要求：移动网络环境
取号需要经过蜂窝网络，wifi 状态或者未开启蜂窝网络的情况下，无法完成校验。


------------


<br>
### 2、对接流程
<br>
引入submail的js sdk
引入地址：<script src=" https://www.mysubmail.com/libraries/js/vfmobile.min.js " type="text/javascript" charset="utf-8"></script>
<br>
**初始化**

    var connection = VFM.init({
       appid:"",
       success:function(data){
       },
       error:function(data){
       }
    });
<br>
**data参数说明**

netType：网络环境；4g、5g、cellular、wifi、unknown
当netType为4g、5g、cellular时可进行本机验证
提示：因Ios系统限制，Ios手机无法在h5页面获取手机网络环境状态

msg：初始化状态信息
appid：初始化使用的appid
code：状态码
| code 状态码 | 描述        |
| ----------- | ----------- |
| 0           | 初始化成功  |
| 500         | 接口无响应  |
| 1301        | 无效的appid |
| 1311        | appid不存在 |
| 1107        | appid未授权 |
| 1109        | appid被禁用 |
| 1110        | 账户被禁用  |
| 1111        | 产品未授权  |

<br>
**取号**

     VFM.getTokenInfo({
         success:function(res){
         },
         error:function(res){
         },
    })
<br>
**res参数说明**
res.code 等于 0 表示获取token成功
    res.message=获取token成功
    res.token;得到的token
    res.userInformarion;得到的浏览器指纹
res.code 不等于 0 时表示获取token失败
    res.message = 取号失败信息
    res.YDData;运营商错误信息
    res.CTData;运营商错误信息
    res.CUData;运营商错误信息
    res.respCode;运营商错误码
	

<br>

运营商错误码描述：[运营商错误码](https://www.mysubmail.com/documents/IGfNu1 "运营商错误码")


------------