# 用户信息

<!-- toc -->

## post /customer

**注册**

*注册成为云平台用户*

*可以选择注册成为个人用户和企业用户*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| cus_name | String | Yes | 用户名 |
| short_name | String| No | 昵称 |
| passwd | String | Yes | 密码 |
| cus_type | String | Yes | 用户类型，企业对应FIRM，个人对应SELF |
| tel | String | No | 固定电话 |
| mobile | String | Yes | 手机 |
| email | String | Yes | 邮箱 |
| verification_code | String | Yes | 验证码 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| cus_name | string | Yes | 用户名 |

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/customer" --data '
{
    "cus_name":"51idc",
    "short_name":"idc",
    "passwd":"123abc",
    "cus_type":"FIRM",
    "tel":"021-9621312",
    "mobile":"13312345864",
    "email":"test@51idc.com",
    "verification_code":"133264"
}'
```

#### 响应内容:
* 成功
```js
{
    "cus_name": "51idc"
} 
```
* 验证码错误
Http Status:400
```js
{
  "code": "10120020",
  "detail": "SError({Code:10124000020 Message:Verification code does not match Extra:map[]})",
  "message": "10124000020"
}
```
* 密码格式错误
Http Status:400
```js         
{             
  "code": "10120023",
  "detail": "SError({Code:10124000023 Message:ill-formatted password Extra:map[]})",
  "message": "10124000023"
}             
```
* 邮箱已存在
Http Status:400                                                                                                                                                                                                    
```js           
{               
  "code": "10120018",
  "detail": "SError({Code:10120018 Message:SError({Code:10124000019 Message:customer's email already existed Extra:map[]}) Extra:map[]})",
  "message": "10120018"
}               
``` 
* 手机已存在
Http Status:400
```js
{  
  "code": "10120017",
  "detail": "SError({Code:10120017 Message:SError({Code:10124000019 Message:customer's name already existed Extra:map[]}) Extra:map[]})",
  "message": "10120017"
}                                                                                                                                                                                                                  
```

* 客户名已存在
Http Status:400
```js
{
  "code": "10120019",
  "detail": "SError({Code:10120019 Message:SError({Code:10124000019 Message:customer's name already existed Extra:map[]}) Extra:map[]})",
  "message": "10120019"
}
```
* 非法参数
Http Status:400
```js
{    
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid params Extra:map[]})",
  "message": "10124000001"
}    
``` 
## GET /customer

**获取用户信息**

*获取用户的基本信息*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| cus_name | String | No | 用户名 |
| cus_type | String | No | 用户类型,firm对应企业用户，self对应个人用户 |
| tel | String | No | 固定电话 |
| address | String | No | 地址 |
| postcode | String | No | 邮编 |
| fax | String | No | 传真 |
| mobile | String | No | 手机 |
| email | String | No | 邮箱 |
| cred_type | String | No | 证件类型，身份证对应identity，<br>军官证对应military，<br>驾照对应driver |
| credentials | String | No | 证件编号 |
| permit_number | String | No | 营业执照编号 |
| permit_addr | String | No | 营业执照图片地址 |
| organizationcode | String | No | 组织机构代码证编号 |
| organizationCode_addr | String | No | 组织机构代码证图片地址 |
| authorization | String | No | 服务授权码 |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://api.51idc.com/v2/zone/ac1/customer"
```

#### 响应内容:

```js
{
    "cus_name": "51idc",
    "cus_type": "FIRM",
    "tel": "021-4648",
    "address": "呼兰西路",
    "postcode": "242200",
    "fax": "445646",
    "mobile": "134123456",
    "cred_type": "DRIVER",
    "credentials": "146548796454515614546",
    "permit_number": "123",
    "permit_addr": "http://wwww.51idc.com",
    "organizationcode": "456",
    "organizationCode_addr": "http://www.51idc.com",
    "authorization": "121"
}
```
## PUT /customer

**修改用户基本信息**

*修改用户的基本信息*


### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| post_field | String | No | 可选字段，"auth"修改服务授权码 |
| tel | String | No | 固定电话 |
| address | String | No | 地址 |
| postcode | String | No | 邮编 |
| fax | String | No | 传真 |
| authorization | String | No | 授权码 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

**NONE**
### 示例

