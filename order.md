# 订单
## GET /orders

**获取订单列表**

*详细描述*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| end_time | String | NO | 订单结束时间
| start_time | String | NO | 订单开始时间 |
| order_type | String | NO | 订单类型 ADDNEW(新增) RENEW(续约) |
| search_word | String | NO | 搜索关键词，支持订单编号，名称 |
| resource_type | String | NO | 资源的类型 CLOUD(云资源) IDC(物理架构) |
| offset | Int | NO | 数据偏移量，默认为0 |
| limit | Int | NO | 默认值: 10|
| account_type | String | NO | 账户类型 MAIN(主账号) BUSINESS（商务）TECHNOLOGY(技术) CHILD（子账号） |
| order_state | String | NO | 订单状态 PREPAID（已支付）NOTPAY（未支付）SUSPEND(已终止) EXPIREING(即将到期) |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| orders | Objects | Yes | 订单列表 |
| total_count | Int | Yes | 根据过滤条件得到的总数 |

### Order

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| order_name | String | Yes | 订单列表 |
| order_number | Int | Yes | 根据过滤条件得到的总数 |
| resource_type | String | Yes | 资源的类型 CLOUD(云资源) IDC(物理架构) |
| account_type| String | Yes | 账户类型 admin(主账号) sub（子账号） |
| pay_way | String | Yes | PREPAY（包年包月）POSTPAY（按需） |
| product_name | String | Yes | 产品名称 |
| order_state | String | Yes | 订单状态 PREPAID（已支付）NOTPAY（未支付）SUSPEND(已终止) EXPIREING(即将到期) |
| create_time | String | Yes | 创建时间 |
| price | double | Yes | 价格 |
| price_details | Object[] | Yes | 价格详情 |

### price_details
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| details_name | String | Yes | 资源名称 |
| details_price | double | Yes | 资源单价 |

### 示例

#### 发送请求

```bash

$ curl -XGET "http://api.51idc.com/v2/zone/ac1/orders"

```

#### 响应内容:

```js

{

 "key": "value"

}

```