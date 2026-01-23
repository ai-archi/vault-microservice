# {{domainName}} 领域概览

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{domainName}} 领域的职责、边界、技术栈和与其他领域的交互关系。

> **说明**：本文档是单个领域的概览文档。系统级的领域划分和领域依赖关系请参考 [[../../01-overview/01-domains-overview.md]] 文档。

## 领域定义

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

## 技术栈

### 核心技术

| 技术类型 | 技术选型 | 说明 |
|---------|---------|------|
| 编程语言 | {{programmingLanguage}} | {{programmingLanguageNote}} |
| 框架/库 | {{framework}} | {{frameworkNote}} |
| 数据存储 | {{storage}} | {{storageNote}} |
| 消息/事件 | {{messaging}} | {{messagingNote}} |

### 特殊技术需求

{{specialTechnicalRequirements}}

> **说明**：基础设施层技术工具（如日志、加密、ID生成等）的详细说明请参考 [[../../shared/overview/01-shared-modules-overview.md]] 文档。

## 领域交互

### 依赖的其他领域

| 依赖领域 | 依赖类型 | 交互方式 | 说明 |
|---------|---------|---------|------|
| {{dependentDomain1}} | {{dependencyType1}} | {{interactionMethod1}} | {{description1}} |
| {{dependentDomain2}} | {{dependencyType2}} | {{interactionMethod2}} | {{description2}} |

**依赖类型说明**：
- **强依赖**：本领域必须依赖该领域才能正常工作
- **弱依赖**：本领域可以独立工作，但依赖该领域提供增强能力
- **事件依赖**：通过领域事件进行解耦的依赖关系

### 被其他领域依赖

| 依赖方领域 | 依赖类型 | 交互方式 | 说明 |
|-----------|---------|---------|------|
| {{dependentByDomain1}} | {{dependencyType1}} | {{interactionMethod1}} | {{description1}} |
| {{dependentByDomain2}} | {{dependencyType2}} | {{interactionMethod2}} | {{description2}} |

### 领域接口

#### 对外提供的接口

| 接口类型 | 接口名称 | 说明 | 详细文档 |
|---------|---------|------|---------|
| REST API | {{apiName1}} | {{apiDescription1}} | [[../04-apis/01-rest-api.md]] |
| 领域事件 | {{eventName1}} | {{eventDescription1}} | [[../02-domain/01-domain-model.md]] |

#### 依赖的外部接口

| 接口类型 | 接口名称 | 提供方 | 说明 |
|---------|---------|--------|------|
| REST API | {{externalApiName1}} | {{provider1}} | {{description1}} |
| 领域事件 | {{externalEventName1}} | {{provider1}} | {{description1}} |

## 目录结构

{{domainName}} 领域采用 DDD 分层架构，目录结构如下：

```
{{domainId}}/
├── 01-overview/          # 领域概览
│   ├── 01-domain-overview.md    # 领域概览（本文档）
│   └── 02-domain-structure.md   # 领域目录结构详细说明
├── 02-domain/           # 领域层
│   ├── 01-domain-model.md       # 领域模型
│   └── 02-use-cases.md          # 业务用例
├── 03-application/      # 应用层
│   ├── 01-application-overview.md
│   └── 02-application-services.md
├── 04-apis/             # API层
│   ├── 01-rest-api.md
│   └── 02-event-api.md
└── 05-infrastructure/   # 基础设施层
    └── 01-infrastructure-overview.md
```

> **详细说明**：领域目录结构的详细说明请参考 [[02-domain-structure.md]] 文档。

## 核心概念

{{domainName}} 领域的核心概念包括：

- **{{concept1}}**：{{concept1Description}}
- **{{concept2}}**：{{concept2Description}}
- **{{concept3}}**：{{concept3Description}}

> **详细说明**：领域术语的完整定义请参考 [[../02-domain/01-domain-model.md]] 和系统级的 [[../../01-overview/04-glossary.md]] 文档。

## 相关文档

### 领域内文档

- [[02-domain-structure.md]] - 领域目录结构详细说明
- [[../02-domain/01-domain-model.md]] - 领域模型（聚合、实体、值对象、领域服务）
- [[../02-domain/02-use-cases.md]] - 业务用例文档
- [[../03-application/01-application-overview.md]] - 应用层概览
- [[../03-application/02-application-services.md]] - 应用服务设计
- [[../04-apis/01-rest-api.md]] - REST API 定义
- [[../04-apis/02-event-api.md]] - 事件接口定义

### 系统级文档

- [[../../01-overview/01-domains-overview.md]] - 系统级领域概览（所有领域的划分和依赖关系）
- [[../../01-overview/02-domain-mapping.md]] - 子领域映射（核心域/支撑域/通用域划分）
- [[../../01-overview/03-bounded-context.md]] - 限界上下文定义
- [[../../01-overview/04-glossary.md]] - 全局领域术语表

### 共享资源

- [[../../02-shared/01-overview/01-shared-modules-overview.md]] - 共享模块概览

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |
