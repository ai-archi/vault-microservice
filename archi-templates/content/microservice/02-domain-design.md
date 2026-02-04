# {{subdomainName}} 领域设计

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档包含 {{subdomainName}} 子领域的**领域模型**与**业务用例**。领域事件定义以本文档「领域事件定义」节为单一真实来源（SSOT）；用例中仅链接到前文，不重复定义。

---

# 第一部分：领域模型

## 领域模型图

```mermaid
classDiagram
    class {{AggregateRoot1}} {
        +{{property1}}
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

## 聚合设计

### {{aggregate1}}

#### 聚合根

{{aggregateRoot1}}

#### 聚合描述

{{aggregateDescription1}}

#### 聚合边界

**边界内**：
{{aggregateBoundaryInside1}}

**边界外**：
{{aggregateBoundaryOutside1}}

#### 聚合内实体

| 实体名称    | 类型   | 描述             | 关系                                          |
| ----------- | ------ | ---------------- | --------------------------------------------- |
| {{entity1}} | 实体   | {{description1}} | {{aggregateRoot1}} 聚合根拥有多个 {{entity1}} |
| {{entity2}} | 值对象 | {{description2}} | {{aggregateRoot1}} 聚合根包含 {{entity2}}     |

#### 聚合根属性

| 属性名称      | 类型      | 描述             | 约束            |
| ------------- | --------- | ---------------- | --------------- |
| {{property1}} | {{type1}} | {{description1}} | {{constraint1}} |
| {{property2}} | {{type2}} | {{description2}} | {{constraint2}} |

#### 聚合根方法

| 方法名称    | 参数            | 返回值          | 描述             | 业务规则          |
| ----------- | --------------- | --------------- | ---------------- | ----------------- |
| {{method1}} | {{parameters1}} | {{returnType1}} | {{description1}} | {{businessRule1}} |
| {{method2}} | {{parameters2}} | {{returnType2}} | {{description2}} | {{businessRule2}} |

#### 不变性约束

1. **{{constraint1}}**：{{constraintDescription1}}
2. **{{constraint2}}**：{{constraintDescription2}}
3. **{{constraint3}}**：{{constraintDescription3}}

#### 生命周期

**创建**：
{{lifecycleCreation1}}

**运行**：
{{lifecycleRuntime1}}

**销毁**：
{{lifecycleDestruction1}}

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
        +{{method1}}()
    }
    class {{ValueObject1}} {
        +{{property1}}
        +{{property2}}
    }

    {{AggregateRoot1}} *-- {{Entity1}}
    {{AggregateRoot1}} *-- {{ValueObject1}}
```

### {{aggregate2}}

#### 聚合根

{{aggregateRoot2}}

#### 聚合描述

{{aggregateDescription2}}

#### 聚合边界

{{aggregateBoundary2}}

## 实体详细设计

### {{entity1}}

#### 实体定义

{{entityDefinition1}}

#### 实体属性

| 属性名称      | 类型      | 描述             | 约束            |
| ------------- | --------- | ---------------- | --------------- |
| {{property1}} | {{type1}} | {{description1}} | {{constraint1}} |
| {{property2}} | {{type2}} | {{description2}} | {{constraint2}} |

#### 实体行为方法

| 方法名称    | 参数            | 返回值          | 描述             | 业务规则          |
| ----------- | --------------- | --------------- | ---------------- | ----------------- |
| {{method1}} | {{parameters1}} | {{returnType1}} | {{description1}} | {{businessRule1}} |
| {{method2}} | {{parameters2}} | {{returnType2}} | {{description2}} | {{businessRule2}} |

#### 业务规则

1. **{{rule1}}**：{{ruleDescription1}}
2. **{{rule2}}**：{{ruleDescription2}}

### {{entity2}}

#### 实体定义

{{entityDefinition2}}

#### 实体属性

| 属性名称      | 类型      | 描述             | 约束            |
| ------------- | --------- | ---------------- | --------------- |
| {{property3}} | {{type3}} | {{description3}} | {{constraint3}} |

## 值对象详细设计

### {{valueObject1}}

#### 值对象定义

{{valueObjectDefinition1}}

#### 值对象属性

| 属性名称      | 类型      | 描述             |
| ------------- | --------- | ---------------- |
| {{property1}} | {{type1}} | {{description1}} |
| {{property2}} | {{type2}} | {{description2}} |

#### 值对象不变性

{{valueObjectImmutability1}}

### {{valueObject2}}

#### 值对象定义

{{valueObjectDefinition2}}

#### 值对象属性

| 属性名称      | 类型      | 描述             |
| ------------- | --------- | ---------------- |
| {{property3}} | {{type3}} | {{description3}} |

## 领域服务设计

### {{domainService1}}

#### 服务描述

{{serviceDescription1}}

#### 服务职责

{{serviceResponsibilities1}}

#### 服务接口定义

| 方法名称    | 参数            | 返回值          | 描述             | 业务规则          |
| ----------- | --------------- | --------------- | ---------------- | ----------------- |
| {{method1}} | {{parameters1}} | {{returnType1}} | {{description1}} | {{businessRule1}} |
| {{method2}} | {{parameters2}} | {{returnType2}} | {{description2}} | {{businessRule2}} |

#### 接口示例

```dart
abstract class I{{DomainService1}} {
  /// {{description1}}
  {{returnType1}} {{method1}}({{parameters1}});

  /// {{description2}}
  {{returnType2}} {{method2}}({{parameters2}});
}
```

#### 服务实现说明

{{implementationDescription1}}

#### 业务规则和约束

{{businessRulesAndConstraints1}}

#### 使用场景

{{usageScenarios1}}

### {{domainService2}}

#### 服务描述

{{serviceDescription2}}

#### 服务职责

{{serviceResponsibilities2}}

#### 服务接口定义

| 方法名称    | 参数            | 返回值          | 描述             | 业务规则          |
| ----------- | --------------- | --------------- | ---------------- | ----------------- |
| {{method3}} | {{parameters3}} | {{returnType3}} | {{description3}} | {{businessRule3}} |

## 领域事件定义

> **重要**：本节是领域事件定义的**单一真实来源（SSOT）**。用例与 API 文档中提及的事件应链接到本部分。

### {{domainEvent1}}

#### 事件定义

{{eventDefinition1}}

#### 事件属性

| 属性名称      | 类型      | 描述             | 必填          |
| ------------- | --------- | ---------------- | ------------- |
| {{property1}} | {{type1}} | {{description1}} | {{required1}} |
| {{property2}} | {{type2}} | {{description2}} | {{required2}} |

#### 事件结构

```json
{
  "eventType": "{{domainEvent1}}",
  "eventId": "{{eventId}}",
  "timestamp": "{{timestamp}}",
  "aggregateId": "{{aggregateId}}",
  "aggregateType": "{{aggregateType}}",
  "version": {{version}},
  "data": {
    "{{property1}}": "{{value1}}",
    "{{property2}}": "{{value2}}"
  }
}
```

#### 事件发布者

{{eventPublisher1}}

#### 事件订阅者

{{eventSubscribers1}}

#### 事件流说明

{{eventFlowDescription1}}

### {{domainEvent2}}

#### 事件定义

{{eventDefinition2}}

#### 事件属性

| 属性名称      | 类型      | 描述             | 必填          |
| ------------- | --------- | ---------------- | ------------- |
| {{property3}} | {{type3}} | {{description3}} | {{required3}} |

## Repository 接口定义

### I{{AggregateRoot1}}Repository

#### 接口定义

```dart
abstract class I{{AggregateRoot1}}Repository {
  /// 根据ID查找聚合根
  Future<{{AggregateRoot1}}?> findById(String id);

  /// 保存聚合根
  Future<void> save({{AggregateRoot1}} aggregate);

  /// 删除聚合根
  Future<void> delete(String id);

  /// 查找所有聚合根
  Future<List<{{AggregateRoot1}}>> findAll();
}
```

#### 方法签名

| 方法名称 | 参数                         | 返回值                           | 描述               |
| -------- | ---------------------------- | -------------------------------- | ------------------ |
| findById | String id                    | Future<{{AggregateRoot1}}?>      | 根据 ID 查找聚合根 |
| save     | {{AggregateRoot1}} aggregate | Future<void>                     | 保存聚合根         |
| delete   | String id                    | Future<void>                     | 删除聚合根         |
| findAll  | void                         | Future<List<{{AggregateRoot1}}>> | 查找所有聚合根     |

#### 接口契约

**前置条件**：findById: id 不能为空；save: aggregate 不能为空且通过聚合根业务规则验证；delete: id 不能为空。

**后置条件**：findById: 存在则返回聚合根否则 null；save: 已持久化且状态一致；delete: 已从持久化删除。

**不变式**：所有方法执行后聚合根一致性边界保持不变；状态变化必须通过聚合根方法进行。

### I{{AggregateRoot2}}Repository

#### 接口定义

```dart
abstract class I{{AggregateRoot2}}Repository {
  Future<{{AggregateRoot2}}?> findById(String id);
  Future<void> save({{AggregateRoot2}} aggregate);
}
```

## 业务规则和约束

### 聚合级别规则

1. **{{aggregateRule1}}**：{{aggregateRuleDescription1}}
2. **{{aggregateRule2}}**：{{aggregateRuleDescription2}}

### 实体级别规则

1. **{{entityRule1}}**：{{entityRuleDescription1}}
2. **{{entityRule2}}**：{{entityRuleDescription2}}

### 值对象级别规则

1. **{{valueObjectRule1}}**：{{valueObjectRuleDescription1}}
2. **{{valueObjectRule2}}**：{{valueObjectRuleDescription2}}

### 领域服务级别规则

1. **{{serviceRule1}}**：{{serviceRuleDescription1}}
2. **{{serviceRule2}}**：{{serviceRuleDescription2}}

## 领域模型关系

### 聚合间关系

```mermaid
graph LR
    A[{{Aggregate1}}] -->|领域事件| B[{{Aggregate2}}]
    A -->|引用ID| C[{{Aggregate3}}]
    D[{{Aggregate2}}] -->|领域事件| E[{{Aggregate4}}]
```

### 关系说明

| 源聚合               | 目标聚合             | 关系类型              | 描述             |
| -------------------- | -------------------- | --------------------- | ---------------- |
| {{sourceAggregate1}} | {{targetAggregate1}} | {{relationshipType1}} | {{description1}} |
| {{sourceAggregate2}} | {{targetAggregate2}} | {{relationshipType2}} | {{description2}} |

---

# 第二部分：业务用例

## 用例列表

| 用例 ID | 用例名称     | 优先级        | 描述             |
| ------- | ------------ | ------------- | ---------------- |
| UC-001  | {{useCase1}} | {{priority1}} | {{description1}} |
| UC-002  | {{useCase2}} | {{priority2}} | {{description2}} |
| UC-003  | {{useCase3}} | {{priority3}} | {{description3}} |

## 用例详细说明

### UC-001: {{useCase1}}

#### 用例描述

{{useCaseDescription1}}

#### 参与者

{{actors1}}

#### 前置条件

{{preconditions1}}

#### 后置条件

{{postconditions1}}

#### 主流程

1. {{step1}}
2. {{step2}}
3. {{step3}}

#### 备选流程

**备选流程 A**: {{alternativeFlowA}}

1. {{stepA1}}
2. {{stepA2}}

**备选流程 B**: {{alternativeFlowB}}

1. {{stepB1}}
2. {{stepB2}}

#### 异常流程

**异常流程 1**: {{exceptionFlow1}}

1. {{exceptionStep1}}
2. {{exceptionStep2}}

#### 业务规则

{{businessRules1}}

#### 涉及聚合

{{involvedAggregates1}}

#### 领域事件

此用例发布的领域事件请参考：[[#{{domainEvent1}}|{{domainEvent1}}]]、[[#{{domainEvent2}}|{{domainEvent2}}]]

> 事件定义维护在本文档「领域事件定义」中作为单一真实来源。

#### 用例图

```mermaid
sequenceDiagram
    participant User
    participant ApplicationService
    participant AggregateRoot
    participant Repository

    User->>ApplicationService: {{action1}}
    ApplicationService->>AggregateRoot: {{method1}}()
    AggregateRoot->>AggregateRoot: {{businessLogic1}}
    AggregateRoot->>Repository: {{saveMethod}}()
    AggregateRoot-->>ApplicationService: {{domainEvent1}}
    ApplicationService-->>User: {{response1}}
```

### UC-002: {{useCase2}}

#### 用例描述

{{useCaseDescription2}}

#### 参与者

{{actors2}}

#### 前置条件

{{preconditions2}}

#### 后置条件

{{postconditions2}}

#### 主流程

1. {{step1}}
2. {{step2}}
3. {{step3}}

## 用例关系

### 用例关系图

```mermaid
graph TD
    A[{{useCase1}}] --> B[{{useCase2}}]
    A --> C[{{useCase3}}]
    B --> D[{{useCase4}}]
```

### 包含关系

| 主用例           | 包含用例             | 描述             |
| ---------------- | -------------------- | ---------------- |
| {{mainUseCase1}} | {{includedUseCase1}} | {{description1}} |

### 扩展关系

| 基础用例         | 扩展用例              | 扩展点              | 描述             |
| ---------------- | --------------------- | ------------------- | ---------------- |
| {{baseUseCase1}} | {{extendingUseCase1}} | {{extensionPoint1}} | {{description1}} |

## 业务价值

{{businessValue}}

## 相关文档

- [[01-domain-overview.md]] - 领域概览
- [[03-domain-application.md]] - 应用层设计
- [[04-domain-api-design.md]] - API 设计

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人           |
| -------- | ---- | -------- | ---------------- |
| {{date}} | 1.0  | 初始版本 | {{domainExpert}} |