#### 发送请求
* 修改基本属性
```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer" --data '
{
    "tel":"021-45612",
    "address":"宝山",
    "postcode":"201900",
    "fax":"021-45612"
}'
```
* 修改服务授权码
```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer" --data '
{
    "post_field": "auth",
    "authorization":"201900"
}'
```
#### 响应内容:

```js
```


## GET /customer/available:cusname

**查询用户名是否可用**

*用户名唯一，注册时需要查询是否可用*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| cus_name | String | Yes | 用户名 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| available | String | Yes | 用户名 |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://api.51idc.com/v2/customer/available?cusname=51idc"
```

#### 响应内容:
* 用户名可用
```js
{
    "available": {
        "cus_name":"51idc"
    }
} 
```
* 用户名不可用
Http Status:202
```js
{
  "code": "10120012",
  "detail": "SError({Code:10122020012 Message:customer name already existed Extra:map[]})",
  "message": "10122020012"
}
```
## GET /customer/contacts

**获取用户联系人信息**

*获取用户联系人的基本信息*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| offset | Int | No | 数据偏移量，默认为0 |
| limit | Int | No | 返回数据长度，默认为10，最大100 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| contacts | Object[] | Yes | [<br>{<br>&nbsp;&nbsp;"contact_id": "*String*",<br>&nbsp;&nbsp;"name": "*String*",<br>&nbsp;&nbsp;"sex": "*String*",<br>&nbsp;&nbsp;"tel": "*String*",<br>&nbsp;&nbsp;"mobile": "*String*",<br>&nbsp;&nbsp;"email": "*String*",<br>&nbsp;&nbsp;"con_type": "*String* STYPE or JTYPE",<br>&nbsp;&nbsp;"cred_type": "*String*",<br>&nbsp;&nbsp;"credentials": "*String*",<br>}<br>] |
| total_count | Int | Yes | - |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://api.51idc.com/v2/zone/ac1/customer/contacts"
```

#### 响应内容:

```js
   {
   "contacts": [
      {
         "contact_id": "con_YZAKUZF",
         "name": "小张",
         "sex": "m",
         "tel": "021-25228622",
         "mobile": "13751247782",
         "email": "test@163.com",
         "con_type": "jtype",
         "cred_type": "identity",
         "credentials": "330104598502150915"
      },
      {
         "contact_id": "con_USBENSE",
         "name": "小李",
         "sex": "m",
         "tel": "",
         "mobile": "15721460942",
         "email": "test2@heheda.net",
         "con_type": "stype",
         "cred_type": "identity",
         "credentials": "728923198511293151"
      }
   ],
   "total_count": 2
}
 
```
## post /customer/contacts

**增加联系人**

*增加用户联系人*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| name | String | Yes | 姓名 |
| sex | String | No | 性别 |
| tel | String | No | 固定电话 |
| mobile | String | Yes | 手机 |
| email | String | Yes | 类型 |
| con_type | String | No | 联系人类型 |
| cred_type | String | No | 证件类型 |
| credentials | String | No | 证件号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| contact_id | String | Yes | ID |
| name | String | Yes | 姓名 |
| sex | String | No | 性别 |
| tel | String | No | 固定电话 |
| mobile | String | No | 手机 |
| email | String | No | 类型 |
| con_type | String | No | 联系人类型 |
| cred_type | String | No | 证件类型 |
| credentials | String | No | 证件号 |

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/zone/ac1/customer/contacts" --data '
{
     "name": "小李",
     "sex": "M",
     "tel": "",
     "mobile": "15721460942",
     "email": "test2@heheda.net",
     "con_type": "STYPE",
     "cred_type": "IDENTITY",
     "credentials": "728923198511293151"
}'
```

#### 响应内容:
* 成功
```js
{
     "contact_id": "con_USBENSE",
     "name": "小李",
     "sex": "M",
     "tel": "",
     "mobile": "15721460942",
     "email": "test2@heheda.net",
     "con_type": "STYPE",
     "cred_type": "IDENTITY",
     "credentials": "728923198511293151"
}
```
* 非法的手机格式
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid mobile params. Extra:map[]})",
  "message": "10124000001"
}
```
* 非法的电话格式
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid mobile params. Extra:map[]})",
  "message": "10124000001"
}
```
* 非法的邮箱格式
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid email params. Extra:map[]})",
  "message": "10124000001"
}
```
* 非法参数
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid params Extra:map[]})",
  "message": "10124000001"
}
```
## PUT /customer/contacts/:contact_id

**修改联系人信息**

*修改用户联系人信息*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| contact_id | String | Yes | 联系人ID列表 |
#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| name | String | No | 姓名 |
| sex | String | No | 性别 |
| tel | String | No | 固定电话 |
| mobile | String | No | 手机 |
| email | String | No | 类型 |
| con_type | String | No | 联系人类型 |
| cred_type | String | No | 证件类型 |
| credentials | String | No | 证件号 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| contact_id | String | Yes | ID |
| name | String | No | 姓名 |
| sex | String | No | 性别 |
| tel | String | No | 固定电话 |
| mobile | String | No | 手机 |
| email | String | No | 类型 |
| con_type | String | No | 联系人类型 |
| cred_type | String | No | 证件类型 |
| credentials | String | No | 证件号 |

**NONE**
### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/contacts/con_USBENSE --data '
{
    "name":"name",
    "sex":"F",
    "tel":"",
    "mobile":"",
    "email":"",
    "con_type":"",
    "cred_type":"",
    "credentials":""
}'
```

