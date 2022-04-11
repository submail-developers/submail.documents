# DEMEO:InternationalSMS/XSend

<br>

## 代码示例

```
<?php
    /*****************
     * 非加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     国际短信-创建/管理AppID中获取
    //手机号支持单个
    //模板ID   国际短信-创建/管理国际短信模板中获得
    //国际短信模板对应变量
    //  若模板为：【SUBMAIL】您的验证码是@var(code)，请在@var(time)内输入。国际短信模板对应变量如下
    //  变量名和自定义内容相对应即可
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $to = '+81********';                                                            //收信人 手机号码
    $project_id = 'F***U';                                                           //模板ID
    $vars = json_encode(array(                                                      //模板对应变量
        'code' => '1111',
        'time' => '三分钟'
    ));

    $post_data = array(
        "appid"     => $appid,
        "signature" => $appkey,
        "to"        => $to,
        "project"   => $project_id,
        "vars"      => $vars
    );

    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api-v4.mysubmail.com/internationalsms/xsend.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 1,
        CURLOPT_POSTFIELDS     => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);



    /*****************
     * 加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     国际短信-创建/管理AppID中获取
    //手机号支持单个
    //模板ID   国际短信-创建/管理国际短信模板中获得
    //国际短信模板对应变量
    //  若模板为：【SUBMAIL】您的验证码是@var(code)，请在@var(time)内输入。国际短信模板对应变量如下
    //  变量名和自定义内容相对应即可
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $to = '+81********';                                                            //收信人 手机号码
    $project_id = 'F***U';                                                           //模板ID
    $vars = json_encode(array(                                                      //模板对应变量
        'code' => '1111',
        'time' => '三分钟'
    ));

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api-v4.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 0
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output, true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        "appid"        => $appid,
        "to"           => $to,
        "project"      => $project_id,
        "vars"         => $vars,
        "timestamp"    => $timestamp,
        "sign_type"    => 'md5',
        "sign_version" => 2,
    );
    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['vars']);
    ksort($temp);
    reset($temp);
    $tempStr = "";
    foreach ($temp as $key => $value) {
        $tempStr .= $key . "=" . $value . "&amp;";
    }
    $tempStr = substr($tempStr, 0, -1);
    //生成签名
    $post_data['signature'] = md5($appid . $appkey . $tempStr . $appid . $appkey);


    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api-v4.mysubmail.com/internationalsms/xsend.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 1,
        CURLOPT_POSTFIELDS     => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);


```