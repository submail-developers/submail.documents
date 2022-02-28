# DEMO:ShortUrl/Group
<br>

## 代码示例

<br>

### 短网址群组

```
<?php
    /*****************
    *
    * 非加密请求 示例代码
    *
    ******************/
    //---------------------------------get  获取短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组ID   短网址-创建/管理短网址群组中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $group = 'f3***************************f1';                                     //短网址群组ID

    $post_data = array(
        'appid'     => $appid,
        'signature' => $appkey,
        'group'     => $group,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => "https://service.mysubmail.com/shorturl/group?".http_build_query($post_data) ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);


    //---------------------------------post  生成短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组昵称
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $name = '短网址群组昵称';                                                          //短网址群组昵称

    $post_data = array(
        'appid'     => $appid ,
        'signature' => $appkey ,
        'name'      => $name
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl/group' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------put 更新短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组ID   短网址-创建/管理短网址群组中获得
    //短网址群组昵称
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $group = 'f3***************************f1';                                     //短网址群组ID
    $name = '短网址群组昵称';                                                          //短网址群组昵称

    $post_data = array(
        'appid'     => $appid ,
        'signature' => $appkey ,
        'group'     => $group ,
        'name'      => $name
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl/group' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'PUT' ,
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------delete 删除短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组ID   短网址-创建/管理短网址群组中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $group = 'f3***************************f1';                                     //短网址群组ID

    $post_data = array(
        'appid'     => $appid ,
        'signature' => $appkey ,
        'group'     => $group ,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl/group' ,
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
    //---------------------------------get  获取短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组ID   短网址-创建/管理短网址群组中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $group = 'f3***************************f1';                                     //短网址群组ID

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
        "group"         => $group ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['group']);
    ksort($temp);
    reset($temp);
    $tempStr = "";
    foreach ($temp as $key => $value) {
        $tempStr .= $key . "=" . $value . "&amp;";
    }
    $tempStr = substr($tempStr, 0, count($tempStr) - 2);
    //生成签名
    $post_data['signature'] = md5($appid . $appkey . $tempStr . $appid . $appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => "https://service.mysubmail.com/shorturl/group?".http_build_query($post_data) ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------post  生成短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组昵称
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $name = '短网址群组昵称';                                                          //短网址群组昵称

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
        "name"          => $name ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['name']);
    ksort($temp);
    reset($temp);
    $tempStr = "";
    foreach ($temp as $key => $value) {
        $tempStr .= $key . "=" . $value . "&amp;";
    }
    $tempStr = substr($tempStr, 0, count($tempStr) - 2);
    //生成签名
    $post_data['signature'] = md5($appid . $appkey . $tempStr . $appid . $appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl/group' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------put 更新短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组ID   短网址-创建/管理短网址群组中获得
    //短网址群组昵称
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $group = 'f3***************************f1';                                     //短网址群组ID
    $name = '短网址群组昵称';                                                          //短网址群组昵称

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
        "name"          => $name ,
        "group"         => $group ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['name']);
    unset($temp['group']);
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
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl/group' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'PUT' ,
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);




    //---------------------------------delete 删除短网址群组数据-------------------------------------
    //appid参数 appkey参数在     短网址-创建/管理AppID中获取
    //短网址群组ID   短网址-创建/管理短网址群组中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $group = 'f3***************************f1';                                     //短网址群组ID

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
        "group"         => $group ,
        "timestamp"     => $timestamp,
        "sign_type"     => 'md5',
    );

    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['group']);
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
        CURLOPT_URL             => 'https://service.mysubmail.com/shorturl/group' ,
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