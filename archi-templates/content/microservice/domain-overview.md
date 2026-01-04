# {{serviceName}} 领域概览

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的领域模型概览，包括总体领域划分和子领域说明。

## 领域定义

### 领域名称

{{domainName}}

### 领域描述

{{domainDescription}}

### 领域边界

{{domainBoundary}}

## 总体领域划分

### 领域划分图

```mermaid
mindmap
  root(({{domainName}}))
    核心域
      {{coreDomain1}}
      {{coreDomain2}}
    支撑域
      {{supportingDomain1}}
      {{supportingDomain2}}
    通用域
      {{genericDomain1}}
      {{genericDomain2}}
```

## 子领域分类

### 核心域（Core Domain）

| 子领域名称 | 描述 | 重要性 |
|-----------|------|--------|
| {{coreDomain1}} | {{description1}} | {{importance1}} |
| {{coreDomain2}} | {{description2}} | {{importance2}} |

### 支撑域（Supporting Domain）

| 子领域名称 | 描述 | 重要性 |
|-----------|------|--------|
| {{supportingDomain1}} | {{description1}} | {{importance1}} |
| {{supportingDomain2}} | {{description2}} | {{importance2}} |

### 通用域（Generic Domain）

| 子领域名称 | 描述 | 重要性 |
|-----------|------|--------|
| {{genericDomain1}} | {{description1}} | {{importance1}} |
| {{genericDomain2}} | {{description2}} | {{importance2}} |

## 领域模型概览

### 主要聚合

| 聚合名称 | 所属子领域 | 描述 |
|---------|-----------|------|
| {{aggregate1}} | {{subdomain1}} | {{description1}} |
| {{aggregate2}} | {{subdomain2}} | {{description2}} |

### 主要实体

| 实体名称 | 所属聚合 | 描述 |
|---------|---------|------|
| {{entity1}} | {{aggregate1}} | {{description1}} |
| {{entity2}} | {{aggregate2}} | {{description2}} |

## 领域事件概览

| 事件名称 | 发布者 | 订阅者 | 描述 |
|---------|--------|--------|------|
| {{event1}} | {{publisher1}} | {{subscriber1}} | {{description1}} |
| {{event2}} | {{publisher2}} | {{subscriber2}} | {{description2}} |

## 相关文档

- [[subdomain-mapping.md]] - 子领域映射
- [[bounded-context.md]] - 限界上下文
- [[glossary.md]] - 领域术语表
- [[core-domain/README.md]] - 核心域详情

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |

