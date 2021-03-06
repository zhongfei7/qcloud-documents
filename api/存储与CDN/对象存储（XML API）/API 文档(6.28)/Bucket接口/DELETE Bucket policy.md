## 功能描述
DELETE Bucket policy 请求可以向 Bucket 删除权限策略。

>注意：只有 Bucket 所有者有权限发起该请求。
- 假如您没有拥有 DELETE Bucket policy 的权限，则返回 403 Access Denied；
- 假如您拥有 DELETE Bucket policy 的权限，但不是存储桶所有者时，将返回 405 Method Not Allowed；
- 如果权限策略不存在，将返回 204 No Content。

## 请求

### 请求示例：

```
DELETE /?policy Http/1.1
Host:<bucketname-APPID>.cos.<Region>.myqcloud.com
Date: date
Authorization: Auth String
```
> Authorization: Auth String (详细参见 [请求签名](https://cloud.tencent.com/document/product/436/7778) 章节)

### 请求行

```
DELETE /?policy Http/1.1
```

该 API 接口接受 `DELETE` 请求。

### 请求头

#### 公共头部

该请求操作的实现使用公共请求头，了解公共请求头详情，请查阅 [公共请求头部](https://cloud.tencent.com/document/product/436/7728 "公共请求头部") 章节。

#### 非公共头部

该请求操作无特殊的请求头部信息。

#### 请求参数

无特殊请求参数。

## 响应

### 响应头

#### 公共响应头

该响应使用公共响应头，了解公共响应头详情，请参见 [公共响应头部](https://cloud.tencent.com/document/product/436/7729 "公共响应头部") 章节。

#### 特有响应头

该请求操作无特殊的响应头部信息。
### 响应体
该请求响应体为空。

## 实际案例

### 请求

```json
DELETE /?policy HTTP/1.1
Host:bucket01-1251668577.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814613;32557710613&q-key-time=1484814613;32557710613&q-header-list=host&q-url-param-list=policy&q-signature=57c9a3f67b786ddabd2c208641944ec7f9b02f98
```

### 响应

```json
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:30:21 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc5MWRfNDQyMDRlXzNiMDRfZTEw
```
