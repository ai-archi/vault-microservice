# {{subdomainName}} 聚合根详细说明

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档详细说明 {{subdomainName}} 子领域中的聚合根（Aggregate Root）。

## 聚合根列表

| 聚合根名称 | 英文名称 | 描述 | 一致性边界 |
|-----------|---------|------|-----------|
| {{aggregateRoot1}} | {{englishName1}} | {{description1}} | {{consistencyBoundary1}} |
| {{aggregateRoot2}} | {{englishName2}} | {{description2}} | {{consistencyBoundary2}} |

## 聚合根详细说明

### {{aggregateRoot1}}

#### 聚合根定义

{{aggregateRootDefinition1}}

#### 聚合边界

{{aggregateBoundary1}}

#### 聚合内实体

| 实体名称 | 类型 | 描述 | 关系 |
|---------|------|------|------|
| {{entity1}} | 实体 | {{description1}} | {{relationship1}} |
| {{entity2}} | 值对象 | {{description2}} | {{relationship2}} |

#### 聚合根属性

| 属性名称 | 类型 | 描述 | 约束 |
|---------|------|------|------|
| {{property1}} | {{type1}} | {{description1}} | {{constraint1}} |
| {{property2}} | {{type2}} | {{description2}} | {{constraint2}} |

#### 聚合根方法

| 方法名称 | 参数 | 返回值 | 描述 | 业务规则 |
|---------|------|--------|------|---------|
| {{method1}} | {{parameters1}} | {{returnType1}} | {{description1}} | {{businessRule1}} |
| {{method2}} | {{parameters2}} | {{returnType2}} | {{description2}} | {{businessRule2}} |

#### 不变性约束

{{invariantConstraints1}}

#### 生命周期

{{lifecycle1}}

#### 聚合图

```mermaid
classDiagram
    class {{AggregateRoot1}} {
        +{{property1}}
        +{{method1}}()
        +{{method2}}()
    }
    class {{Entity1}} {
        +{{property1}}
    }
    class {{ValueObject1}} {
        +{{property1}}
        +{{property2}}
    }
    
    {{AggregateRoot1}} *-- {{Entity1}}
    {{AggregateRoot1}} *-- {{ValueObject1}}
```

### {{aggregateRoot2}}

#### 聚合根定义

{{aggregateRootDefinition2}}

#### 聚合边界

{{aggregateBoundary2}}

#### 聚合内实体

| 实体名称 | 类型 | 描述 | 关系 |
|---------|------|------|------|
| {{entity3}} | 实体 | {{description3}} | {{relationship3}} |

## 聚合间关系

### 关系图

```mermaid
graph LR
    A[{{AggregateRoot1}}] -->|领域事件| B[{{AggregateRoot2}}]
    A -->|引用ID| C[{{AggregateRoot3}}]
```

### 关系说明

| 源聚合 | 目标聚合 | 关系类型 | 描述 |
|--------|---------|---------|------|
| {{sourceAggregate1}} | {{targetAggregate1}} | {{relationshipType1}} | {{description1}} |
| {{sourceAggregate2}} | {{targetAggregate2}} | {{relationshipType2}} | {{description2}} |

## 聚合设计原则

### 一致性边界

{{consistencyBoundary}}

### 事务边界

{{transactionBoundary}}

### 并发控制

{{concurrencyControl}}

## 相关文档

- [[README.md]] - 子领域说明
- [[domain-model.md]] - 领域模型
- [[domain-events.md]] - 领域事件定义

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |

