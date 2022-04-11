# DEMO:Template/Put

### 示例代码

<br>

#### 依赖

```
import (
	"crypto/md5"
	"encoding/hex"
	"encoding/json"
	"fmt"
	"io"
	"io/ioutil"
	"net/http"
	"sort"
	"strconv"
	"strings"
)
```

#### 配置信息

```
const (
	API    = "https://api-v4.mysubmail.com/internationalsms/template"
	APPID  = "10***"
	APPKEY = "f8a5**********************778df"
)
```

#### 非加密代码示例

```
    postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = APPKEY
	postdata["template_id"] = "zcMxF4"
	postdata["sms_title"] = "短信标题" //此标题无实际使用意义
	postdata["sms_content"] = "Your verification code is @var(code), please enter it within @var(time)minutes."

	data_str, _ := json.Marshal(postdata)
	data := strings.NewReader(string(data_str))
	req, _ := http.NewRequest("PUT", API, data)
	req.Header.Add("Content-Type", "application/json")
	resp, _ := http.DefaultClient.Do(req)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))

```



#### 加密代码示例

```
    //所需参数
	postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = ""
	postdata["template_id"] = "zcMxF4"
	postdata["sms_title"] = "title"
	postdata["sms_content"] = "Your verification code is @var(code), please enter it within @var(time)minutes."
	postdata["timestamp"] = ""
	postdata["sign_type"] = "md5"
	//获取服务器时间戳，该时间戳为 UNIX 时间戳，也可以自己生成
	q, _ := http.Get("https://api-v4.mysubmail.com/service/timestamp")
	r, _ := ioutil.ReadAll(q.Body)
	m := make(map[string]float64)
	json.Unmarshal(r, &amp;m)
	postdata["timestamp"] = strconv.FormatFloat(m["timestamp"], 'f', -1, 64)
	//签名加密
	sign := make(map[string]string)
	sign["appid"] = postdata["appid"]
	sign["template_id"] = postdata["template_id"]
	sign["sms_title"] = postdata["sms_title"]
	sign["sms_content"] = postdata["sms_content"]
	sign["timestamp"] = postdata["timestamp"]
	sign["sign_type"] = postdata["sign_type"]
	keys := make([]string, 0, 32)
	for key, _ := range sign {
		keys = append(keys, key)
	}
	sort.Strings(keys)
	sign_list := make([]string, 0, 32)
	for _, key := range keys {
		sign_list = append(sign_list, key+"="+sign[key])
	}
	sign_str := APPID + APPKEY + strings.Join(sign_list, "&amp;") + APPID + APPKEY
	mymd5 := md5.New()
	io.WriteString(mymd5, sign_str)
	postdata["signature"] = hex.EncodeToString(mymd5.Sum(nil))

	//PUT请求
	data_str, _ := json.Marshal(postdata)
	data := strings.NewReader(string(data_str))
	req, _ := http.NewRequest("PUT", API, data)
	req.Header.Add("Content-Type", "application/json")
	resp, _ := http.DefaultClient.Do(req)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))
	
```