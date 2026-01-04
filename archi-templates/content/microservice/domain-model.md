# {{subdomainName}} 领域模型

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{subdomainName}} 子领域的领域模型，包括聚合、实体、值对象和领域事件。

## 领域模型图

```mermaid
classDiagram
    class {{AggregateRoot1}} {
        +{{method1}}()
        +{{method2}}()
    }
    class {{Entity1}} {
        +{{property1}}
        +{{method1}}()
    }
    class {{ValueObject1}} {
        +{{property1}}
        +{{property2}}
    }
    class {{DomainService1}} {
        +{{method1}}()
    }
    
    {{AggregateRoot1}} --> {{Entity1}}
    {{AggregateRoot1}} --> {{ValueObject1}}
    {{AggregateRoot1}} ..> {{DomainService1}}
```

## 聚合

### {{aggregate1}}

#### 聚合根

{{aggregateRoot1}}

#### 聚合描述

{{aggregateDescription1}}

#### 聚合边界

{{aggregateBoundary1}}

#### 聚合内实体

| 实体名称 | 类型 | 描述 |
|---------|------|------|
| {{entity1}} | 实体 | {{description1}} |
| {{entity2}} | 值对象 | {{description2}} |

### {{aggregate2}}

#### 聚合根

{{aggregateRoot2}}

#### 聚合描述

{{aggregateDescription2}}

#### 聚合边界

{{aggregateBoundary2}}

## 实体

### {{entity1}}

#### 实体定义

{{entityDefinition1}}

#### 实体属性

| 属性名称 | 类型 | 描述 | 约束 |
|---------|------|------|------|
| {{property1}} | {{type1}} | {{description1}} | {{constraint1}} |
| {{property2}} | {{type2}} | {{description2}} | {{constraint2}} |

#### 实体行为

{{entityBehavior1}}

### {{entity2}}

#### 实体定义

{{entityDefinition2}}

#### 实体属性

| 属性名称 | 类型 | 描述 | 约束 |
|---------|------|------|------|
| {{property3}} | {{type3}} | {{description3}} | {{constraint3}} |

## 值对象

### {{valueObject1}}

#### 值对象定义

{{valueObjectDefinition1}}

#### 值对象属性

| 属性名称 | 类型 | 描述 |
|---------|------|------|
| {{property1}} | {{type1}} | {{description1}} |
| {{property2}} | {{type2}} | {{description2}} |

#### 值对象不变性

{{valueObjectImmutability1}}

### {{valueObject2}}

#### 值对象定义

{{valueObjectDefinition2}}

## 领域服务

### {{domainService1}}

#### 服务描述

{{serviceDescription1}}

#### 服务方法

| 方法名称 | 参数 | 返回值 | 描述 |
|---------|------|--------|------|
| {{method1}} | {{parameters1}} | {{returnType1}} | {{description1}} |
| {{method2}} | {{parameters2}} | {{returnType2}} | {{description2}} |

## 领域事件

### {{domainEvent1}}

#### 事件定义

{{eventDefinition1}}

#### 事件属性

| 属性名称 | 类型 | 描述 |
|---------|------|------|
| {{property1}} | {{type1}} | {{description1}} |
| {{property2}} | {{type2}} | {{description2}} |

#### 事件发布者

{{eventPublisher1}}

#### 事件订阅者

{{eventSubscribers1}}

## 领域模型关系

### 关系图

```mermaid
graph LR
    A[{{Aggregate1}}] --> B[{{Entity1}}]
    A --> C[{{ValueObject1}}]
    D[{{Aggregate2}}] --> E[{{Entity2}}]
    A -->|领域事件| F[{{DomainEvent1}}]
    D -->|领域事件| F
```

## 业务规则

### 规则1

{{businessRule1}}

### 规则2

{{businessRule2}}

## 相关文档

- [[README.md]] - 子领域说明
- [[use-cases.md]] - 业务用例
- [[aggregates.md]] - 聚合根详细说明
- [[domain-events.md]] - 领域事件定义

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |

