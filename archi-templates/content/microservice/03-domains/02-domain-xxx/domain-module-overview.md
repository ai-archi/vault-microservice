# {{domainName}} 模块概览

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

本文档为 {{domainName}} 领域的模块总览，涵盖领域定义、技术栈、领域交互、应用层与领域层设计、基础设施与 API 设计。单文档按 DDD 组织，系统级领域划分见 [[../01-overview/01-domains-overview.md]]。

---

## 1. 概述与领域定义

### 领域名称

{{domainName}}

### 领域描述

{{domainDescription}}

### 领域职责

{{domainName}} 领域主要负责：

- {{responsibility1}}
- {{responsibility2}}
- {{responsibility3}}

### 领域边界

**{{domainName}} 领域包含**：

- ✅ {{inScope1}}
- ✅ {{inScope2}}
- ✅ {{inScope3}}

**{{domainName}} 领域不包含**：

- ❌ {{outScope1}}
- ❌ {{outScope2}}

---

## 2. 技术栈与领域交互

### 核心技术

| 技术类型  | 技术选型                | 说明                        |
| --------- | ----------------------- | --------------------------- |
| 编程语言  | {{programmingLanguage}} | {{programmingLanguageNote}} |
| 框架/库   | {{framework}}           | {{frameworkNote}}           |
| 数据存储  | {{storage}}             | {{storageNote}}             |
| 消息/事件 | {{messaging}}           | {{messagingNote}}           |

### 特殊技术需求

{{specialTechnicalRequirements}}

### 依赖的其他领域

| 依赖领域             | 依赖类型            | 交互方式               | 说明             |
| -------------------- | ------------------- | ---------------------- | ---------------- |
| {{dependentDomain1}} | {{dependencyType1}} | {{interactionMethod1}} | {{description1}} |
| {{dependentDomain2}} | {{dependencyType2}} | {{interactionMethod2}} | {{description2}} |

### 被其他领域依赖

| 依赖方领域             | 依赖类型            | 交互方式               | 说明             |
| ---------------------- | ------------------- | ---------------------- | ---------------- |
| {{dependentByDomain1}} | {{dependencyType1}} | {{interactionMethod1}} | {{description1}} |
| {{dependentByDomain2}} | {{dependencyType2}} | {{interactionMethod2}} | {{description2}} |

### 领域接口摘要

| 类型     | 名称                | 说明                  |
| -------- | ------------------- | --------------------- |
| 端口     | {{portName1}}       | {{portDesc1}}         |
| 仓储     | {{repositoryName1}} | {{repositoryDesc1}}   |
| REST API | {{apiName1}}        | {{apiDescription1}}   |
| 领域事件 | {{eventName1}}      | {{eventDescription1}} |

---

## 3. 架构设计

### 架构定位

{{domainName}} 在系统架构中的位置：

```
┌─────────────────────────────────────┐
│  调用方 / 上游领域                    │
│  通过端口或 API 调用本领域            │
└──────────────┬──────────────────────┘
               │ 端口 / API
┌──────────────▼──────────────────────┐
│  {{domainName}}                      │
│  应用层、领域层                       │
└──────────────┬──────────────────────┘
               │ 使用
┌──────────────▼──────────────────────┐
│  基础设施层                          │
│  仓储实现、外部客户端、技术组件       │
└─────────────────────────────────────┘
```

### 设计原则

- {{designPrinciple1}}
- {{designPrinciple2}}
- {{designPrinciple3}}

---

## 4. 核心概念与目录结构

### 核心概念

{{domainName}} 领域的核心概念包括：

- **{{concept1}}**：{{concept1Description}}
- **{{concept2}}**：{{concept2Description}}
- **{{concept3}}**：{{concept3Description}}

### 代码目录结构（DDD 分层）

```
src/main/java/{{packagePath}}/
├── interfaces/       # 表现层：REST 控制器、DTO、契约
├── application/     # 应用层：应用服务、用例编排
├── domain/          # 领域层：实体、值对象、领域服务、仓储接口、端口
└── infrastructure/  # 基础设施层：仓储实现、外部客户端、技术组件
```

---

## 5. 领域层设计

### 5.1 领域模型与聚合

#### 领域模型图

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

#### 聚合设计：{{aggregate1}}

- **聚合根**：{{aggregateRoot1}}
- **聚合描述**：{{aggregateDescription1}}
- **聚合边界**：边界内 {{aggregateBoundaryInside1}}；边界外 {{aggregateBoundaryOutside1}}

| 实体/值对象 | 类型   | 描述             |
| ----------- | ------ | ---------------- |
| {{entity1}} | 实体   | {{description1}} |
| {{entity2}} | 值对象 | {{description2}} |

#### 聚合设计：{{aggregate2}}

- **聚合根**：{{aggregateRoot2}}
- **聚合描述**：{{aggregateDescription2}}
- **聚合边界**：{{aggregateBoundary2}}

### 5.2 领域服务与端口

#### {{domainService1}}

- **服务描述**：{{serviceDescription1}}
- **服务职责**：{{serviceResponsibilities1}}

| 方法名称    | 参数            | 返回值          | 描述             |
| ----------- | --------------- | --------------- | ---------------- |
| {{method1}} | {{parameters1}} | {{returnType1}} | {{description1}} |
| {{method2}} | {{parameters2}} | {{returnType2}} | {{description2}} |

#### 仓储与端口定义

| 类型 | 名称                          | 说明               |
| ---- | ----------------------------- | ------------------ |
| 仓储 | I{{AggregateRoot1}}Repository | 聚合根持久化与查询 |
| 端口 | {{portName1}}                 | {{portDesc1}}      |

### 5.3 领域事件定义

> **重要**：本节是领域事件定义的单一真实来源（SSOT）。

#### {{domainEvent1}}

- **事件定义**：{{eventDefinition1}}
- **事件属性**：{{property1}}（{{type1}}）、{{property2}}（{{type2}}）
- **发布者**：{{eventPublisher1}}
- **订阅者**：{{eventSubscribers1}}

```json
{
  "eventType": "{{domainEvent1}}",
  "eventId": "{{eventId}}",
  "timestamp": "{{timestamp}}",
  "aggregateId": "{{aggregateId}}",
  "aggregateType": "{{aggregateType}}",
  "version": {{version}},
  "data": {}
}
```

#### {{domainEvent2}}

- **事件定义**：{{eventDefinition2}}

---

## 6. 应用层设计

### 应用层定位与职责

1. **用例编排**：将请求转化为对领域服务和聚合根的调用
2. **数据转换**：API 层 DTO 与领域对象之间的转换
3. **事务管理**：确保领域操作的原子性和一致性
4. **权限检查**：授权与权限验证
5. **异常处理**：领域异常转换为 API 响应

### 应用服务清单

| 服务名       | 职责                | 关联用例     |
| ------------ | ------------------- | ------------ |
| {{service1}} | {{responsibility1}} | {{useCase1}} |
| {{service2}} | {{responsibility2}} | {{useCase2}} |

### 应用服务设计：{{service1}}

- **职责**：{{serviceResponsibility1}}
- **命令**：{{command1}} — {{commandDescription1}}；输入 {{commandInput1}}，输出 {{commandOutput1}}
- **错误处理**：{{domainException1}} → {{httpStatus1}}/{{errorCode1}}；{{domainException2}} → {{httpStatus2}}/{{errorCode2}}

### CQRS 与事务

- **命令流程**：参数验证 → 权限检查 → 加载聚合根 → 执行业务方法 → 保存 → 发布领域事件 → 返回结果
- **查询流程**：参数验证 → 权限检查 → 构建查询 → 执行 → 转 DTO → 返回
- **事务边界**：应用服务方法为事务边界；{{transactionManagement}}

---

## 7. API 设计

### REST API 基础信息

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

### 接口详细说明：{{api1}}

- **端点**: `{{endpoint1}}`，**方法**: {{httpMethod1}}，**认证**: {{authentication1}}
- **描述**: {{apiDescription1}}
- **请求体示例**：{{property1}}、{{property2}}
- **成功响应**：{{successCode}}；**错误响应**：{{errorCode1}}（{{errorMessage1}}）、{{errorCode2}}（{{errorMessage2}}）

### 事件驱动 API

