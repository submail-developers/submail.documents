# DEMO:Factor/Simple

<br>

## 概览
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

<br>

## 代码示例

```java
package com.submail.demo.factor;
import com.alibaba.fastjson.JSONObject;
import com.submail.demo.RequestEncoder;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;
import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.util.TreeMap;

public class FactorSimple {
    public static final String TIMESTAMP = "https://api.mysubmail.com/service/timestamp";
    private static final String URL = "https://tpa.mysubmail.com/factor/simple.json";

    public static void main(String[] args) throws UnsupportedEncodingException {
        TreeMap<String, String> requestData = new TreeMap<String, String>();
        String appid = "";
        String appkey = "";
        String name="";
        String idNo = "";
        String mobile="";
        //组合请求数据
        requestData.put("appkey",appkey);
        requestData.put("name", URLEncoder.encode(name,"UTF-8"));
        requestData.put("idNo", idNo);
        requestData.put("mobile", mobile);
        requestData.put("timestamp",getTimestamp());
        String signStr = RequestEncoder.formatRequest(requestData);
        requestData.put("signature", RequestEncoder.encode("SHA-256", signStr));
        requestData.put("appid", appid);
        requestData.remove("appkey");
        System.out.println("requestData = " + requestData);
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

    //获取时间戳
    private static String getTimestamp() {
        CloseableHttpClient closeableHttpClient = HttpClientBuilder.create().build();
        HttpGet httpget = new HttpGet(TIMESTAMP);
        try {
            HttpResponse response = closeableHttpClient.execute(httpget);
            HttpEntity httpEntity = response.getEntity();
            String jsonStr = EntityUtils.toString(httpEntity, "UTF-8");
            if (jsonStr != null) {
                JSONObject json = JSONObject.parseObject(jsonStr);
                return json.getString("timestamp");
            }
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

---
### RequestEncoder

```java
package com.submail.demo;

/**
 * @author zhang
 * @date 2021/8/4 - 5:52 下午
 */

import java.security.MessageDigest;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;

public class RequestEncoder {
    private static final char[] HEX_DIGITS = {'0', '1', '2', '3', '4', '5',
            '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};

    public static String encode(String algorithm, String str) {
        if (str == null) {
            return null;
        }
        try {
            MessageDigest messageDigest = MessageDigest.getInstance(algorithm);
            messageDigest.update(str.getBytes("UTF-8"));
            return getFormattedText(messageDigest.digest());
        } catch (Exception e) {
            throw new RuntimeException(e);
        }

    }

    private static String getFormattedText(byte[] bytes) {
        int len = bytes.length;
        StringBuilder buf = new StringBuilder(len * 2);
        for (int j = 0; j < len; j++) {
            buf.append(HEX_DIGITS[(bytes[j] >> 4) &amp; 0x0f]);
            buf.append(HEX_DIGITS[bytes[j] &amp; 0x0f]);
        }
        return buf.toString();
    }

    public static String formatRequest(Map<String, String> data) {
        Set<String> keySet = data.keySet();
        Iterator<String> it = keySet.iterator();
        StringBuffer sb = new StringBuffer();
        while (it.hasNext()) {
            String key = it.next();
            Object value = data.get(key);
            if (value instanceof String) {
                sb.append(key + "=" + value + "&amp;");
            }
        }
        if (sb.length() != 0) {
            System.out.println("sb.substring(0, sb.length() - 1) = " + sb.substring(0, sb.length() - 1));
            return sb.substring(0, sb.length() - 1);
        }
        return null;
    }
}
```