# {{serviceName}} API 契约定义

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档定义 {{serviceName}} 微服务的 API 契约（API Contract），包括接口契约、数据契约和错误契约。

## 契约类型

### REST API 契约

{{restApiContract}}

### 事件 API 契约

{{eventApiContract}}

## 接口契约

### 请求契约

#### 请求头

| 头名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| {{header1}} | {{headerType1}} | {{required1}} | {{headerDescription1}} |
| {{header2}} | {{headerType2}} | {{required2}} | {{headerDescription2}} |

#### 请求体契约

{{requestBodyContract}}

### 响应契约

#### 响应头

| 头名称 | 类型 | 描述 |
|------|------|------|
| {{responseHeader1}} | {{headerType1}} | {{headerDescription1}} |

#### 响应体契约

{{responseBodyContract}}

## 数据契约

### 数据模型

#### {{dataModel1}}

```json
{
  "{{field1}}": "{{type1}}",
  "{{field2}}": "{{type2}}",
  "{{field3}}": {
    "{{nestedField1}}": "{{nestedType1}}"
  }
}
```

#### 数据验证规则

| 字段 | 验证规则 | 错误消息 |
|------|---------|---------|
| {{field1}} | {{validationRule1}} | {{errorMessage1}} |
| {{field2}} | {{validationRule2}} | {{errorMessage2}} |

### 数据类型定义

| 类型名称 | 定义 | 示例 |
|---------|------|------|
| {{type1}} | {{typeDefinition1}} | {{example1}} |
| {{type2}} | {{typeDefinition2}} | {{example2}} |

## 错误契约

### 错误响应格式

```json
{
  "error": {
    "code": "{{errorCode}}",
    "message": "{{errorMessage}}",
    "details": {
      "{{detailField1}}": "{{detailValue1}}"
    },
    "timestamp": "{{timestamp}}",
    "path": "{{requestPath}}"
  }
}
```

### 错误码定义

| 错误码 | HTTP状态码 | 描述 | 处理建议 |
|--------|-----------|------|---------|
| {{errorCode1}} | {{httpStatusCode1}} | {{errorDescription1}} | {{handlingSuggestion1}} |
| {{errorCode2}} | {{httpStatusCode2}} | {{errorDescription2}} | {{handlingSuggestion2}} |

## 版本契约

### 版本策略

{{versionStrategy}}

### 版本兼容性

| 版本 | 兼容性 | 说明 |
|------|--------|------|
| {{version1}} | {{compatibility1}} | {{description1}} |
| {{version2}} | {{compatibility2}} | {{description2}} |

### 版本废弃计划

| 版本 | 废弃日期 | 替代版本 | 迁移指南 |
|------|---------|---------|---------|
| {{deprecatedVersion1}} | {{deprecationDate1}} | {{replacementVersion1}} | {{migrationGuide1}} |

## 契约测试

### 契约测试策略

{{contractTestingStrategy}}

### 契约测试工具

{{contractTestingTools}}

### 契约测试用例

{{contractTestCases}}

## 契约文档

### OpenAPI/Swagger

{{openApiSpec}}

### GraphQL Schema

{{graphqlSchema}}

## 契约变更管理

### 变更流程

{{changeProcess}}

### 变更通知

{{changeNotification}}

## 相关文档

- [[rest-api.md]] - REST API文档
- [[event-api.md]] - 事件接口文档
- [[../02-domain/domain-overview.md]] - 领域概览

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{architect}} |