#### 响应内容:
* 成功
```js
{
    "contact_id": "con_USBENSE",
    "name":"name",
    "sex":"F",
    "tel":"",
    "mobile":"",
    "email":"",
    "con_type":"",
    "cred_type":"",
    "credentials":""
} 
```
* 非法的手机格式
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid mobile params. Extra:map[]})",
  "message": "10124000001"
}
```
* 非法的电话格式
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid mobile params. Extra:map[]})",
  "message": "10124000001"
}
```
* 非法的邮箱格式
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid email params. Extra:map[]})",
  "message": "10124000001"
}
```
* 非法参数
```js
{
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid params Extra:map[]})",
  "message": "10124000001"
}
```
## DELETE /customer/contacts/:contact_ids

**删除联系人 支持批量**

*删除一个或多个用户的联系人*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| contact_ids | String[] | Yes | 联系人ID列表,逗号分割 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

### 示例

#### 发送请求

```bash
$ curl -XDELETE "http://api.51idc.com/v2/zone/ac1/customer/contacts/con_USEWFAB,con_OIHYDNV"
```

#### 响应内容:

```js
{
    "contact_ids": [
        "con_USEWFAB",
        "con_OIHYDNV"
    ]
}
```
## GET /customer/accountmanager

**获取客户经理信息**

*获取用户的客户经理基本信息*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| name | String | No | 客户经理名 |
| mobile | String | No | 手机 |
| email | String | No | 邮箱 |
| qq | String | No | QQ |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://api.51idc.com/v2/zone/ac1/customer/accountmanager"
```

#### 响应内容:

```js
{
    "name": "51idc",
    "mobile": "134123456"
    "email": "242200@test.com",
    "qq": "445646"
}
```
## GET /customer/accounts

**获取登录帐号**

*获取用户的所有登录帐号*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| search_word | String | No | 模糊查询字段 |
| status | String | No | 状态过滤，ACTIVITY 或 DISABLED 或 空 |
| offset | Int | No | 数据偏移量，默认为0 |
| limit | Int | No | 返回数据长度，默认为10，最大100 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| accounts | Object[] | Yes | [<br>{<br>&nbsp;&nbsp;"login_id": "*String*",<br>&nbsp;&nbsp;"account_type": "*String*",<br>&nbsp;&nbsp;"last_logintime": "*TimeStamp*",<br>&nbsp;&nbsp;"last_loginip": "*String*",<br>&nbsp;&nbsp;"status": "*String*"DISABLED or ACTIVITY<br>}<br>] |
| total_count | Int | Yes | - |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://api.51idc.com/v2/zone/ac1/customer/accounts"
```

#### 响应内容:

```js
{
   "accounts": [
      {
         "login_id": "test@51idc.com",
         "account_type": "ADMIN",
         "last_logintime": "2013-08-30T05:13:32Z",
         "last_loginip": "1.1.1.1",
         "status": "ACTIVITY"
      },
      {
         "login_id": "test@51idc.com",
         "account_type": "SUB",
         "last_logintime": "2013-08-30T05:13:32Z",
         "last_loginip": "1.1.1.1",
         "status": "ACTIVITY"
      }
   ],
   "total_count": 2
}
 
```
## post /customer/accounts

**增加新账户**

*增加新登录账户*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| login_id | String | Yes | 登录账户 |
| passwd | String | Yes | 密码 |
| account_type | String | Yes | 账户类型, ADMIN对应主帐号,SUB对应子帐号 |
| mobile | String | Yes | 手机 |
| verification_code | String | Yes | 验证码 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| login_id | string | Yes | 账户 |

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/zone/ac1/customer/accounts" --data '
{
    "login_id":"",
    "passwd":"123abc",
    "account_type":"ADMIN",
    "mobile":"12345678945",
    "verification_code":"123456"
}'
```

#### 响应内容:
* 成功
```js
{
    "login_id": ""
} 
```
* 邮箱已存在
Http Status:400                                                                                                                                                                                                    
```js           
{               
  "code": "10120018",
  "detail": "SError({Code:10120018 Message:SError({Code:10124000019 Message:customer's email already existed Extra:map[]}) Extra:map[]})",
  "message": "10120018"
}               
``` 
* 非法参数
Http Status:400
```js
{    
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid params Extra:map[]})",
  "message": "10124000001"
}
```   
* 非法的邮箱格式
```js
{  
  "code": "10120001",
  "detail": "SError({Code:10124000001 Message:invalid email params. Extra:map[]})",
  "message": "10124000001"
}  
```
* 密码格式错误
Http Status:400
```js         
{             
  "code": "10120023",
  "detail": "SError({Code:10124000023 Message:ill-formatted password Extra:map[]})",
  "message": "10124000023"
}             
```

## GET /customer/account

**获取登录信息**

*获取用户的登录信息*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| login_id | string | Yes | 用户登录ID |
| mobile | string | Yes | 绑定手机 |
| wechat | string | Yes | 绑定微信 |
| authorization | string | Yes | 服务授权码 |
### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/account --data '
{
    "login_id":"test@51idc.com",
    "mobile":"",
    "wechat":"",
    "authorization":"1006"
}'
```
## DELETE /customer/accounts/:account_id

**删除登录账户 支持批量**

*删除一个或多个用户的登录账户*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| verification_code | String | Yes | 验证码 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

### 示例

#### 发送请求(手机)
```bash
$ curl -XDELETE "http://api.51idc.com/v2/zone/ac1/customer/accounts/:account_id" --data '{
    "verification_code": "652312"
}'
```
#### 发送请求(微信)
```bash
$ curl -XDELETE "https://open.weixin.qq.com/connect/oauth2/authorize?appid=APPID&redirect_uri=http%3A%2F%2Fapi.51idc.com%2Fv2%2Fzone%2Fac1%2Fcustomer%2Faccounts%2F%3Aaccount_id%3Fevent_id%3D1476347159&response_type=code&scope=snsapi_base#wechat_redirect "
```

#### 响应内容:

```js
{
    "account_id": ""
}
```
## PUT /customer/accounts/:account_id/disabled

**禁用账户**

*修改用户登录账户状态*

### 请求

#### 请求 Body 参数
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| reason | String | No | 理由 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| account_id | String | Yes | 登录Id |
| status | String | Yes | 状态 |

**NONE**
### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/accounts/test@51idc.com/disabled --data '
{
    "reason": "test"
}'

```

#### 响应内容:

```js
{
    "account_id": "test@51idc.com",
    "status": "DISABLED"
} 
```
## PUT /customer/accounts/:account_id/undisabled

**解禁账户**

*修改用户登录账户状态*

### 请求

#### 请求 Body 参数
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| reason | String | Yes | 理由 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| account_id | String | Yes | 登录Id |
| status | String | Yes | 状态 |

