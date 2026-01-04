# {{serviceName}} REST API 文档

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档定义 {{serviceName}} 微服务的 REST API 接口规范。

## API 基础信息

### 基础 URL

{{baseUrl}}

### API 版本

{{apiVersion}}

### 认证方式

{{authenticationMethod}}

### 内容类型

{{contentType}}

## API 接口列表

| 接口路径      | HTTP 方法       | 描述             | 认证要求          |
| ------------- | --------------- | ---------------- | ----------------- |
| {{endpoint1}} | {{httpMethod1}} | {{description1}} | {{authRequired1}} |
| {{endpoint2}} | {{httpMethod2}} | {{description2}} | {{authRequired2}} |

## API 接口详细说明

### {{api1}}

#### 接口信息

- **端点**: `{{endpoint1}}`
- **方法**: {{httpMethod1}}
- **认证**: {{authentication1}}
- **描述**: {{apiDescription1}}

#### 请求参数

##### 路径参数

| 参数名         | 类型           | 必填          | 描述                  |
| -------------- | -------------- | ------------- | --------------------- |
| {{pathParam1}} | {{paramType1}} | {{required1}} | {{paramDescription1}} |

##### 查询参数

| 参数名          | 类型           | 必填          | 描述                  |
| --------------- | -------------- | ------------- | --------------------- |
| {{queryParam1}} | {{paramType1}} | {{required1}} | {{paramDescription1}} |
| {{queryParam2}} | {{paramType2}} | {{required2}} | {{paramDescription2}} |

##### 请求体

```json
{
  "{{requestField1}}": "{{requestValue1}}",
  "{{requestField2}}": "{{requestValue2}}"
}
```

| 字段名            | 类型           | 必填          | 描述                  |
| ----------------- | -------------- | ------------- | --------------------- |
| {{requestField1}} | {{fieldType1}} | {{required1}} | {{fieldDescription1}} |
| {{requestField2}} | {{fieldType2}} | {{required2}} | {{fieldDescription2}} |

#### 响应格式

##### 成功响应 (200 OK)

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "{{responseField1}}": "{{responseValue1}}",
    "{{responseField2}}": "{{responseValue2}}"
  }
}
```

| 字段名             | 类型           | 描述                  |
| ------------------ | -------------- | --------------------- |
| {{responseField1}} | {{fieldType1}} | {{fieldDescription1}} |
| {{responseField2}} | {{fieldType2}} | {{fieldDescription2}} |

##### 错误响应

| HTTP 状态码         | 错误码         | 描述                  |
| ------------------- | -------------- | --------------------- |
| {{httpStatusCode1}} | {{errorCode1}} | {{errorDescription1}} |
| {{httpStatusCode2}} | {{errorCode2}} | {{errorDescription2}} |

#### 示例

##### 请求示例

```bash
curl -X {{httpMethod1}} "{{baseUrl}}{{endpoint1}}" \
  -H "Authorization: Bearer {{token}}" \
  -H "Content-Type: application/json" \
  -d '{
    "{{requestField1}}": "{{requestValue1}}"
  }'
```

##### 响应示例

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "{{responseField1}}": "{{responseValue1}}"
  }
}
```

### {{api2}}

#### 接口信息

- **端点**: `{{endpoint2}}`
- **方法**: {{httpMethod2}}
- **认证**: {{authentication2}}
- **描述**: {{apiDescription2}}

## API 版本管理

| 版本         | 发布日期         | 状态        | 废弃计划             |
| ------------ | ---------------- | ----------- | -------------------- |
| {{version1}} | {{releaseDate1}} | {{status1}} | {{deprecationPlan1}} |
| {{version2}} | {{releaseDate2}} | {{status2}} | {{deprecationPlan2}} |

## API 性能指标

| 接口     | 平均响应时间         | 最大并发            | SLA      |
| -------- | -------------------- | ------------------- | -------- |
| {{api1}} | {{avgResponseTime1}} | {{maxConcurrency1}} | {{sla1}} |
| {{api2}} | {{avgResponseTime2}} | {{maxConcurrency2}} | {{sla2}} |

## API 安全

### 认证机制

{{authenticationMechanism}}

### 授权策略

{{authorizationStrategy}}

### 数据加密

{{dataEncryption}}

### 限流策略

{{rateLimitingStrategy}}

## 相关文档

- [[event-api.md]] - 事件接口文档
- [[api-contract.md]] - API 契约定义
- [[../02-domain/domain-overview.md]] - 领域概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
