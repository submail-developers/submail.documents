## API 错误代码与描述

<br>


| 错误代码 | 描述                                                   | Description                                                  |
| -------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| 1004     | URL不能为空                                            | The URL can not empty                                        |
| 1005     | 无效url                                                | Invalid URL                                                  |
| 1006     | 无效域名                                               | Invalid Domain                                               |
| 1007     | 请将密码限制在256个字符以内                            | Please limit the Password to 256 characters                  |
| 1008     | 请求超过单月限制                                       | Request exceeds month limit                                  |
| 1009     | 密码访问权限被拒绝                                     | Password access permission denied                            |
| 1010     | 访问限制权限被拒绝                                     | Access limit permission denied                               |
| 1011     | 没有设置过期权限                                       | Expire permission denied                                     |
| 1012     | 请将有效期限制在365天内                                | Please limit the expiration to 365 days                      |
| 1013     | url被列入系统黑名单                                    | The URL is blocked by system blocklist                       |
| 1014     | 超过频率限制，请限制短链接的请求频率在每分钟60次以内。 | Exceed the frequency limit, please limit the request of shorturl get type to 60 times per minute. |
| 1015     | URL参数不正确                                          | URL parameter is incorrect                                   |
| 1016     | URL不存在或短URL已过期                                 | URL does not exist or Short URL expired                      |
| 1017     | 短链接群组超出限制                                     | Short URL Group exceeds limit                                |
| 1018     | pause参数设置为String类型，"true"或者"false"           | The pause parameter should be set to true or false value as a string |
| 1019     | 请把有效期限制在30天内                                 | Please limit the expiration to 30 days                       |
| 1020     | 请把有效期限制在90天内                                 | Please limit the expiration to 90 days                       |
| 1021     | 请把有效期限制在3年之内                                | Please limit the expiration to 3 years                       |

---

**注：** 当 API  返回 307或者 309错误时，服务器会给出具体的 JSON decoding 错误原因。

```
json_decoding_error 参数将以数字形式标注错误代码

json_decoding_error:

1 = 到达了最大堆栈深度

2 = 无效或异常的 JSON

3 = 控制字符错误，可能是编码不对

4 = 语法错误

5 = 异常的 UTF-8 字符，也许是因为不正确的编码
```



------