# {{subdomainName}} API 设计

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档定义 {{subdomainName}} 领域的完整 API 设计，包括 REST API 端点、事件驱动 API 和 API 契约规范。

> **说明**：本文档是单个领域的 API 设计文档。系统级的 API 导航和协议列表请参考系统级文档。

## API 设计原则

### 总体设计原则

{{apiDesignPrinciples}}

### REST API 设计原则

{{restApiPrinciples}}

### 事件 API 设计原则

{{eventApiPrinciples}}

## REST API 设计

### 基础信息

| 项目     | 说明                     |
| -------- | ------------------------ |
| 基础 URL | {{baseUrl}}              |
| API 版本 | {{apiVersion}}           |
| 认证方式 | {{authenticationMethod}} |
| 内容类型 | {{contentType}}          |

### 接口列表

| 接口路径      | HTTP 方法       | 描述             | 认证要求          | 业务用例     |
| ------------- | --------------- | ---------------- | ----------------- | ------------ |
| {{endpoint1}} | {{httpMethod1}} | {{description1}} | {{authRequired1}} | {{useCase1}} |
| {{endpoint2}} | {{httpMethod2}} | {{description2}} | {{authRequired2}} | {{useCase2}} |

### 接口详细说明

#### {{api1}}

##### 接口信息

- **端点**: `{{endpoint1}}`
- **方法**: {{httpMethod1}}
- **认证**: {{authentication1}}
- **描述**: {{apiDescription1}}
- **关联用例**: [[02-domain-design.md#UC-001|{{useCase1}}]]

##### 请求参数

###### 路径参数

| 参数名         | 类型      | 必填          | 描述             | 约束条件        |
| -------------- | --------- | ------------- | ---------------- | --------------- |
| {{pathParam1}} | {{type1}} | {{required1}} | {{description1}} | {{constraint1}} |

###### 查询参数

| 参数名          | 类型      | 必填          | 描述             | 默认值            |
| --------------- | --------- | ------------- | ---------------- | ----------------- |
| {{queryParam1}} | {{type1}} | {{required1}} | {{description1}} | {{defaultValue1}} |

###### 请求头

| 头名称      | 类型      | 必填          | 描述             |
| ----------- | --------- | ------------- | ---------------- |
| {{header1}} | {{type1}} | {{required1}} | {{description1}} |

###### 请求体

```json
{
  "{{property1}}": "{{value1}}",
  "{{property2}}": "{{value2}}"
}
```

**请求体字段说明**：

| 字段名     | 类型      | 必填          | 描述             |
| ---------- | --------- | ------------- | ---------------- |
| {{field1}} | {{type1}} | {{required1}} | {{description1}} |
| {{field2}} | {{type2}} | {{required2}} | {{description2}} |

##### 响应参数

###### 成功响应（2xx）

**状态码**: {{successCode}} ({{successMessage}})

**响应体**：

```json
{
  "code": 0,
  "message": "success",
  "data": {
    "{{property1}}": "{{value1}}",
    "{{property2}}": "{{value2}}"
  }
}
```

**响应字段说明**：

| 字段名          | 类型      | 描述               |
| --------------- | --------- | ------------------ |
| code            | integer   | 错误码，0 表示成功 |
| message         | string    | 响应消息           |
| data            | object    | 响应数据           |
| data.{{field1}} | {{type1}} | {{description1}}   |

###### 错误响应（4xx/5xx）

**错误情况 1**：

- **状态码**: {{errorCode1}} ({{errorMessage1}})
- **场景**: {{errorScenario1}}
- **响应体**：

```json
{
  "code": {{errorCode1}},
  "message": "{{errorMessage1}}",
  "errors": [
    {
      "field": "{{fieldName}}",
      "reason": "{{reason}}"
    }
  ]
}
```

**错误情况 2**：

- **状态码**: {{errorCode2}} ({{errorMessage2}})
- **场景**: {{errorScenario2}}

##### 业务规则

{{businessRules1}}

##### 使用示例

**请求示例**：

```bash
curl -X {{httpMethod1}} "{{baseUrl}}{{endpoint1}}" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {{token}}" \
  -d '{
    "{{property1}}": "{{value1}}"
  }'
```

**响应示例**：

```json
{
  "code": 0,
  "message": "success",
  "data": {
    "{{property1}}": "{{value1}}"
  }
}
```

#### {{api2}}

##### 接口信息

- **端点**: `{{endpoint2}}`
- **方法**: {{httpMethod2}}
- **认证**: {{authentication2}}
- **描述**: {{apiDescription2}}

##### 请求参数

...（参考上述结构）

##### 响应参数

...（参考上述结构）

## 事件驱动 API 设计

### 基础信息

| 项目       | 说明                    |
| ---------- | ----------------------- |
| 消息中间件 | {{messageMiddleware}}   |
| 事件格式   | {{eventFormat}}         |
| 序列化方式 | {{serializationMethod}} |

### 发布事件列表

| 事件名称   | 事件类型       | 主题/队列  | 描述             | 发布条件                         |
| ---------- | -------------- | ---------- | ---------------- | -------------------------------- | ---------- |
| {{event1}} | {{eventType1}} | {{topic1}} | {{description1}} | [[02-domain-design.md#{{event1}} | 查看详情]] |
| {{event2}} | {{eventType2}} | {{topic2}} | {{description2}} | [[02-domain-design.md#{{event2}} | 查看详情]] |

### 订阅事件列表

| 事件名称             | 事件来源    | 处理逻辑     | 描述             |
| -------------------- | ----------- | ------------ | ---------------- |
| {{subscribedEvent1}} | {{source1}} | {{handler1}} | {{description1}} |
| {{subscribedEvent2}} | {{source2}} | {{handler2}} | {{description2}} |

### 发布事件详细说明

#### {{event1}}

##### 事件信息

- **事件名称**: {{event1}}
- **事件类型**: {{eventType1}}
- **主题/队列**: {{topic1}}
- **描述**: {{eventDescription1}}
- **发布时机**: {{publishTrigger1}}
- **关联用例**: [[02-domain-design.md#用例详细说明|查看用例]]

##### 事件结构

```json
{
  "eventType": "{{event1}}",
  "eventId": "{{eventId}}",
  "timestamp": "{{timestamp}}",
  "aggregateId": "{{aggregateId}}",
  "aggregateType": "{{aggregateType}}",
  "version": {{version}},
  "source": "{{domainName}}",
  "data": {
    "{{property1}}": "{{value1}}",
    "{{property2}}": "{{value2}}"
  }
}
```

##### 事件字段说明

| 字段名             | 类型      | 描述                          | 必填          |
| ------------------ | --------- | ----------------------------- | ------------- |
| eventType          | string    | 事件类型标识                  | 是            |
| eventId            | string    | 事件唯一 ID                   | 是            |
| timestamp          | string    | 事件发生时间（ISO 8601 格式） | 是            |
| aggregateId        | string    | 聚合根 ID                     | 是            |
| aggregateType      | string    | 聚合根类型                    | 是            |
| version            | integer   | 聚合根版本                    | 是            |
| source             | string    | 事件源（服务名或领域名）      | 是            |
| data.{{property1}} | {{type1}} | {{description1}}              | {{required1}} |
| data.{{property2}} | {{type2}} | {{description2}}              | {{required2}} |

##### 事件发布者

- **服务/领域**: {{serviceName}}
- **发布点**: [[03-domain-application.md#应用服务详细设计|查看应用服务]]
- **发布频率**: {{publishFrequency}}

##### 事件订阅者

| 订阅方          | 处理逻辑     | 用途         |
| --------------- | ------------ | ------------ |
| {{subscriber1}} | {{handler1}} | {{purpose1}} |
| {{subscriber2}} | {{handler2}} | {{purpose2}} |

##### 事件流说明

{{eventFlowDescription1}}

##### 使用示例

**事件示例**：

```json
{
  "eventType": "{{event1}}",
  "eventId": "550e8400-e29b-41d4-a716-446655440000",
  "timestamp": "2024-01-24T10:30:00Z",
  "aggregateId": "user-001",
  "aggregateType": "User",
  "version": 1,
  "source": "user-domain",
  "data": {
    "{{property1}}": "{{value1}}"
  }
}
```

#### {{event2}}

##### 事件信息

...（参考上述结构）

## API 契约规范

### 数据格式规范

#### 通用数据结构

##### 响应格式

所有 REST API 响应遵循以下统一格式：

```json
{
  "code": 0,
  "message": "string",
  "data": null | {} | []
}
```

**字段说明**：

- `code`: HTTP 状态码的业务映射码，0 表示成功，非 0 表示失败
- `message`: 人类可读的响应消息
- `data`: 响应数据，可以是 null、对象或数组

##### 分页格式

```json
{
  "code": 0,
  "message": "success",
  "data": {
    "items": [],
    "pagination": {
      "page": 1,
      "pageSize": 20,
      "totalCount": 100,
      "totalPages": 5
    }
  }
}
```

##### 错误响应格式

```json
{
  "code": 400,
  "message": "Bad Request",
  "errors": [
    {
      "field": "fieldName",
      "reason": "Field is required"
    }
  ]
}
```

#### 数据类型规范

| 数据类型 | JSON 表示 | 说明            | 示例                     |
| -------- | --------- | --------------- | ------------------------ |
| 字符串   | string    | UTF-8 编码      | `"hello"`                |
| 整数     | integer   | 64 位整数       | `12345`                  |
| 浮点数   | number    | IEEE 754 双精度 | `123.45`                 |
| 布尔值   | boolean   | true/false      | `true`                   |
| 日期时间 | string    | ISO 8601 格式   | `"2024-01-24T10:30:00Z"` |
| 日期     | string    | YYYY-MM-DD 格式 | `"2024-01-24"`           |
| 时间     | string    | HH:mm:ss 格式   | `"10:30:00"`             |
| 空值     | null      | -               | `null`                   |
| 数组     | array     | 有序集合        | `[1, 2, 3]`              |
| 对象     | object    | 无序集合        | `{"key": "value"}`       |

### 错误处理规范

#### 标准错误码

| 错误码 | HTTP 状态 | 含义           | 用途             |
| ------ | --------- | -------------- | ---------------- |
| 0      | 200/201   | 成功           | 请求成功处理     |
| 400    | 400       | 请求参数错误   | 参数验证失败     |
| 401    | 401       | 未授权         | 认证失败         |
| 403    | 403       | 禁止访问       | 权限不足         |
| 404    | 404       | 资源不存在     | 请求的资源不存在 |
| 409    | 409       | 冲突           | 业务状态冲突     |
| 500    | 500       | 服务器内部错误 | 服务端异常       |
| 503    | 503       | 服务不可用     | 服务暂时不可用   |

#### 错误处理流程

{{errorHandlingFlow}}

### 版本控制策略

#### API 版本管理

{{versioningStrategy}}

#### 向后兼容性

{{backwardCompatibility}}

### 认证与授权

#### 认证方式

{{authenticationMethods}}

#### 授权策略

{{authorizationStrategy}}

### 性能与限流

#### 性能要求

| 指标            | 要求                | 说明         |
| --------------- | ------------------- | ------------ |
| 平均响应时间    | {{avgResponseTime}} | P50 响应时间 |
| 99 分位响应时间 | {{p99ResponseTime}} | P99 响应时间 |
| 吞吐量          | {{throughput}}      | 每秒请求数   |

#### 限流策略

{{rateLimitingStrategy}}

## 相关文档

### 领域内文档

- [[01-domain-overview.md]] - 领域概览
- [[02-domain-design.md]] - 领域模型与业务用例（包含完整事件定义）
- [[03-domain-application.md]] - 应用服务（API 实现）

### 系统级文档

- [[../01-overview/01-domains-overview.md]] - 系统级领域概览
- [[../01-overview/01-domains-overview.md#限界上下文]] - 限界上下文与上下文映射

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人           |
| -------- | ---- | -------- | ---------------- |
| {{date}} | 1.0  | 初始版本 | {{domainExpert}} |
