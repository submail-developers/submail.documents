# DEMEO:InternationalSMS/Verifyphonenumber

- 支持JDK版本：1.5以上 
- 依赖的jar包：httpclient-4.5.3.jar、httpcore-4.4.14.jar、commons-logging1.1.1.jar、fastjson-1.2.75.jar


```java
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.3</version>
</dependency>
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpcore</artifactId>
    <version>4.4.14</version>
</dependency>
<dependency>
    <groupId>commons-logging</groupId>
    <artifactId>commons-logging</artifactId>
    <version>1.1.1</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.75</version>
</dependency>
```

## 代码示列
### VerifyphonenumberDemo
```java
package com.submail.demo.intersms;
import com.alibaba.fastjson.JSONObject;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.util.TreeMap;

public class Verifyphonenumber {
    public static final String TIMESTAMP = "https://api.mysubmail.com/service/timestamp";
    private static final String URL = "https://api.mysubmail.com/service/verifyphonenumber.json";
    public static final String TYPE_MD5 = "md5";
    public static final String TYPE_SHA1 = "sha1";

    public static void main(String[] args) {
        TreeMap<String, String> requestData = new TreeMap<String, String>();
        String to = "+86176xxxx5149";
        requestData.put("to", to);
        //post请求
        HttpPost httpPost = new HttpPost(URL);
        httpPost.setHeader("Accept", "application/json");
        httpPost.setHeader("Content-Type", "application/json");
        StringEntity entity = new StringEntity(JSONObject.toJSONString(requestData), "UTF-8");
        httpPost.setEntity(entity);
        try {
            CloseableHttpClient closeableHttpClient = HttpClientBuilder.create().build();
            HttpResponse response = closeableHttpClient.execute(httpPost);
            HttpEntity httpEntity = response.getEntity();
            if (httpEntity != null) {
                String jsonStr = EntityUtils.toString(httpEntity, "UTF-8");
                System.out.println(jsonStr);
            }
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```