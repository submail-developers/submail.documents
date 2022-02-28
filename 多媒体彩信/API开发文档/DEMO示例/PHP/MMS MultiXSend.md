# DEMO:MMS/MultiXSend

<br>

## 代码示例

```

    <?php
    /*****************
     * 非加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     彩信-创建/管理AppID中获取
    //手机号支持一个/多个， 放到手机号码列表中即可
    //模板ID   彩信-创建/管理彩信模板中获得
    //彩信模板对应变量
    //  若模板为：【SUBMAIL】您的验证码是@var(code)，请在@var(time)内输入。彩信模板对应变量如下
    //  变量名和自定义内容相对应即可
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $to_address_array = array('153xxxxxxxx','152xxxxxxxx');                         //收信人 手机号码列表
    $project = "F***U";                                                             //彩信模板ID
    $multi = array();
    foreach ($to_address_array as $value) {
        $multi[] = array(
            'to'    => $value,
            'vars'  => array('code' => '1111','time' => '三分钟')                    //彩信模板对应变量
        );
    }

    $post_data = array(
        "appid"     => $appid,
        "signature" => $appkey,
        "project"   => $project,
        "multi"     => json_encode($multi),
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/mms/multixsend.json',
        CURLOPT_RETURNTRANSFER  => 1,
        CURLOPT_POST            => 1,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);




    /*****************
     * 加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     彩信-创建/管理AppID中获取
    //手机号支持一个/多个， 放到手机号码列表中即可
    //模板ID   彩信-创建/管理彩信模板中获得
    //彩信模板对应变量
    //  若模板为：【SUBMAIL】您的验证码是@var(code)，请在@var(time)内输入。彩信模板对应变量如下
    //  变量名和自定义内容相对应即可
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $to_address_array = array('153xxxxxxxx','152xxxxxxxx');                         //收信人 手机号码列表
    $project = "F***U";                                                             //彩信模板ID
    $multi = array();
    foreach ($to_address_array as $value) {
        $multi[] = array(
            'to'    => $value,
            'vars'  => array('code' => '1111','time' => '三分钟')                    //彩信模板对应变量
        );
    }

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER  => 1,
        CURLOPT_POST            => 0
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        "appid"         => $appid,
        "project"       => $project,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
        "sign_version"  => 2,
        "multi"         => json_encode($multi),
    );
    $temp = $post_data;
    unset($temp['multi']);
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
        CURLOPT_URL             => 'https://api.mysubmail.com/mms/multixsend.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data,
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);


```