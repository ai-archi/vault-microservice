# {{serviceName}} 外部依赖清单

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档列出 {{serviceName}} 微服务的所有外部依赖，包括其他微服务、第三方服务和基础设施依赖。

## 依赖分类

### 微服务依赖

| 服务名称 | 依赖类型 | 接口类型 | 描述 | SLA要求 |
|---------|---------|---------|------|---------|
| {{microservice1}} | {{dependencyType1}} | {{interfaceType1}} | {{description1}} | {{slaRequirement1}} |
| {{microservice2}} | {{dependencyType2}} | {{interfaceType2}} | {{description2}} | {{slaRequirement2}} |

### 第三方服务依赖

| 服务名称 | 提供商 | 依赖类型 | 描述 | SLA |
|---------|--------|---------|------|-----|
| {{thirdPartyService1}} | {{provider1}} | {{dependencyType1}} | {{description1}} | {{sla1}} |
| {{thirdPartyService2}} | {{provider2}} | {{dependencyType2}} | {{description2}} | {{sla2}} |

### 基础设施依赖

| 依赖名称 | 类型 | 描述 | 高可用性 |
|---------|------|------|---------|
| {{infrastructure1}} | {{infrastructureType1}} | {{description1}} | {{highAvailability1}} |
| {{infrastructure2}} | {{infrastructureType2}} | {{description2}} | {{highAvailability2}} |

## 依赖关系图

```mermaid
graph TB
    A[{{serviceName}}] --> B[{{microservice1}}]
    A --> C[{{microservice2}}]
    A --> D[{{thirdPartyService1}}]
    A --> E[数据库]
    A --> F[消息队列]
    A --> G[缓存]
```

## 依赖健康检查

### 健康检查配置

{{healthCheckConfig}}

### 健康检查频率

{{healthCheckFrequency}}

## 依赖降级策略

### 降级策略

{{degradationStrategy}}

### 熔断器配置

{{circuitBreakerConfig}}

### 重试策略

{{retryStrategy}}

## 依赖监控

### 监控指标

{{monitoringMetrics}}

### 告警规则

{{alertRules}}

## 依赖变更管理

### 变更通知

{{changeNotification}}

### 版本兼容性

{{versionCompatibility}}

## 相关文档

- [[../01-overview/context-diagram.md]] - 系统上下文图
- [[../03-apis/rest-api.md]] - REST API文档
- [[runbook.md]] - 故障处理手册

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{architect}} |

