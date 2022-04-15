# DEMO: Group/Get - 获取短网址群组

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
	API    = "https://service.mysubmail.com/shorturl/group"
	APPID  = "10***"
	APPKEY = "f8a5**********************778df"
)
```

#### 非加密代码示例

```
    data := make(map[string]string)
	data["appid"] = APPID
	data["signature"] = APPKEY
	var data_str string
	data_arr := make([]string, 0, 32)
	for k, v := range data {
		data_arr = append(data_arr, k+"="+v)
	}
	data_str = strings.Join(data_arr, "&amp;")
	q, _ := http.Get(API + "?" + data_str)
	r, _ := ioutil.ReadAll(q.Body)
	m := make(map[string]interface{})
	json.Unmarshal(r, &amp;m)
	fmt.Println(m)

```



#### 加密代码示例

```
    data := make(map[string]string)
	data["appid"] = APPID
	data["signature"] = ""
	data["sign_type"] = "md5"
	//获取服务器时间戳，该时间戳为 UNIX 时间戳，也可以自己生成
	q, _ := http.Get("https://api.mysubmail.com/service/timestamp")
	r, _ := ioutil.ReadAll(q.Body)
	t := make(map[string]float64)
	json.Unmarshal(r, &amp;t)
	data["timestamp"] = strconv.FormatFloat(t["timestamp"], 'f', -1, 64)
	//签名加密
	sign := make(map[string]string)
	sign["appid"] = data["appid"]
	sign["timestamp"] = data["timestamp"]
	sign["sign_type"] = data["sign_type"]
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
	data["signature"] = hex.EncodeToString(mymd5.Sum(nil))

	var data_str string
	data_arr := make([]string, 0, 32)
	for k, v := range data {
		data_arr = append(data_arr, k+"="+v)
	}
	data_str = strings.Join(data_arr, "&amp;")
	resonse, _ := http.Get(API + "?" + data_str)
	result, _ := ioutil.ReadAll(resonse.Body)
	m := make(map[string]interface{})
	json.Unmarshal(result, &amp;m)
	fmt.Println(m)
	
```