### 通用 ###
通常返回的Json格式为
```json
{"code":0,"info":null,"data":[{"name1":"value1","name2":"value2"},{"name1":"value1","name2":"value2"}]}
或
{"code":0,"info":null,"data":{"name1":"value1","name2":"value2"}}
```
错误返回：
```json
{"code":-1,"info":"xxxxxxx","data":null}
```

* code代表返回状态，0为正常返回，负数为出现错误
* info代表出错信息，正常返回为null
* data代表返回的数据，出现错误时返回null


### 案例 ###
#### 首页-获取5条热点案例 ####

```http
http://服务器地址/cases/gethot
```
**返回**：
正确返回：

* code：0
* info：null
* data：Json数组，每条包括：
	* id：案例ID
	* title：案例标题
	* image_id：标题图片标识
	* type：0 //区分案例与新闻
	* created：创建时间

```json
{"code":0,"info":null,"data":[{"id":"4","title":"123","image_id":"2","type":"0","created":"2017-01-02 22:55:01"},{"id":"6","title":"qewrrewtw","image_id":"2","type":"0","created":"2017-01-03 17:31:07"}]}
```

错误返回1：

* code：-1
* info：no more rows!
* data：null
	
错误返回2：

* code：-2
* info：server error!
* data：null
	
#### 详情页-获取案例内容 ####
```http
http://服务器地址/cases/read/:id
```
**请求参数**：
* id：案例ID

```http
http://localhost/tp/public/index.php/cases/read/4
```

**返回**：
正确返回：

* code：0
* info：null
* data：
	* id:案例标识
	* title：案例标题
	* created：创建时间
	* image_id：图像标识
	* identifyimg_id:识别图标识
	* body：案例内容
	* like_num：点赞数目
	* comment_num:评论数目
	* type：0 //区分案例与新闻

```json
{"code":0,"info":null,"data":{"id":"4","title":"123","body":"312323","image_id":"2","identifyimg_id":"0","created":"2017-01-02 22:55:01","like_num":"5","comment_num":"0","type":"0"}}
```

错误返回1：

* code：-1
* info：there's no this row!
* data：null

```json
{"code":-1,"info":"there's no this row!","data":null}
```
	
错误返回2：

* code：-2
* info：server error!
* data：null


### 新闻 ###
#### 首页-获取5条热点新闻 ####

```http
http://服务器地址/news/gethot
```
**返回**：
正确返回：

* code：0
* info：null
* data：Json数组，每条包括：
	* id：新闻ID
	* title：新闻标题
	* image_id：标题图片ID
	* type：1 //区分案例与新闻

```json
{"code":0,"info":null,"data":[{"id":"3","title":"\u5176\u5473\u65e0\u7a77\u82e5","image_id":"3","type":"1","created":"2017-01-03 17:50:42"},{"id":"4","title":"\u989d\u5916\u82e5\u65e0\u7fa4\u82e5","image_id":"0","type":"1","created":"2017-01-03 17:50:55"},{"id":"5","title":"\u4e8c","image_id":"3","type":"1","created":"2017-01-03 17:51:54"}]}
```

错误返回1：

* code：-1
* info：no more rows!
* data：null
	
错误返回2：

* code：-2
* info：server error!
* data：null



#### 详情页-获取新闻内容 ####
```http
http://服务器地址/news/read/:id
```
**请求参数**：
* id：新闻ID

```http
http://localhost/tp/public/index.php/news/read/3
```

**返回**：
正确返回：

* code：0
* info：null
* data：
	* id:新闻标识
	* title：新闻标题
	* created：创建时间
	* image_id：图像标识
	* body：新闻内容
	* like_num：点赞数目
	* comment_num:评论数目
	* type：1 //区分案例与新闻

```json
{"code":0,"info":null,"data":{"id":"3","title":"\u5176\u5473\u65e0\u7a77\u82e5","body":"\u5384\u9f50\u5c14\u7fa4\u65e0\u82e5","image_id":"3","created":"2017-01-03 17:50:42","like_num":"0","comment_num":"0","type":"1"}}
```

错误返回1：

* code：-1
* info：there's no this row!
* data：null
	
```json
{"code":-1,"info":"there's no this row!","data":null}
```

错误返回2：

* code：-2
* info：server error!
* data：null

### 案例与新闻 ###
#### 首页-第一次获取12条最新列表，后续每次6条 ####
```http
http://服务器地址/ncs/getlist/[:last_time]
```
**请求参数**：
* last_time:上次拉取的最后一条的时间，第一次拉取不需要，后续拉取需要

```http
http://localhost/tp/public/index.php/ncs/getlist
http://localhost/tp/public/index.php/ncs/getlist/2017-01-02 22:55:01
```

**返回**：
正确返回：

* code：0
* info：null
* data：Json数组，每条包括：
	* id:案例或新闻标识
	* title：标题
	* image_id：图像标识
	* type：区别案例0或新闻1
	* created：创建时间

```json
{"code":0,"info":null,"data":[{"id":"5","title":"\u4e8c","image_id":"3","type":"1","created":"2017-01-03 17:51:54"},{"id":"4","title":"\u989d\u5916\u82e5\u65e0\u7fa4\u82e5","image_id":"0","type":"1","created":"2017-01-03 17:50:55"},{"id":"3","title":"\u5176\u5473\u65e0\u7a77\u82e5","image_id":"3","type":"1","created":"2017-01-03 17:50:42"},{"id":"6","title":"qewrrewtw","image_id":"2","type":"0","created":"2017-01-03 17:31:07"},{"id":"4","title":"123","image_id":"2","type":"0","created":"2017-01-02 22:55:01"}]}
```

错误返回1：

* code：-1
* info：no more rows!
* data：null

```json
{"code":-1,"info":"there's no this row!","data":null}
```
	
错误返回2：

* code：-2
* info：server error!
* data：null



### 图片 ###
#### 获取原图 ####
```http
http://服务器地址/images/downpic/:id
```
**请求参数**：
* id：图片标识

```http
http://localhost/images/downpic/2
```

**返回**：
正确返回：

* code:0
* info:null
* data:
	* link:缩略图片链接
	
```json
{"code":0,"info":null,"data":{"link":"http://localhost/tp/public/img/123.jpg"}}
```

错误返回：

* code：-1
* info:get image link error!
* data:null

#### 获取缩略图 ####
```http
http://服务器地址/images/read/:id2w
```
**请求参数**：
* id：图片标识

**返回**：
正确返回：

* code:0
* info:null
* data:
	* link:缩略图片链接
	
错误返回：

* code：-1
* info:get image link error!
* data:null

#### 获取相册图片列表，第一次张，后续每次6张 ####
```http
http://服务器地址/images/getlist/[:last_time]
```
**请求参数**：
* last_time:上次拉取的最后一条的时间，第一次拉取不需要，后续拉取需要

```http
http://localhost/tp/public/index.php/images/getlist
http://localhost/tp/public/index.php/images/getlist/2017-01-06 20:53:38
```

**返回**：
正确返回：

* code：0
* info：null
* data：Json数组，每条包括：
	* id:图像标识
	* created：创建时间

```json
{"code":0,"info":null,"data":[{"id":"8","created":"2017-01-06 20:53:56"},{"id":"7","created":"2017-01-06 20:53:38"}]}
```

错误返回1：

* code：-1
* info：no more rows!
* data：null
	
错误返回2：

* code：-2
* info：server error!
* data：null


### 评论 ###
#### 第一次获取20条评论列表，后续每次10条 ####
```http
http://服务器地址/comments/getlist/:id/:type/[:last_time]
```
**请求参数**：
* id：案例或新闻标识
* type：区分案例0或新闻1
* last_time:上次拉取的最后一条的时间，第一次拉取不需要，后续拉取需要

```http
http://localhost/tp/public/index.php/comments/getlist/4/12w
http://localhost/tp/public/index.php/comments/getlist/4/1/2017-01-11 16:02:50
```

**返回**：
正确返回：

* code：0
* info：null
* data：Json数组，每条包括：
	* id：评论标识
	* body：评论内容
	* user：评论用户名
	* created：创建时间

```json
{"code":0,"info":null,"data":[{"id":"5","body":"hsdfhafhabc","user":"aaa","created":"2017-01-11 16:02:50"}]}
```

错误返回1：

* code：-1
* info：no more rows!
* data：null

```json
{"code":-1,"info":"no more rows","data":null}
```
   
错误返回2：
* code：-2
* info：server error!
* data：null

#### 新增评论 ####
```http
http://服务器地址/comments/add/:id/:type
```
**请求参数**：
* id：案例或新闻标识
* type：区分案例0或新闻1
* body：评论内容
* user：评论用户名

```http
http://localhost/comments/add/4/1?body=aaaa&user=bbb
```

**返回**：
正确返回：
* code：0
* info：create success!
* data：null
	      
错误返回：
* code：-1
* info：create failed!
* data：null

### 反馈 ###
#### 新增反馈 ####
```http
http://服务器地址/feedback/add
```
**请求参数**：
* user：反馈用户名
* contact：用户联系方式(可为空)
* body：反馈内容

```http
http://localhost/feedback/add?user=bbb&contact=ccc&body=aaaa
http://localhost/feedback/add?user=bbb&body=aaaa
```

**返回**：
正确返回：
* code：0
* info：create success!
* data：null

错误返回：
* code：-1
* info：create failed!
* data：null
