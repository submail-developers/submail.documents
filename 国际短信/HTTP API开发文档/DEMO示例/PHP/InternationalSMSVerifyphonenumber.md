#DEMEO:InternationalSMS/Verifyphonenumber

<br>

## 代码示列

```
<?php

    //手机号支持单个                               
    $to = '+84********';

    $post_data = array(
        "to"        => $to,                                            //号码
    );

    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/service/verifyphonenumber.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 1,
        CURLOPT_POSTFIELDS     => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);

    echo json_encode($output);



```