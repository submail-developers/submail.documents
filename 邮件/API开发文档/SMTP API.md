## SMTP API

<br>

### **概览**

<br>

SUBMAIL 的 `SMTP API` 使用电子邮件协议的自定义指令。开发者通过在邮件头中插入 `x-submail-smtp-api` 指令灵活地控制发送请求，如添加联系人、将地址簿添加至发送队列，或使用文本变量或超链接变量来灵活地控制邮件内容，甚至在SMTP API 中使用模板。

要使用 SUBMAIL `SMTP API`，开发者需要在邮件头中插入` x-submail-smtp-api` 指令，并将请求的参数编码成 JSON 字符串。

一个简单的请求看起来是这样的：

<br>
#### 代码示例

```
{
  "to":[
           "leo <leo>",
           "retro@submail.cn"
          ],
 "addressbook":[
           "subscribe",
           "WbRfn3"
          ]
}
```

---

<br>

### **X-SUBMAIL-SMTP-API 邮件标头指令**

<br>

`x-submail-smtp-api` 指令是一个标准的 JSON 格式，包含几个部分的关联数组。使用 SMTP 协议请求 SUBMAIL 发送的邮件中包含有效的 `x-submail-smtp-api` 指令时，SUBMAIL 将会对此指令进行解析并将其应用到邮件事务。

---

<br>

### **to 指令**

<br>

`to` : 联系人组数，包含可选的显示名称。SUBMAIL 支持完整的[RFC 822 电邮地址协议](http://en.wikipedia.org/wiki/Email_address)，请在提交请求前检查邮件地址的有效性。


```
{
   "to":[
          "leo <leo>",
          "retro <retro>",
          "<service>",
          "account@submail.cn"
          ]
}
```

---

<br>

### **addressbook 指令**

<br>

`addressbook：`地址簿指令。使用地址簿指令将地址簿中的联系人添加到发送队列，你可以在 addressbook 指令中加入 subscribe 来添加订阅用户，或使用地址簿标示。请参见[获取项目 ID](https://www.mysubmail.com/documents/eFhpI1)。


```
{
   "addressbook":[
             "subscribe",
             "j5lVv1"
            ]
}
```

---

<br>

### **template 指令**

<br>

`template：`邮件模板指令。邮件模板指令允许开发者使用在 SUBMAIL MAIL 应用中创建的邮件项目，要使用该项目发送，请在此指令中添加邮件项目标示。请参见[获取项目 ID](https://www.mysubmail.com/documents/eFhpI1)。


```
{
     "template":"DKFzD4"
}
```

---

<br>

### **vars 指令**

<br>

`vars：`文本变量指令。使用 vars 文本变量灵活的控制邮件内容。请参见[文本变量](https://www.mysubmail.com/documents/TOYJC1)。


```
{
     "vars":{
               "key1":"value",
               "key2":"value",
               "key3":"value"
             }
}
```

<br>

### **links 指令**

<br>

`links：`超链接变量指令。使用 links 超链接变量灵活的控制邮件中的超链接。请参见[超链接变量](https://www.mysubmail.com/documents/uDRmO1)。


```
{
     "links":{
               "key1":"value",
               "key2":"value",
               "key3":"value"
             }
}
```

---

<br>

### **代码示例**

<br>

完整功能的 `x-submail-smtp-api JSON `字符串示例


```
{
  "to":[
        "leo <leo>",
  ],
 "addressbook":[
        "subscribe",
        "WbRfn3"
  ],
  "template":"DKFzD4",
  "vars":{
        "key1":"value",
        "key2":"value",
        "key3":"value"
  },
 "links":{
        "key1":"value",
        "key2":"value",
        "key3":"value"
  }

}
```
<br>

使用 `perl` 语言编写的 `x-submail-smtp-api` 指令示例


```
#!/usr/local/bin/perl -w

use strict;
use JSON;

my $header = {
        to => ['leo '],
        addressbook => ['subscribe','WbRfn3'],
        template => 'DKFzD4',
        vars => { 'key1' => 'value', 'key2' => 'value', 'key3' => 'value' },
        links => { 'key1' => 'value', 'key2' => 'value', 'key3' => 'value' }
};

my $json = JSON->new;
$json->space_before(1);
$json->space_after(1);
my $js = $json->encode($header);
$js =~ s/(.{1,72})(\s)/$1\n /g;
my $headers = "X-SUBMAIL-SMTP-API: $js";
print "$headers\n";
```

---

<br>

### **错误代码**

<br>

`x-submail-smtp-api` 无返回码，它通常返回 `SMTP` 错误代码。通常在测试 `x-submail-smtp-api` 时，开发者可前往  [API 错误日志](https://www.mysubmail.com/chs/mail/errorlog) 中查看 `x-submail-smtp-api` 返回的错误代码。
<br>
##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/i22PE4)

------
