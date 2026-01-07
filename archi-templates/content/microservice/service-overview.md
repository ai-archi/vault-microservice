# {{serviceName}} 服务概览

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: {{version}}

## 服务简介

{{serviceDescription}}

> **说明**: 本文档从**技术/架构视角**描述服务的定位、职责和技术特性。产品定位、目标用户和价值主张等业务信息请参考 [[../02-product/product-overview.md]] 文档。

## 服务定位

### 技术定位

{{technicalPosition}}

### 在微服务架构中的角色

{{roleInMicroservicesArchitecture}}

### 服务边界

{{serviceBoundary}}

## 服务职责

### 核心职责

{{coreResponsibilities}}

### 职责边界

{{responsibilityBoundaries}}

## 服务上下文

> **说明**: 本部分以文字形式描述服务的上下文关系，可视化的系统上下文图请参考 [[context-diagram.md]] 文档。

### 上游服务

| 服务名称 | 交互方式 | 描述 |
|---------|---------|------|
| {{upstreamService1}} | {{interactionMethod1}} | {{description1}} |
| {{upstreamService2}} | {{interactionMethod2}} | {{description2}} |

### 下游服务

| 服务名称 | 交互方式 | 描述 |
|---------|---------|------|
| {{downstreamService1}} | {{interactionMethod1}} | {{description1}} |
| {{downstreamService2}} | {{interactionMethod2}} | {{description2}} |

### 外部依赖

| 依赖类型 | 依赖名称 | 描述 |
|---------|---------|------|
| {{dependencyType1}} | {{dependencyName1}} | {{description1}} |
| {{dependencyType2}} | {{dependencyName2}} | {{description2}} |

## 服务特性

### 关键特性

{{keyFeatures}}

### 非功能性需求

> **说明**: 本服务需要满足的非功能性需求，这些需求会影响系统上下文中的交互设计。

- **性能**: {{performanceRequirement}}
- **可用性**: {{availabilityRequirement}}
- **可扩展性**: {{scalabilityRequirement}}
- **安全性**: {{securityRequirement}}

## 技术栈概览

> **说明**: 本部分提供技术栈的概览信息，详细的架构设计和技术选型理由请参考 [[architecture.md]] 文档。

### 编程语言与框架

{{programmingLanguagesAndFrameworks}}

### 数据存储

{{dataStorage}}

### 消息中间件

{{messageMiddleware}}

### 基础设施

{{infrastructure}}

## 相关文档

- [[context-diagram.md]] - 系统上下文图
- [[architecture.md]] - 架构概览
- [[../02-product/product-overview.md]] - 产品概览（产品/业务视角）
- [[../03-domain/domain-overview.md]] - 领域概览

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | {{version}} | 初始版本 | {{architect}} |

