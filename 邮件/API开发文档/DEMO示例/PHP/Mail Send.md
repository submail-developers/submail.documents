# DEMO:Mail/Send

<br>

## 代码示例

<br>

```
<?php
    /*****************
     * 非加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //附件地址 : 本机内文件地址
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $attachments = curl_file_create('/Users/duan/Desktop/1.png');           //附件地址
    $subject = '邮件主题';                                                            //邮件主题
    $from = 'from@domain.com';                                                      //发送人 邮箱
    $to = 'to@domain.com';                                                          //接收人 地址
    $html = '<body>邮件内容...</body>';                                              //邮件内容

    $post_data = array(
        "appid"       => $appid,
        "signature"   => $appkey,
        "attachments" => $attachments,
        "subject"     => $subject,
        "from"        => $from,
        "to"          => $to,
        "html"        => $html,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/mail/send.json',
        CURLOPT_RETURNTRANSFER  => 1,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);




    /*****************
     * 加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //附件地址 : 本机内文件地址
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $attachments = curl_file_create('/Users/duan/Desktop/1.png');           //附件地址
    $subject = '邮件主题';                                                            //邮件主题
    $from = 'from@domain.com';                                                      //发送人 邮箱
    $to = 'to@domain.com';                                                          //接收人 地址
    $html = '<body>邮件内容...</body>';                                              //邮件内容

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

    $post_data = Array (
        "appid" => $appid,
        "attachments" => $attachments,
        "subject" => $subject,
        "from" => $from,
        "to" => $to,
        "html" => $html,
        "sign_version" => 2,
        "sign_type" => 'md5',
        "timestamp" => $timestamp,
    );

    $temp = $post_data;
    unset($temp['attachments']);
    unset($temp['html']);
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
        CURLOPT_URL             => 'https://api.mysubmail.com/mail/send.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);


```