**NONE**
### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/accounts/test@51idc.com/undisabled --data '
{
    "reason": "test"
}'
```

#### 响应内容:

```js
{
    "account_id": "test@51idc.com"
    "status": "ACTIVITY"
} 
```


## GET /customer/profession

**获取业务信息**

*获取用户的业务信息*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| industry_application | String | No | 行业应用 |
| main_business | String | No | 主营业务 |
| website | String | No | 用户网址 |

### 示例

#### 发送请求

```bash
$ curl -XGET "http://api.51idc.com/v2/zone/ac1/customer/profession"
```

#### 响应内容:

```js
{
    "industry_application": "",
    "main_business": "",
    "website": ""
}
```

## PUT /customer/profession

**修改业务信息**

*修改用户业务信息*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| industry_application | String | No | 行业应用 |
| main_business | String | No | 主营业务 |
| website | String | No | 用户网址 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
**NONE**
### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/profession --data '
{
    "industry_application":"",
    "main_business":"",
    "website":""
}'
```
## PUT /customer/accounts/:account_id/passwd

**修改密码**

*修改登录密码*

### 请求
#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| account_id | String | Yes | 用户登录ID |

#### 请求 Body 参数(手机方式)

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| new_passwd | String | Yes | 新密码 |
| verification_code | String | Yes | 验证码 |
#### QueryString 参数(微信方式)
|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| new_passwd | String | Yes | 新密码，需base64编码 |
| event_id | String | Yes | 轮寻ID，当前时间戳 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
**NONE**
### 示例

#### 发送请求 (手机)

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/accounts/test@51idc.com/passwd --data '
{
    "new_passwd":"",
    "verification_code":""
}'
```
#### 发送请求 (微信)

```bash
$ curl -XGET "https://open.weixin.qq.com/connect/oauth2/authorize?appid=APPID&redirect_uri=http%3A%2F%2Fapi.51idc.com%2Fv2%2Fzone%2Fac1%2Fcustomer%2Faccounts%2Ftest%4051idc.com%2Fpasswd%3Fnew_passwd%3D123%26event_id%3D1476347159&response_type=code&scope=snsapi_base#wechat_redirect--data 
```
## PUT /customer/accounts/:account_id/phone

**绑定手机**

*绑定账户手机*

### 请求

#### QueryString 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| account_id | String | Yes | 用户登录ID |
#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| vcode_for_old | String | Yes | 原绑定手机验证码 |
| new_mobile | String | Yes | 新手机号 |
| vcode_for_new | String | Yes | 新手机验证码 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息
**NONE**
### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/accounts/test@51idc.com/passwd --data '
{
    "mobile":"",
    "verification_code":"",
    "action_type":0
}'
```
## post /verification_code

**登录用户获取验证码**

*给登录用户手机发送验证码*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| addition | String | No | 附加字段 |
| smsype | String | Yes | 验证类型，certify |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/verification_code" --data '
{
    "addition":"123abc",
    "smstype":"certify"
}'
```
#### 响应内容:
* 成功
```js
{} 
```
* 未绑定手机
Http Status:400
```js
{
  "code": "10120026",
  "detail": "SError({Code:10124000026 Message:please bind your phone first Extra:map[]})",
  "message": "10124000026"
}
```
## post /verification_code_withphone

**获取验证码**

*给手机发送验证码*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| addition | String | No | 附加字段 |
| smsype | String | Yes | 验证类型，certify |
| mobile | String | Yes | 手机 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 示例

#### 发送请求

```bash
$ curl -XPOST "http://api.51idc.com/v2/verification_code_withphone" --data '
{
    "addition":"123abc",
    "smstype":"certify",
    "mobile":"13312345864"
}'
```
## put /customer/image

**获取验证码**

*给手机发送验证码*

### 请求

#### 请求 Body 参数

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |
| obj_type | String | Yes | 操作对象类型，permit表示营业执照，organize表示组织机构代码证|
| obj_name | String | Yes | 对象名字 |
| obj_addr | String | Yes | 服务保存文件名 |

### 服务端响应

#### 响应头信息

`NULL`

#### 响应 Body 信息

|参数名 | 类型 | 是否必选 | 描述 |
| :-- | :-- | :-- | :-- |

### 示例

#### 发送请求

```bash
$ curl -XPUT "http://api.51idc.com/v2/zone/ac1/customer/image" --data '
{
    "obj_type":"permit",
    "obj_name":"test.jpg",
    "obj_addr":"201610/20/7fe99d3c-4719-497e-9718-6261e2258eb2.jpg"
}'
```
