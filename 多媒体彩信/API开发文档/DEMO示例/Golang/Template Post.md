# DEMO:Template/Post

#### 示例代码

<br>

#### 依赖

```
import (
	"bytes"
	"crypto/md5"
	"encoding/hex"
	"encoding/json"
	"fmt"
	"io"
	"io/ioutil"
	"mime/multipart"
	"net/http"
	"sort"
	"strconv"
	"strings"
)
```

#### 配置信息

```
const (
	API    = "https://api-v4.mysubmail.com/mms/template"
	APPID  = "10***"
	APPKEY = "f8a5**********************778df"
)
```

#### 非加密代码示例

```
    postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = APPKEY
	postdata["mms_title"] = "彩信标题"
	postdata["mms_signature"] = "【SUBMAIL】"
	postdata["mms_subject"] = "彩信模板项目"
	//页面内容代码
	page1 := make(map[string]interface{})
	page2 := make(map[string]interface{})
	page1["text"] = "这是彩信的第一页"
	page2["text"] = "这是彩信的第二页"
	page1["image"] = map[string]string{
		"data": "iVBORw0KGgoAAAANSUhEUgAAAA4AAAAYCAYAAADKx8xXAAABYWlDQ1BrQ0dDb2xvclNwYWNlRGlzcGxheVAzAAAokWNgYFJJLCjIYWFgYMjNKykKcndSiIiMUmB/yMAOhLwMYgwKicnFBY4BAT5AJQwwGhV8u8bACKIv64LMOiU1tUm1XsDXYqbw1YuvRJsw1aMArpTU4mQg/QeIU5MLikoYGBhTgGzl8pICELsDyBYpAjoKyJ4DYqdD2BtA7CQI+whYTUiQM5B9A8hWSM5IBJrB+API1klCEk9HYkPtBQFul8zigpzESoUAYwKuJQOUpFaUgGjn/ILKosz0jBIFR2AopSp45iXr6SgYGRiaMzCAwhyi+nMgOCwZxc4gxJrvMzDY7v////9uhJjXfgaGjUCdXDsRYhoWDAyC3AwMJ3YWJBYlgoWYgZgpLY2B4dNyBgbeSAYG4QtAPdHFacZGYHlGHicGBtZ7//9/VmNgYJ/MwPB3wv//vxf9//93MVDzHQaGA3kAFSFl7jXH0fsAAABsZVhJZk1NACoAAAAIAAQBGgAFAAAAAQAAAD4BGwAFAAAAAQAAAEYBKAADAAAAAQACAACHaQAEAAAAAQAAAE4AAAAAAAAAkAAAAAEAAACQAAAAAQACoAIABAAAAAEAAAAOoAMABAAAAAEAAAAYAAAAADh6st4AAAAJcEhZcwAAFiUAABYlAUlSJPAAAAGVSURBVDgRvZQ7zwFREIbfXetSKYhoRCGUGoVGo1aTaDUSxdYqP8DvkEhEwT8QEpUSlU6iUEhEiEvEMpPs5JwQm0/xnWLznpl5zuWd3TWSyaSDH4b5A8OI0e12nVQq9cbfbjdst1vMZjP0ej04jn4wYzQaObFY7A1UA5fLBbZtY7PZSFgDx+MxJ3w+HyKRCDKZDPx+P8cOhwOq1aqAlqiXaLfb6hSmaWI4HMKyLITDYV5otVpxzVdzHo8H5vO5LJbL5UR/Banq1S4pXi6XorWjBoNBTtC9CCiXy4hGoxw7Ho9YLBafwcFgIAlV7Pd7tFotNQTPo1I13ZWMUofWDndVcjGRSCCfzyObzXI9vQD1el16qYGlUkldlHWlUkGtVmNNDjebTdb6/m8Y0O/3cb/fOZNOp6XCE6TK8/nMQCgU+hsYCAQEcIXnjoVCAW5/T6eTy0F7AYrFIifI1Xg8zo66rlJiOp1ynh6aqxL9INbrNRqNhnyX2o5qPfXter1it9uh0+lgMpmoaRj//s/xdFU7nzL5GXwCoj+HhCbGKa0AAAAASUVORK5CYII=",
		"type": "image/png",
	}
	page2["image"] = map[string]string{
		"data": "iVBORw0KGgoAAAANSUhEUgAAAA4AAAAYCAYAAADKx8xXAAABYWlDQ1BrQ0dDb2xvclNwYWNlRGlzcGxheVAzAAAokWNgYFJJLCjIYWFgYMjNKykKcndSiIiMUmB/yMAOhLwMYgwKicnFBY4BAT5AJQwwGhV8u8bACKIv64LMOiU1tUm1XsDXYqbw1YuvRJsw1aMArpTU4mQg/QeIU5MLikoYGBhTgGzl8pICELsDyBYpAjoKyJ4DYqdD2BtA7CQI+whYTUiQM5B9A8hWSM5IBJrB+API1klCEk9HYkPtBQFul8zigpzESoUAYwKuJQOUpFaUgGjn/ILKosz0jBIFR2AopSp45iXr6SgYGRiaMzCAwhyi+nMgOCwZxc4gxJrvMzDY7v////9uhJjXfgaGjUCdXDsRYhoWDAyC3AwMJ3YWJBYlgoWYgZgpLY2B4dNyBgbeSAYG4QtAPdHFacZGYHlGHicGBtZ7//9/VmNgYJ/MwPB3wv//vxf9//93MVDzHQaGA3kAFSFl7jXH0fsAAABsZVhJZk1NACoAAAAIAAQBGgAFAAAAAQAAAD4BGwAFAAAAAQAAAEYBKAADAAAAAQACAACHaQAEAAAAAQAAAE4AAAAAAAAAkAAAAAEAAACQAAAAAQACoAIABAAAAAEAAAAOoAMABAAAAAEAAAAYAAAAADh6st4AAAAJcEhZcwAAFiUAABYlAUlSJPAAAAGVSURBVDgRvZQ7zwFREIbfXetSKYhoRCGUGoVGo1aTaDUSxdYqP8DvkEhEwT8QEpUSlU6iUEhEiEvEMpPs5JwQm0/xnWLznpl5zuWd3TWSyaSDH4b5A8OI0e12nVQq9cbfbjdst1vMZjP0ej04jn4wYzQaObFY7A1UA5fLBbZtY7PZSFgDx+MxJ3w+HyKRCDKZDPx+P8cOhwOq1aqAlqiXaLfb6hSmaWI4HMKyLITDYV5otVpxzVdzHo8H5vO5LJbL5UR/Banq1S4pXi6XorWjBoNBTtC9CCiXy4hGoxw7Ho9YLBafwcFgIAlV7Pd7tFotNQTPo1I13ZWMUofWDndVcjGRSCCfzyObzXI9vQD1el16qYGlUkldlHWlUkGtVmNNDjebTdb6/m8Y0O/3cb/fOZNOp6XCE6TK8/nMQCgU+hsYCAQEcIXnjoVCAW5/T6eTy0F7AYrFIifI1Xg8zo66rlJiOp1ynh6aqxL9INbrNRqNhnyX2o5qPfXter1it9uh0+lgMpmoaRj//s/xdFU7nzL5GXwCoj+HhCbGKa0AAAAASUVORK5CYII=",
		"type": "image/png",
	}
	mms_content := [2]map[string]interface{}{page1, page2}
	mms_content_bytes, _ := json.Marshal(mms_content)
	postdata["mms_content"] = string(mms_content_bytes)

	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range postdata {
		_ = writer.WriteField(key, val)
	}
	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))

```



#### 加密代码示例

```
    //所需参数
	postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = APPKEY
	postdata["mms_title"] = "彩信标题"
	postdata["mms_signature"] = "【SUBMAIL】"
	postdata["mms_subject"] = "彩信模板项目"
	//页面内容代码
	page1 := make(map[string]interface{})
	page2 := make(map[string]interface{})
	page1["text"] = "这是彩信的第一页"
	page2["text"] = "这是彩信的第二页"
	page1["image"] = map[string]string{
		"data": "iVBORw0KGgoAAAANSUhEUgAAAA4AAAAYCAYAAADKx8xXAAABYWlDQ1BrQ0dDb2xvclNwYWNlRGlzcGxheVAzAAAokWNgYFJJLCjIYWFgYMjNKykKcndSiIiMUmB/yMAOhLwMYgwKicnFBY4BAT5AJQwwGhV8u8bACKIv64LMOiU1tUm1XsDXYqbw1YuvRJsw1aMArpTU4mQg/QeIU5MLikoYGBhTgGzl8pICELsDyBYpAjoKyJ4DYqdD2BtA7CQI+whYTUiQM5B9A8hWSM5IBJrB+API1klCEk9HYkPtBQFul8zigpzESoUAYwKuJQOUpFaUgGjn/ILKosz0jBIFR2AopSp45iXr6SgYGRiaMzCAwhyi+nMgOCwZxc4gxJrvMzDY7v////9uhJjXfgaGjUCdXDsRYhoWDAyC3AwMJ3YWJBYlgoWYgZgpLY2B4dNyBgbeSAYG4QtAPdHFacZGYHlGHicGBtZ7//9/VmNgYJ/MwPB3wv//vxf9//93MVDzHQaGA3kAFSFl7jXH0fsAAABsZVhJZk1NACoAAAAIAAQBGgAFAAAAAQAAAD4BGwAFAAAAAQAAAEYBKAADAAAAAQACAACHaQAEAAAAAQAAAE4AAAAAAAAAkAAAAAEAAACQAAAAAQACoAIABAAAAAEAAAAOoAMABAAAAAEAAAAYAAAAADh6st4AAAAJcEhZcwAAFiUAABYlAUlSJPAAAAGVSURBVDgRvZQ7zwFREIbfXetSKYhoRCGUGoVGo1aTaDUSxdYqP8DvkEhEwT8QEpUSlU6iUEhEiEvEMpPs5JwQm0/xnWLznpl5zuWd3TWSyaSDH4b5A8OI0e12nVQq9cbfbjdst1vMZjP0ej04jn4wYzQaObFY7A1UA5fLBbZtY7PZSFgDx+MxJ3w+HyKRCDKZDPx+P8cOhwOq1aqAlqiXaLfb6hSmaWI4HMKyLITDYV5otVpxzVdzHo8H5vO5LJbL5UR/Banq1S4pXi6XorWjBoNBTtC9CCiXy4hGoxw7Ho9YLBafwcFgIAlV7Pd7tFotNQTPo1I13ZWMUofWDndVcjGRSCCfzyObzXI9vQD1el16qYGlUkldlHWlUkGtVmNNDjebTdb6/m8Y0O/3cb/fOZNOp6XCE6TK8/nMQCgU+hsYCAQEcIXnjoVCAW5/T6eTy0F7AYrFIifI1Xg8zo66rlJiOp1ynh6aqxL9INbrNRqNhnyX2o5qPfXter1it9uh0+lgMpmoaRj//s/xdFU7nzL5GXwCoj+HhCbGKa0AAAAASUVORK5CYII=",
		"type": "image/png",
	}
	page2["image"] = map[string]string{
		"data": "iVBORw0KGgoAAAANSUhEUgAAAA4AAAAYCAYAAADKx8xXAAABYWlDQ1BrQ0dDb2xvclNwYWNlRGlzcGxheVAzAAAokWNgYFJJLCjIYWFgYMjNKykKcndSiIiMUmB/yMAOhLwMYgwKicnFBY4BAT5AJQwwGhV8u8bACKIv64LMOiU1tUm1XsDXYqbw1YuvRJsw1aMArpTU4mQg/QeIU5MLikoYGBhTgGzl8pICELsDyBYpAjoKyJ4DYqdD2BtA7CQI+whYTUiQM5B9A8hWSM5IBJrB+API1klCEk9HYkPtBQFul8zigpzESoUAYwKuJQOUpFaUgGjn/ILKosz0jBIFR2AopSp45iXr6SgYGRiaMzCAwhyi+nMgOCwZxc4gxJrvMzDY7v////9uhJjXfgaGjUCdXDsRYhoWDAyC3AwMJ3YWJBYlgoWYgZgpLY2B4dNyBgbeSAYG4QtAPdHFacZGYHlGHicGBtZ7//9/VmNgYJ/MwPB3wv//vxf9//93MVDzHQaGA3kAFSFl7jXH0fsAAABsZVhJZk1NACoAAAAIAAQBGgAFAAAAAQAAAD4BGwAFAAAAAQAAAEYBKAADAAAAAQACAACHaQAEAAAAAQAAAE4AAAAAAAAAkAAAAAEAAACQAAAAAQACoAIABAAAAAEAAAAOoAMABAAAAAEAAAAYAAAAADh6st4AAAAJcEhZcwAAFiUAABYlAUlSJPAAAAGVSURBVDgRvZQ7zwFREIbfXetSKYhoRCGUGoVGo1aTaDUSxdYqP8DvkEhEwT8QEpUSlU6iUEhEiEvEMpPs5JwQm0/xnWLznpl5zuWd3TWSyaSDH4b5A8OI0e12nVQq9cbfbjdst1vMZjP0ej04jn4wYzQaObFY7A1UA5fLBbZtY7PZSFgDx+MxJ3w+HyKRCDKZDPx+P8cOhwOq1aqAlqiXaLfb6hSmaWI4HMKyLITDYV5otVpxzVdzHo8H5vO5LJbL5UR/Banq1S4pXi6XorWjBoNBTtC9CCiXy4hGoxw7Ho9YLBafwcFgIAlV7Pd7tFotNQTPo1I13ZWMUofWDndVcjGRSCCfzyObzXI9vQD1el16qYGlUkldlHWlUkGtVmNNDjebTdb6/m8Y0O/3cb/fOZNOp6XCE6TK8/nMQCgU+hsYCAQEcIXnjoVCAW5/T6eTy0F7AYrFIifI1Xg8zo66rlJiOp1ynh6aqxL9INbrNRqNhnyX2o5qPfXter1it9uh0+lgMpmoaRj//s/xdFU7nzL5GXwCoj+HhCbGKa0AAAAASUVORK5CYII=",
		"type": "image/png",
	}
	mms_content := [2]map[string]interface{}{page1, page2}
	mms_content_bytes, _ := json.Marshal(mms_content)
	postdata["mms_content"] = string(mms_content_bytes)

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
	sign["mms_title"] = postdata["mms_title"]
	sign["mms_signature"] = postdata["mms_signature"]
	sign["mms_subject"] = postdata["mms_subject"]
	sign["mms_content"] = postdata["mms_content"]
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

	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range postdata {
		_ = writer.WriteField(key, val)
	}
	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))
	
```