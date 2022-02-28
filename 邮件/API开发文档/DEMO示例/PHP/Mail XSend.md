# DEMO:Mail/XSend
<br>

## 代码示例

<br>

```
<?php
<?php
    /*****************
     * 非加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     邮件-创建/管理AppID中获取
    //邮件模板ID   邮件-创建/管理邮件模板中获得
    //邮件模板对应变量
    //  若模板为：您的验证码是@var(code)，请在@var(time)内输入。邮件模板对应变量如下
    //  变量名和自定义内容相对应即可
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $from = 'from@domain.com';                                                      //发送人 邮箱
    $to = 'to@domain.com';                                                          //接收人 地址
    $project = 'F*****U';                                                           //邮件模板ID
    $vars = json_encode(array(                                                      //邮件模板对应变量
        'code' => '1111',
        'time' => '三分钟'
    ));

    $post_data = Array(
        "appid"     => $appid,
        "signature" => $appkey,
        "from"      => $from,
        "to"        => $to,
        "project"   => $project,
        "vars"      => $vars,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/mail/xsend.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);



    /*****************
     * 加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     邮件-创建/管理AppID中获取
    //邮件模板ID   邮件-创建/管理邮件模板中获得
    //邮件模板对应变量
    //  若模板为：您的验证码是@var(code)，请在@var(time)内输入。邮件模板对应变量如下
    //  变量名和自定义内容相对应即可
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $from = 'from@domain.com';                                                      //发送人 邮箱
    $to = 'to@domain.com';                                                          //接收人 地址
    $project = 'F*****U';                                                           //邮件模板ID
    $vars = json_encode(array(                                                      //邮件模板对应变量
        'code' => '1111',
        'time' => '三分钟'
    ));

    //通过接口，获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/service/timestamp.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);
    $timestamp = $output['timestamp'];

    $post_data = Array(
        "appid"         => $appid,
        "from"          => $from,
        "to"            => $to,
        "project"       => $project,
        "vars"          => $vars,
        "sign_version"  => 2,
        "sign_type"     => 'md5',
        "timestamp"     => $timestamp,
    );

    $temp = $post_data;
    unset($temp['vars']);
    ksort($temp);
    reset($temp);
    $tempStr = "";
    foreach ($temp as $key => $value) {
        $tempStr.=$key."=".$value."&amp;";
    }
    $tempStr = substr($tempStr,0,-1);
    //生成签名
    $post_data['signature'] = md5($appid.$appkey.$tempStr.$appid.$appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/mail/xsend.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);

```