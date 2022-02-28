# DEMO:ShortUrl

<br>

## 代码示例
<br>
```
<?php
    /*****************
     * 非加密请求 示例代码
     ******************/
    //---------------------------------get  获取短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址   短网址-创建/管理短网址模板中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $short_url = 'https://******.cn/******';                                        //短网址

    $post_data = array(
        'appid'     => $appid,
        'signature' => $appkey,
        'short_url' => $short_url
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => "https://service.mysubmail.com/shorturl?".http_build_query($post_data) ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------post  创建短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //目标网址
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $url = 'https://www.*********.com';                                             //目标网址

    $post_data = array(
        'appid'     => $appid ,
        'signature' => $appkey ,
        'url'       => $url ,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl' ,
        CURLOPT_RETURNTRANSFER  => 1,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------put 更新短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址   短网址-创建/管理短网址模板中获得
    //目标网址
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $short_url = 'https://******.cn/******';                                        //短网址
    $url = 'https://www.*********.com';                                             //目标网址

    $post_data = array(
        'appid'     => $appid,
        'signature' => $appkey,
        'short_url' => $short_url,
        'url'       => $url,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'PUT',
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);




    //---------------------------------delete 删除短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址   短网址-创建/管理短网址模板中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $short_url = 'https://******.cn/******';                                        //短网址

    $post_data = array(
        'appid'     =>  $appid,
        'signature' =>  $appkey,
        'short_url' =>  $short_url,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL => 'https://service.mysubmail.com/shorturl',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'DELETE' ,
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);




    /*****************
     * 加密请求 示例代码
     ******************/
    //---------------------------------get  获取短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址   短网址-创建/管理短网址模板中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $short_url = 'https://******.cn/******';                                        //短网址

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output, true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        "appid"         => $appid ,
        "short_url"     => $short_url ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['short_url']);
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
    curl_setopt_array($ch , array(
        CURLOPT_URL             => "https://service.mysubmail.com/shorturl?".http_build_query($post_data) ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);




    //---------------------------------post  创建短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //目标网址
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $url = 'https://www.*********.com';                                             //目标网址

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output, true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        "appid"         => $appid ,
        "url"           => $url ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['url']);
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
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl' ,
        CURLOPT_RETURNTRANSFER  => 1,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------put 更新短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址   短网址-创建/管理短网址模板中获得
    //目标网址
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $short_url = 'https://******.cn/******';                                        //短网址
    $url = 'https://www.*********.com';                                             //目标网址

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output, true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        "appid"         => $appid ,
        "short_url"     => $short_url ,
        'url'           => $url ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['url']);
    unset($temp['short_url']);
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
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'PUT',
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------delete 删除短网址数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址   短网址-创建/管理短网址模板中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $short_url = 'https://******.cn/******';                                        //短网址

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output, true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        "appid"         => $appid ,
        "short_url"     => $short_url ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['short_url']);
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
    curl_setopt_array($ch , array(
        CURLOPT_URL => 'https://service.mysubmail.com/shorturl',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'DELETE' ,
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);

```