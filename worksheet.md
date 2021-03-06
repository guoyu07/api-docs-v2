# 工单

<!-- toc -->

## GET /event_type

**获取事件类型列表**

### 示例

#### 发送请求

```bash

$ curl -XGET "http://api.51idc.com/v2/event_type"

```

#### 响应内容:

```js

{

 "key": "value"

}

```

## GET /datacenter

**获取数据中心列表**

### 示例

#### 发送请求

```bash

$ curl -XGET "http://api.51idc.com/v2/datacenter"

```

#### 响应内容:

```js

{

 "key": "value"

}

```

## GET /tickets

**获取工单列表**

*详细描述*

### 请求

#### Body 参数
| 参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| end_time | String | NO | 工单结束时间 |
| start_time | String | NO | 工单开始时间 |
| ticket_state | String | NO | 工单状态(TODO,DOING,DONE,CLOSED) |
| search_word | String | NO | 搜索关键词，支持工单编号，名称 |
| business_type | String | NO | 业务类型(CLOUD,IDC) |
| offset | Int | NO | 数据偏移量，默认为0 |
| limit | Int | NO | 默认值: 10|
| event_type | String | NO | 事件类型 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| tickets | Objects | Yes | 工单列表 |
| total_count | Int | Yes | 根据过滤条件得到的总数 |

### tickets

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| title | String | Yes | 工单标题 |
| id | Int | Yes | 工单编号 |
| state | String | Yes | 工单状态 (TODO,DOING,DONE,CLOSED) |
| business_type | String | Yes | 业务类型(CLOUD,IDC) |
| event_type | String | Yes | 事件类型 |
| datacenter | String | Yes | 数据中心 |
| device_info | String | Yes | 设备信息 |
| create_time | String | Yes | 创建时间 |
| update_time | double | Yes | 更新时间 |


### 示例

#### 发送请求

```bash

$ curl -XGET "http://api.51idc.com/v2/tickets"

```

#### 响应内容:

```js

{

 "key": "value"

}

```


## POST /ticket

**提交工单**

*详细描述*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| title | String | Yes | 工单标题 |
| business_type | String | Yes | 业务类型(IDC,CLOUD) |
| event_type | String | Yes | 事件类型 |
| device_info | String | Yes |  设备信息 |
| datacenter | String | Yes | 数据中心 |
| content | String | Yes | 工单内容 |
| secret_content | String | Yes | 机密信息 |
| contacts_email | String | Yes | 联系人邮箱 |
| contacts_phone | String | Yes | 联系人电话 |
| contacts_name | String | Yes | 联系人名称 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/ticket" --data '
{
    "key": "value"
}'
```

#### 响应内容:

```js
{
    "key": "value"
}
```


## GET /ticket/:id

**获取工单详情**

*详细描述*

### 请求

#### Body 参数
| 参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| id | String | Yes | 工单编号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| title | String | Yes | 工单标题 |
| state | String | Yes | 工单状态 (TODO,DOING,DONE,CLOSED) |
| business_type | String | Yes | 业务类型(CLOUD,IDC) |
| event_type | String | Yes | 事件类型 |
| datacenter | String | Yes | 数据中心 |
| device_info | String | Yes | 设备信息 |
| create_time | String | Yes | 创建时间 |
| update_time | String | Yes | 更新时间 |
| charge_one_name | String | Yes | 工单第一负责人 |
| charge_two_name | String | Yes | 工单第二负责人 |
| content | String | Yes | 工单内容 |
| contacts_phone | String | Yes | 联系人电话 |
| contacts_email | String | Yes | 联系人邮箱 |
| contacts_name | String | Yes | 联系人名称 |
| create_type | String | Yes | 创建人类型(cus,ser) |


### 示例

#### 发送请求

```bash

$ curl -XGET "http://api.51idc.com/v2/ticket/:id"

```

#### 响应内容:

```js

{

 "key": "value"

}

```


## GET /reply/:id

**获取回复详情**

*详细描述*

### 请求

#### Body 参数
| 参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| id | String | NO | 工单编号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| ReplyDetail | List | Yes | 回复详情 |


#### ReplyDetail
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| reply_name  | String | Yes | 回复人 |
| reply_time  | String | Yes | 回复时间 |
| reply_content  | String | Yes | 回复内容 |
| reply_type  | String | Yes | 回复类型(cus,ser) |


### 示例

#### 发送请求

```bash

$ curl -XGET "http://api.51idc.com/v2/reply/:id"

```

#### 响应内容:

```js

{

 "key": "value"

}

```


## POST /reply

**提交回复**

*详细描述*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| content | String | Yes | 回复内容 |
| secret_content | String | Yes | 机密信息 |
| id | String | Yes | 工单编号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/zone/ac1/reply" --data '
{
    "key": "value"
}'
```

#### 响应内容:

```js
{
    "key": "value"
}
```

## POST /assess

**提交评价**

*详细描述*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| assess | String | Yes | 评价级别(BAD(差评) GOOD(一般) BEST(好评)) |
| advice | String | Yes | 意见建议 |
| id | String | Yes | 工单编号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/zone/ac1/assess" --data '
{
    "key": "value"
}'
```

#### 响应内容:

```js
{
    "key": "value"
}
```

## PUT /ticket/:id

**关闭工单**

*详细描述*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| id | String | Yes | 工单编号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

参考: *[Job 数据结构](/job.html)*

### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/ticket/:id" --data '
{
    "key": "value"
}'
```

#### 响应内容:

```js
{
    "key": "value"
}
```
## GET /devinfo

**获取设备信息**

*详细描述*

### 请求

#### Body 参数
| 参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| datacenter | String | Yes | 数据中心代码 |
| limit | String | Yes | 默认值:5 |
| offset | String | Yes | 偏移量 |
| dev_no | String | No | 设备编号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| dev_items | List | Yes | 配置列表 |
| total_count | int | Yes | 总数 |


#### ReplyDetail
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| rack_no  | String | Yes | 机柜编号 |
| dev_no  | String | Yes | 设备编号 |
| ip_address  | String | Yes | IP地址 |
| assets_no  | String | Yes | 资源编号 |
| dev_model  | String | Yes | 设备型号 |
| is_shelve  | String | Yes | 是否下架 |


### 示例

#### 发送请求

```bash

$ curl -XGET "http://dev.api.51idc.com/v2/devinfo?datacenter=JH&limit=0&offset=5&dev_no=test-005

```

#### 响应内容:

```js

{

 "key": "value"

}

```