| 事件名称   | 事件类型       | 主题/队列  | 描述             |
| ---------- | -------------- | ---------- | ---------------- |
| {{event1}} | {{eventType1}} | {{topic1}} | {{description1}} |
| {{event2}} | {{eventType2}} | {{topic2}} | {{description2}} |

### API 契约与规范

- **响应格式**：code、message、data；**分页**：items、pagination（page、pageSize、totalCount、totalPages）
- **错误格式**：code、message、errors（field、reason）
- **版本控制**：{{versioningStrategy}}；**向后兼容**：{{backwardCompatibility}}
- **认证与授权**：{{authenticationMethods}}；{{authorizationStrategy}}
- **性能与限流**：平均响应时间 {{avgResponseTime}}，P99 {{p99ResponseTime}}；{{rateLimitingStrategy}}

---

## 8. 基础设施层设计

### 架构定位

基础设施层实现领域层定义的仓储与端口，封装数据访问、外部客户端与技术组件。

### 技术工具

| 工具类型   | 说明                           | 本领域使用场景 |
| ---------- | ------------------------------ | -------------- |
| 异常处理   | 统一异常捕获、分类与处理       | {{toolUsage1}} |
| 日志记录   | 应用日志与错误日志             | {{toolUsage2}} |
| ID 生成器  | 唯一标识符（UUID、有序 ID 等） | {{toolUsage3}} |
| 序列化服务 | JSON/二进制序列化与反序列化    | {{toolUsage4}} |
| 加密服务   | 数据加解密                     | {{toolUsage6}} |

### 基础设施能力

| 能力类型 | 说明                                      | 本领域使用场景      |
| -------- | ----------------------------------------- | ------------------- |
| 数据访问 | Repository 实现、数据映射、事务、查询优化 | {{dataAccessUsage}} |
| 网络通信 | HTTP/WebSocket 客户端、连接管理、重试     | {{networkUsage}}    |
| 消息队列 | 消息发布/订阅、路由、持久化               | {{messagingUsage}}  |

### 端口实现与关键组件

- **仓储实现**：{{AggregateRoot1}}RepositoryImpl 等，实现领域层定义的仓储接口
- **端口实现**：{{portName1}} 的具体实现类，依赖基础设施（DB、HTTP 客户端等）

---

## 9. 错误处理

### 错误处理策略

{{errorHandlingStrategy}}

### 异常映射

| 领域异常             | HTTP 状态码     | 错误响应码     | 说明             |
| -------------------- | --------------- | -------------- | ---------------- |
| {{domainException1}} | {{httpStatus1}} | {{errorCode1}} | {{description1}} |
| {{domainException2}} | {{httpStatus2}} | {{errorCode2}} | {{description2}} |

### 标准错误码

| 错误码 | HTTP 状态 | 含义           |
| ------ | --------- | -------------- |
| 0      | 200/201   | 成功           |
| 400    | 400       | 请求参数错误   |
| 401    | 401       | 未授权         |
| 403    | 403       | 禁止访问       |
| 404    | 404       | 资源不存在     |
| 409    | 409       | 冲突           |
| 500    | 500       | 服务器内部错误 |

---

## 10. 使用方式（调用方）

{{usageDescription}}

### 调用示例

{{usageExample}}

---

## 11. 可选：表现层

若本领域有特定 UI 需求，可在此说明表现层定位、页面结构、组件使用、状态管理与路由。

- **页面**：{{page1}}（{{page1Description}}）、{{page2}}（{{page2Description}}）
- **与应用层关系**：调用应用服务完成业务操作，通过 DTO 绑定 UI；详见上文「应用层设计」。
- **技术栈（可选）**：{{uiFramework}}、{{stateManagement}}、{{routing}}

---

## 12. 相关文档

### 领域内

- 本文档为 {{domainName}} 的 DDD 合一设计；领域事件以「5.3 领域事件定义」为 SSOT。

### 系统级

- [[../01-overview/01-domains-overview.md]] - 系统级领域概览（领域划分、依赖、术语表等）

### 组件

- 技术工具（日志、加密、ID 等）见各 03-component-xxx 的模块概览。

---

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人           |
| -------- | ---- | -------- | ---------------- |
| {{date}} | 1.0  | 初始版本 | {{domainExpert}} |
