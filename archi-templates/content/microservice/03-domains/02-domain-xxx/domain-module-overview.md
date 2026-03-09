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
| 仓储     | {{repositoryName1}} | {{repositoryDesc1}}；对应代码目录 domain.port 与 infrastructure.persistence |
| REST API | {{apiName1}}        | {{apiDescription1}}；对应 interfaces.controller 与 §7 接口列表 |
| 领域事件 | {{eventName1}}      | {{eventDescription1}}；发布者见 §6 应用层，订阅者见 §5.3 |

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

> **填写说明**：代码目录结构需展开到**子包与关键类/文件**，便于实现落地；以下为推荐结构，按本领域替换占位符并删减或新增包。若本领域以 Spring Boot Starter 方式提供，可增加 `config/` 与 `META-INF/spring`；若仅库形态则可不含 `interfaces/` 或仅保留端口 API。  
> 占位符约定：`{{domainModule}}` 为模块简短名（用于 AutoConfiguration/Properties 类名，如 AppUser、Auth）；`{{controllerClass}}` 为主控制器类名（如 UserController）；`{{AggregateRoot1}}`、`{{portName1}}`、`{{service1}}` 等与 §5、§6 一致。

以下包结构以**单模块**为例；若拆分为多模块（如 domain-core、infrastructure、server），包名前缀保持 `{{packagePath}}`，将 infrastructure、interfaces 迁出到独立 artifact 时仍按本结构归属。

```
src/main/java/{{packagePath}}/
├── config/                          # 可选：Spring Boot 自动配置（Starter 时必选）
│   ├── {{domainModule}}AutoConfiguration.java   # 条件装配端口实现、应用服务、Controller
│   └── {{domainModule}}Properties.java          # 配置属性
├── interfaces/                      # 表现层：REST 控制器、DTO、契约
│   ├── controller/                 # REST 控制器
│   │   └── {{controllerClass}}.java # 与 §7 接口列表对应的端点
│   ├── dto/                         # 请求/响应 DTO（与 API 契约一致）
│   │   ├── request/                # 创建/更新/查询请求 DTO
│   │   └── response/               # 单条/列表/分页响应 DTO
│   └── convert/                     # 可选：VO 与 application 层 Command/Result 转换
├── application/                     # 应用层：用例编排、Command/Query
│   ├── {{service1}}.java            # 主应用服务
│   └── dto/                         # 命令与查询 DTO
│       ├── command/                # CreateXxxCommand、UpdateXxxCommand 等
│       └── query/                  # 查询条件 DTO（若 CQRS 可扩展读模型）
├── domain/                          # 领域层：实体、值对象、端口、领域异常
│   ├── model/                      # 聚合根与值对象（或按子域分包）
│   │   ├── {{AggregateRoot1}}.java # 聚合根：属性与领域行为
│   │   └── {{ValueObject1}}.java   # 值对象
│   ├── port/                       # 仓储与能力端口接口定义
│   │   ├── I{{AggregateRoot1}}Repository.java   # 聚合根持久化与查询
│   │   └── {{portName1}}.java                    # 对外能力端口（见 §2 领域接口摘要）
│   └── exception/                  # 领域异常
│       └── {{domainException1}}.java
└── infrastructure/                  # 基础设施层：仓储实现、端口实现、技术组件
    ├── persistence/                # 持久化
    │   ├── {{AggregateRoot1}}RepositoryImpl.java # 实现 I{{AggregateRoot1}}Repository
    │   ├── entity/                 # JPA/MyBatis 实体（若适用）
    │   │   └── {{AggregateRoot1}}Entity.java
    │   └── mapper/                 # 可选：Entity ↔ 聚合 映射
    ├── port/                       # 端口实现（对外暴露的端口在此实现）
    │   └── Default{{portName1}}.java   # {{portName1}} 的实现类
    └── event/                      # 可选：领域事件发布
        └── {{domainModule}}DomainEventPublisher.java

src/main/resources/
└── META-INF/spring/                 # 可选：若本域提供自动配置
    └── org.springframework.boot.autoconfigure.AutoConfiguration.imports
```

#### 分层与包职责对照

| 层 | 包 | 职责 | 对应本文档 |
| --- | --- | --- | --- |
| 领域层 | domain.model | {{AggregateRoot1}}、{{ValueObject1}} 等聚合与值对象 | §5.1 聚合设计、§5.2 端口 |
| 领域层 | domain.port | I{{AggregateRoot1}}Repository、{{portName1}} 接口定义 | §5.2 领域服务与端口、§2 领域接口摘要 |
| 领域层 | domain.exception | 领域异常类 | §9 错误处理 |
| 应用层 | application | {{service1}}、Command/Query DTO，用例编排 | §6 应用层设计 |
| 表现层 | interfaces.controller、interfaces.dto | REST 控制器、请求/响应 DTO，与 §7 API 契约一致 | §7 API 设计 |
| 基础设施层 | infrastructure.persistence | 仓储实现、实体与表映射、物理数据模型（表结构模板） | §8 基础设施层设计 |
| 基础设施层 | infrastructure.port | {{portName1}} 等端口实现 | §5.2、§8、§10 使用方式 |

**约束**：domain 不依赖 application、infrastructure、interfaces；application 仅依赖 domain 的 port 与 model；interfaces 依赖 application；infrastructure 实现 domain.port，可依赖技术组件与第三方库。

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

基础设施层实现领域层定义的仓储与端口，封装数据访问、外部客户端与技术组件，并维护物理数据模型（表结构模板），作为本领域持久化结构的单一真实来源（SSOT）。

### 物理数据模型与表结构模板

> **填写说明**：本节用于描述本领域的**物理数据模型**，包括表清单、关键字段、约束与演进策略，同时给出**DDL 模板**，为 `alavten-db-migration`（或其他迁移工程）中的实际脚本提供规范示例。

#### 表清单概览

| 表名                    | 归属聚合/子域          | 业务含义             | 备注（分区、多租户等）              |
| ----------------------- | ---------------------- | -------------------- | ----------------------------------- |
| {{tableName1}}         | {{aggregateOrSubdomain1}} | {{tableBizDesc1}} | {{tableNote1}}                      |
| {{tableName2}}         | {{aggregateOrSubdomain2}} | {{tableBizDesc2}} | {{tableNote2}}                      |

#### 表结构示例：{{tableName1}}

> 建议与 `server/alavten-db-migration` 中的迁移脚本命名规范保持一致，例如 `V{{version}}__{{module}}_{{changeSummary}}.sql`，并在此给出**推荐列/索引/约束结构**。

```sql
-- 示例：{{tableName1}} 物理表结构模板
CREATE TABLE {{tableName1}} (
    id              BIGINT          NOT NULL COMMENT '主键ID，雪花或序列',
    tenant_id       BIGINT          NOT NULL COMMENT '租户ID（如适用）',
    {{bizColumn1}}  VARCHAR(128)    NOT NULL COMMENT '{{bizColumn1Desc}}',
    {{bizColumn2}}  VARCHAR(256)    NULL     COMMENT '{{bizColumn2Desc}}',
    status          VARCHAR(32)     NOT NULL COMMENT '状态',
    created_at      TIMESTAMP       NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    created_by      VARCHAR(64)     NOT NULL COMMENT '创建人',
    updated_at      TIMESTAMP       NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    updated_by      VARCHAR(64)     NOT NULL COMMENT '更新人',
    PRIMARY KEY (id),
    KEY idx_{{tableName1}}_tenant   (tenant_id),
    KEY idx_{{tableName1}}_status   (status)
) COMMENT='{{tableBizDesc1}}';
```

#### 表结构与领域模型映射

- `{{AggregateRoot1}}` ↔ `{{tableName1}}`：主实体与主表映射关系，标明关键字段与值对象展开方式。
- 值对象持久化策略：内联列（如地址、区间）或独立表；若为独立表，补充对应表名与外键策略。
- 约束策略：唯一约束、业务主键、软删除标记、多租户隔离（tenant_id / schema）等。

> 若本领域涉及多存储引擎（如关系型数据库 + KV/文档库），可按存储类型分组给出表/集合结构模板。

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

- **仓储实现**：置于 `infrastructure.persistence/`，如 {{AggregateRoot1}}RepositoryImpl，实现 domain.port 中的 I{{AggregateRoot1}}Repository；含实体映射、表结构或 Mapper，并维护本领域的物理数据模型（表结构定义与演进模板，如 DDL 片段、迁移脚本示例），与上文“物理数据模型与表结构模板”保持一致。
- **端口实现**：置于 `infrastructure.port/`，如 Default{{portName1}}，实现 domain.port 中的 {{portName1}}；依赖仓储、技术组件（DB、HTTP 客户端、消息等），供上游或 Starter 装配为 Bean。

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
