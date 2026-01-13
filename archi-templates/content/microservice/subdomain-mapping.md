# {{serviceName}} 子领域映射

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的子领域映射和上下文映射（Context Mapping），包括与其他微服务的集成关系。

## 子领域映射

### 子领域分类

```mermaid
graph LR
    A[{{domainName}}] --> B[核心域]
    A --> C[支撑域]
    A --> D[通用域]
    B --> E[{{coreDomain1}}]
    B --> F[{{coreDomain2}}]
    C --> G[{{supportingDomain1}}]
    C --> H[{{supportingDomain2}}]
    D --> I[{{genericDomain1}}]
    D --> J[{{genericDomain2}}]
```

### 子领域详细映射

| 子领域名称 | 类型 | 描述 | 重要性 | 投资优先级 |
|-----------|------|------|--------|-----------|
| {{subdomain1}} | 核心域 | {{description1}} | {{importance1}} | {{priority1}} |
| {{subdomain2}} | 支撑域 | {{description2}} | {{importance2}} | {{priority2}} |
| {{subdomain3}} | 通用域 | {{description3}} | {{importance3}} | {{priority3}} |

> **说明**：
> - 技术工具（如异常处理、日志、ID生成器等）属于基础设施层，不属于通用域。技术工具文档详见 [[infrastructure/tools/01-tools-overview.md]]。
> - 数据访问抽象提供通用抽象接口（IRepository<T>、IQueryBuilder<T>、ITransactionManager），属于基础设施层抽象，不属于通用域。具体业务域的Repository接口（如 `I{{AggregateRoot1}}Repository`）定义在各自的领域模型文档中，属于领域层。数据访问抽象文档详见 [[infrastructure/data-access/01-data-access-abstraction.md]]。

## 基础设施层技术工具

基础设施层技术工具不属于子领域，但为所有子领域提供技术支持。这些工具提供纯粹的技术能力，不包含业务逻辑，是纯粹的技术实现。

### 工具列表

基础设施层技术工具包括以下工具：

| 工具名称         | 英文名称                   | 描述                                                                                                          | 优先级 |
| ---------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------- | ------ |
| 异常处理         | Exception Handling         | 统一的异常捕获、分类和处理机制，支持异常恢复和错误报告                                                        | P1     |
| 日志             | Logging                    | 应用日志和错误日志的记录和管理                                                                                | P1     |
| ID 生成器        | ID Generator               | 唯一标识符生成，包括 UUID、有序 ID 等                                                                          | P1     |
| 序列化服务       | Serialization Service      | 数据序列化和反序列化，支持 JSON、二进制等格式                                                                  | P1     |
| 时间服务         | Time Service               | 时间相关操作，包括时区处理、时间格式化等                                                                        | P2     |
| 加密服务         | Encryption Service         | 数据加密和解密服务，保护敏感数据                                                                                | P0     |
| 数据验证工具     | Data Validation Tool       | 数据格式和规则验证工具                                                                                          | P1     |
| 资源管理工具     | Resource Management Tool   | 系统资源管理，包括内存、CPU 监控和管理                                                                          | P1     |
| 异步任务管理工具 | Async Task Management Tool | 异步任务执行管理，包括 Dart Isolate 池管理、任务队列等                                                        | P0     |
| 缓存管理工具     | Cache Management Tool      | 内存缓存管理，提升数据访问性能                                                                                  | P0     |

### 依赖关系

所有子领域都依赖基础设施层技术工具，通过客户-供应商（C-S）关系使用这些工具：

- **依赖类型**：客户-供应商（C-S）
- **集成方式**：工具类/工具函数
- **使用场景**：所有子领域在实现过程中需要使用各种技术工具能力

## 基础设施层数据访问抽象

数据访问抽象不属于子领域，但为所有子领域提供数据访问的通用抽象接口支持。

**数据访问抽象**：
- **类型**：基础设施层抽象
- **描述**：提供通用的数据访问抽象接口（IRepository<T>、IQueryBuilder<T>、ITransactionManager），支持 Repository 模式，实现领域层与基础设施层的解耦
- **重要性**：高
- **投资优先级**：P0

**职责划分**：
- **数据访问抽象**：仅提供通用抽象接口，属于基础设施层抽象
- **具体业务域Repository接口**：定义在各业务域的领域模型文档中（如 `I{{AggregateRoot1}}Repository` 在{{coreDomain1}}域的领域模型文档中），属于领域层
- **Repository实现**：在基础设施层实现领域层定义的具体Repository接口

**详细文档**：[[infrastructure/data-access/01-data-access-abstraction.md]]

### 相关文档

- [[infrastructure/01-infrastructure-overview.md]] - 基础设施层概览
- [[infrastructure/tools/01-tools-overview.md]] - 技术工具概览（包含详细设计和使用说明）
- [[infrastructure/data-access/01-data-access-abstraction.md]] - 数据访问抽象设计

## 上下文映射（Context Mapping）

> **说明**：上下文映射描述了子领域（限界上下文）之间的协作关系。详细的上下文映射关系定义请参考 [[bounded-context.md#上下文映射关系]] 文档。

### 上下文映射概览

{{serviceName}} 采用本地优先架构（或微服务架构），所有子领域通过领域事件和接口抽象实现解耦。主要的协作模式包括：

- **发布-订阅（P-S）**：通过事件总线实现异步通信
- **客户-供应商（C-S）**：通过接口抽象实现同步调用
- **共享内核（SK）**：多个子领域共享通用能力
- **防腐层（ACL）**：隔离外部系统，保护领域模型

### 与其他微服务的集成关系（如适用）

| 微服务名称 | 关系类型 | 描述 | 集成方式 |
|-----------|---------|------|---------|
| {{microservice1}} | {{relationshipType1}} | {{description1}} | {{integrationMethod1}} |
| {{microservice2}} | {{relationshipType2}} | {{description2}} | {{integrationMethod2}} |
| {{microservice3}} | {{relationshipType3}} | {{description3}} | {{integrationMethod3}} |

> 详细的上下文映射关系、关系类型说明和集成策略请参考 [[bounded-context.md]] 文档。

## 领域间依赖关系

### 依赖关系图

```mermaid
graph TD
    A[核心域] --> B[支撑域]
    A --> C[通用域]
    B --> C
    A --> D[{{microservice1}}]
    B --> E[{{microservice2}}]
```

### 依赖清单

| 依赖方 | 被依赖方 | 依赖类型 | 描述 |
|--------|---------|---------|------|
| {{dependent1}} | {{dependency1}} | {{dependencyType1}} | {{description1}} |
| {{dependent2}} | {{dependency2}} | {{dependencyType2}} | {{description2}} |

## 集成策略

### 同步集成

{{synchronousIntegration}}

### 异步集成

{{asynchronousIntegration}}

### 数据一致性

{{dataConsistency}}

## 相关文档

- [[domain-overview.md]] - 领域概览
- [[bounded-context.md]] - 限界上下文（详细的上下文映射关系）
- [[../01-overview/context-diagram.md]] - 系统上下文图

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |

