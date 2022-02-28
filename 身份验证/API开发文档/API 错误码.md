# API 错误代码与描述
| 错误代码 | 描述                                                         | Description                                                  |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1201     | 不正确的 APP ID                                              | Incorrect APP ID.                                            |
| 1202     | 请求的 APPID 已设置 IP 白名单，您的 IP 不在此白名单范围      | APPID has been set IP whitelist, your IP is not in the scope of this white list. |
| 1203     | 您的账户余额不足                                             | Your credits is not enough to support your api request.      |
| 1204     | signature 参数无效                                           | Invalid signature.                                           |
| 1205     | appkey 无效                                                  | Invalid appkey.                                              |
| 1206     | APPID被禁用                                                  | This APP has been disabled.                                  |
| 1208     | 错误的 UNIX 时间戳                                           | Invalid timestamp.                                           |
| 1209     | 缺少参数                                                     | Lack of necessary parameters.                                |
| 1210     | 空的appid                                                    | Empty APP ID.                                                |
| 1211     | 空的appkey                                                   | Empty appkey.                                                |
| 1212     | 空的signature                                                | Empty signature.                                             |
| 1213     | 时间戳超时                                                   | Timestamp timeout.                                           |
| 1214     | 手机号码不正确                                               | Mobile length should be 11.                                  |
| 1215     | 身份证号码不正确                                             | IdCard length should be 18.                                  |
| 1217     | 接口发生错误                                                 | API gateway error（运营商错误码）.                           |
| 1218     | 服务被禁用                                                   | Your factor service was disabled                             |
| 1219     | 账户被禁用                                                   | Your account has been disabled.                              |
| 1221     | 获取token失败                                                | Fail to get token.                                           |
| 1222     | 用户名字非法                                                 | Invalid name.                                                |
| 1223     | 数据库出现错误                                               | Database Error.                                              |
| 1225     | 存储消费日志失败                                             | Credit Deduction Log Failed.                                 |
| 1226     | 获取固定消费配置信息失败                                     | Faile To Get Fixed Billing Config.                           |
| 1227     | 获取梯度消费配置信息失败                                     | Faile To Get Gradient Billing Config.                        |
| 1229     | 身份证有效日期-开始日期 格式非法                             | Invalid beginDate.                                           |
| 1230     | 身份证有效日期-结束日期 格式非法                             | Invalid endDate.                                             |
| 1231     | base64数据 格式错误                                          | Picture Format Error.                                        |
| 1232     | 文件格式非法 只支持 file、base64两种格式                     | Invalid File_type.                                           |
| 1233     | 文件为空                                                     | Empty File.                                                  |
| 1234     | 文件过大  只支持*M以内                                       | The file should be less than *M.                             |
| 1235     | 文件同步失败                                                 | The file synchronize filed.                                  |
| 1236     | 图片只支持png、jpeg、jpg格式                                 | The Picture only supports png、jpeg、jpg                     |
| 1237     | 用户动作序列参数非法  只支持 BLINK 眨眼;MOUTH 张嘴; NOD 点头; YAW 摇头 | Invalid Motions.                                             |
| 1238     | 活体检测通过的难易程度参数非法 只支持 0:简单模式;1: 正常模式;2:困难模式;3:地狱模式 | Invalid Complexity.                                          |
| 1239     | 是否需要返回照片 参数非法  只支持 Y/N                        | Invalid Image_flag.                                          |
| 1240     | 视频文件为空                                                 | Empty Video.                                                 |
| 1241     | 视频文件格式错误 只支持mp4、avi、wmv、mov、rmvb              | The Video only supports mp4、avi、wmv、mov、rmvb.            |

</br>
</br>


# 运营商结果编码说明
| code参数 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| 0        | 请求成功                                                     |
| -1       | 请求失败                                                     |
| -1000    | 不一致                                                       |
| -1001    | 无效的 token                                                 |
| -1002    | 参数不能为空;                                                |
| -1003    | 参数不符合 base64 的格式                                     |
| -1004    | 数据不存在                                                   |
| -1005    | 参数格式不合法                                               |
| -1006    | 无效的通道或者无权限                                         |
| -1007    | 已注销                                                       |
| -1008    | 未认证                                                       |
| -1009    | 手机号身份证号验证一致;手机号姓名验证不一致                  |
| -1010    | 手机号身份证号验证不一致，手机号姓名验证一致                 |
| -1011    | 姓名和身份证号码不匹配                                       |
| -1012    | 其他不一致                                                   |
| -1013    | 手机号状态异常(手机号已销号、停机、空号、号码错误、号码为副 卡等) |
| -1014    | 手机号 T-1 月前已离网(预留暂不返回)                          |
| -1015    | 手机号错误(没有匹配的运营商,不支持虚拟号段)                  |
| -1016    | 库中无此身份证记录                                           |
| -1017    | 库中无此手机信息                                             |
| -1018    | 库中无此信息                                                 |
| -1019    | 不支持的手机号                                               |
| -1020    | 运营商查询不到该手机号                                       |
| -1021    | 通道返回失败                                                 |
| -1022    | 比对成功                                                     |
| -1023    | 身份证号码姓名不一致                                         |
| -1024    | 库中无此号                                                   |
| -1025    | 身份核验成功，数据非法"                                      |
| -1026    | 数据非法                                                     |
| -1027    | 身份核验成功，人脸识别系统异常                               |
| -1028    | 照片质量不合格                                               |
| -1029    | 上传图片文件过大                                             |
| -1030    | 身份核验成功，库中无照片                                     |
| -1031    | 身份核验成功，特征提取失败                                   |
| -1032    | 身份核验成功，检测到多于一张人脸                             |
| -1033    | 身份核验成功，图片不合法                                     |
| -1034    | 人像比对服务异常                                             |
| -1035    | 不一致，手机号已实名，但是身份证和姓名均与实名信息不一致     |
| -1036    | 不一致，手机号已实名，手机号和证件号一致，姓名不一致         |
| -1037    | 不一致，手机号已实名，手机号和姓名一致，身份证不一致         |
| -1039    | 认证不一致，认证未通过                                       |
| -1040    | 认证不一致，无效卡号                                         |
| -1041    | 认证不一致，持卡人信息有误                                   |
| -1042    | 认证不一致，手机号码有误                                     |
| -1043    | 认证不一致，交易次数超限                                     |
| -1044    | 认证不一致，此卡被没收                                       |
| -1045    | 认证不一致，该卡已过期                                       |
| -1046    | 认证不一致，此卡无对应发卡行                                 |
| -1047    | 认证不一致，此卡已挂失                                       |
| -1048    | 认证不一致，发卡行不支持此交易                               |
| -1049    | 认证不一致，未开通无卡支付                                   |
| -1050    | 认证不一致，受限制的卡                                       |
| -1051    | 认证不一致，作弊卡、吞卡                                     |
| -1052    | 认证不一致，该卡未初始化或睡眠卡                             |
| -1053    | 认证不一致，无法识别的卡                                     |
| -1054    | 认证不一致，密码错误次数超限                                 |
| -1055    | 认证不一致，姓名校验不通过                                   |
| -1056    | 认证不一致，身份证号码有误                                   |
| -1057    | 认证不一致，手机号码不合法                                   |
| -1058    | 认证不一致，银行卡号码有误                                   |
| -1059    | 认证不一致，数据校验不通过                                   |
| -1060    | 所传对比人像图片为空                                         |
| -1061    | 份证号不能为空                                               |
| -1062    | 身份证名字不能为空                                           |
| -1063    | 网络错误                                                     |
| -1064    | 图片大小超限                                                 |
| -1065    | 图片解密错误                                                 |
| -1066    | OCR 提取机构信息失败                                         |
| -1067    | OCR 提取信息失败                                             |
| -1068    | OCR 提取信息失败,请检查证件的有效性                          |
| -1069    | 查询失败                                                     |
| -1070    | 请检查身份证号码的有效性                                     |
| -1071    | 请检查手机号码的有效性                                       |
| -1072    | 请检查姓名的有效性                                           |
| -1073    | 请检查银联卡号的有效性                                       |
| -1074    | 无法解析图片文件，请检查 base64 字符串的有效性               |
| -1075    | 认证通过                                                     |
| -1077    | 文件类型错误                                                 |
| -1078    | 文件 BASE64 参数为空                                         |
| -1079    | 文件参数为空                                                 |
| -1080    | 无记录                                                       |
| -1081    | 系统判断为不同人                                             |
| -1082    | 特征提取失败                                                 |
| -1083    | 活体认证不通过                                               |
| -1084    | 查无记录                                                     |
| -1085    | 同一个样本重复调用次数达到上限                               |
| -3001    | client have no authorized user                               |
| -3002    | user is disabled                                             |
| -3003    | user Unauthenticated                                         |
| -3004    | client have no authorized certificate                        |
| -3005    | client is disabled                                           |
| -3006    | have no apiInterface                                         |
| -3007    | client have expire                                           |
| -3008    | apiInterface is disabled                                     |
| -3009    | client have no authorized interfaceAccount                   |
| -3010    | interface is disabled                                        |
| -3011    | interface have expire                                        |
| -3012    | interface is Surplus number not enough                       |
| -3013    | IP address is restricted                                     |
| -9006    | 通道无效或者无权限                                           |
| -9007    | 短信签名错误                                                 |
| -9008    | 非法的短信内容                                               |
| -5001    | 非法请求                                                     |