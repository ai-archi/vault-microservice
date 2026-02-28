# {{serviceName}} 审计日志规范

**创建日期**: {{date}}  
**安全工程师**: {{securityEngineer}}  
**版本**: 1.0

## 概述

本文档定义 {{serviceName}} 微服务的审计日志（Audit Log）规范。

## 审计日志范围

### 需要审计的操作

| 操作类型 | 描述 | 审计级别 |
|---------|------|---------|
| {{operationType1}} | {{description1}} | {{auditLevel1}} |
| {{operationType2}} | {{description2}} | {{auditLevel2}} |

### 审计事件类型

{{auditEventTypes}}

## 审计日志格式

### 日志结构

```json
{
  "timestamp": "{{timestamp}}",
  "eventType": "{{eventType}}",
  "userId": "{{userId}}",
  "userName": "{{userName}}",
  "action": "{{action}}",
  "resource": "{{resource}}",
  "resourceId": "{{resourceId}}",
  "result": "{{result}}",
  "ipAddress": "{{ipAddress}}",
  "userAgent": "{{userAgent}}",
  "details": {
    "{{detailField1}}": "{{detailValue1}}"
  }
}
```

### 日志字段定义

| 字段名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| timestamp | string | 是 | 事件发生时间 |
| eventType | string | 是 | 事件类型 |
| userId | string | 是 | 用户ID |
| action | string | 是 | 操作动作 |
| resource | string | 是 | 资源类型 |
| result | string | 是 | 操作结果 |

## 审计日志存储

### 存储位置

{{auditLogStorage}}

### 存储策略

{{storageStrategy}}

### 保留期限

{{retentionPeriod}}

## 审计日志查询

### 查询接口

{{queryInterface}}

### 查询权限

{{queryPermissions}}

## 审计日志分析

### 分析指标

{{analysisMetrics}}

### 异常检测

{{anomalyDetection}}

## 合规要求

{{complianceRequirements}}

## 相关文档

- [[threat-model.md]] - 威胁建模
- [[authz-authn.md]] - 鉴权认证策略
- [[data-protection.md]] - 数据保护

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{securityEngineer}} |

