# 映像

<!-- toc -->

## POST /images

**创建映像**

*将已关机的主机创建为映像*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| instance | String | Yes |  要被制作成的主机ID  |
| image_name | String | No | 映像名称 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://dev2.51idc.cn/v2/zone/ac1/images" --data '
{ 
    "instance":"i-IN234BH",
    "image_name":"TEST"
}'
```

#### 响应内容:


## DELETE /images/:img_id

**删除映像**

*详细描述*

### 请求

#### 请求 Query 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| img_id | String[] | Yes |  需要删除的映像ID  |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XDELETE "http://dev2.51idc.cn/v2/zone/ac1/images/img-9SSE88S,img-992IIII" --data '
'
```

#### 响应内容:

## PUT /images

**修改映像属性**

*详细描述*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| image | String | Yes |  需要修改的映像ID  |
| image_name | String | No |  要修改的映像名称  |
| description | String | No |  要修改的映像描述  |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPUT "http://dev2.51idc.cn/v2/zone/ac1/images" --data '
{
       "image":"img-IDNC88D",
	   "image_name":"TEST",
	   "description":"note"
}
'
```

#### 响应内容:

## GET /images

**获取映像列表**

*详细描述*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| images | String[] | No |  要过滤的映像列表  |
| processor_type | String | No |  映像支持的处理器类型，有效值为 64bit 和 32bit  |
| os_family | String | No |  映像操作系统发行版，有效值为 centos，ubuntu，debian，fedora 和 windows 等  |
| visibility | String | No |  映像的可见范围，有效值为 public 和 private  |
| provider | String | No |  映像提供者。初始青云系统会提供一系列默认映像，其 provider 为 system 。 当用户捕获主机后，被捕获的“自有”映像的 provider 为 self 。  |
| status | String[] | No |  映像状态: pending, available, deprecated, suspended, deleted, ceased  |
| search_word | String | No |  搜索关键词，支持映像ID，映像名称  |
| offset | String | No |  数据偏移量，默认为0  |
| limit | String | No |  返回数据长度，默认为10，最大100  |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| create_time | String | No |  创建时间  |
| default_passwd | String | No |  映像默认密码  |
| size | String | No |  映像空间大小，单位为 GB  |
| platform | String | No |  映像操作系统平台，有效值为 linux 和 windows  |
| provider | String | No |  映像提供者。初始青云系统会提供一系列默认映像，其 provider 为 system 。 当用户捕获主机后，被捕获的“自有”映像的 provider 为 self 。  |
| status_time | String | No |  状态产生时间  |
| status | String | No |  映像状态  |
| description | String | No |  映像描述  |
| image_id | String | No |  映像ID  |
| image_name | String | No |  映像名称  |
| transition_status | String | No |  过渡状态  |
| visibility | String | No |  映像的可见范围，有效值为 public 和 private  |
| os_family | String | No |  映像操作系统发行版，有效值为 centos，ubuntu，debian，fedora 和 windows 等  |
| default_user | String | No |  默认用户  |
| processor_type | String | No |  映像支持的处理器类型，有效值为 64bit 和 32bit  |
| recommended_type | String | No |  运行该映像的推荐主机配置  |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://dev2.51idc.cn/v2/zone/ac1/images" --data '
'
```

#### 响应内容:

## POST /check_users

**验证用户名是否可用**


### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| image | String | Yes |  要验证的镜像id  |
| username | String | Yes | 要验证的用户名 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://dev2.51idc.cn/v2/zone/ac1/check_users" --data '
{
    "instance":"i-IN234BH",
    "image_name":"TEST"
}'
```

#### 响应内容:


## POST /image_users

**获取镜像已共享的用户列表**


### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| image | String | Yes |  要验证的镜像id  |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://dev2.51idc.cn/v2/zone/ac1/image_users" --data '
{
    "instance":"i-IN234BH",
    "image_name":"TEST"
}'
```

#### 响应内容:


## POST /image_shared

**共享镜像给用户**


### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| usernames | String[] | Yes |  要共享给的用户  |
| image | string | Yes |  要共享的镜像ID  |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://dev2.51idc.cn/v2/zone/ac1/image_users" --data '
{
    "instance":"i-IN234BH",
    "image_name":"TEST"
}'
```

#### 响应内容:



## POST /image_unshared

**取消镜像共享**


### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| users | String[] | Yes |  要取消共享给的用户  |
| image | string | Yes |  要取消共享的镜像ID  |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://dev2.51idc.cn/v2/zone/ac1/image_users" --data '
{
    "instance":"i-IN234BH",
    "image_name":"TEST"
}'
```

#### 响应内容:


